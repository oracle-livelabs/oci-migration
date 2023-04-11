# Set up Oracle Enterprise Command Center Framework

To set up Oracle Enterprise Command Center Framework, you must configure the Oracle Enterprise Command Center Framework components, verify the server status in the server logs, apply the latest Oracle WebLogic Server 12.2.1.4 Critical Patch Update (CPU), and configure the JNDI to connect to Oracle E-Business Suite.

## Introduction

*Describe the lab in one or two sentences, for example:* This lab walks you through the steps to ...

Estimated Time: -- minutes

### About <Product/Technology> (Optional)
Enter background information here about the technology/feature or product used in this lab - no need to repeat what you covered in the introduction. Keep this section fairly concise. If you find yourself needing more than two sections/paragraphs, please utilize the "Learn More" section.

### Objectives

*List objectives for this lab using the format below*

In this lab, you will:
* Objective 1
* Objective 2
* Objective 3

### Prerequisites (Optional)

*List the prerequisites for this lab using the format below. Fill in whatever knowledge, accounts, etc. is needed to complete the lab. Do NOT list each previous lab as a prerequisite.*

This lab assumes you have:
* An Oracle Cloud account
* All previous labs successfully completed


*This is the "fold" - below items are collapsed by default*

## Task 1: Configure Oracle Enterprise Command Center Framework Components

Run the $ECC_BASE/Oracle/quickInstall/envSetup.sh script. When prompted, select and run the following options in the order shown:

Option 2 - Install Weblogic Server

Option 3 - Create ECC Domain

The script performs the following actions:

1. Prompts you to provide the Oracle Enterprise Command Center Framework database password and configures the JNDI for the Oracle Enterprise Command Center Framework schema.

2. Prompts you to provide the Oracle Enterprise Command Center Framework domain admin password and configures that password for the current installation.

<pre style=""><code class="hljs ini">Important: These credentials are used to connect to the Oracle Enterprise Command Center Framework domain admin server. Note that the password entered here is not stored anywhere. Administrators must remember the password.
</code></pre>

3. Updates the ecc.env environment file and generates the ecc-config.properties file in the $ECC_BASE/Oracle/quickInstall/env/ecc directory, unless you have specified a directory for a custom ecc-config.properties file in the ECC_CONFIG_LOC property in the EccConfig.properties file.

4. Initializes the solr.properties configuration file.

5. Configures the ports for the Oracle Enterprise Command Center Framework domain admin server and managed server, as specified in the EccConfig.properties file.

6. Configures the heap space for the Oracle Enterprise Command Center Framework domain admin server and managed server, as specified in the EccConfig.properties file.

7. Creates the default srcdb source system and system connections for both the srcdb system and the ebsdb system.

8. Creates the Oracle Enterprise Command Center Framework database JNDI connection.

9. Starts the Oracle Enterprise Command Center Framework domain admin server and the managed server, including ZooKeeper.

At this point, you should validate whether all the applications are running. To do so, enter 6 to exit the script.

## Task 2: Verify Server status in the Server Logs

Check the server logs to verify that the admin server and managed servers have started successfully.

1. Navigate to the log for each server using the following paths. To verify the server startup status, check that each log contains the following message: "Server state changed to RUNNING".

The path to the Oracle Enterprise Command Center Framework domain admin server log is: $ECC_BASE/Oracle/Middleware/user_projects/domains/ecc_domain/bin/domain.log

The path to the Oracle Enterprise Command Center Framework managed server log is: $ECC_BASE/Oracle/Middleware/user_projects/domains/ecc_domain/bin/ecc.log

The path to the Oracle Enterprise Command Center Framework administration application logs is determined by the directory specified in the ECC_LOG_DIR property in the EccConfig.properties file. The default location is $ECC_BASE/Oracle/quickInstall/logs/ecc.

2. To verify that the Oracle Enterprise Command Center Framework managed server was started successfully, navigate to the following URL and check that the Oracle Enterprise Command Center Framework administration UI appears correctly.

http://<ECC_HOST_NAME>:<ECC_MANAGED_PORT>/ecc

where <ECC_HOST_NAME> is the host name of the Oracle Enterprise Command Center Framework system and <ECC_MANAGED_PORT> is the port specified for the Oracle Enterprise Command Center Framework managed server.

