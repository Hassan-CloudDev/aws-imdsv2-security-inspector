\# AWS EC2 IMDSv2 Metadata Inspector



A simple Bash script to fetch EC2 instance metadata using IMDSv2 (Instance Metadata Service Version 2) with token-based authentication.



\## Overview

IMDSv1 uses simple GET requests, which can be vulnerable to SSRF (Server-Side Request Forgery) attacks. IMDSv2 fixes this by requiring a session token (via PUT request) before retrieving any metadata.



This script demonstrates how to request a session token and use it to securely query basic instance details.



\## Script Usage



1\. Make the script executable:

&#x20;  ```bash

&#x20;  chmod +x imdsv2\_inspector.sh



Run the script:

./imdsv2\_inspector.sh



\##Script Details (imdsv2\_inspector.sh)



\#!/bin/bash

TOKEN=$(curl -s -X PUT "\[http://169.254.169.254/latest/api/token](http://169.254.169.254/latest/api/token)" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")



echo "Instance ID: $(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \[http://169.254.169.254/latest/meta-data/instance-id](http://169.254.169.254/latest/meta-data/instance-id))"

echo "Instance Type: $(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \[http://169.254.169.254/latest/meta-data/instance-type](http://169.254.169.254/latest/meta-data/instance-type))"

echo "Availability Zone: $(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" \[http://169.254.169.254/latest/meta-data/placement/availability-zone](http://169.254.169.254/latest/meta-data/placement/availability-zone))"

&#x20;



