# Creating Identity and Access Management (IAM) Resources and OCI Vault

## Introduction
This lab walks you through the steps to prepare your Oracle Cloud Infrastructure Tenancy

Estimated Lab Time: 30 minutes

### About Identity and Access Management (IAM)
The Oracle Cloud Infrastructure (OCI) Identity and Access Management (IAM) Service allows you to control who has access to your cloud resources. You control the types of access a group of users has and to which specific resources. 

### Objectives

The purpose of this lab is to give you an overview of the IAM Service components and an example scenario to help you understand how they work together.

In this lab, you will:
* Sign-in to your OCI Tenancy to access the Console
* Manage access by creating 
    - Demo Compartment
    - OCI Group
    - Policies
    - New Local User


### Prerequisites

* Oracle Cloud Infrastructure administrator account credentials (User, Password, and Tenancy)

* To sign in to the Console, you need the following: 

    - Tenant, Username and Password
    - URL for the Console: [https://cloud.oracle.com] (https://cloud.oracle.com)
    - Oracle Cloud Infrastructure supports the latest versions of Google Chrome, Firefox, and Internet Explorer 11



## Task 1: Creating a Demo Compartment

**Compartments Overview:**
A compartment is a collection of cloud assets, like compute instances, load balancers, databases, etc. By default, a root compartment was created for you when you created your tenancy (ie, when you registered for the trial account). It is possible to create everything in the root compartment, but Oracle recommends that you create sub-compartments to help manage your resources more efficiently. If we were to begin creating a project on our desktops, we would first create a folder to house our project. This is essentially what we are doing on OCI.
More on compartments [here](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managingcompartments.htm)

1.	Sign into the OCI console and click on the three-line menu, which is located on the top left. Scroll down till the bottom of the menu, click on **Identity & Security** -> **Compartments**. 
    ![Click on the hamburger menu from top left and then identity & security and compartments](./images/oci-home-console.png " ")

2.  Click on the blue **Create Compartment** button to create a new one.

    ![Click on the create compartment button](./images/createcompartment.png " ")

3.	Give the Compartment a Name and Description 
    Copy the fields below
    Name:
    ```
    <copy>Demo</copy>
    ``` 
    Description:
    ```
    <copy>Demo</copy>
    ``` 

    Be sure your root compartment is shown as the parent compartment. Press the blue **Create Compartment button** when ready.

    ![Specify the detail to create the compartment](./images/compartment.png " ")

    You have just created a compartment for all of your work in this Test Drive.
    ![The page shows the compartment has been created](./images/compartmentdemo.png " ")

## Task 2: Creating a Group
**Group Overview:** 
A user's permissions to access services come from the group(s) to which they belong. More on groups [here](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managinggroups.htm)

1.	After creating the compartment, you should see the **Identity** column on the left. Under it, navigate to **Groups**. 
(Alternatively, you can go to the three-line menu on the top -> **Identity & Security** -> **Groups**.)

    ![Click on groups from the left side of the identity menu](./images/groupnav.png "")

2.	As you see here, we only have an Administrators group. OCI's best practices advise us to not rely on the Admins to create resources. 
Click **Create Group**.
    ![Click on create groups to proceed with group creation](./images/groupadd.png "")

3.	Give the Group a name and description
    Copy the fields below
    
    Name:
    ```
    <copy>oci-group</copy>
    ``` 
    Description:
    ```
    <copy>New group for OCI users</copy>
    ``` 

    Click **Create**

    ![Confirm the group creation on the OCI console](./images/creategroup.png "")

4.	Your new group is displayed.

    ![Group created can be seen on the OCI console](./images/newgroup.png "")
   
## Task 3: Creating a Policy
**Policies Overview**:
Policies define the permissions for a group Policies explain what actions members of a group can perform, and in which compartments. Users can access services and perform operations based on the policies set for the groups.
More on policies [here](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/policies.htm)

Now, let’s create a security policy that gives users in your group (oci-group), permissions to provision PeopleSoft Cloud Manager, in your assigned Compartment (Demo). 

1. Navigate to **Policies** under **Identity**. 
(Alternatively, you can go to the three-line menu on the top -> **Identity & Security** -> **Policies**.)
    
    ![Click on Policies under Identity ](./images/policynav.png "")    

2. On the left side, navigate to **COMPARTMENT** and select **ROOT compartment**. 

    ![select the root compartment](./images/compartmentselect.png "")

3. After you have selected the **ROOT** compartment, click **Create Policy**.

    Copy the fields below. Give the group a
        
    a) Name:
    ```
    <copy>Policy-for-oci-group</copy>
    ``` 
    b) Description:
    ```
    <copy>Policy for OCI Group</copy>
    ``` 
    c) Verify it's in the **root** compartment

    d) Toggle the radio button to **"Show manual editor"**

    ![Follow the OCI console to create the policy](./images/policybuilder.png "")

