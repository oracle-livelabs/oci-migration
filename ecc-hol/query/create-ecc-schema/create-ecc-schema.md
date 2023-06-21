#  Create ECC schema 


### Introduction


This lab walks you through the steps to create ECC schema and install weblogic server so that you can set up Oracle Enterprise Command Center Framework

Estimated Time: 30 minutes

### Objectives
In this lab, you will:

* Validate if EBS responsibility tree is up
* Validate if EBS run edition can be sourced
* Extract quickInstall
* Create ECC schema and install Weblogic Server


### Prerequisites

This lab assumes you have:
* Completed the previous lab successfully 

##  

## Task 1: Validate if EBS responsibility tree is up

1. Open Chrome browser, and from the address bar navigate to http://apps.example.com:8000 

    ```
  	 <copy>http://apps.example.com:8000 </copy>
    ```




2. Login with following credentials:


    ```
  	 Username= eccadmin
Password= welcome1
    ```


3. Verify if EBS homepage is displayed, like in below image:
    ![Login to EBS](../images/verify1.png "EBS login")
4. Ensure if the responsibility tree is up, like shown in below image:

    ![View EBS responsibility tree](../images/verify2.png "EBS responsibility tree")

**Note:** If you are not able to type in the remote desktop, then please hit the command key


## Task 2: Validate if EBS run edition can be sourced 

1. Open a terminal window for EBS to,<n> Source EBS edition</n>. Copy/Paste the following command (case is important) in the terminal :

    ```
  	 <copy>source /u01/install/APPS/EBSapps.env run</copy>
    ```


2. In the image below, you can see how you should source the running EBS edition on the terminal.
    ![Source Run edition in EBS](../images/validateterminal1.png "Source run edition" )

## Task 3: Extract quickInstall 

1. Now open a new terminal for ECC, leave the previous EBS terminal open. Within the ECC terminal, navigate to /u01 directory by using below command

    ```
  	 <copy>cd /u01</copy>
    ```



2. .bsx files are downloaded in /u01 directory. Extract the .bsx files by running the below command from /u01 directory 


    ```
  	 <copy>for f in *.bsx; do sh $f; done</copy>
    ```


    ![Extract quickInstall](../images/quickinstall.png "Extract quickInstall")

3. This process will take a few minutes. After extraction is completed, navigate to cd /u01/Oracle/quickInstall

    ```
  	 <copy>cd /u01/Oracle/quickInstall</copy>
    ```



**Note:** In this directory (Oracle/quickInstall) there is a file called "EccConfig.properties", which has all the parameters predefined for this Hands-on-lab. You don't have to change any parameters but described below are some important parameters you should keep in mind. 


**ECC_BASE**- The root directory where you extracted the .bsx files. This property is set to the value /u01 by default.

**ECC\_CONFIG\_LOC**- You can optionally set this property to the location of a custom ecc-config.properties file. Oracle Enterprise Command Center Framework will then use the properties file in this location instead of the standard ecc-config.properties file created in the $ECC_BASE/Oracle/quickInstall/env/ecc directory.

**ECC\_LOG\_DIR**- The directory where the Oracle Enterprise Command Center Framework administration application log files should be generated. For cluster setup, this directory must be shared between all nodes. All nodes must have read and write access to this shared directory.

**EBS\_MIDDLETIER\_HOST\_FQDN**- The fully qualified domain name (FQDN) for the Oracle E-Business Suite application tier. If the Oracle E-Business Suite instance uses a proxy or load balancer, use the FQDN for the web entry point instead.

**EBS\_MIDDLETIER\_PORT**- The Oracle E-Business Suite application tier port. If the Oracle E-Business Suite instance uses a proxy or load balancer, use the port for the web entry point instead. If you plan to enable TLS for communication between Oracle E-Business Suite and the Oracle Enterprise Command Center Framework installation, then you should use port 4443 here. See Enabling TLS for Oracle Enterprise Command Center Framework, Release 12.2, My Oracle Support Knowledge Document 2496445.1.

**EBS\_MIDDLETIER\_PROTOCOL**- The Oracle E-Business Suite application tier protocol, either http or https. If the Oracle E-Business Suite instance uses a proxy or load balancer, use the protocol for the web entry point instead. If you plan to enable TLS for communication between Oracle E-Business Suite and the Oracle Enterprise Command Center Framework installation, then you must set the protocol to https here. See Enabling TLS for Oracle Enterprise Command Center Framework, Release 12.2, My Oracle Support Knowledge Document 2496445.1.

