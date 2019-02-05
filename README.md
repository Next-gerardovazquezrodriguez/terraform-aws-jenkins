# Jenkins Terraform Module for AWS#

This Terraform module deploys a Jenkins Master Server providing high availability and scalability.

## Usage

Check valid versions on:
* Github Releases: <https://github.com/jnonino/terraform-aws-jenkins/releases>
* Terraform Module Registry: <https://registry.terraform.io/modules/jnonino/jenkins/aws>

	module "jenkins" {
        source              = "jnonino/jenkins/aws"
        version             = "1.0.0"
        name_preffix        = "${var.name_preffix}"
        profile             = "${var.profile}"
        region              = "${var.region}"
        vpc_id              = "${module.networking.vpc_id}"
        public_subnets_ids  = [ "${module.networking.public_subnets_ids}" ]
        private_subnets_ids = [ "${module.networking.private_subnets_ids}" ]
    }

## Output values

* jenkins_master_alb_id: Jenkins Master Application Load Balancer ID.
* jenkins_master_alb_arn: Jenkins Master Application Load Balancer ARN.
* jenkins_master_alb_arn_suffix: Jenkins Master Application Load Balancer ARN Suffix.
* jenkins_master_alb_dns_name: Jenkins Master Application Load Balancer DNS Name.
* jenkins_master_alb_zone_id: Jenkins Master Application Load Balancer Zone ID.
