# Getting Started with Terraform

Terraform, developed by HashiCorp, is a widely adopted open-source Infrastructure as Code (IaC) tool. It enables users to define, provision, and manage cloud and on-premises infrastructure resources using a declarative configuration language.
Follow this step-by-step guide to learn about the Terraform basics. In this tutorial, you will learn how to install Terraform and use it to build, change, and destroy infrastructure. 

## Prerequisites
* If you are using macOS, install the Homebrew package manager by following the instructions listed here: [Homebrew](https://brew.sh/)
* If you do not have Docker, install the Rancher Desktop by following the instructions listed here: [Rancher Desktop](https://rancherdesktop.io/)

## Install Terraform

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the compressed binary application executable file deliverable for your platform, machine, or environment on which you like to run code and do development.
For example, if you are using macOS, run the following commands to install Terraform.
```shell
$ brew tap hashicorp/tap
$ brew install hashicorp/tap/terraform
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/Install1.png)</kbd>


## Build infrastructure

In this tutorial, you will use Terraform to build infrastructure, more specifically, deploy a Docker container. 

Create a directory named `terraform-demo` on your local machine.

```console
$ mkdir terraform-demo
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/Directory1.png)

Navigate to this directory.
```shell
$ cd terraform-demo
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/changedirectory.png)</kbd>

Next, create a file named `main.tf` inside this directory. This file will hold the Terraform configuration code for your Docker container. 

```shell
$ touch main.tf
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/touch.png)</kbd>

Open `main.tf` in your text editor, paste the following lines in this file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:////Users/divyasingal/.rd/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "training"
  ports {
    internal = 80
    external = 8000
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/configuration1.png)</kbd>

## Initialize the Terraform directory

Initialize the Terraform configuration directory using the `init` command.  This downloads and installs the providers defined in the configuration, which in this case is the Docker provider.

```shell
$ terraform init
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/initialization.png)</kbd>

Check for any errors in the above initialization command.

## Create the infrastructure

If the `terraform init` command ran successfully, provision the infrastructure using the `terraform apply` command. The command below may take a few minutes to run and will display a message indicating when the infrastructure has been created.

```shell
$ terraform apply
```
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/apply.png)</kbd>

Confirm that the Docker container is deployed.

<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/created.png)</kbd>

## Destroy the infrastructure
Once you no longer need the infrastructure, you may destroy it to reduce the resources used. In this tutorial, you will destroy the Docker container that you created in the previous step.

```shell
$ terraform destroy
```
Look for a message at the bottom of the output asking for confirmation. When prompted, answer `yes` to allow Terraform to destroy the infrastructure it had created earlier. 
<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/destroy-confirmation.png)</kbd>

Confirm that the infrastructure is destroyed.

<kbd>![](https://github.com/divyasingal/HashiAssignment/blob/ContentImprovements/images/destroyed.png)</kbd>

## Next Steps
Now that you have learned how to deploy infrastructure using Terraform, continue to learn more about [Terraform providers](https://developer.hashicorp.com/terraform/language/providers).
