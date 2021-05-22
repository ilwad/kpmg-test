# Overview

We will use terraform as a tool for building an Infrastructure-as-code. IAC consists in the ability to transform a given set of requirements into code that defines a network with all of its components and connections. 
This terraform code will spin a tree-tier network in AWS that we use as a base to build on top of it.
Our tier will consist of  a public subnet and 2 private subnets. The private subnets are meant to be used by an application layer and a database layer. The public subnet is where we'll execute our administration tasks and where all public traffic is routed to. For our admin tasks, we'll launch an EC2 instance in the public subnet and use it as a jump box to connect to an EC2 instance deployed in the application layer
# Prerequisites

## Dependencies

First and foremost, we'll need to have [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started) and the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed, as well as an active AWS account. Please refer to the official documentation to do so. Installing Terraform on Linux and macOS is easier, but if you're on Windows, I'd recommend installing Terraform using [Chocolatey](https://chocolatey.org/packages/terraform) (because it is easier)

## Configuration

We have chosen a simple modularised code and certain  hard-coded values such as AMI, instance type AZ can be shifted to varialble files

# ./compute.tf
We'll use one that is free, supported and maintained by AWS: Amzon Linux 2

# ./keys.tf
To access our instances, we'll need to register a key pair consisting of a private key and a public key.

# ./network.tf
CIDR block of 172.16.0.0/16
1 public subnet and 2 private subnets spread out in one 1 availability zone
1 public EC2 instance
1 private EC2 instance

# ./outputs.tf
output values that might be needed by other code or engineers

# ./providers.tf
The terraform block contains the required_providers block which specifies the provider local name, the source address and the version

# ./security.tf
the virtual firewall around an instance or component that controls inbound and outbound traffic

# ./versions.tf
one Provider version and one Terraform version defined

To run the code 

terraform init
terraform plan
if you like what you see in your plan then you can run
terraform apply -auto-approve


To destroy everything
terraform destroy -auto-approve

