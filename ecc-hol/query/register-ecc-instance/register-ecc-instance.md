# Register ECC Instance as FND Node and Create EBS JNDI

### Introduction


This lab walks you through the steps to Register ECC Instance as FND Node and Create EBS JNDI so that you can set up Oracle Enterprise Command Center Framework



Estimated Time: 30 minutes

### Objectives
In this lab, you will:
* Register ECC Instance as FND Node and Create EBS JNDI
* Validate EBS JNDI
* Integrate ECC with EBS instance
* Integrate EBS with ECC


### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 

##  

## Task 1: Register ECC Instance as FND Node

1. On the ECC terminal Enter **Option 6** to exit the Options screen and Source EBSapps running edition

    ```
  	 <copy>source /u01/install/APPS/EBSapps.env run </copy>
    ```



    ![Source EBSapps running edition](../images/exitsource.png "Source EBSapps running edition")


2. Run the following java command on EBS machine to register ECC instance as FND NODE, this will create "ebsdb_APPS.EXAMPLE.COM.dbc" file:

    ```
  	 <copy>java oracle.apps.fnd.security.AdminDesktop apps/apps CREATE NODE_NAME=apps.example.com DBC=/u01/install/APPS/fs2/inst/apps/ebsdb_apps/appl/fnd/12.0.0/secure/ebsdb.dbc</copy>
    ```

**Note:** Copy here works because you are on the same machine

3. Copy the "ebsdb_APPS.EXAMPLE.COM.dbc" file to the ECC instance

    ```
  	 <copy>cp ebsdb_APPS.EXAMPLE.COM.dbc /u01/Oracle/quickInstall/connection.dbc</copy>
    ```



    ![Copy the "ebsdb_APPS.EXAMPLE.COM.dbc" file to the ECC instance](../images/fnd2.png "Copy file to the ECC instance")


    ![Copy the "ebsdb_APPS.EXAMPLE.COM.dbc" file to the ECC instance](../images/fndnode.png "Copy file to the ECC instance")

## Task 2: Update Oracle EBS user name 

**EBS\_ECC\_USER** is the Oracle E-Business Suite user name (FND user) with which Oracle Enterprise Command Center Framework connects to Oracle E-Business Suite using the JNDI configuration. 

1.  Make sure that from ECC terminal you update EBS\_ECC\_USER value in /u01/Oracle/quickInstall/EccConfig.properties  to ECC\_DISCOVERY\_HOL\_{yourname}, to do that follow the below steps:

   - In ECC terminal type vi /u01/Oracle/quickInstall/EccConfig.properties to open the file
   - To insert or update please enter "i" on the keyboard
   - Update EBS\_ECC\_USER property
   - Enter "Esc" on the keyboard and enter ":wq" and then press "Enter" to save the file

    ![Update EBS_ECC_USER value](../images/namechange.png "Update EBS_ECC_USER value")



## Task 3: Create EBS JNDI

1. From the ECC terminal, execute the ./envSetup.sh script and when prompted choose **Option 4** to Create EBS JNDI.


    ```
  	 <copy>./envSetup.sh</copy>
    ```


    ![Choose Option 4 ](../images/selectoption.png "Choose Option 4 ")




    ![Create EBS JNDI](../images/jndi1.png "Create EBS JNDI")
    ![Provide a password to create new FND user](../images/jndi22.png "Provide a password to create new FND user")

   * When prompted provide a password to create new FND user as **welcome1**
   * Password for ECC Domain weblogic was previously set by you as **welcome1**
   * Password for EBS Schema apps is always **apps**

## Task 4: Validate EBS JNDI

1. Open the browser and copy paste the below URL to access ECC Admin console: 
    ```
  	 <copy>http://apps.example.com:7775/console</copy>
    ```




2. Enter ECC admin user credentials 
    ```
  	 Username:weblogic
Password:welcome1
    ```


3. You should see the below screen
    ![Login to weblogic](../images/weblogicmain.png "Login to weblogic")

4. Go to the "Data Sources" in "Services" tab as shown below
    ![Navigate to services tab](../images/weblogic10.png "Navigate to services tab")

5. Click on "JNDI" with the name “ebsdb” as indicated below

    ![Click on JNDI with the name “ebsdb”](../images/ebsdb1.png "Click on JNDI with the name ebsdb")

6. Go to "Monitoring" -> "Testing" tab
    ![Navigate to testing tab](../images/monitoring10.png "Navigate to testing tab")

7. Select "eccManaged Server" and click on "Test Data Source"

    ![Click on Test data source](../images/monitoring11.png "Click on Test data source")

8. You should see a success message in green as shown below


    ![Success message in green](../images/monitoring12.png "Success message in green")


## Task 5: Integrate ECC with EBS Instance


