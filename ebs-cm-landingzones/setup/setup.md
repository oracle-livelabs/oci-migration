# Set Up the Landing Zone

## Introduction

*Describe the lab in one or two sentences, for example:* This lab walks you through the steps to ...

Estimated Lab Time: -- minutes

### About <Product/Technology> (Optional)
Enter background information here about the technology/feature or product used in this lab - no need to repeat what you covered in the introduction. Keep this section fairly concise. If you find yourself needing more than two sections/paragraphs, please utilize the "Learn More" section.

### Objectives

*List objectives for this lab using the format below*

In this lab, you will:
* Objective 1
* Objective 2
* Objective 3

### Prerequisites (Optional)

*List the prerequisites for this lab using the format below. Fill in whatever knowledge, accounts, etc. is necessary to complete the lab. Do NOT list each previous lab as a prerequisite.*

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

*Description here*

1. In the Oracle Cloud Infrastructre (OCI) Console navigation menu, under **Marketplace**, select **All Applications**.

	![Image alt text](images/sample1.png)

2. From the Marketplace applications page:

    a. Navigate to **Filter**, then **Type**, and select **Stack**.

    b. In the search bar, enter "E-Business Suite".

    c. Click the application **Oracle E-Business Suite: Tenancy Admin Stack for Landing Zones**.

    d. In the **Version** drop-down list, ensure the default is selected. 
    
    e. In the **Compartment** drop-down list, select the root compartment.

    f. Review and accept the Terms of Use.

    g. Click **Launch Stack**.

4. On the Stack Information screen, enter the following values:

    a. **Name**: Default is Oracle E-Business Suite: Tenancy Admin Stack for Landing Zones-<date&time>.

    b. **Description**: Add a description for the stack.

    c. Click **Next**.

5. On the Configure Variables screen, enter the following values:

    a. **Landing Zone Prefix**: ``ebshol``

    b. **Parent Compartment**: Select your compartment as the parent compartment for your resources.

    c. **EBS workload environment categories**: Using the drop-down list, add the following categories - **Production**, **QA**

    d. Click **Next**.

6. On the Review screen, verify the information, and click **Create**.

## Task 3: Create the Network

*Description here*

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

    a. **Name**: Default is Oracle E-Business Suite: Network Admin Stack for Landing Zones-<date&time>.

    b. **Description**: Add a description for the stack.

    c. Click **Next**.

5. On the Configure Variables screen, enter the following values:

    a. **Landing Zone Prefix**: ``ebshol``

    b. **Parent Compartment**: Select your compartment as the parent compartment for your resources.

    c. **EBS workload environment categories**: Using the drop-down list, add the following categories - **Production**, **QA**

    d. Click **Next**.

6. On the Review screen, verify the information, and click **Create**.

## Learn More

* [Learn About Deploying Terraform Stacks for E-Business Suite and Cloud Manager](https://docs.oracle.com/en/solutions/deploy-landing-zone-e-business-suite-cm/learn-deploying-terraform-stacks-e-business-suite-and-cloud-manager1.html#GUID-CAA809AC-2A7F-40F9-96E9-493C2F388494)

## Acknowledgements
* **Author** 
  - Santiago Bastidas, Product Management Director
* **Contributors** 
  -  Terri Noyes, Product Management Director
* **Last Updated By/Date** 
  - Tiffany Romero, May 2024
