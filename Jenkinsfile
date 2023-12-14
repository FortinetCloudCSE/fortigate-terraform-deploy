void setBuildStatus(String message, String state, String repo_url) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: repo_url],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

pipeline {
    agent any

    stages {
       stage('Get directories to be scanned'){
        steps{
           script {
             checkout scm
             def commitHash = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
             def changedDirectories = sh(returnStdout: true, script: "git diff --name-only --diff-filter=ACMRT ${commitHash}^ ${commitHash} | xargs -I {} dirname {} | sort | uniq | tail -n +2").trim()
             env.CHANGED_DIRECTORIES = changedDirectories
             echo "Changed directories: ${changedDirectories}"
          }
        }
       }
       stage('Run tflint on changed directories') {
           steps {
             script {
               def changedDirectories = env.CHANGED_DIRECTORIES
               def directoriesArray = changedDirectories.split('\n')
               for (def directory in directoriesArray) {
                 sh "cd ${directory} && tflint --recursive --minimum-failure-severity=error"
               }
             }
           } 
       }
       stage('Running FortiDevSec scans...') {
           steps {
               echo "Running SAST scan..."
               sh 'env | grep -E "JENKINS_HOME|BUILD_ID|GIT_BRANCH|GIT_COMMIT" > /tmp/env'
               sh 'docker pull registry.fortidevsec.forticloud.com/fdevsec_sast:latest'
               sh 'docker run --rm --env-file /tmp/env --mount type=bind,source=$PWD,target=/scan registry.fortidevsec.forticloud.com/fdevsec_sast:latest'
           }
        }
    }
    post {
     success {
        setBuildStatus("Build succeeded", "SUCCESS", "${GIT_URL}");
     }
     failure {
        setBuildStatus("Build failed", "FAILURE", "${GIT_URL}");
     }
  }
}
