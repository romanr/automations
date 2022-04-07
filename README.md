# automations

This repository contains some of the automations I've developed throughout my career as a DevSecOps Engineer.

- [Graylog Configuration Script](./graylog.sh)

In the last quarter, I was responsible for implementing Graylog as our main logging solution.

On the first try, I followed the easy way, using an official Graylog AMI (Amazon Machine Images). But then I realized that it would not be enough to meet my needs. I needed something more flexible and configurable, so I decided to install it from scratch.

I provisioned the instance by terraform and automated the installation and configuration with shell script.

As I needed an efficient logging solution, our data needed to be persistent and that is why I chose to use EBS (Elastic Block Store).

The Graylog was made available as a module within our infrastructure, through terraform, so we could create an instance both in development and production environment. But we needed to ensure that the production logs had a long retention time for the sake of future audits. So I decided to send the production daily logs to an s3 bucket, since elasticsearch would keep a smaller retention number.

I used AWS SSM Parameter store for keeping the secret variables, such as GRAYLOG_PASSWORD.

Requirements:

AWS EC2 (Ubuntu, AWS Cli)
AWS EBS (Size depends on your data volume)
AWS SSM Parameter Store (Pre-generated password for Graylog)
This was the script responsible for doing all that process in less then 15 minutes:
