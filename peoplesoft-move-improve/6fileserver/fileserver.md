# Setting Up File Storage System

## Introduction
This lab walks you through the steps to setting up your file server for PeopleSoft Cloud Manager.

Estimated Lab Time: 45 minutes

### About File Storage Service (FSS)
The PeopleSoft Cloud Manager file server is used with the Cloud Manager Repository feature to automatically download updates. You use the Cloud Manager Infrastructure Settings page to create a File Storage service file system.

The file system created in File Storage service is a cluster file system for managing general purpose file data stored outside an Oracle Database. The file system is accessed through a mount target. The file system must have at least one export in one mount target in order for instances to mount the file system.
The mount target provides the IP address or DNS name that is used in the mount command when connecting NFS clients to a file system. A single mount target can export many file systems. The export path controls how NFS clients access file systems when they connect to a mount target.

For more detailed explanations of the File Storage service concepts, see [Overview of File Storage](https://docs.oracle.com/en-us/iaas/Content/File/Concepts/filestorageoverview.htm) in the Oracle Cloud Infrastructure documentation.

### Objectives

The purpose of this lab is to give you an overview of the IAM Service components and an example scenario to help you understand how they work together.

In this lab, you will:
* Create a Mount Target on OCI
* Use existing Mount Target to create a File System in Cloud Manager


### Prerequisites

* Oracle Cloud Infrastructure account credentials (User, Password, and Tenant)



## Task 1: Creating a Mount Target

Sign back into the OCI Console if not already logged in. 

1. Navigate to the three-line menu on the top -> **Storage** -> **Mount Targets**.

    ![Navigate to the three-line menu on the top, click Storage and then Mount Targets](./images/navmt.png " ")

2. Ensure that you're in the **Demo** compartment by using the dropdown on the left. Then, click **Create Mount Target**
    
    ![Select the demo compartment from the left and click on create mount targets](./images/createmt.png " ")

3. Now fill out the required **Mount Target Information**
    * New Mount Target Name: **psft-mount-target**
    * Availability Domain: **____AD-1**
    * Virtual Cloud Network: **psftvcn**
    * Subnet: **cm(Regional)**
    
    ![Provide all information required for creating the mount target](./images/mtinfo.png " ")
    Click **Create**
4. You should see a dialog box pop up saying that it has successfully been created. Go ahead and click **View Details**
    
    ![click on view details to check the mount target created](./images/viewdetails.png " ")
    ![view mount target information on the console ](./images/mtcreated.png " ")

## Task 2: Refreshing OCI Metadata in Cloud Manager

1. In Cloud Manager, go to **Cloud Manger Settings**

    ![In Cloud Manager, go to Cloud Manger Settings](./images/cmsettings.png " ")

2. On the left, click **Infrastructure Settings**
   
    ![On the left, click Infrastructure Settings](./images/refresh.png " ")

3. The messages should change to **OCI metadata refresh is in progress. Check status through process monitor page.**

    ![The messages should change to OCI metadata refresh is in progress. Check status through process monitor page](./images/inprogress.png " ")

4. You may need to refresh the page. You may move onto Task 3 once you see that the refresh has been successful with a recent timestamp.
    
    ![You may need to refresh the page to have it successful](./images/successful.png " ")

## Task 3: Configuring File Server
1. On the left side, navigate down to File Server

    ![On the left side, navigate down to File Server](./images/fileserver.png "")

2. Enter Mount Taget Information
    * Switch the radio button to **Yes** for **Use existing Mount Target**
    * Using the dropdown, select the Mount Taget we created: **psft-mount-target**
    
    ![Enter the Mount target inforamtion and click create](./images/mtsetup.png " ")

    Click **Create**.
    
3. Refresh the page and watch the Fss Status change to: **Creating File Storage Service**
    
    ![Refresh the page and watch the Fss Status change to: Initiating File Storage Service](./images/initiating.png " ")

## Task 4: Monitoring File Server Configuration

The following are screenshots of monitoring the progress of the File Server creation.
1. Example of **More Info** in progress

    ![Click on More info to check the progress](./images/moreinfo.png " ")

2. Navigate to **Logs** on the left, then use the dropdown to change the **Log Directory**, choose the **Log File** you wish to see, and put a higher value in **No of lines** to view more and then click **Fetch Logs** like so:

    ![click on logs to check the status of the FSS](./images/logs.png " ")

3. On the Mount Target Details page on the OCI Console, you'll see the Export Path has been created. (Use the 3-line menu on the top, **Storage** --> **Mount Targets**. Select the mount target we created: **psft-mount-target** to view the details)

    ![OCI console shows the MT targets created](./images/exportpath.png " ")

4. The file server should be created within 10 minutes. ‘**FSS Configured**' will appear when the File Server has completed configuring

    ![The FSS is configured](./images/configured.png " ")



 Please wait until the file server status shows ‘**FSS Configured**' to continue.


You may now **proceed to the next lab.**


## Acknowledgements
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect; Megha Gajbhiye, Principal Cloud Architect
<<<<<<< HEAD:peoplesoft-move-improve/peoplesoft-move-improve/6fileserver/fileserver.md
* **Last Updated By/Date** - Ziyad Choudhury, Principal Cloud Architect, August 2023
=======
* **Last Updated By/Date** - Deepak Kumar M, Principal Cloud Architect, March 2023
>>>>>>> upstream/main:peoplesoft-move-improve/7fileserver/fileserver.md
