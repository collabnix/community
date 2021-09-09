# Terraform  



![My image](https://raw.githubusercontent.com/collabnix/terraform/master/images/wordle.png)

Terraform Labs brings you tutorials that help you get hands-on experience using Terraform, Kubernetes & Cloud. Here you will find complete documentation of labs and tutorials around Terraform CLI, Configuration Language, sub-commands, providers, Registry and much more..

# An Ultimate Terraform Hands-on Labs
- [Beginners Track](https://collabnix.github.io/terraform/)
- [Intermediate Track](https://github.com/collabnix/terraform/blob/master/intermediate/README.md)
- [Advanced Track](https://github.com/collabnix/terraform/blob/master/experts/README.md)


# Terraform Workshop/Labs

- [Getting Started: Why, What & How about Terraform?](getting-started/README.md)

   - [The problem of provisioning everything manually](getting-started/the-problem.md)
   - [The concept of Infrastructure as a Code (IaC)](getting-started/iac.md)
   - [Where terraform comes in?](getting-started/terraform.md)
   - [Use cases of Terraform](getting-started/use-cases.md)
   - [Terraform Vs Ansible]()
   - [Terraform Vs Chef]()
   - [Terraform Vs Puppet]()
## Installing Terraform

- [MacOS](https://github.com/collabnix/terraform/blob/master/beginners/os/mac/README.md)
- [Linux](https://github.com/collabnix/terraform/tree/master/beginners/os/linux)
- [Windows](https://github.com/collabnix/terraform/tree/master/beginners/os/windows)
- [Raspberry Pi]()

## From Terraform INIT To APPLY

- [Terraform providers](https://github.com/collabnix/terraform/blob/master/beginners/providers/README.md)
- [Terraform resources](https://github.com/collabnix/terraform/blob/master/beginners/resources/README.md)
- [Variable Resources](https://github.com/collabnix/terraform/blob/master/beginners/resources/variables/README.md)
- [Output Resources](https://github.com/collabnix/terraform/blob/master/beginners/resources/output/README.md)
- [Terraform CLI](https://github.com/collabnix/terraform/blob/master/beginners/CLI/README.md)
- [Init-plan-apply !](https://github.com/collabnix/terraform/blob/master/beginners/init-plan-apply/README.md)

## Setting up Cloud Account

#### AWS

- [Setting up AWS account credentials](https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/setup-credentials.html)
- [Launch an EC2 instance](https://registry.terraform.io/modules/terraform-aws-modules/ec2-instance/aws/latest)
- [Create a S3 bucket for storage](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html)
- [Launch an RDS with mysql engine](https://registry.terraform.io/modules/terraform-aws-modules/rds/aws/latest)
- [Deploy a Single Web Server](https://aws.amazon.com/websites/)
- [Deploy a Configurable Web Server](https://enterprise.arcgis.com/en/server/10.3/cloud/amazon/deploy-web-app-linux-aws.htm)
- [Deploy Cluster of Web Servers](https://www.caucho.com/resin-4.0/admin/deploy-cloud.xtp)
- [Deploy a Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html)
- [Create a VPC](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc)
- [Deploy a subnet in VPC with security groups/firewall rules](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc)
- [Cleaning Up]()

#### Azure

- [Getting started with Terraform in Azure](https://github.com/collabnix/terraform/blob/master/beginners/azure/README.md)
- [Create a Virtual Network in Azure](https://github.com/collabnix/terraform/blob/master/beginners/azure/virtualnetwork)
- [Create a Linux Virtual Machine in Azure](https://github.com/collabnix/terraform/tree/master/beginners/azure/linuxVM)
- [Create a Windows-10 Virtual Machine in Azure](https://github.com/collabnix/terraform/tree/master/beginners/azure/windowsVM)
- [Create a Storage account and Host a static website in Azure](https://github.com/collabnix/terraform/tree/master/beginners/azure/storageAccount)
- [Create Multiple Resources in Azure using for_each](https://github.com/collabnix/terraform/tree/master/beginners/azure/multiple_resources)
- [Create AKS Cluster with Container Monitoring](https://github.com/collabnix/terraform/tree/master/beginners/azure/aks_cluster)

- [How to use Modules](https://github.com/collabnix/terraform/tree/master/beginners/azure/module_example)

### GCP

- [Setting up Terraform for Google Cloud Platform](https://github.com/collabnix/terraform/blob/master/beginners/gcp/README.md)
- Terraform vs Google Deployment Manager
- Launch a Compute Engine Instance
- Create a New VPC and Public Subnet
- Auto Scale and Load Balance the Managed Instance Groups
- Deploy a web server
- Cleaning Up

## Managing Terraform State

- What is Terraform State
- Shared Storage for State Files
- Locking State Files
- Isolating State Files
- File Layouts
- Read-only States
- Import Terraform state

## Terraform Backends

- What are terraform backends ?
- List of supported Remote backends
- Using remote backends in a collaborative environments

## Terraform Modules

- Why Terraform Modules
- When to write Terraform Modules


## Terrafrom Enterprise (TFE)
- Additional features of TFE
- Integration of TFE with Github
- Creating organisation
- Configuring backends






