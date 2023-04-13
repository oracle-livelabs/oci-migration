# Run Dataload


### Introduction

This lab walks you through the steps to run dataload so that you can set up Oracle Enterprise Command Center Framework



Estimated Time: 15 minutes

### Objectives
In this lab, you will:
* Run dataload
* Identify Common dataload and set up issues


### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 


##  

## Task 1: Set up RBAC

1. To perform RBAC setup with the UMX\_ECC\_RBACAuto.sh script, you should type the following command (case is important):

    ```
  	 <copy>source /u01/install/APPS/EBSapps.env run</copy>
    ```




2. Move to the $FND_TOP/bin directory for your Oracle E-Business Suite instance using the following command: 
    ```
  	 <copy>cd $FND_TOP/bin</copy>
    ```




3. Run the script using the following command:

    ```
  	 <copy>./UMX_ECC_RBACAuto.sh</copy>
    ```


4. When prompted, enter the user name and password of the APPS (username and password is **apps**) user for the Oracle E-Business Suite instance.

5. When prompted, enter the full path and file name for your .csv input file. If your file is named UMX\_ECC\_RBAC.csv and is present in the same directory as the UMX\_ECC\_RBACAuto.sh file, then the script uses that file by default and does not prompt you for the file name and path.

6. The following example shows sample output from the script:

    ```
  	 -bash-3.00$ ./UMX_ECC_RBACAuto.sh
APPS username:apps
APPS password:
Enter csv file name with full path : /slot/ems2120/appmgr/apps/apps_st/appl/UMX_ECC_RBAC.csv
Executing for Permission_set EAM_ECC_ACCESS_PS , Responsibility_name FND_RESP|EAM|MSU_VIS_OPS|STANDARD and ECC_Role UMX|EAM_ECC_ACCESS_ROLE
old   6: L_MENU_NAME varchar2(100) := '&1';
new   6: L_MENU_NAME varchar2(100) := 'EAM_ECC_ACCESS_PS';
old   8: l_responsibility_name varchar2(300) := '&2';
new   8: l_responsibility_name varchar2(300) := 'FND_RESP|EAM|MSU_VIS_OPS|STANDARD';
old  10: ecc_role_name varchar2(300) := '&3';
new  10: ecc_role_name varchar2(300) := 'UMX|EAM_ECC_ACCESS_ROLE';
Completed Successfully

PL/SQL procedure successfully completed.
-bash-3.00$
    ```



  


## Task 2: Validate RBAC set up

After you run the script, ensure that the responsibilities you set up are assigned to the users who should have access to the Enterprise Command Centers.

Please refer to Section 8.2 from [Enterprise Command Center- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)


## Task 3: Validate Import of ECC applications

1. Navigate to http://apps.example.com:8000 in the browser with below credentials 

    ```
  	 Username: eccuser
Password: welcome1
    ```



    
2. Navigate to "Payables Manager" and then to "Payables Command Center"
    ![Navigate to "Payables Manager" and then to "Payables Command Center"](../images/validateeccuser.png "Payables Command Center")
3. Because you are yet to run the dataload you will not see any data just yet but the page should load like below

    ![No data visible in dashboard](../images/eccuser2.png "No data visible in dashboard")

## Task 4: Submit a Job
Each product with an Enterprise Command Center provides a concurrent program to load its product-specific data into the Oracle Enterprise Command Center Framework installation. 

Here we will take the example of Oracle Payables with the respective Data Load Concurrent Program "Payables Command Center Data Load".Run this program now to perform an initial full load. 

You should also schedule the data load programs periodically to perform incremental loads to update the data available in the Enterprise Command Center dashboards. For details, see your product documentation.
 
### Execution Flow

1. The following diagram gives an overview of a Data load process:
    ![Data load techincal overview](../images/dataload.png "Data load techincal overview")


Jobs should be submitted from EBS concurrent program and hence the tracking should be exposed to the concurrent program job.
Concurrent program keeps polling the status of the job from ECC and display the current status of the job

1. Login in EBS (From the browser navigate to http://apps.example.com:8000) using below credentials:

    ```
  	 Username: eccuser
Password: welcome1
    ```


2. Once you login, navigate to "Payables Manager" and then to "Payables Command Center"


    ![Go to Payables Command Center](../images/validateeccuser.png "Go to Payables Command Center")

3. Change the function id to **1011696** in the url as indicated in the image below and hit enter

    ![Change function ID](../images/eccuser3.png "Change function ID")

4. You will see the below "Schedule request" page 

    ![Schedule request](../images/eccuser4.png "Schedule request")




5. Choose "Payables Command Center Data Load" in the Program name by copying it from below and pasting in the Program Name

    ```
  	 <copy>Payables Command Center Data Load</copy>
    ```


6. You should see the below screen

    ![Payables Command Center Data Load](../images/ipl1.png "Payables Command Center Data Load")
7. Go to "Parameters" tab and then select **FULL_LOAD** as Load Type and Click "Continue"

    ![Enter parameters](../images/ipl2.png "Enter parameters")
8. Click "Submit"
    ![Click submit](../images/ipl3.png "Click submit")
9. You should see the below screen once the data load is successful

    ![Successful data load message](../images/ipl4.png "Successful data load message")
10. You can track the dataload 
    ![Track dataload in EBS](../images/ipl5.png "Track dataload in EBS")
11. Or You can also track the dataload by copying the Concurrent Program ID then navigating to ECC Developer i.e., (Navigating to http://apps.example.com:8000/ecc) and then to Data Load Tracking Page using admin credentials provided below:


    ```
  	 Username: eccadmin
Password: welcome1
    ```


12. You can check the respective job using the Concurrent Program ID, as shown in below image

    ![Track dataload in ECC](../images/ipl6.png "Track dataload in ECC")


13. From ECC:
    - User can check details for each query in real time.
    - It reflects the current load status: Number of successful rows and number of failed rows.
    - It shows when the query started, how much time spent at the DB, the sql text and the operation.
    - User can cancel the running job

    SQL Trace can be enabled by passing “TRUE” value while starting the data load Concurrent Program.
    The trace log file will be generated with the ECC Data Load sub-request “Job ID” as the identifier. The “Job ID” is noted in the log file of sub-request.

14. Data Load job structure request:
    - One “Audit Request” per job
    - One “Dataset Key” per dataset included at the job
    - One “Audit Load Rule” per load rule for each “Audit Dataset”
    - One “Audit Load Detail” for each query retrieved from the load rule for each “Audit Load Rule”


15. The following image describes Self Job Concurrency Matrix

    ![Self Job Concurrency Matrix](../images/matrix.png "Self Job Concurrency Matrix") 

For details on Data load tuning, ETL Job parameters, SQL Plan statistics and common issues please refer to the [Enterprise Command Center- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)

## Task 5: Validate successful Job submission



1. Open the browser and navigate to http://apps.example.com:8000 from eccuser

    ```
  	 Username: eccuser
Password: welcome1
    ```


2. And then to "Payables Manager" responsibility and then to "Payabales Command Center" and see if the page loads as below. This proves that the data load was successful

    ![Successful Data load](../images/payables1000.png "Successful Data load") 

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




