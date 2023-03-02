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

## Task 1: Creating a New Environment Template and General Details

Navigate to Cloud Manager Dashboard -> **Environment Template**
    ![Navigate to Cloud Manager Dashboard  and then Environment Template](./images/dashtemp.png "")
 
Click **Add New Template** button.
    ![click on add new template button](./images/addtemp.png "")

1. Fill out the General Settings as follows:
    - Name: **PUMFT**
    - Description **HCM 9.2 FT: Linux and Windows node**
    ![Provide template name and description](./images/tempnamedescription.png "")

2. For Select PeopleSoft Image, click the **search icon**. Do NOT type anything. If your DPK was downloaded properly, it should appear in the Search Results. If you can't see it yet, please wait and refresh the page after awhile. Since we subscribed to the HCM channel in Lab 7, we see **PEOPLESOFT HCM UPDATE IMAGE 9.2.40 - NATIVE OS** 
    ![Search the PeopleSoft image from the search icon](./images/imagesearch.png "")
    ![The PSFT image results appear on screen](./images/hcmsearch.png "")

  Click **Next** when you have this:
    ![Enter all information and click next ](./images/tempname.png "")

## Task 2: Select Topology

1. Click the **search icon** and select **PUM Fulltier** for the topology
2. Expand **Custom Attributes** and select **PUM Fulltier** again from the drop down.
3. Click on **Edit Custom Attributes**
    ![Select the PUM Fulltier and click on edit custom attributes](./images/selecttopv2.png "")
4. Fill in the Region and Availability Domains as follows:
    * Region: **us-ashburn-1**
    * Primary Availability Domain: **________-AD-1** (Depends on the AD you selected. In this case, we are using Ashburn)
    * Default Compartment: **Demo**
    * Default Virtual Cloud Network: **PSFTVCN(Demo)** 
    
    ![Provide all the information for Region and AD](./images/regioninfo.png "")

5. Now, expand **Full Tier** > **General Settings**
    * Line 6- Database Name: **MYPUMDB**
    * Line 9- Database Operator Id: **PS**
    ![Enter the Database name and operator id](./images/gensettings.png "")

6. Now, expand **Full Tier** > **Network Settings**
    * Compartment: **Demo**
    * Subnet For Primary Instance: **ft**
    ![Under the demo compartment select the subnet ft](./images/ftnetwork.png "")

7. Now, expand **PeopleSoft Client** > **Network Settings**
    * Compartment: **Demo**
    * Subnet For Primary Instance: **win**
    ![Under the demo compartment select the subnet win](./images/winnetwork.png "")

8. Scroll back up and click on **Validate Network**
    ![Click on validate button](./images/validatenetwork.png "")

  You should see something like this:
    ![The network validation is successful](./images/validationok.png "")

Click **Next**

## Task 3: Security and Policies

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


## Task 4: Summary

Review the Environment Template and click **Submit**
    ![Click on submit after verifying the values](./images/submit.png "")

You should now see your Environment Template here:
    ![The environment template is now created](./images/finishedtemp.png "")


You may now **proceed to the next lab.**


## Acknowledgments
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect 
* **Last Updated By/Date** - Deepak Kumar M, Principal Cloud Architect, March 2023