4. Add Policy Statements **Show manual editor**
    
    a) Enter the following Statements to the empty field:
    
    ```
    <copy>Allow group oci-group to manage all-resources in compartment Demo
    Allow group oci-group to read all-resources in tenancy
    Allow group oci-group to manage App-catalog-listing in tenancy
    Allow group oci-group to use tag-namespaces in tenancy</copy>
    ```  

    ![Follow the OCI console for policy builder screen](./images/finalpolicy2.png "")    

    b) Click **Create**.

    *NOTE*: If you used a different name for the group and/or compartment, then you'll need to adjust these statements accordingly.

## Task 4: Creating a User

Currently, we are signed in as an Administrator. Since we don't want Admins creating all the resources, we will create a **New User** that will install Cloud Manager.
   
1. Navigate to **Users** under **Identity**.
 Alternatively, you can go to the three-line menu on the top -> **Identity & Security** -> **Users**. 
2. Click **Create User**.
    ![Click on users under the identity menu](./images/usercreate.png "") 
3. Select **IAM user** on the right. This is crucial. Do *NOT* create an IDCS user.

    ![Select IAM user on the right](./images/useriam.png "")    

4. In the New User dialog box, copy the fields below to give the user a 
        
    a) Name:
    ```
    <copy>User02</copy>
    ``` 
    b) Description:
    ```
    <copy>User 02</copy>
    ``` 

    ![Confirm the screen to create the IAM user](./images/iam-user.png "")

5. Click **Create**.

## Task 5: Managing User

1. Now, let's set a password. Click **Create/Reset Password**.

    ![Click on create/reset password for the user](./images/userdetail.png "")

3. In the dialog, click **Create/Reset Password**.

    ![In the dialog, click create/reset password](./images/create-user.png "")

4. The new one-time password is displayed. Click the **Copy** button, save this in a notepad for later, and then click **Close**.
    
    ![Click the Copy button, save this password in a notepad](./images/newpassword.png "")

5. Scroll down and click on **Add User to Group**.

    ![Scroll down and click on Add User to Group](./images/scrolladdgroup.png "")

6. Select the group you just created, and click on **Add**.

    ![Select the group you just created, and click on Add](./images/adduser.png "")

7. Click on **top-right icon button** and **Sign out** of the admin user account.

    ![Click on top-right icon button and sign out](./images/signout.png "")

    This time, you will sign in using the local credentials box with the user you created. Note that the user you created is not part of the Identity Cloud Services.

8. Click **Oracle Cloud Infrastructure Direct Sign-In** 
    
    This will expand fields for non-federated accounts. Enter the username **User02** and the password that you copied to a note in step 4.

    ![Login to the OCI console using the direct sign-in option](./images/newsignin.png "")


    *Note*: Since this is the first-time sign-in, the user will be prompted to change the temporary password, as shown in the screen capture below.
    

9. Set the new password to **Psft@1234** (or create your own but be sure to note it down). Click on **Save New Password**. 
    ```
    <copy>Psft@1234</copy>
    ```
    ![Set the password of your choice](./images/changepassword.png "")


    You are now logged in as local user: **User02**

## Task 6: Setup API Keys for User02

