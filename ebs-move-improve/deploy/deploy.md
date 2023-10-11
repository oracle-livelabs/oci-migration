# Oracle E-Business Suite Cloud Manager Deployment and Configuration

## Introduction
In this lab, we will deploy the Oracle E-Business Suite Cloud Manager using the Marketplace Application:
Oracle E-Business Suite Cloud Manager Stack for Demos.

Estimated Lab Time: 30 minutes

<!--
Watch this short video to preview how to deploy your Oracle E-Business Suite Cloud Manager.

[](youtube:vzIJ4LFOi0s)
-->

### **Objectives**

* Deploy and Configure Oracle E-Business Suite Cloud Manager
* Verifying login into Oracle E-Business Suite Cloud Manager

### **Prerequisites**

* Tenancy Admin User
* Tenancy Admin Password
* Lab 1 for preparing your tenancy completed with your IAM with Identity Domains information documented in your key-data.txt file.
    * `Cloud_Manager_Admin_Username`
    * `Cloud_Manager_Admin_Password`
    * `Client_Tenant`
    * `Client_ID`
    * `Client_Secret`

## Task 1: Sign in to the Oracle Cloud Infrastructure Console

Use the tenancy administrator credentials to sign in to Oracle Cloud Infrastructure console.

1. Reference your ``key-data.txt`` file and locate the tenancy administrator credentials.

2. Sign in to the Oracle Cloud Infrastructure console using the following:

    * **User name**: ``Tenancy Admin User``
    * **Password**: ``Tenancy Admin Password``

## Task 2: Deploy and Configure Oracle E-Business Suite Cloud Manager

You will now deploy an E-Business Suite Cloud Manager using a Marketplace stack. The stack creates the following cloud resources:

  - A compartment to contain resources required by Oracle E-Business Suite Cloud Manager.

  - An EBS Cloud Manager Administrators IAM user and group, as well as the policies required to manage the compartment.

  - Network resources – including a VCN, an internet gateway, subnets, route tables, security lists, and security rules.

  - A Compute instance for running the Oracle E-Business Suite Cloud Manager.

Then, the stack will configure Oracle E-Business Suite Cloud Manager to work with your OCI tenancy and the newly created OCI resources.

1. In the Oracle Cloud Infrastructure console navigation menu, under **Marketplace** select **All Applications**.

  ![This screenshot depicts the navigation to All Applications within the Oracle Cloud Infrastructure console navigation menu.](./images/1.png " ")

2. From the Marketplace applications page:

    a. Select **Stack** under Filter > Type

    b. In the search bar type "E-Business Suite"

    c. Click the application **Oracle E-Business Suite Cloud Manager Stack for Demos**

    ![This screenshot shows the Marketplace applications page and the Oracle E-Business Suite Cloud Manager Stack for Demos which must be selected.](./images/2.png " ")

3. In the version drop-down list, ensure that the default is selected.

4. In the Compartment drop-down list, select the parent compartment of the compartment where the Oracle E-Business Suite Cloud Manager Compute instance will be deployed. For example, mycompanytenancy(root).

5. Review and accept the Terms of Use.

6. Click **Launch Stack**.

  ![This screenshot shows the Oracle E-Business Suite Cloud Manager Stack for Demos in the Marketplace and highlights the Version drop-down list and the check box which must be selected to accept the Terms of Use.](./images/3.png " ")

7. On the Stack Information screen, enter the following values:

    a. **Name**: (default: Oracle E-Business Suite Cloud Manager Stack for Demos-<date&time>)

    b. **Description**: Add a description for the stack

    c. The last two variables should be greyed out.

      1. **Compartment**: (the one chosen previously)

      2. **Terraform Version**: 0.12.x

    d. Click **Next**.

    ![This screenshot shows the Create Stack page and within the Stack Information section, highlighted are the Name field, Description field, and the Next button.](./images/4.png " ")

