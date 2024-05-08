# Set Up the Landing Zone

## Introduction

In this lab, you will deploy a Terraform-based landing zone template to your tenancy. This template meets the security guidance prescribed in the CIS Oracle Cloud Infrastructure Foundations Benchmark and fulfills Oracle E-Business Suite (EBS)-specific workload requirements.

Estimated Lab Time: 25 minutes

### About Oracle Cloud Infrastructure Marketplace Stacks

We will be using resource manager stacks available on the Oracle Cloud Infrastructure (OCI) Marketplace to deliver the templates. 

### Objectives

In this lab, you will:
* Set up a compartments structure,  administrative groups, and policies that make up the landing zone foundation.
* Set up the network required to deploy EBS workloads and EBS Cloud Manager.

### Prerequisites (Optional)

This lab assumes you have:
* An Oracle Cloud account
* All previous labs successfully completed

## Task 1: Sign in to the Oracle Cloud Infrastructure Console

Use the tenancy administrator credentials to sign in to Oracle Cloud Infrastructure (OCI) Console.

1. Reference your ``key-data.txt`` file and locate the tenancy administrator credentials.

2. Sign in to the Oracle Cloud Infrastructure console using the following:

    * **User name**: ``Tenancy Admin User``
    * **Password**: ``Tenancy Admin Password``


## Task 2: Create the Foundation

The following diagram depicts the compartment distribution based on CIS OCI Foundations Benchmark as well as the application compartment for EBS with its own internal distribution per category of environments.

![Diagram of the landing zone foundation.](images/tenancy-admin-diagram.png)

1. In the Oracle Cloud Infrastructre (OCI) Console navigation menu, under **Marketplace**, select **All Applications**.

2. From the Marketplace applications page:

    a. Navigate to **Filter**, then **Type**, and select **Stack**.

    b. In the search bar, enter "E-Business Suite".

    c. Click the application **Oracle E-Business Suite: Tenancy Admin Stack for Landing Zones**.

    d. In the **Version** drop-down list, ensure the default is selected. 
    
    e. In the **Compartment** drop-down list, select the root compartment.

    f. Review and accept the Terms of Use.

    g. Click **Launch Stack**.

3. On the Stack Information screen, enter the following values:

    a. **Name**: Default is Oracle E-Business Suite: Tenancy Admin Stack for Landing Zones-&lt;date&time&gt;.

    b. **Description**: Add a description for the stack.

    c. Click **Next**.

4. On the Configure Variables screen, enter the following values:

    a. **Landing Zone Prefix**: ``ebshol``

    b. **Parent Compartment**: Select your compartment as the parent compartment for your resources.

    c. **EBS workload environment categories**: Using the drop-down list, add the following categories - **Production**, **QA**

    d. Click **Next**.

5. On the Review screen, verify the information and click **Create**.

## Task 3: Create the Network

*Description here*
<!--Add image to describe what is being deployed-->

1. In the Oracle Cloud Infrastructre (OCI) Console navigation menu, under **Marketplace**, select **All Applications**.

	![Image alt text](images/sample1.png)

2. From the Marketplace applications page:

    a. Navigate to **Filter**, then **Type**, and select **Stack**.

    b. In the search bar, enter "E-Business Suite".

    c. Click the application **Oracle E-Business Suite: Network Admin Stack for Landing Zones**.

    d. In the **Version** drop-down list, ensure the default is selected. 
    
    e. In the **Compartment** drop-down list, select the ebshold-Network.

    f. Review and accept the Terms of Use.

    g. Click **Launch Stack**.

4. On the Stack Information screen, enter the following values:

    a. **Name**: Default is Oracle E-Business Suite: Network Admin Stack for Landing Zones-&lt;date&time&gt;.

    b. **Description**: Add a description for the stack.

    c. Click **Next**.

5. On the Configure variables screen, enter the following values:

    a. **Security compartment**: Select ``ebshol-Security`` from the drop-down list.

    b. **Workload identifier**: Select ``identity-ebshol-ebs`` from the drop-down list.

    c. Ensure **Create VCN** is selected (this is the default).

    d. Ensure **Configure EBS Cloud manager subnets** is selected by default.

    e. Select the **Public EBS Cloud Manager load balancer** checkbox. The EBS Cloud Manager instance subnet CIDR will auto-populate.

    f. Ensure **Create subnets for an EBS environment** is selected (this is the default).

    g. In the **Environment category identifier** drop-down list, select ``identity-ebshol-ebs-Production``. The application tier subnet and database tier subnet CIDRs will auto-populate.

    h. Select the **Create default load balancer tier subnet** checkbox. The Loadbalancer subnet CIDR will auto-populate.

    i. Select the **Create external load balancer and application tier subnets** checkbox. The external load balancer and external application tier subnet CIDRs will auto-populate. 

    j. In the Bastion section, ensure the **Create bastion subnet** and **Use bastion service** checkboxes are selected (this is the default). The Bastion allow list and Bastion TTL Limit will be prepopulated.

    k. Click **Next**.

6. On the Review screen, verify the information, and click **Create**.

## Learn More

* [Deploy a secure landing zone that meets the CIS Foundations Benchmark for Oracle Cloud](https://docs.oracle.com/en/solutions/cis-oci-benchmark/index.html)
* [Learn About Deploying Terraform Stacks for E-Business Suite and Cloud Manager](https://docs.oracle.com/en/solutions/deploy-landing-zone-e-business-suite-cm/learn-deploying-terraform-stacks-e-business-suite-and-cloud-manager1.html#GUID-CAA809AC-2A7F-40F9-96E9-493C2F388494)

## Acknowledgements
* **Author** - Santiago Bastidas, Product Management Director
* **Contributors** -  Terri Noyes, Product Management Director; Tiffany Romero, EBS Documentation
* **Last Updated By/Date** - Tiffany Romero, May 2024
