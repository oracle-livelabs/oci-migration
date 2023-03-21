# Migrate SOA Suite On-premises to SOA Suite Marketplace on Oracle Cloud Infrastructure

## Introduction

This lab will walk you through the process of migrating an existing 'on-premises' SOA Suite to SOA Suite on Marketplace for Oracle Cloud Infrastructure (OCI). SOA Suite on Marketplace, SOA Cloud Service, and Managed File Transfer (MFT) Cloud Service can be migrated manually following these steps. Side-by-side upgrade from one version to another follows the same process. 

Attached below is a sample architecture of the final solution:
![architecture](./images/architecture.png)

Estimated Lab Time: 90 minutes.

### Objectives

*Perform the end-to-end migration of a local SOA Suite to Oracle Cloud Infrastructure (OCI), provisioning SOA Suite on OCI with the Marketplace.*

In this workshop, you will:
- Provision a demo environment to use as the SOA 'on-premises' environment to be migrated.
- Prepare your OCI tenancy and the virtual network to deploy the target SOA Suite Marketplace on OCI environment.
- Provision the Operational Database on OCI, required to deploy SOA Suite Marketplace on OCI.
- Provision SOA Suite on OCI with the Marketplace.
- Upgrade the SOA on-premises application to be migrated to the latest version.
- Migrate the upgraded SOA on-premises application to SOA Suite on OCI.

>**Note:** This lab will only showcase migration of one application. For a complete guide to migrate SOA to SOA on OCI, refer to the **Learn More** section.


### Prerequisites

*In order to run this workshop you need:*

* A private/public SSH key-pair.
* Firefox browser (recommended as Chrome security may prevent you from loading HTTPS self-signed certificates).
* An OCI account.
* A Compartment in the tenancy with `manage all-resources` permission to provision the resources.
* A SSH key pair to connect to provisioned instances.

You may proceed to the next lab.

## Learn More

[Side-by-Side Upgrade for Oracle SOA Suite on Marketplace](https://docs.oracle.com/en/cloud/paas/soa-cloud/liftshift/migration-side-side-upgrade-soa-mp.html#GUID-6F77D620-0962-43A4-A503-A70E706C3D02)

## Acknowledgements

 - **Author** - Akshay Saxena, September 2020
 - **Last Updated By/Date** - Akshay Saxena, September 2020