8. On the Configure Variables screen, enter the following values:

    a. **Resource Prefix**: ``ebshol``

      - Note: This value must be a unique identifier to your tenancy.

    b. **Single Compartment Setup**: Make sure it is checked.

    c. **Parent Compartment**: Select your compartment as the parent compartment for your resources.

    d. **EBS Cloud Manager Administrator Username**: ``ebscm.admin@example.com``

    e. **EBS Cloud Manager Administrator Email**: This can be a personal email account.

    f. **Create New REST API key**: Make sure it is checked.

    ![This screenshot shows the Create Stack page and within the Configure variables section, shows the Setup Details and the EBS Cloud Manager Administrator Details which must be completed.](./images/5.png " ")

    g. **Server Host for EBS Cloud Manager Login URL**: ``myebscm.ebshol.org``

    h. **EBS Cloud Manager Shape**: ``VM.Standard.E2.2``

    i. **EBS Cloud Manager Admin Password**:
      - Note: This password is what will allow you to login to the cloud manager instance that is created and **CAN** be different than the user password for logging into the OCI Console.
      - Add this password to your ``key-data.txt`` file.

    j. **Public Key**:

      1. Use an existing or generate a new ssh key. Paste the public key pair.

      For more information on ssh keys, visit: [Generating an SSH Key Pair](https://www.oracle.com/webfolder/technetwork/tutorials/obe/cloud/compute-iaas/generating_ssh_key/generate_ssh_key.html)

    k. **EBS Cloud Manager Availability Domain**: Choose the availability domain that ends in **-1** from the list.

      ![This screenshot shows the Create Stack page and within the Configure variables section, shows the EBS Cloud Manager Instance Details which must be completed.](./images/6.png " ")

    l. **Custom CIDR Ranges**: Leave unchecked.

    m. **EBS Cloud Manager Access CIDR**: ``0.0.0.0/0``

    n. Enter the values from the ``key-data.txt`` file as shown below.

      1. **IDCS Client ID**: `Client_ID`

      2. **IDCS Client Secret**: `Client_Secret`

      3. **IDCS Client Tenant**: `Client_Tenant`

    o. Click **Next**.

    ![This screenshot shows the Create Stack page and within the Configure variables section, shows the EBS Cloud Manager Network Details and the IDCS Details which must be completed.](./images/7.png " ")

9. On the Review screen, verify the information, and click **Create**.

  ![This screenshot shows the Review section withing the Create Stack page. This screen is where you must verify the information entered to create the stack.](./images/8.png " ")

10. This takes you to the Stack Details page for your newly created stack. You will notice that the job status will cycle through **Accepted**, **In Progress**, and **Succeeded**. This will take some time to complete.

  ![This screenshot is of the Stack Details page of the newly created stack.](./images/9.png " ")

  After the job succeeds, you will have all the network resources (VCN, load balancer, subnets, and so on) required to deploy the Oracle E-Business Suite Cloud Manager Compute instance.

11. You will find the details related to the EBS Cloud Manager Instance and Load Balancer at the bottom of your log output as shown below:

  Copy and paste **Private IP**, **Public IP**, **Login URL**, and **LB Public IP** to the equivalent fields in your ``key-data.txt`` file. These variables are needed for the remainder of the procedures in this lab.

  ![This screenshot is of the stack log output, highlighting the private IP, public IP, login URL, and load balacer public IP information that you must note in your key-data.txt file.](./images/11.png " ")

## Task 3: Log in to Oracle E-Business Suite Cloud Manager

Before logging into the Oracle E-Business Suite Cloud Manager web application, you need to add the **hostname** in the Login URL to your local computer hosts file.

Follow the instructions below to perform this configuration:

Edit the local ``hosts`` file on your laptop and add an entry.

**For Windows users**

  1. Navigate to Notepad in your start menu.

  2. Hover over Notepad, right-click, and select the option **Run as Administrator**.

  3. In Notepad, navigate to ``File > Open``.

  4. Browse to ``C:\\Windows\System32\drivers\etc``.

  5. Find the file "hosts".

      ![This screenshot depicts the navigation to the hosts file within Windows Explorer. ](./images/12.png " ")

  6. In the hosts file, scroll down to the end of the content.

  7. Add the following entry to the very end of the file: ``<lb_public_ip> myebscm.ebshol.org``

  8. Save the file.

**For Mac users**

  1. Open a Terminal Window.

  2. Enter the following command:

    ```
    <copy>
    sudo vi /etc/hosts
    </copy>
    ```

  This will then require your local computer password to edit the file. Enter the password and you should see a screen similar to the one shown below.

  3. Type 'i' to edit the file.

  4. Go to the last line and add the following entry as show below: ``<lb_public_ip> myebscm.ebshol.org``

  5. Once you have finished editing the file, hit 'esc' and type ':wq' to save and exit.

  ![This screenshot shows how to edit the hosts file on a Mac.](./images/13.png " ")

Type the Login URL generated and documented to your ``key-data.txt`` previously into your browser.

Log into the Oracle E-Business Suite Cloud Manager using your IDCS credentials for the EBS Cloud Manager account as documented in your ``key-data.txt`` file.

  Note: It may take some additional time for the load balancer to be properly configured. Sometimes it may take up to 30 minutes or an hour to configure. If you would like to check on the status of the load balancer,  in OCI go to **Networking** > **Load Balancers** and then check the **Overall Heatlh** status. If it is OK, the connection can be established. 

  Note: If your login URL is not working or if your compute instance which contains the Cloud Manager image was ever stopped/turned off you may need to check and see if the application is running. The command for this can be found in the Lab "Optional: Managing the EBS Cloud Manager Virtual Machine."

  Note: Your browser may give you an error when attempting to access the EBS Cloud Manager. If you run into an error using the EBS login URL try using a different browser or an incognito session. If this does not solve the problem, try adding ``:443`` after the url (i.e. ``https://myebscm.ebshol.org:443``).

  ![This screenshot is of the Oracle Cloud Account Sign In page.](./images/14.png " ")

Once logged in, you are on the **Environments page**.

  ![This screenshot is of the Environments page within the Oracle E-Business Suite Cloud Manager user interface.](./images/15.png " ")

You may now proceed to the next lab.

## Acknowledgements

* **Authors:** 
  * Quintin Hill, Cloud Engineering
  * Vijay Kumar Vudari Satyanarayana, Principal Cloud Architect
  * Danish Ansari, Principal Cloud Architect

* **Contributors:** 
  - Santiago Bastidas, Product Management Director
  - William Masdon, Cloud Engineering
  - Mitsu Mehta, Cloud Engineering
  - Chris Wegenek, Cloud Engineering
* **Last Updated By/Date:** Tiffany Romero, EBS Documentation, May 2023


