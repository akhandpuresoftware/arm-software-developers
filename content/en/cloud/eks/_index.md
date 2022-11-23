---
title: "Elastic Kubernetes Service on Arm-based Instances" 
type: docs
hide_summary: true
weight: 3
description: >
    Learning path for software developers about how to provision EKS cluster on Arm-based instance and then deployment of Wordpress(with Mysql) on Elastic Kubernetes Service. 
---

## Learning Objectives 

By the end of this learning path, you will be able to:

* Provision EKS cluster on Arm-based instance
* Deploy Wordpress(with Mysql) on Elastic Kubernetes Service

## Prerequisites

* An Amazon Web Services(AWS) account
* The AWS CLI, [installed](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and [configured](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)
* [AWS IAM Authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)
* The [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/), also known as `kubectl`
* Terraform

## Sections

|          Type | Content                       |
| ---           | ---                                 |
| How-To        | [What is EKS](/content/en/cloud/aws/introduction.md)
| How-To        | [Provision EKS cluster on Arm-based instance](/content/en/cloud/aws/eks.md) |
| How-To        | [Deploy Wordpress(with Mysql) on Elastic Kubernetes Service](/content/en/cloud/aws/terraform.md) |


## References and Documentation

| Type          | Content             |
| ---           | ---                 |
| Documentation | [Creating an AWS account](https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-creating.html) |
| Documentation | [EKS DOcumentation](https://aws.amazon.com/eks/) |
| Documentation | [Wordpress deployment Documentation](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/) |


[<-- Return to Learning Path](/content/en/cloud/aws/#sections)
