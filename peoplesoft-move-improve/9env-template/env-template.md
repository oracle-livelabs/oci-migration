# Creating New Environment Template

## Introduction

This lab walks you through the steps to create a new environment template from the previously downloaded PeopleSoft Image

Estimated Lab Time: 20 minutes

### Objectives
The purpose of this lab is to show you how to create a new environment template from a downloaded PeopleSoft Image in order to create a new PeopleSoft Environment.

In this lab, you will:
* Create a new environment template

Let's take a look at the Network Topology again, so we can understand what we are configuring.

We have already provisioned Cloud Manager in a private subnet (cm) and the Bastion in a private subnet (bastion). We created a template of 2 nodes:
* Linux Full Tier in private subnet (ft)
* PeopleSoft Client in private subnet (win)


![PeopleSoft CM deployed Architecture](./images/architecture.png "")

### Prerequisites
- A PeopleSoft Cloud Manager Instance
- A downloaded PeopleSoft Image

## Task 1: Creating the HCMVault password group. 
Navigate to Cloud Manager Dashboard ->  **My Settings**
![Dashbaord My Settings](./images/Mysettings.png "")

Select **Password Group**

Select **Add New Group**
![Password Group](./images/Password_Group.png "")


Create Group Name **HCMVault**

Description **PS HCM Vault Configuration**

Compartment of Vault **Demo**

Vault Name **PSVault**

Database Access Password **DBAccessPW**

Database Administrator Password **DBAdminPW**

Database Connect Password **DBConnectPW**

Database Operator Password **PS**

Gateway Administrator Password **IntegrationPW1**


![HCMVault Settings](./images/HCMVaultSettings.png "")

Web Profile Password for user PTWEBSERVER  **WewbprofilePW1**

Weblogic Adminstration Password  **WeblogicPW**

Windows Administrator Password **WinPW**

Select **Save**
![HCMVault additional Settings](./images/HCMVaultsettings2.png "")
## Task 2: Creating a New Environment Template and General Details

Navigate to Cloud Manager Dashboard -> **Environment Template**
    ![Navigate to Cloud Manager Dashboard  and then Environment Template](./images/dashtemp.png "")
 
Click **Add New Template** button.
    ![click on add new template button](./images/addtemp.png "")

1. Fill out the General Settings as follows:
    - Name: **PUMFT**
    - Description **HCM 9.2 FT: Linux and Windows node**
    ![Provide template name and description](./images/tempnamedescription.png "")

2. For Select PeopleSoft Image, click the **search icon**. Do NOT type anything. If your DPK was downloaded properly, it should appear in the Search Results. If you can't see it yet, please wait and refresh the page after awhile. Since we subscribed to the HCM channel in Lab 7, we see **PEOPLESOFT HCM UPDATE IMAGE 9.2.046 - NATIVE OS** 
    ![Search the PeopleSoft image from the search icon](./images/imagesearch.png "")
    ![The PSFT image results appear on screen](./images/hcmsearch.png "")

  Click **Next** when you have this:
    ![Enter all information and click next ](./images/tempname.png "")

## Task 3: Select Topology

1. Click the **search icon** and select **PUM Fulltier** for the topology
2. Expand **Custom Attributes** and select **PUM Fulltier** again from the drop down.
3. Select **HCMVault** from the Password group drop down.
3. Click on **Edit Custom Attributes**
    ![Select the PUM Fulltier and click on edit custom attributes](./images/selecttopv2.png "")
4. Fill in the Region and Availability Domains as follows:
    * Region: **us-phoenix-1**
    * Primary Availability Domain: **________-AD-1** (Depends on the AD you selected. In this case, we are using Phoenix)
    * Default Compartment: **Demo**
    * Default Virtual Cloud Network: **psftcm(Demo)** 
    
    ![Provide all the information for Region and AD](./images/regioninfo.png "")

5. Now, expand **Full Tier** > **General Settings**
    * Line 8-  Database Operator id: **PS**
    * Line 13- Database Name: **MYPUMDB** 
    ![General Settings](./images/gensettings.png "")

6. Now, expand **Full Tier** > **Network Settings**
    * Compartment: **Demo**
    * Virtual Cloud Network: **psftcm(Demo)**
    * Subnet For Primary Instance: **ft**
    ![Under the demo compartment select the subnet ft](./images/ftnetwork.png "")

7. Now, expand **PeopleSoft Client** > **Network Settings**
    * Compartment: **Demo**
    * Virtual Cloud Network **psftcm(Demo)**
    * Subnet For Primary Instance: **win**
    ![Under the demo compartment select the subnet win](./images/winnetwork.png "")

8. Scroll back up and click on **Validate Network**
    ![Click on validate button](./images/validatenetwork.png "")

  You should see something like this:
    ![The network validation is successful](./images/validationok.png "")

Click **Next**

## Task 4: Security and Policies

Now, we'll select the Zone and Role Names

1. Click the **search icon** for **Zone Name**
    ![Search for the zone by clicking the search icon](./images/searchzone.png "")

  Select **Test**
    ![Select the test zone from the list](./images/searchtest.png "")

2. Click the **search icon** for **Role Name**
    ![Click the search icon for Role name](./images/searchrole.png "")

  Expand the **Search Criteria** at the top, type in **PACL\_CAD**, and click **Search**
    ![Type PACL_CAD on the search criteria](./images/searchrole1.png "")
  Select **PACL\_CAD**
    ![Select PACL_CAD from the search criteria](./images/searchrole2.png "")

When you see this, click **Next**
  ![Click on next after verifying the values](./images/17next.png "")


## Task 5: Summary

Review the Environment Template and click **Submit**
    ![Click on submit after verifying the values](./images/submit.png "")

You should now see your Environment Template here:
    ![The environment template is now created](./images/finishedtemp.png "")


You may now **proceed to the next lab.**


## Acknowledgements
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect; Megha Gajbhiye, Principal Cloud Architect
* **Last Updated By/Date** - Ziyad Choudhury, Principal Cloud Architect, August 2023

