# Set Up Oracle Cloud Infrastructure for JDE Trial Edition Deployment

## Introduction

To establish proper access to a JD Edwards (JDE) Trial Edition, the Oracle Cloud Infrastructure (OCI) tenancy needs to be set up.

In this tutorial, the recently provisioned OCI Trial tenancy will be set up for JDE Trial Edition deployment.

Estimated Time: 10 minutes

### About Product/Technology

A compartment will be created to organize your tenancy. A compartment is essentially a folder within the OCI console. A virtual cloud network (VCN) will then be created. The Oracle VCNs provide customizable and private cloud networks on OCI. Lastly, security list rules for JDE, which are virtual firewall to control traffic at the packet level, will be created.

### Objectives

To set up the OCI tenancy, in this tutorial, you will:
*   Create a compartment.
*   Create a VCN.
*   Establish security list rules for JDE.

### Prerequisites

To have the greatest success in completing this tutorial make sure you have a general knowledge of OCI and its web interface.

## Task 1: Generate an SSH Key Pair

In this section you will generate a Secure Shell (SSH) key pair that you will use to connect to your instance.

**Note:**  If you have a previously generated key available, you can use that key and skip to **Create a Compartment**.

### For Mac/Linux

1. Generate ssh-keys for your machine if you don’t have one. If an id\_rsa and id\_rsa.pub key pair is present, they can be reused. By default, these are stored in ~/.ssh folder.

2. Enter the following command if you are using MAC or Linux Desktop:  

    ```
    # ssh-keygen
    ```

3. Make sure permissions are restricted, sometimes ssh will fail if private keys have permissive permissions. Enter the following command to ensure this:

    ```
    # chmod 0700 ~/.ssh  
    # chmod 0600 ~/.ssh/id_rsa  
    # chmod 0644 ~/.ssh/id_rsa.pub
    ```

### For Windows

There are many tools available for Windows users to create SSH key pairs and connect to a Linux server.  In this guide, we provide instructions for both Git Bash and Putty, but you only need to follow the steps below for either Git Bash *or* Putty, but not both.

### Git Bash:

1.  Install Git for windows if not already installed. Download the latest release of [Git](https://github.com/git-for-windows/git/releases/) for Windows and install, accepting all the default settings.

2.  Open Git Bash by either selecting the **Launch Git Bash** checkbox in the installer *or* by navigating to it from the Windows Start Menu:

    ![](./images/lab1-gitsetup.png " ")

    ![](./images/lab1-gitbash.png " ")

3.  Generate ssh-keys using the command `ssh-keygen` in Git Bash and then press “Enter” for all te steps:

        # ssh-keygen  

        Generating public/private rsa key pair. Enter file in which to save the key
        (/c/Users/username/.ssh/id_rsa): (Press enter for this step)
        Created directory '/c/Users/username/.ssh'.
        Enter passphrase (empty for no passphrase): (Press enter for this step)
        Enter same passphrase again: (Press enter for this step)
        Your identification has been saved in /c/Users/username/.ssh/id_rsa.
        Your public key has been saved in /c/Users/username/.ssh/id_rsa.pub

    **Note:**
     * In Git Bash, C:\Users\username\ is shown as /c/Users/username/
     * These instructions will create a minimally secure ssh key for you (and one well suited for this tutorial). For production environments we recommend an SSH-2 RSA key with 4096 bits and a passphrase. For example, ssh-keygen -t rsa -b 4096 -N "<myPassphrase>" -f ~/keys/id_rsa -C "This is my comment".

### Puttygen:

1.  Install Puttygen (PUTTY) for Windows if it is not already installed. Download the latest release of [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and the 64-bit MSI Installer and install, accepting all the default settings.

2.  Open PuTTYgen:

    ![](./images/lab1-puttygen.png " ")

3.  In the PuTTY Key Generator, ensure that the **Type of key to generate** is set to **RSA** and the number of bits in a generated key is set to **2048**, and then click the **Generate** button.

    ![](./images/lab1-puttykey.png " ")

4.  After clicking on **Generate**, move the mouse around the blank area to generate randomness for the SSH key to be generated.

    ![](./images/lab1-keygenerator.png " ")

5.  In the PuTTY Key Generator dialog box, select all the characters in the **Public key for pasting into OpenSSH authorized_keys file** field, and then right-click and select **Copy**.

    **Note:** Ensure that you select all the characters and not just the ones shown in the narrow window. Scroll down as necessary.

    ![](./images/lab1-copykey.png " ")

6.  Paste the copied string into a plain text editor (such as Notepad) and save the plain text file. Save it to a known location with any file name but ensure that it has the extension .pub (for example, OCISSHKey.pub) to indicate that it is a public key. Make note of this file name as you will need it later.

7.  Save the OpenSSH private key. In the same PuTTY Key Generator window, from the **Conversions** menu, select **Export OpenSSH key** option.

    ![](./images/lab1-exportkey.png " ")

8.  PuTTYgen will ask you to verify that the key will be saved without a passphrase. Click **Yes**.

    ![](./images/lab1-puttyyes.png " ")

9.  Save the file to the same known location with any file name but ensure that the file has no extension on it (for example, OCISSHKey). Make note of this file name as you will need it later.

10. Save the Windows private key. In the same PuTTY Key Generator window, click **Save private key**.

    ![](./images/lab1-puttyprivatekey.png " ")

11. Again, click **Yes** to verify saving the key without a passphrase.

12. Save this file to the same known location with any file name and a .ppk extension (for example, OCISSHKey.ppk).


## Task 2: Create a Compartment

In this part of the tutorial, we create a compartment to organize the resources we will create.

Compartments are the primary building blocks you use to organize your cloud resources. You use compartments to organize and isolate your resources to make it easier to manage and secure access to them.

When your tenancy is provisioned, a root compartment is created for you. Your root compartment holds *all* your cloud resources.

1.  Please log into to your OCI tenancy, if you are not already signed in. Example for Ashburn location:

    ```
    <copy>
    https://console.us-ashburn-1.oraclecloud.com/
    </copy>
    ```


2.  On the Oracle Cloud Console home page, click the navigation menu in the upper-left corner, select **Identity**, and then select **Compartments**.

    ![](./images/dropdown-menu.png " ")

    ![](./images/navigation-menu.png " ")

3.	Click **Create Compartment**.

    ![](./images/create-compartment.png " ")

4.  Choose a Name (for example, **TestDrive**), fill out the form and click **Create Compartment**.

    **Note:** The parent compartment should be the root compartment.

    ![](./images/test-drive.png " ")

## Task 3:  Create a VCN

1.	To create a VCN on OCI, on the Oracle Cloud Console home page, under **Quick Actions**, click **Set up a network with a wizard**.

    ![](./images/vcn-wizard.png " ")

2.	Select **VCN with Internet Connectivity**, and then click **Start VCN Wizard**.

    ![](./images/internet-connectivity.png " ")

3.  In this window, fill in the following fields with the information shown below:

    1. **VCN NAME:** TestDriveVCN (or any other unique name for the VCN)

    2. **COMPARTMENT:** TestDrive (or any other compartment previously created)

    3. **VCN CIDR BLOCK:** 10.0.0.0/16

    4. **PUBLIC SUBNET CIDR BLOCK:** 10.0.2.0/24

    5. **PRIVATE SUBNET CIDR BLOCK:** 10.0.1.0/24

    6. **USE DNS HOSTNAMES IN THIS VCN:** Make sure this is selected.

       ![](./images/dns-hostname.png " ")

4.  Then, scroll down to the bottom and click **Next**.

5.	On the Review and Create page, click on **Create**.

6.  On the Created Virtual Cloud Network page wait until you see the following graphic.

    ![](./images/creation-complete.png " ")

7.  Then click on **View Virtual Cloud Network**.

    ![](./images/vcn-button.png " ")


## Task 4:  Establish Security List Rules for JDE

With the VCN in place, define the open inbound and outbound ports that will be available to instances created within the VCN.

1.	From the details page of the TestDriveVCN, under the **Resources** section in the left pane, select **Security Lists**.

    ![](./images/security-lists.png " ")

2.	In the **Security Lists** section, click **Default Security List for TestDriveVCN** link.  

    ![](./images/default-security-list.png " ")

3.	On Default Security List, under **Resources** section, click **Add Ingress Rules**.
    ![](./images/ingress-rules.png " ")

4.  Set a new ingress rule with the following properties:
    1.  **STATELESS**: unchecked
    2.  **SOURCE TYPE**: CIDR
    3.  **SOURCE CIDR**: 0.0.0.0/0
    4.  **IP PROTOCOL**: TCP
    5.  **SOURCE PORT RANGE**: All
    6.  **DESTINATION PORT RANGE**: 443,7005-7006,7072,7077,9703,9705,8080
    7.  **DEESCRIPTION**: JDE Trial

    Click **Add Ingress Rules** when complete.
    ![](./images/ingress-rule-details.png " ")

    These Ingress Rules will be sufficient to allow the network traffic required for the JDE Trial Edition.

## Summary

In this tutorial, OCI has been set up for the networking required to be able to access a JDE Trial Edition that will be created in Create a Trial Edition Instance in Oracle Cloud Infrastructure.

## Acknowledgements
* **Author:** Tarani Meher, Principal JDE Specialist
* **Contributors:**
    * Jeff Kalowes, Principal JDE Specialist
    * Tarani Meher, Principal JDE Specialist
    * Mani Julakanti, Principal JDE Specialist
* **Last Updated By/Date:** Tarani Meher, Principal JDE Specialist, 03/2023
