# Introduction

## About this Workshop

WildFly is the open source version of the well-known JBoss web server.

This lab will walk you through the process of migrating an existing on-premises JBoss application to WildFly on Oracle Cloud Infrastructure (OCI). The application we will migrate is a Java application with a datasource connecting to a database that will be migrated to Oracle Autonomous Database on OCI along with the application.

Estimated Lab Time: 80 minutes

### About Product/Technology

- WildFly is the open source version of the well-known JBoss Java application server.
- Terraform is an open source engine to deploy infrastructure-as-code and is used to deploy the network, compute and database resources.

The reference architecture looks like the following:

![](./images/architecture-wildfly-oci.png)

### Objectives

*Perform the end-to-end migration of a JBoss/WildFly application to Oracle Cloud Infrastructure (OCI) with an Oracle Autonomous Database, provisioning with terraform.*

In this lab, you will:
- Provision a demo environment to use as the on-premises environment to be migrated.
- Provision a JBoss/WildFly cluster on OCI, with an Autonomous Database with Terraform.
- Migrate the application database from the on-premises environment to the Oracle Autonomous Database.
- Migrate the application to the JBoss/WildFly deployment on OCI.
- Optionally learn to scale the JBoss/WildFly cluster.
- Tear down the workshop.

### Prerequisites

In order to run this workshop you need:

* A Mac OS X, Windows or Linux machine.
* An SSH key-pair.
* Firefox browser.
* A OCI account with a Compartment setup.
* Git installed.
* Terraform 0.12 installed.

You may proceed to the next lab.

## Acknowledgements

 - **Author** - Subash Singh, Emmanuel Leroy
 - **Last Updated By/Date** - Emmanuel Leroy, May 2021
