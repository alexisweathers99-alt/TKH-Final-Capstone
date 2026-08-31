# Secure Automated Web Architecture

## Description
This project provisions a secure, automated web server infrastructure on AWS using Terraform. It builds a custom VPC with public networking, a hardened security group, and an EC2 instance running Apache — with the entire deployment validated through an automated GitHub Actions security pipeline before going live.

## Technologies Used
- AWS (VPC, EC2, Security Groups, Internet Gateway)
- Terraform
- GitHub Actions
- tfsec

## Architecture
The VPC (10.0.0.0/16) contains a single public subnet with an Internet Gateway and route table directing outbound traffic to 0.0.0.0/0. The security group restricts SSH (port 22) access to a single home IP address, while allowing HTTP (port 80) traffic from anywhere, since the server is intended to be publicly accessible. All outbound traffic is permitted so the instance can install packages during boot. The EC2 instance itself uses IMDSv2 (token-required metadata access) and an encrypted root volume to reduce its attack surface, both enforced after an automated tfsec scan flagged their absence.