1. From the ECC terminal, execute the ./envSetup.sh script and choose **Option 5** to integrate ECC with EBS instance 

    ```
  	 <copy> ./envSetup.sh</copy>
    ```



2. When prompted to proceed with EBS integration submit "y" as shown below:


    ![choose Option 5 ](../images/option6.png "choose Option 5 ")

3.  Here, please enter password as **welcome1** for both ECC DB user and ECC admin user weblogic  

    ![Enter password for both ECC DB user and ECC admin user weblogic](../images/m11.png "Enter password")

    ![Integrate ECC with EBS Instance](../images/m22.png "Integrate ECC with EBS Instance")

## Task 6: Integrate EBS with ECC 

 1. Log in to Oracle E-Business Suite as a system administrator i.e., Open the browser and navigate to http://apps.example.com:8000 

    ```
  	 Username= SYSADMIN
Password= welcome1
    ```


 2. Navigate to System Administrator: Oracle Applications Manager > AutoConfig.

    ![Click on Autofig](../images/autoconfig10.png "Click on Autofig")

 3. Select the application tier context file, and choose "Edit Parameters"

    ![choose Edit Parameters](../images/autoconfig2.png "choose Edit Parameters")

 4. Search for the s\_ecc\_conf\_comment variable by selecting OA_VAR in the search list of values and entering s\_ecc\_conf\_comment in the search text box. Then, click the "Go" button.

    ![Find variables](../images/autoconfig3.png "Find variables")

 **Note:** 
 If  number sign (#) is present in Value field then remove it from the Value field for the s\_ecc\_conf\_comment variable to ensure that this variable is not commented. Then, click the "Save" button.
 
 Enter a reason for the update, such as Enabling Oracle Enterprise Command Center Framework. Then choose the OK button.
 
 Similarly, search for the following variables and set their values as appropriate for your installation:

    1. **s\_ecc\_protocol** - The protocol for accessing the Oracle Enterprise Command Center Framework administration UI.
    2. **s\_ecc\_web_host** - The Oracle Enterprise Command Center Framework host name.
    3. **s\_ecc\_managed\_server\_port** - The port for the Oracle Enterprise Command Center Framework managed server.
    4. **s\_ecc\_conf\_update** - A flag to update the ecc.conf file. If Oracle Enterprise Command Center Framework is enabled, use this variable to specify whether the ecc.conf file should be updated. The default value is true, which means ecc.conf will be updated during every AutoConfig run. To retain the contents of ecc.conf, such as when you are enabling TLS for the Oracle Enterprise Command Center Framework installation, set this variable to false.

 ![Set variables](../images/autoconfig.png "Set variables")

 5. Open EBS terminal and then run AutoConfig. For running Autoconfig you need to first source the EBS running edition using below command

    ```
  	 <copy>source /u01/install/APPS/EBSapps.env run</copy>
    ```


6. Then, navigate to below location

    ```
  	 <copy>cd $ADMIN_SCRIPTS_HOME</copy>
    ```



7. Run the below script

    ```
  	 <copy>./adautocfg.sh</copy>
    ```


8. It will prompt you for apps password which is by default **apps** 

    ![Run autoconfig](../images/autoconfig4.png "Run autoconfig")
    ![Run autoconfig](../images/autoconfig101.png "Run autoconfig")

9. Once Autoconfig runs successfully then navigate to below location:

    ```
  	 <copy>cd $ADMIN_SCRIPTS_HOME</copy>
    ```



    ![Navigate to $ADMIN_SCRIPTS_HOME ](../images/adh12.png "Navigate to $ADMIN_SCRIPTS_HOME")




10. And then, run the following script to check OHS status:


    ```
  	 <copy>./adapcctl.sh status</copy>
    ```

    ![Check OHS status](../images/adh22.png "Check OHS status")

11. And then, run the following script to stop OHS:


    ```
  	 <copy>./adapcctl.sh stop</copy>
    ```


    ![Stop OHS](../images/adh77.png "Stop OHS")   

12. And then, run the following script to start OHS:

    ```
  	 <copy>./adapcctl.sh start</copy>
    ```


    ![Start OHS](../images/adh44.png "Start OHS ")

13. And then, run the following script again to check the OHS status if it has successfully started:

    ```
  	 <copy> ./adapcctl.sh status</copy>
    ```



    ![Check OHS status](../images/adh55.png "Check OHS status")

## Task 7: Validate integration of EBS and ECC 

1. Navigate to http://apps.example.com:8000 in the browser with below credentials 


    ```
  	 Username: SYSADMIN
Password: welcome1
    ```


    
2. Navigate to ECC Developer, you should see "Activity audit" application as below if the integration is successful
    ![Validate integration of EBS and ECC](../images/activityaudit300.png "Validate integration")


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

