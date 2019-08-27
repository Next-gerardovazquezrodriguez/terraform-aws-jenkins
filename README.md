# Jenkins Terraform Module for AWS #

This Terraform module deploys a Jenkins Master Server providing high availability and scalability.

[![CircleCI](https://circleci.com/gh/jnonino/terraform-aws-jenkins/tree/master.svg?style=svg)](https://circleci.com/gh/jnonino/terraform-aws-jenkins/tree/master)
[![](https://img.shields.io/github/license/jnonino/terraform-aws-jenkins)](https://github.com/jnonino/terraform-aws-jenkins)
[![](https://img.shields.io/github/issues/jnonino/terraform-aws-jenkins)](https://github.com/jnonino/terraform-aws-jenkins)
[![](https://img.shields.io/github/issues-closed/jnonino/terraform-aws-jenkins)](https://github.com/jnonino/terraform-aws-jenkins)
[![](https://img.shields.io/github/languages/code-size/jnonino/terraform-aws-jenkins)](https://github.com/jnonino/terraform-aws-jenkins)
[![](https://img.shields.io/github/repo-size/jnonino/terraform-aws-jenkins)](https://github.com/jnonino/terraform-aws-jenkins)

## Usage

Check valid versions on:
* Github Releases: <https://github.com/jnonino/terraform-aws-jenkins/releases>
* Terraform Module Registry: <https://registry.terraform.io/modules/jnonino/jenkins/aws>

    	module "jenkins" {
            source              = "jnonino/jenkins/aws"
            version             = "1.0.0"
            name_preffix        = var.name_preffix
            profile             = var.profile
            region              = var.region
            vpc_id              = module.networking.vpc_id
            public_subnets_ids  = module.networking.public_subnets_ids
            private_subnets_ids = module.networking.private_subnets_ids
        }

The networking module should look like this:

        module "networking" {
    	    source          = "jnonino/networking/aws"
            version         = "2.0.3"
            name_preffix    = "base"
            profile         = "aws_profile"
            region          = "us-east-1"
            vpc_cidr_block  = "192.168.0.0/16"
            availability_zones                          = [ "us-east-1a", "us-east-1b", "us-east-1c", "us-east-1d" ]
            public_subnets_cidrs_per_availability_zone  = [ "192.168.0.0/19", "192.168.32.0/19", "192.168.64.0/19", "192.168.96.0/19" ]
            private_subnets_cidrs_per_availability_zone = [ "192.168.128.0/19", "192.168.160.0/19", "192.168.192.0/19", "192.168.224.0/19" ]
    	}

Check versions for this module on:
* Github Releases: <https://github.com/jnonino/terraform-aws-networking/releases>
* Terraform Module Registry: <https://registry.terraform.io/modules/jnonino/networking/aws>

## Output values

* jenkins_master_alb_id: Jenkins Master Application Load Balancer ID.
* jenkins_master_alb_arn: Jenkins Master Application Load Balancer ARN.
* jenkins_master_alb_arn_suffix: Jenkins Master Application Load Balancer ARN Suffix.
* jenkins_master_alb_dns_name: Jenkins Master Application Load Balancer DNS Name.
* jenkins_master_alb_zone_id: Jenkins Master Application Load Balancer Zone ID.
