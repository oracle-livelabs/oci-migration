# Manage Extensibility

### Introduction

Because Oracle E-Business Suite is used across many industries and environments, users may have special requirements like merging development in one place or moving development from a test environment to a production environment. This lab details the steps needed to do so and also discusses how as an admin you can keep track of ECC usage.

Estimated Time: 30 minutes


### Objectives

In this lab, you will:

* Publish changes to other environments
* Track Usage using activity audit


### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 


##  

## Task 1 : Publish changes to other environments

* Users need to move their development across environments and sometimes multiple users working on the same application in different environments want to merge their development. For all of these use cases, ECC allows users to both export an application (along with the underlying pages and data sets) and import an application (along with the underlying pages and data sets) into a different environment. 
* The Administrator UI allows you to export or import any application. This capability helps in sharing the application for a quick assessment, creating a backup before extending, moving an application to a different environment, or restoring the shipped state of a command center. An application can be exported for any specific language, and an application can be imported preserving any custom pages or custom load rules.

1. Login to EBS apps (From the browser URL navigate to http://<VNC\_Public\_IP\>:8000) with below credentials

    ```
  	 Username: sysadmin
Password: welcome1
    ```

2. Navigate to ECC Developer -> ECC Developer
    ![ECC developer](../images/val1.png "ECC developer")

3. Navigate to "Export/Import" tab under "Administration" section.
    ![ECC developer](../images/image1.png "ECC developer")
4. Select "Procurement" application from the application drop down.
    ![ECC developer](../images/admin400.png "ECC developer")
5. To select "English", select Language as "en" from the Language drop down and then click on "Export"
     ![ECC developer](../images/ext100.png "ECC developer")

6. You will see a success message, indicating that the application has been exported.
     ![ECC developer](../images/admin4.png "ECC developer")
7. Likewise, to import an application you have to click on the "Import" tab and then select the application. For instance, if you were to be in a separate environment you could select the application we just exported and then this application will:
    * Replace the existing Procurement application with our new Procurement application, overriding all of the underlying pages and data sets associated.
    * Create a new Procurement application, along with all underlying pages and data sets if there wasn't an application called "Procurement" 
     ![ECC developer](../images/admin5.png "ECC developer")



## Task 2: Track usage using Activity Audit
* The Activity Audit dashboard is designed to support two use cases: tracking user activity and tracking search activity.


* The Activity Audit dashboard gives full insight into the use of the Enterprise Command Center dashboards. It allows business analysts and administrators to know whether dashboards are being used or not, who uses them, and at what times and which dashboard is used more. It also helps generate valuable new insights into user searches.

* Activity Audit provides the following benefits:

    * Capitalize on ECC investment

        * Track dashboard usage

        * Capture audit trail of user activities on dashboards

        * Tune deployment and tune extract, transform, and load (ETL) processes

    * Tune business operations

        * Monitor search activity

        * Identify and analyze user intents

        * Resolve issues as they arise
* Application and Data set details

    * Dataset Name: Activity Audit

    * Dataset Key: activity-audit

    * Application Name: Activity Audit

    * Application Short Name: activity-audit

    * Page Name: Activity Tracker

    * Page Short Name: activity-tracker
* To access the dashboard, navigate to the Activity Audit section in the Administration UI or you can click on the "Activity audit" application from Home.

     ![ECC developer](../images/admin6.png "ECC developer")
     ![ECC developer](../images/activityaudit3.png "ECC developer")

* You can also choose to view individual application/page details as well. Click on the Page name filter from the Available refinements section and filter for "XX Local Agreements" page

## Task 3: Share Personalization

**Goal**: As an admin I want to share the "Account analsyis" personalization changes done by "eccuser" user, to all users with the same responsibility

**Note:** In Lab 3: Power User Personalization, as "eccuser" user we made multiple personalization changes to Account analysis dashboard. We now want to share those personalization changes to all users with the same responsibility. 


1. Login to EBS apps (Navigate to http://<VNC\_Public\_IP\>:8000) with below credentials

    ```
  	 Username: sysadmin
Password: welcome1
    ```

2. Navigate to ECC Developer -> ECC Developer
    ![Procurement Command Center](../images/val1.png "ECC Developer")

3. Navigate to "About" menu -> "Monitoring" tab. Click on "Trigger Incremental Load" link under "Activity Audit Data Load Controls".
   ![ECC developer](../images/admin66.png "ECC Developer")
3. Navigate to "Activity Audit" Dashboard -> "Personalization Tracking" tab. The personalizations made by ECCUSER are visible
    ![Procurement Command Center](../images/newecc1.png "ECC Developer")
5. Click on the three dots to expand the row actions for the personalization made on GL Account Analysis page and then click on  "Share Personalization". As soon as share personalization is clicked, the page is copied. A message with the page key is provided upon the successful copying of page. The message disappears only when user explicitly clicks on close button corresponding to the message.
     ![Procurement Command Center](../images/newecc2.png "Procurement Command Center")


6. Click the hyperlink, a drawer opens with page detail of the copied page and the user can make amendments and save the changes. Note that the first copy has the number 1, and the nth copy would have the number n. Change the short name to "xx-gl-aa" and name to "General Ledger Command Center Account Analysis" click Save. 
    ![Procurement Command Center](../images/newecc3.png "Procurement Command Center")
7. A message appears inside the drawer indicating that the changes are saved. The drawer is closed automatically. If the user clicks Cancel, the drawer is closed immediately

2.	Create a new FND Function for custom Indirect Procurement Dashboard:
     * Navigate to EBS Home Page -> Functional Administrator responsibility -> Core Services -> Functions
        ![Functional Administrator](../images/functionaladministratorpath.png "Functional Administrator")
        ![Functions Menu](../images/functions.png "Functions Menu")

     * Search with Code as 
                                                            ```
  	    <copy>GL_ECC_ACC_ANALYSIS</copy>
            ```
     * Click on the “Duplicate” icon displayed for GL\_ECC\_ACC\_ANALYSIS
          ![Duplicate Function](../images/gl1001.png "Duplicate Function")

     * Change the details in the duplicate function page as mentioned below:
          * Name: 
                                                                      ```
  	    <copy>XX General Ledger Command Center Account Analysis</copy>
            ```
          * Code: 
                   ```
  	    <copy>XX_GL_ECC_ACC_ANALYSIS</copy>
            ```
          
     ![Duplicate Function](../images/gl1002.png "Duplicate Function")

     * Click on the “Continue” button
     * Change the value for HTML Call to 
                                  ```
  	    <copy>GWY.jsp?targetAppType=ECC&targetPage=/web/eccapp/gl/xx-gl-aa</copy>
            ```
     * Click on the “Submit” button

          ![Create Function](../images/gl1003.png "Create Function") 
          ![Create Function](../images/gl1004.png "Create Function") 


3. Add the new FND Function to Procurement Command Center Permission Set:
    * Navigate to EBS Home Page -> Functional Administrator responsibility -> Security -> Permission Sets
        ![Permission Set](../images/permissionset.png "Permission Set")
    * Search with permission set name as 
                                        ```
  	    <copy>General Ledger</copy>
            ```
    * Click on “Update” button for “General Ledger Command Center Access Permission Set"
        ![Update Permission Set](../images/gl1005.png "Update Permission Set")
    * In the permission set manager section, click on “+” icon to add below permission details
        * Permission: 
                                                        ```
  	    <copy>XX General Ledger Command Center Account Analysis</copy>
            ```
        * Click on the magnifying icon to select the correct permission set
        * Click on “Apply” button to save the permission set
        ![Add Function to Permission Set](../images/gl1006.png "Add Function to Permission Set")
        ![Add Function to Permission Set](../images/gl10061.png "Add Function to Permission Set")

4.  Clear Application Cache:
    * Navigate to EBS Home Page -> Functional Administrator responsibility -> Core Services -> Caching Framework -> Global Configuration
        ![Clear Cache](../images/gl1007.png "Clear Cache")
    * Click on “Clear All Cache” button and then click on "Yes"
        ![Clear Cache](../images/gl1008.png "Clear Cache")

1.	From **General Ledger Super User** responsibility navigate to **General Ledger Command Center**
          ![Indirect Procurement](../images/gl1009.png "Indirect Procurement")
2.	Click on EBS Settings icon
3.	Click on “Personalize Page” option
          ![Personalize Page](../images/gl1010.png "Personalize Page")

4. Personalize the Rich Container:

    * A rich content container is an OA component which is designed to embed/enclose an external content within an OA Framework page. The rich content container component accepts the URL of the rich content, in this case an ECC dashboard.
    This rich content is then enclosed within an iFrame within an OA Framework page. 
    In this case, through Oracle EBS and ECC integration, users are allowed to drill down from Oracle EBS to ECC. The rich container requires an FND function of the ECC dashboard page, which will allow the user to access the respective ECC dashboard inside EBS.
          ![Personalize Rich Container](../images/gl1011.png "Personalize Rich Container")

5.	Update the below details and click on the “Apply” button
     * Destination Function: 
                                                      ```
  	    <copy>XX_GL_ECC_ACC_ANALYSIS</copy>
            ```
          ![Update Rich Container Details](../images/gl1012.png "Update Rich Container Details")

6. Click on “Return to Application” to access the dashboard
          ![Return to Application](../images/gl1013.png "Return to Application")
          ![combined view of account segment and hierarchy](../images/f2000.png "Combined view of account segment and hierarchy")



You may now **proceed to the next lab**


## Learn More
* [Enterprise Command Center- User Guide](https://docs.oracle.com/cd/E26401_01/doc.122/e22956/T27641T671922.htm)
* [Enterprise Command Center- Administration Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f34732/toc.htm)
* [Enterprise Command Center- Extending Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f21671/T673609T673618.htm)
* [Enterprise Command Center- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)
* [Enterprise Command Center- Direct from Development videos](https://learn.oracle.com/ols/course/ebs-enterprise-command-centers-direct-from-development/50662/60350)
* [Enterprise Command Center for E-Business Suite- Technical details and Implementation](https://mylearn.oracle.com/ou/component/-/117416)

## Acknowledgements

* **Author**- Muhannad Obeidat, VP

* **Contributors**-  Muhannad Obeidat, Nashwa Ghazaly, Mikhail Ibraheem, Rahul Burnwal, Manikanta Kumar and Sriram Sumaithangi

* **Last Updated By/Date**- Sriram Sumaithangi, April 2025

