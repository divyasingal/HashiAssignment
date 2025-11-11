# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC).
You can follow this step-by-step guide to learn the Terraform basics. In this tutorial, you will learn how to install Terraform and use it to build, change, and destroy infrastructure as code (IaC). 

## Prerequisites
If you are using macOS, install the Homebrew package manager by following the instructions listed here: [Homebrew](https://brew.sh/)

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

![](https://github.com/turbonomic/training/blob/main/images/ZN205InstanaOperator.png)
Navigate to this directory.
```shell
$ cd terraform-demo
```
Next, create a file named `main.tf` inside this directory. This file will hold the Terraform configuration code for your Docker container. 

```shell
$ touch main.tf
```

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
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```
## Initialize the Terraform directory

Initialize the Terraform configuration directory using the `init` command.  This downloads and installs the providers defined in the configuration, which in this case is the Docker provider.

```shell
$ terraform init
```

Check for any errors in the above initialization command.

## Create the infrastructure

If the `terraform init` command ran successfully, provision the infrastructure using the `terraform apply` command. The command below may take a few minutes to run and will display a message indicating when the infrastructure has been created.

```shell
$ terraform apply
```

## Destroy the infrastructure
Once you no longer need the infrastructure, you may destroy it to reduce the resources used. In this tutorial, you will destroy the Docker container that you created in the previous step.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. When prompted, answer `yes` to allow Terraform to destroy the infrastructure it had created earlier. 
