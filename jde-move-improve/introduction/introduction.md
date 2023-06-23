# Introduction

## About This Workshop

This tutorial will serve as a foundation for the rest of the workshop and provide you with the tools necessary to complete the steps required to install JDE EnterpriseOne Release 23 Trial Edition on Oracle Cloud Infrastructure (OCI).

The workshop will also demonstrate how to deploy JD Edwards EnterpriseOne Release 23 Trial Edition to OCI.

Upon completion of this tutorial, you will have a working deployment of JD Edwards EnterpriseOne Trial Edition with Tools Release 9.2.7.3 and Applications Release 9.2 on a fully functional suite. You can use it to verify functionality and to investigate proofs of concept (POC).

Estimated Time: 2 hours (additional time may be needed for first-time users)

### About the Product/Technology

Trial Edition is for training and demonstration purposes only. It can be used to verify functionality and to investigate POC. The Trial Edition on OCI Compute contains only the Pristine (PS920) environment, which is one of the four standard JD Edwards EnterpriseOne environments.  

This single image is built using an Oracle Linux VM instance containing these JD Edwards EnterpriseOne servers:

* Enterprise Server

* Database Server

* HTML Web Server

* BI Publisher (BIP) Server

* Application Interface Service (AIS) Server


### Objectives

In this lab, you will:
* Request and obtain a trial OCI subscription.
* Generate an SSH Key for OCI connection.
* Deploy the JDE Trial Edition to OCI.
* Configure JDE Trial Edition.
* Sign in to JDE Trial Edition.


### Prerequisites

* OCI supports the latest versions of Google Chrome and Firefox (Firefox is preferred).
* Valid email address.
* Credit card: *You will not be charged*
* Phone (Oracle will send you an SMS based text message for verification purposes).
* *For Windows users only:* A Windows SSH utility is required to generate SSH key pairs on the client machine and to connect to the Linux based server using Secure Shell (SSH). We suggest either you either download and install the [PuTTY tool](http://www.putty.org/), or [Git BASH](https://gitforwindows.org/). Installation instructions are included in this tutorial.

## Summary

### JDE Trial Edition on Oracle Cloud Infrastructure Overview

JD Edwards EnterpriseOne is a comprehensive suite of integrated global business applications. The machine image provided by Oracle allows organizations to create a trial instance of JD Edwards EnterpriseOne Release 23 in the Oracle Compute Cloud. This 'All-in-One' Demo/Sandbox image enables customers to explore new functionality in JD Edwards EnterpriseOne Release 23, and Tools Release 9.2.7.3 without installing JD Edwards EnterpriseOne in their data centers. New functionality may include:

* New industry modules.
* One view financial statements.
* Internet of Things orchestrator.
* UX one content and foundation.

### Before You Begin

* It is desirable to have a fundamental understanding of the OCI.
* It is highly recommended that you review the extensive collateral information, including training, at these sites:
    * [Oracle Cloud Infrastructure](https://www.oracle.com/cloud/)
    * [LearnJDE](https://docs.oracle.com/cd/E84502_01/learnjde/cloud_overview.html)

* You must have sufficient resources in OCI to install and run JD Edwards EnterpriseOne Trial Edition.
* Minimum Shape: VMStandard2.2 (2 OCPUs and 30 GB memory).
* Recommended Shape: VMStandard2.4 (4 OCPUs and 30 GB memory).
* Boot Volume Storage of 120 GB.

At this point, you are ready to start creating instances in OCI.

## Acknowledgements
* **Author:** Tarani Meher, Principal JDE Specialist
* **Contributors:**
    * Jeff Kalowes, Principal JDE Specialist
    * Tarani Meher, Principal JDE Specialist
    * Mani Julakanti, Principal JDE Specialist
* **Last Updated By/Date:** Tarani Meher, Principal JDE Specialist, 06/2023