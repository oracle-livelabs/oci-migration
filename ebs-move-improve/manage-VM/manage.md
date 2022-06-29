# Managing the Oracle EBS Cloud Manager Virtual Machine

## Introduction
Within the Virtual Machine that the Cloud manager runs on, you can also preform a number of management tasks that give you more control of the instance. Here we will go over a few of the main commands that are available.

### **Objectives**

* Starting the EBS Cloud Manager application.
* Stopping the EBS Cloud Manager application.

### **Prerequisites**

* Tenancy Admin User
* Tenancy Admin Password
* Lab 2 completed with your Instance Public IP added in your key-data.txt file.
    * `Cloud_Manager_Instance_Public_IP`
    * `SSH_Public_Key`




## Connect to an Oracle Cloud Infrastructure Compute Instance using a Mac, Linux or Unix based machine using Command Line SSH.



Mac OS X amd many Linux machines include a command-line SSH client as part of the operating system. 

To use it on Mac OS, go to **Finder**, select **Go** and select **Utilities** from the top menu. Then look for **Terminal**. To connect over SSH you can use the following command on a Linux or UNIX style system:

    $ ssh –i </path/to/privateKey> opc@<PublicIP_Address>

For example:

    $ ssh -i ./keys/id_rsa opc@XXX.XXX.XXX.XX

Once connected, you can continue.

## Connect to an Oracle Cloud Infrastructure Compute Instance using a Windows based machine

**Method 1:** Using SSH with Git Bash

1.  Launch Git Bash.

    ![](./images/git-bash.png " ")

2.  To connect over SSH you can use the following command on a Linux or UNIX style system.

        $ ssh –i </path/to/privateKey> opc@<PublicIP_Address>

    For example:

        $ ssh -i ./keys/id_rsa opc@XXX.XXX.XXX.XX

    **Note:** Do not copy and paste the line above into Git Bash. Unpredictable results may occur.

3.  If, after entering the ssh command, you receive a message like in the screen shot below, reply with YES.

    ![](./images/continue-connecting.png " ")

4. Once connected, you can continue to Step 3.

**Method 2:** Using SSH with Putty for Windows

For Windows, you can also use a tool like PUTTY to set up PuTTY to connect to an OCI instance.

1.	Launch **PuTTY**.

    ![](./images/putty.png " ")

2. Within the PuTTY session, under the **Session** category, enter the public IP address (for example, XXX.XXX.XXX.XX) from the instance information in the **Host Name** field, and then select **Connection** and select **Data**.

   ![](./images/putty-configuration.png " ")

3.  In the **Auto-login username** field, enter **opc**. From the Category navigation tree, select **Connection**, select **SSH**, and then select **Auth**.

    ![](./images/putty-authentication.png " ")

4.  Use **Browse** to locate the ppk version of your SSH public keyfile in the location where you saved it. (If you do not have a ppk version of your SSH keyfile then you will need to create one) 

    Return to the **Session**.

    ![](./images/putty-ssh.png " ")

5.  In the Session category, enter a unique label (for example, JDE Trial Edition) for the connection in the **Saved Sessions** field, and click **Save**. This will retain all settings for future connections.

    ![](./images/putty-save.png " ")

6.  Connect to the instance by clicking **Open**.

    ![](./images/putty-open.png " ")

7.  PuTTY will open a command window. On first connection, a Security Alert window will appear. Click **Yes** to accept that you trust the connection to this host.

    ![](./images/trust-connection.png " ")
1. Connect to the EBS Cloud Manager virtual machine.

    SSH into the EBS CM instance from your local machine by using the IP address and the SSH private key you used during the deployment of the EBS CM instance. 

    ```
    <copy>
    ssh -i <private_ssh_key_filepath> opc@<Source_EBS__public_IP>
    </copy>
    ```
## Starting the Cloud Manger Application within the virtual machine

Now that you have connected to the compute instance you can now preform the commands to start the EBS Cloud Manager Services by entering these commands.

    ```
    <copy>
    sudo su - oracle
    </copy>
    ```

    ```
    <copy>
    cd /u01/install/APPS/apps-unlimited-ebs/bin
    </copy>
    ``` 

    ```
    <copy>  
    sh ebscloudmgrctl.sh startall
    </copy>
    ```

Then enter the Oracle E-Business Suite Cloud Manager administrator password when prompted.

After running these commands your services should turn on. If they were already on then nothing will happen.

## Stopping the Cloud Manger Application within the virtual machine

While you are connected to the compute instance you can also preform the commands to stop the EBS Cloud Manager Services by entering these commands.

    ```
    <copy>
    sudo su - oracle
    </copy>
    ```

    ```
    <copy>
    cd /u01/install/APPS/apps-unlimited-ebs/bin
    </copy>
    ``` 

    ```
    <copy>  
    sh ebscloudmgrctl.sh stopall
    </copy>
    ```

Then enter the Oracle E-Business Suite Cloud Manager administrator password when prompted.

After running these commands your services should turn off and you will no longer be able to connect to the cloud manager from the web. If they were already off then nothing will happen.

## More Information

[For full documentation on Oracle EBS Cloud Manager click here!](https://docs.oracle.com/cd/E26401_01/doc.122/f35809/toc.htm)

[Learn more now!](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?p180_id=678)


## Acknowledgements

Acknowledgements
* Author: Chris Wegenek, Cloud Engineering
* Last Updated By/Date: Chris Wegenek, Cloud Engineering, October 2021


