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

## Task 2: Update Oracle EBS user name (Optional)
This task is optional. **EBS\_ECC\_USER** is the Oracle E-Business Suite user name (FND user) with which Oracle Enterprise Command Center Framework connects to Oracle E-Business Suite using the JNDI configuration. 

1.  Make sure that from ECC terminal you update EBS\_ECC\_USER value in /u01/Oracle/quickInstall/EccConfig.properties  to ECC\_DISCOVERY\_HOL\_{yourname}, to do that follow the below steps:

   - In ECC terminal copy/paste the below command to open the file
   
    ```
  	 <copy>vi /u01/Oracle/quickInstall/EccConfig.properties</copy>
    ```

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


    ```
* When prompted provide a password to create new FND user as **welcome1**
* Password for ECC Domain weblogic was previously set by you as **welcome1**
* Password for EBS Schema apps is always **apps**
    ```




   

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

## Task 6: Validate integration of ECC with EBS 

Open chrome browser and enter the following URL

```
  	 <copy> http://localhost:7776/ecc</copy>
```
1. You will see the below screen when ECC is integrated with EBS successfully:

    ![User Not Authenticated to Access ECC](../images/auth2.png "User Not Authenticated to Access ECC")


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

