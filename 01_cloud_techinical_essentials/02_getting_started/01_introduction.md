# Introduction

## Project scope

### Goal
Employee directory app, where each employee may be registered and edited, including fields such as location, job title and badges of competences. These are the app's features from a user's perspective. 

From a technical point of view, this app will be built upon a private network using `Amazon VPC` (Virtual private cloud), it will host the backend and frontend code on `EC2` (Elastic cloud). Databases will be stored on `Amazon RDS` (Relational database service), while images will be stored on `S3` (Simple Storage System). The monitoring will be done with `CloudWatch`. Additionally, in order for the application to be robust and fault-tolerant, `Load Balancing`and `EC2 Auto Scaling` will be used. For security, `IAM` (Identity and access management).