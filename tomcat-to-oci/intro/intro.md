# Introduction

## About this Workshop

This tutorial will walk you through the process of migrating an existing on-premises Apache Tomcat application to Oracle Cloud Infrastructure (OCI). The Tomcat application we will migrate is a Java application with a datasource connecting to a database that will be migrated to Oracle Autonomous Database on OCI alongside the application.

Estimated Completion Time: 80 minutes.

### About Product/Technology

- Apache Tomcat is an open source Java application server.
- Terraform is an open source engine to deploy infrastructure-as-code and is used to deploy the network, compute and database resources.

The reference architecture looks like the following:

!["architecture"](./images/architecture-deploy-tomcat.png "architecture")

### Objectives

Perform the end-to-end migration of a Tomcat application to OCI with an Oracle Autonomous Database, provisioning with Terraform.

In this tutorial, you will:
- Provision a demo environment to use as the 'on-premises' environment to be migrated.
- Provision a Tomcat cluster on OCI, with an Oracle Autonomous Database with Terraform.
- Migrate the application database from the 'on-premises' environment to the Oracle Autonomous Database.
- Migrate the application to the Tomcat deployment on OCI.
- Optionally learn to scale the Tomcat cluster.
- Tear down the workshop.

### Prerequisites

In order to run this workshop you need:

* A Mac OS X, Windows or Linux machine (on Windows, use the Windows Linux Subsystem)
* An SSH key pair
* Firefox browser
* A OCI account with a Compartment set up
* Git installed
* Terraform 0.12 installed

## Acknowledgements

 - **Author** - Subash Singh, Emmanuel Leroy, October 2020
 - **Last Updated By/Date** - Emmanuel Leroy, October 2020
