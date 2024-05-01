# Introduction

## About this workshop

This workshop is an extension of previous workshop. It showcases the use of enabling OCI Logging Analytics to extend your EBS environment.

In order to complete this lab you will need the resources created in the [Lift and Shift On-Premises EBS to OCI](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=672&clear=180&session=5980193088668).


Estimated Workshop Time: 2 hours

### **Background**

This lab will leverage the EBS Cloud Manager and affiliated EBS Instances created in the main section of the EBS Lift and Shift Lab. We will now work to incorporate further use of OCI services to enhance our environment.

Notes:

* The workshop is quite detailed and technical. PLEASE take your time and DO NOT skip any steps.
* IP addresses and URLs in the screenshots in this workbook may differ from what you use in the labs as these are dynamically generated.
* For security purposes, some sensitive text (such as IP addresses) may be redacted in the screenshots in this workbook.

### Workshop Overview

* We will enable Logging Analytics to monitor and manage our technological footprint.

This workshop uses the following components: 

* Logging Analytics Service from OCI.

* Virtual Cloud Network and related resources.
    - User-generated using Resource Manager and provided Terraform script.

* Oracle E-Business Suite Cloud Manager and created EBS instances.

### Workshop Architecture

* We will build on top of the architecture created in the EBS Lift and Shift On-Premises EBS to OCI as seen in Figure W-1 below:

![Workshop Architecture Diagram](./images/architecturela.png " ")

### Objectives

In this lab, you will:
* Set up and use OCI Logging Analytics.

### **Prerequisites**

* Complete Workshop: [Lift and Shift On-Premises EBS to OCI](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=672&clear=180&session=5980193088668)
* Logging analytics requires ssh accessable instances, logging service, service connector, and logging analytics service.

**From the previous labs:**

* The IP addresses and SSH path of the instances in your environment.

You may now proceed to the next lab.

## Acknowledgements

* **Author:** Quintin Hill, Cloud Engineering
* **Contributors:** Kumar Varun, Logging Analytics Product Management 
* **Last Updated By/Date:** Nicholas Cusato, Taylor Rees, Stephen Stuart, January 2024
