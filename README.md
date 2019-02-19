# elasticTerraForm

## JMF Feb 2019

#### Table of Contents

1. [Intro](#intro)
2. [Module](#module)


## Intro

This is a demo of using Terraform to spin up an ElasticSearch Cluster on AWS

## Module

Use this module with your own variables to create a cluster in your AWS VPC.

```yaml
module "jmf-elasticsearch" {
  source = "github.com/knowledgewarrior/esTf-aws"

  name                      = "jmf-es"
  vpc_id                    = "vpc-c17079a9"
  subnet_ids                = [ "subnet-c27079aa"]
  zone_id                   = "Z2WVBD768XGJ6P"
  itype                     = "t2.medium.elasticsearch"
  ingress_allow_cidr_blocks = [ "172.31.16.0/20" ]
  access_policies           = <<CONFIG
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Principal": {
      "AWS": [
        "*"
      ]
    },
    "Action": [
      "es:*"
    ],
    "Resource": "arn:aws:es:us-west-2:507712738052:domain/jmf-es/*"
  }
    ]
}      
    CONFIG
}

```