## Task 3: Apply the latest Oracle WebLogic Server 12.2.1.4 Critical Patch Update (CPU)

You should apply the latest Oracle WebLogic Server 12.2.1.4 Critical Patch Update (CPU) to the Oracle WebLogic Server instance for your Oracle Enterprise Command Center Framework installation. Check the Critical Patch Updates, Security Alerts and Bulletins page to review the Oracle Critical Patch Update Advisory for the latest quarterly CPU and search for any CPU patches for Oracle WebLogic Server 12.2.1.4.

To apply an Oracle WebLogic Server CPU patch, perform the following steps:

1. Stop the Oracle Enterprise Command Center Framework admin server and managed server as described in Section B.2: Stopping the Oracle Enterprise Command Center Framework Environment.

2. Source the ecc.env file using the following command:

<pre style=""><code class="hljs ini">source $ECC_BASE/Oracle/quickInstall/env/ecc.env
</code></pre>


3. Override the Oracle home setting using the following command:

<pre style=""><code class="hljs ini">export ORACLE_HOME=$ECC_BASE/Oracle/Middleware
</code></pre>


4. Download the CPU patches related to Oracle WebLogic Server 12.2.1.4 to a temporary staging folder. Set patch_home to the path to that staging folder.

5. Apply the patches in order as listed in the Oracle Critical Patch Update Advisory for the current CPU.

6. Start the Oracle Enterprise Command Center Framework managed server and admin server as described in Section B.1: Starting the Oracle Enterprise Command Center Framework Environment.

<pre style=""><code class="hljs ini">Note: After you complete your initial installation, you should periodically check the Critical Patch Updates, Security Alerts and Bulletins page for any additional Oracle WebLogic Server 12.2.1.4 CPU patches in later quarterly CPUs, and apply them when available.
</code></pre>

## Task 4: Configure the JNDI to connect to Oracle E-Business Suite.

After the managed server has been started successfully, perform the following steps.

1. Log into the Oracle E-Business Suite system as the OS user on the operating system. Source the run edition file system, and then navigate to the $FND_SECURE directory. This directory should contain a local DBC file named after the Oracle E-Business Suite SID. For example: myebssid.dbc

2. Make a note of the following details:

The fully qualified domain name of the target Oracle Enterprise Command Center Framework host system.

The full local DBC file path. For example: /u01/inst/apps/myebssid_myebshost/appl/fnd/12.0.0/secure/myebssid.dbc

3. Run the following Java command, entering the values you noted in the previous step for the NODE_NAME and DBC parameters:

java oracle.apps.fnd.security.AdminDesktop apps/<apps_password> CREATE NODE_NAME=<fully_qualified_domain_name_of_target_ECC_host_system> DBC=<full_local_DBC_file_path>
For more information about running this utility, see: Oracle E-Business Suite Software Development Kit for Java Readme, My Oracle Support Knowledge Document 974949.1.

Make a note of the name and location of the DBC file that is generated after you run the AdminDesktop command. You will need this information to complete step 5 below.

4. You can optionally specify the FND user with which to set up the JNDI. If you want to specify a different user than the one currently set in the EccConfig.properties file, then navigate to the $ECC_BASE/Oracle/quickInstall/ directory on the Oracle Enterprise Command Center Framework system and open the EccConfig.properties file. Set the value for the EBS_ECC_USER property to the FND user you want and then save the file.

5. Locate the DBC file that was generated by the AdminDesktop command in Step 3, and copy this file to the $ECC_BASE/Oracle/quickInstall directory on the Oracle Enterprise Command Center Framework tier. Rename the file to the following name: connection.dbc

6. Run the envSetup.sh script from the $ECC_BASE/Oracle/quickInstall directory. When prompted, select Option 4 - Create EBS JNDI. This option creates two JNDI data sources for the Oracle Enterprise Command Center Framework application:

srcdb - The data source connection to the Oracle E-Business Suite database that Oracle Enterprise Command Center Framework uses to verify the data security

ebsdb - The data source connection to the Oracle E-Business Suite database that Oracle Enterprise Command Center Framework uses during data load

When prompted, enter the Oracle E-Business Suite FND user password and the Oracle Enterprise Command Center Framework domain admin server password.

