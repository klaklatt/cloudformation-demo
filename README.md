# CloudFormation AWS Demo

This git repository contains infrastructure as code (cloudformation) to deploy a common architecture to AWS. It creates a public and private network, a bastion host to connect to your private instances and an expample application behind a loadbalancer. 

## Overview

What we will build:
![aws-diagram](./assets/cloudformation-demo.svg)

## Prerequisites

- AWS account
- AWS cli installed

## Usage

I devided this project into 2 parts:
1. create resources for the base infrastructure
2. create resources for an example application

### 1. Creating infrastructure in AWS
File: 01-cf-base-infrastructure.yaml

This template creates following resources:
- VPC
- 3 private networks (1 for each availability zone in given region)
- 3 public networks (1 for each az as well)
- Internet Gateway
- Nat Gateway in each zone
- Resilient Bastion Host in an autoscaling group

```bash
aws --region eu-central-1 cloudformation deploy --stack-name=cf-demo-base --template-file=01-cf-base-infrastructure.yaml
```

### 2. Create example app in AWS
File: 02-cf-example-app.yaml

This template creates 3 ec2 instances and a loadbalancer as an example.

```bash
aws --region eu-central-1 cloudformation deploy --stack-name=CF-Demo-APP --template-file=02-cf-example-app.yaml
```