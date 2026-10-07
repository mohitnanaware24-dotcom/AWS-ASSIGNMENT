# AWS Project Assignment -- Set 5

## Student

**Name:** Mohit Nanaware

## Overview

This repository contains the implementation and documentation for three
AWS projects completed as part of AWS Project Assignment -- Set 5.

### Projects

1.  **S3 + CloudFront Static Website**
2.  **EC2 Linux Web Server using Amazon Linux and Apache**
3.  **DynamoDB Student Management System**

A separate `screenshots` folder contains the evidence screenshots for
each task.

------------------------------------------------------------------------

# Question 1 -- S3 + CloudFront Static Website

## Objective

Host a static website using Amazon S3 and distribute it through Amazon
CloudFront with HTTPS.

## AWS Services Used

-   Amazon S3
-   Amazon CloudFront
-   CloudFront Origin Access Control (OAC)

## Architecture

``` text
User Browser
     |
     | HTTPS
     v
CloudFront Distribution
     |
     | Origin Access Control
     v
Amazon S3 Bucket
     |
     +-- index.html
     +-- error.html
```

## Implementation

### 1. S3 Bucket

An S3 bucket was created to store the static website files.

The following files were uploaded:

-   `index.html`
-   `error.html`

### 2. CloudFront

A CloudFront distribution was created with the S3 bucket configured as
the origin.

The following configuration was applied:

-   S3 bucket used as origin
-   Origin Access Control enabled
-   Default root object: `index.html`
-   Viewer protocol policy: **Redirect HTTP to HTTPS**

## Testing

The CloudFront distribution was tested using:

**https://dmdgi5z8m2aw0.cloudfront.net**

The website loaded successfully through the CloudFront HTTPS endpoint.

## Result

The static website was successfully deployed to Amazon S3 and delivered
through Amazon CloudFront.

------------------------------------------------------------------------

# Question 2 -- EC2 Linux Web Server

## Objective

Deploy a Linux web server on Amazon EC2, configure an appropriate
Security Group, install Apache, and verify web access.

## AWS Services Used

-   Amazon EC2
-   Amazon VPC / Security Groups
-   Apache HTTP Server

## Architecture

``` text
Administrator
     |
     | SSH - Port 22
     | Restricted to My IP
     v
Amazon EC2
Amazon Linux 2023
     |
     v
Apache HTTP Server
     ^
     |
     | HTTP - Port 80
     | HTTPS - Port 443
     |
Internet Users
```

## EC2 Configuration

-   Operating System: **Amazon Linux 2023**
-   Instance Type: **t3.micro**
-   Web Server: **Apache HTTP Server (httpd)**

## Security Group

The following inbound rules were configured:

  Protocol     Port Source      Purpose
  ---------- ------ ----------- ------------------------------
  SSH            22 My IP       Secure remote administration
  HTTP           80 0.0.0.0/0   Public web access
  HTTPS         443 0.0.0.0/0   Allow HTTPS web traffic

SSH was restricted to the administrator's IP instead of being exposed to
the entire Internet.

## Apache Installation

The following commands were used:

``` bash
sudo dnf update -y
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

The Apache service was confirmed to be:

``` text
Active: active (running)
```

## Testing

The EC2 Public IPv4 address was opened in a browser using HTTP.

The Apache test page loaded successfully, confirming that:

-   EC2 was reachable
-   Apache was running
-   Port 80 was allowed by the Security Group

## HTTPS Note

Port 443 was allowed in the Security Group as required by the
assignment. A fully working HTTPS endpoint would additionally require
TLS/certificate configuration. The completed web-server test was
performed over HTTP.

## Result

The Amazon Linux EC2 web server was successfully deployed and Apache was
successfully installed, started, enabled, and tested.

------------------------------------------------------------------------

# Question 3 -- DynamoDB Student Management System

## Objective

Create a DynamoDB table for student records and demonstrate insert,
retrieve/query, update, and delete operations.

## AWS Service Used

-   Amazon DynamoDB

## Architecture

``` text
User / Administrator
        |
        v