You will need a pair of SSH Keys, as well as a pair of API keys. 

Generate them yourself:
* SSH Keys [https://docs.oracle.com/en/cloud/cloud-at-customer/occ-get-started/generate-ssh-key-pair.html](https://docs.oracle.com/en/cloud/cloud-at-customer/occ-get-started/generate-ssh-key-pair.html)
* API Keys [https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm)



    
1. Verify you have the following 4 keys ((key names can be same or different)): 
    * **API Signing keys**: ``api_key`` and ``api_key.pub``
    * **SSH key pair**: ``id_rsa`` and ``id_rsa.pub``

2. Now, go back to the OCI console where you should still be logged in as **User02**. Click on the **profile button on top right**. Click on your user name - **User02**.

    ![Click on user profile from the top right of the OCI console](./images/api.png "")

3. Scroll to the bottom, on the left side click on **API Keys** and then click on **Add Public Key**

    ![select API keys from the left side of the user menu](./images/apisetup.png "")

4. Click on **Paste public keys** and paste the contents of **api_key.public**. Click on **Add**.  

    ![Paste the api public key created earlier](./images/sampleadd.png "")


## Task 7: Set up OCI Vault, Encryptions and Secrets

You will need to create a vault.
In this workshop we will create the vault in the Demo compartment.
We will create Master Encryption key and vault secrets

1. On the Oracle Cloud Infrastructure Console home page, click the three-line menu (Menu icon) and select **Identity and Security**, then select **Vault**.
![select Vault from the Identity user menu](./images/createvault.png "")


2. Select the Demo Compartment and click the create **Vault** button
![create Vault in Demo Compartment](./images/vaultdemo.png "")


3. Create in Compartment **Demo** and name the Vault **PSVault**
![creation of vault PSVault](./images/psvault.png "")


4. Create the Encryption Key 

5. Select **Identity and Security --> Vault**
![Select vault PSVault](./images/vaultencrypt.png "")
 
6. Select  **Master Encryption Keys**

7. Select **Create Key**
![Create encryption key](./images/masterencrypt.png "")

8. Select Create in Compartment **Demo**

 Use Protection Mode **HSM**

 Name of Key **PSKey**

 Key Shape Algorithm  **AES (Symmetric key used for Encrypt and Decrypt)**

 Key Shape Length **256 bits**
9. Select **Create Key**
![Create encryption key PSKey](./images/pskey.png "")


10. Create Secrets. We need to create 11 Secrets

 Select **Create Secret** 
![Create Secret](./images/createsecret.png "")


11. Create Secret

## Task 8: Setup PeopleSoft Domain password secret

1. Create in Compartment **Demo**

2. Name the Secret **DomainPW2**

3. Use the Encryption Key **PSKey** . This Encryption key was created at an earlier step.

4. Secret Type Template **Plain-Text**

5. Secret Content **PSoft1234**

6. Select **Create Secret** button.

![Create Domain Password](./images/domainpw2.png "")


## Task 9: Setup PeopleSoft Web Profile user password secret

1. Create Secret

2. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

3. Create Secret in Compartment **Demo**

4. Name of the Secret  **WebprofilePW1**

5. Description **Web Profile user password**

6. Encryption Key **PSKey**

7. Secret Type Template **Plain-Text**

8. Secret Contents **PSoft1234**

9. Select **Create Secret** button

![Create Web Profile Secret](./images/webprofilepw1.png "")

## Task 10: Setup PeopleSoft Integration password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create Secret in **Demo** Compartment

3. Name  **IntegrationPW1**

4. Description **Integration Gateway User password**

5. Encryption Key in Demo Compartment **PSKey**

6. Secret Type Template **Plain-Text**

7. Secret Contents **PSoft1234**

8. Select **Create Secret Button**
![Create Integration Gateway User Password](./images/integrationpw1.png "")

## Task 11: Setup Cloud Manager Admin password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in **Demo** Compartment

3. Enter **CMAdminPW1** as the name of the secret.

4. Select **PSKey** as the encryption key.

5. Select **Plain-Text** as the Secret type template.

6. Enter **PSoft123** as the password

7. Select **Create Secret**
![Create CMAdminPW1](./images/cmadminpw1.png)

## Task 12: Setup Windows password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in Compartment **Demo** 

3. Name of the secret **WinPW**

4. Description **Windows Password**

5. Encryption Key **PSKey**

6. Secret Type  Template **Plain-Text**

7. Select **Create Secret** Button
![Create Windows Password](./images/winpw1.png)

## Task 13: Setup WebLogic password secret

1. Create in Compartment **Demo**

2. Provide a Name **WeblogicPW**

3. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

4. Provide this description **WebLogic Admin Password**

5. Encryption Key **PSKey**

6. Secret Type template **Plain-text**

7. Secret Contents type in **PSoft#1234**

8. Select **Create Secret** Button
![Create WebLogic Password](./images/weblogicpw.png)


## Task 14: Setup DB Admin password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in **Demo** Compartment

3. Name **DBAdminPW**

4. Description **DB Admin Password**

5. Encryption Key **PSKey**

6. Secret Type Template **Plain-Text**

7. Secret Contents **PSoft#1234**

8. Select **Create Secret** Button.
![Create Database Administrator Password](./images/dbadminpw1.png)

## Task 15: Setup DB Access Password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in Compartment **Demo**

3. Name **DBAccessPW**

4. Description **DB Access Password**

5. Encryption Key **PSKey**

6. Secret Type Template  **Plain-Text**

7. Secret Contents **Psoft123**

8. Select **Create Secret** Button
![Create Database Access Password](./images/dbaccesspw1.png)

## Task 16: Setup DB Connect password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in **Demo** Compartment.

3. Name **DBConnectPW**

4. Description **Database Connection Password** 

5. Encryption Key **PSKey**

6. Secret Type Template **Plain-Text**

7. Secret Contents **Psoft123**

8. Select **Create Secret** Button.
![Create Secret](./images/dbconnectpw1.png "")

## Task 17: Setup PeopleSoft User password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in Compartment **Demo**

3. Name **PS**

4. Description **PeopleSoft Additional Secret**

5. Encryption Key **PSKey**

6. Secret Type Template **Plain-Text**

7. Secret Contents **PS**

8. Select **Create Secret** Button.
![Create PeopleSoft Access Password](./images/ps1.png)

## Task 18: Setup SearchProxy password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in Compartment **Demo**

3. Name **SearchProxy**

4. Description **PeopleSoft Additional Secret**

5. Encryption Key **PSKey**

6. Secret Type Template **Plain-Text**

7. Secret Contents **Proxy$$1234**

8. Create SearchProxy Secret
![Create SearchProxy](./images/searchproxy.png "")

## Task 19: ElasticSearch password secret

1. Select **Create Secret** 
![Create Secret](./images/createsecret.png "")

2. Create in Compartment **Demo**

3. Name **ElasticSearch**

4. Description **PeopleSoft Additional Secret**

5. Encryption Key **PSKey**

6. Secret Type Template **Plain-Text**

7. Secret Contents **Elastic1234##One**

8. Create SearchProxy Secret
![Create SearchProxy](./images/elasticsearch.png "")


If you have MacOS Ventura you may run into SSH issues to access the LiveLabs PeopleSoft Deployment.
We may have to make minor modifications to the /etc/ssh/ssh_config file.

vi /etc/ssh/ssh_config 

You will need to authenticate with the admin password

scroll all the way to the bottom of the ssh_config file 

and the add the following lines to the bottom of the ssh_config file

**Hostkey Algorithms  +ssh-rsa** 

**PublickeyAcceptedAlgorithms  +ssh-rsa**

Go back up to the beginning of the file and uncomment and edit the following lines

**ForwardAgent yes** 

**ForwardX11 yes**

![Edit config_ssh](./images/ssh_config.png)



You may now **proceed to the next lab.**


## Acknowledgements
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect
* **Last Updated By/Date** - Ziyad Choudhury, Principal Cloud Architect, August 2023