The script uses the user specified in the EBS_ECC_USER property in the $ECC_BASE/Oracle/quickInstall/EccConfig.properties file to configure the JNDI . If the user specified in the EBS_ECC_USER property is a new Oracle E-Business Suite user that does not yet exist in the FND_USERS table, then you must enter and confirm the password when prompted to create the user. If the user already exists in the FND_USERS table, then you must validate the user.

<pre style=""><code class="hljs ini">Note: The following role name is used for the Oracle Enterprise Command Center Framework FND user: UMX|APPS_SCHEMA_CONNECT

</code></pre>


<pre style=""><code class="hljs ini">Note: If the FND_SERVER_SEC profile option is set to Desktop Only or Desktop and Server, then you should set the FND_SERVER_DESKTOP_USER profile option to the node name or names at the user level for the Oracle Enterprise Command Center Framework FND user. The node name should be the fully qualified domain name for the Oracle Enterprise Command Center Framework host. For example: abc.us.example.com

</code></pre>


After completion of this step, there should not be any errors reported.

7. Next, perform JNDI validation from the Oracle Enterprise Command Center Framework domain admin console.

Log in to the Oracle Enterprise Command Center Framework domain admin console at the following URL: http://<ECC_HOST_NAME>:<ECC_ADMIN_PORT>/console

Navigate to Services > Data Sources.

Select the ebsdb JNDI configuration in the right pane.

Navigate to the Monitoring tab and select the Testing subtab.

Select the managed server and choose the Test Data Source button. The following message should appear: Success Test of ebsdb on server <Server Name> was successful.

Navigate back to Services > Data Sources.

Select the srcdb JNDI configuration in the right pane.

Navigate to the Monitoring tab and select the Testing subtab.

Select the managed server and choose the Test Data Source button. The following message should appear: Success Test of srcdb on server <Server Name> was successful.



<pre style=""><code class="hljs ini">Note: If you upgrade your Oracle E-Business Suite database after the initial installation of Oracle Enterprise Command Center Framework, or if you migrate or clone your Oracle E-Business Suite environment, then you must reconfigure the JNDI with the updated DBC file. To do so, repeat the steps in this section, Configuring the JNDI to Connect to Oracle E-Business Suite.

</code></pre>

<pre style=""><code class="hljs ini">Important: If you need to make any additional updates in the property files or rerun any scripts after the initial installation of Oracle Enterprise Command Center Framework, then you should follow these guidelines. This note applies for running all scripts in the quickInstall directory, except for the $ECC_BASE/Oracle/quickInstall/envSetup.sh and $ECC_BASE/Oracle/quickInstall/createEnvFile.sh scripts.

To run the quickInstall scripts, you must first source the $ECC_BASE/Oracle/quickInstall/env/ecc.env environment file once in the current shell session. Use the following command to source the environment file:

source $ECC_BASE/Oracle/quickInstall/env/ecc.env

Also, if you modify any of the following three property files, then you must run the $ECC_BASE/Oracle/quickInstall/createEnvFile.sh script to update the environment file and source the environment file for the current shell session.

$ECC_BASE/Oracle/quickInstall/EccConfig.properties

$ECC_BASE/Oracle/quickInstall/scripts/EccDefault.properties

$ECC_BASE/Oracle/quickInstall/scripts/WLSConfig.properties

Use the following commands to run the script:

cd $ECC_BASE/Oracle/quickInstall
./createEnvFile.sh

After performing these steps, run the following commands to activate the changes in the current Oracle Enterprise Command Center Framework installation:

source $ECC_BASE/Oracle/quickInstall/env/ecc.env
sh $ECC_BASE/Oracle/quickInstall/wlsScripts/updateEccConfigurationProperties.sh

</code></pre>





## Learn More

*(optional - include links to docs, white papers, blogs, etc)*

* [URL text 1](http://docs.oracle.com)
* [URL text 2](http://docs.oracle.com)

## Acknowledgements
* **Author** - <Name, Title, Group>
* **Contributors** -  <Name, Group> -- optional
* **Last Updated By/Date** - <Name, Month Year>




 1. Database Setup
 2. Install Weblogic Server
 3. Create ECC Domain
 4. Create EBS JNDI
 5. Integrate ECC with EBS
 6. Exit:
5
Proceed with Integration? confirm(y) otherwise(n):
y
Enter the password for ECC DB user ECC_Test :
Enter the password for ECC admin user weblogic :