AWS Management Console
        |
        v
Amazon DynamoDB
        |
        v
StudentManagement Table
        |
        +-- StudentID (Partition Key)
```

## Table Configuration

  Setting         Value
  --------------- ---------------------
  Table Name      `StudentManagement`
  Partition Key   `StudentID`
  Data Type       String
  Sort Key        None

`StudentID` was selected as the partition key because it uniquely
identifies each student and allows efficient retrieval of individual
student records.

## Insert Operation

Three student records were inserted.

Example records:

-   `STU001`
-   `STU002`
-   `STU003`

Each item contained student information such as name, course, age and
other attributes.

## Retrieve / Query Operation

A DynamoDB Query operation was performed using:

``` text
StudentID = STU001
```

The query successfully returned the matching student record.

## Update Operation

The `STU001` record was updated.

The Age attribute was updated to:

``` text
21
```

The updated value was verified in the table.

## Delete Operation

The `STU003` record was selected and deleted.

After deletion, the table was refreshed and `STU003` was no longer
present.

## Result

The DynamoDB Student Management System successfully demonstrated:

-   Table creation
-   Item insertion
-   Item retrieval using Query
-   Item update
-   Item deletion

------------------------------------------------------------------------

# Testing Summary

  Question   Test                        Result
  ---------- --------------------------- --------
  Q1         Open CloudFront HTTPS URL   Passed
  Q2         Open EC2 Public IPv4        Passed
  Q2         Verify Apache service       Passed
  Q3         Query STU001                Passed
  Q3         Update STU001               Passed
  Q3         Delete STU003               Passed

------------------------------------------------------------------------

# Screenshots

All evidence screenshots are stored separately in the `screenshots`
folder.

Recommended organization:

``` text
AWS-Project-Set-5/
│
├── README.md
│
└── screenshots/
    │
    ├── Q1_S3_Objects.png
    ├── Q1_CloudFront_General.png
    ├── Q1_CloudFront_Behavior.png
    ├── Q1_CloudFront_Test.png
    │
    ├── Q2_EC2_Instance.png
    ├── Q2_Security_Group.png
    ├── Q2_Apache_Status.png
    ├── Q2_Apache_Test.png
    │
    ├── Q3_DynamoDB_Table.png
    ├── Q3_DynamoDB_Insert.png
    ├── Q3_DynamoDB_Query.png
    ├── Q3_DynamoDB_Update.png
    └── Q3_DynamoDB_Delete.png
```

## Screenshot Evidence

### Question 1

-   `Q1_S3_Objects.png` -- S3 bucket containing website files
-   `Q1_CloudFront_General.png` -- CloudFront configuration and default
    root object
-   `Q1_CloudFront_Behavior.png` -- HTTP to HTTPS redirect
-   `Q1_CloudFront_Test.png` -- Working CloudFront website

### Question 2

-   `Q2_EC2_Instance.png` -- Running EC2 instance
-   `Q2_Security_Group.png` -- Security Group inbound rules
-   `Q2_Apache_Status.png` -- Apache service running
-   `Q2_Apache_Test.png` -- Apache test page

### Question 3

-   `Q3_DynamoDB_Table.png` -- DynamoDB table configuration
-   `Q3_DynamoDB_Insert.png` -- Inserted student records
-   `Q3_DynamoDB_Query.png` -- Query result
-   `Q3_DynamoDB_Update.png` -- Updated student record
-   `Q3_DynamoDB_Delete.png` -- Record deletion verification

------------------------------------------------------------------------

# Final Result

All three AWS projects were successfully implemented and tested.

-   **Q1:** S3 + CloudFront static website -- Completed
-   **Q2:** Amazon Linux EC2 + Apache web server -- Completed
-   **Q3:** DynamoDB Student Management System -- Completed

The `screenshots` folder contains the supporting evidence for each
implementation and testing step.
