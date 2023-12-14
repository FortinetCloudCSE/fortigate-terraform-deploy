# Terraform Deployment Scripts, Cloud CSE Fork
## Introduction
This project includes a set of terraform scripts for getting started with different cloud-providers with Fortinet.

* [AWS](https://github.com/fortinet/fortigate-terraform-deploy/tree/main/aws)
* [Azure](https://github.com/fortinet/fortigate-terraform-deploy/tree/main/azure)
* [GCP](https://github.com/fortinet/fortigate-terraform-deploy/tree/main/gcp)
* [IBM-Cloud](https://github.com/fortinet/fortigate-terraform-deploy/tree/main/ibm)
* [OCI](https://github.com/fortinet/fortigate-terraform-deploy/tree/main/oci)
* [Openstack](https://github.com/fortinet/fortigate-terraform-deploy/tree/main/openstack)

This is a fork of [this repo](https://github.com/fortinet/fortigate-terraform-deploy) for testing and POC development.

To submit updates or changes to this fork, please create a feature branch and PR. Branches must pass certain tests before merging. Currently, these consist of:

* [tflint linter](https://github.com/terraform-linters/tflint)
* [FortiDevSec](https://docs.fortinet.com/document/fortidevsec/23.2.a/user-guide/546812/introduction) static code/IaC scans

First, to gain access to Jenkins and the FortiDevSec console, send an email to fortinetcloudcse@fortinet.com with your GitHub Username and your Fortinet email address (the same one used to log in to FortiCloud). Jenkins login credentials will be sent to you and you will be granted access to the FortiDevSec console.

The Jenkins console may be found at https://jenkins.fortinetcloudcse.com:8443

The FortiDevSec console can be accessed by logging in to [FortiCare](https://support.fortinet.com/welcome/#/) **as an IAM user** and navigating to the FortiDevSec console (you'll be able to do this once you receive confirmation that you've been added as an IAM user with permissions to view the console).

## Sample Git Workflow

This is an example development workflow for creating/submitting repo updates.

* First, clone the repository locally and checkout a feature branch.
  ```
  git clone git@github.com:FortinetCloudCSE/fortigate-terraform-deploy.git
  cd fortigate-terraform-deploy
  git checkout -b my-feature-branch
  ```

* When finished working, commit your changes. 
  ```
  git add -A
  git commit -m "commit message"
  ```

* If you feel you have too many commits with tenuous changes, you can squash them by running a soft reset:
  ```
  git reset --soft <hash commit of last commit you'd like to keep in the history>
  git add -A
  git commit -m "commit message"
  ```

* Before pushing and requesting a PR, check for updates on the main branch and merge them onto your branch and resolve any merge conflicts if necessary.
  ```
  git checkout main
  git pull
  git checkout my-feature-branch
  git rebase -i main
  ```

* Then, commit your changes and push.
  ```
  git add -A
  git commit -m "commit description"
  git push
  ```

* The push will trigger the Jenkins tflint and FortiDevSec tests. Once they pass, submit a PR and request a review. Once your code is reviewed and approved, you are ready to merge your changes to the main branch.
  ```
  git checkout main
  git merge --ff-only my-feature-branch
  git push
  ```

## Support
Fortinet-provided scripts in this and other GitHub projects do not fall under the regular Fortinet technical support scope and are not supported by FortiCare Support Services.
For direct issues, please refer to the [Issues](https://github.com/fortinet/fortigate-terraform-deploy/issues) tab of this GitHub project.
For other questions related to this project, contact [github@fortinet.com](mailto:github@fortinet.com).

## License
[License](https://github.com/fortinet/fortigate-terraform-deploy/blob/master/LICENSE) © Fortinet Technologies. All rights reserved.