**EBS\_MIDDLETIER\_INTERNAL\_HOSTS**- The host name of the Oracle E-Business Suite instances. If there is more than one Oracle E-Business Suite instance behind a load balancer, specify all the Oracle E-Business Suite host names separated by a comma.

For further information please refer to section 4.3.1 of the following document
[Installing Oracle Enterprise Command Center Framework](https://mosemp.us.oracle.com/epmos/faces/ui/km/DocumentDisplay.jspx?_afrLoop=263547950196438&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1can4pxb6b_4#schemabackup)



## Task 4: Create ECC Schema

1. From the ECC terminal make sure that you are in  /u01/Oracle/quickInstall directory and then execute the below script. When prompted choose **Option 1** to create ECC schema. 

    ```
  	 <copy>./envSetup.sh</copy>
    ```
    ![Select Option 1](../images/selectoption.png "Select Option 1")

2. This step creates the ECC schema and provides an option to use the existing ECC user created in the ECC database:


    ```
  	 Selected ECC DB is jdbc:oracle:thin:@ebs.org:1521:ebsdb
Is the user <ECC_DB_USERNAME> existing in ECC database [y/n]?<password>
    ```


3. If you choose option “y”, you are prompted for ECC user credentials to create the ECC schema. If you choose the option “n”, you are prompted to enter ECC database system user credentials to create the ECC user and later create the ECC schema. For this demo enter **"n"**

4. When prompted provide the database system user details, mentioned below:

    ```
  	 Database system username: system
Database system password: manager
Password for ECC DB user: welcome1
Confirm Password for ECC DB user: welcome1
    ```
5. You will see the below screen

    ![Enter database credentials](../images/eccschema0.png "Enter database credentials")


6. Database set up  should be completed successfully. You can verify the logs in $ECC_BASE/Oracle/quickInstall/logs/setup.log

7. Enter **Option 6** to exit and then execute following commands to validate  successful ECC schema creation:

    ```
  	 <copy> source env/ecc.env </copy>
    ```

8. Execute the following command with the credentials mentioned:


    ```
  	 <copy>sqlplus $ECC_DB_USER@"(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=$ECC_HOST_NAME)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=$EBS_DS_NAME)))"</copy>
    ```
    ```
  	 <copy>Password:welcome1</copy>
    ```



    ![Validate ECC dB Connection](../images/systemmanager1.png "Validate ECC dB Connection")

9. If you are able to log in to SQL and receive a SQL> prompt, then the ECC DB connection is available to use. 

10. Exit from the SQL prompt by typing **exit;**

## Task 5: Install Weblogic Server

1. Make sure you are in the  /u01/Oracle/quickInstall directory 

2. Run the ./envSetup.sh script again and when prompted choose **Option 2** to Install Weblogic Server 

    ```
  	 <copy>./envSetup.sh</copy>
    ```
    ![Select Option 2](../images/selectoption.png "Select Option 2")
    ![Install weblogic server](../images/weblogic0.png "Install weblogic server")
    ![Install weblogic server](../images/weblogic.png "Install weblogic server")

You may now **proceed to the next lab**

## Learn More
* [Enterprise Command Center- User Guide](https://docs.oracle.com/cd/E26401_01/doc.122/e22956/T27641T671922.htm)
* [Enterprise Command Center- Admistration Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f34732/toc.htm)
* [Enterprise Command Center- Extending Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f21671/T673609T673618.htm)
* [Enterprise Command Center- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)
* [Enterprise Command Center- Direct from Development videos](https://learn.oracle.com/ols/course/ebs-enterprise-command-centers-direct-from-development/50662/60350)
* [Enterprise Command Center for E-Business Suite- Technical details and Implementation](https://mylearn.oracle.com/ou/component/-/117416)

## Acknowledgements

* **Author**- Muhannad Obeidat, VP

* **Contributors**-  Muhannad Obeidat, Nashwa Ghazaly, Mikhail Ibraheem, Rahul Burnwal and Mohammed Khan

* **Last Updated By/Date**- Mohammed Khan, March 2023

