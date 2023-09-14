# Extensibility: Advanced Flow

### Introduction


This lab walks you through the steps to extend Procurement Command Center by adding a new dashboard for local agreements.



Estimated Time: 45 minutes

### Objectives
In this lab, you will:
* Create a new Dataset
* Create metadata attributes for the dataset
* Update metadata attributes and create attribute groups
* Assign dataset to the application
* Execute data load for the new dataset
* Extend the existing dashboard with required components



### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 

##  

## Task 1:	Create a new dataset

**Goal**: Extend Procurement command center to add a new dashboard for local agreements. Currently, Procurement command center supports only global BPA coverage.

**Create a Data set**

A data set is both a logical and a physical grouping of attributes to support business dashboard operations and use cases. From a logical perspective, it is designed to support several use cases that are accessed through one or more Oracle Enterprise Command Center Framework dashboards. The design typically caters to open‐ended interaction with the underlying data.


At the physical level, the data set stores one or more records with a uniquely identifying key that represents a particular level of detail of the entity stored in the enterprise system. Unique key is used to identify records and data sets.
* ECC\_SPEC\_ID column is unique and single-assigned. Also, ECC\_SPEC\_ID must be of "spec" profile type.



Contents of a data set can be exported with attribute keys and attribute display names as headers. Each attribute stored in the data set is controlled by metadata properties that specify its behavior on the user interface. Additional value-add features such as calculations, bucketing, and precedence rules can also be specified.
        ![Data set](../images/d67.png "Data set")

To create a data set within ECC, follow the below steps:

1. Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials
     ```
  	 Username: sysadmin
Password: welcome1
    ```
2.	Navigate to ECC Developer page -> ECC Developer
        ![Procurement Command Center](../images/ext1.png "Procurement Command Center")
3.	Go to “Datasets” menu under “Data Designer” section
        ![Procurement Command Center](../images/data1.png "Procurement Command Center")
4.	Click on “New Dataset” button
        ![Procurement Command Center](../images/data2.png "Procurement Command Center")
5.	Provide the below details:
    *	Dataset Key: 
                                                                ```
  	    <copy>xx-po-pcc-local-agreements</copy>
            ```
    *	Dataset Name: 
                                                                    ```
  	    <copy>XX PCC Local Agreements</copy>
            ```
    *	Icon: Procurement


6. Now, provide the security handler details using “Security Rules”. There are 2 different security types under security rules, which will provide security to the dataset:
    * Privilege
        
        * To access data of an ECC data set, the user must have at least one data set privileges (which is an Oracle EBS form function).
      

    * Security Handler
        * Once access to the data set is verified by the ECC Security Manager, a security handler is applied for any subsequent query against that data set to ensure that the data access is restricted to the subset, the user is allowed to see.
        * This is the level of security that enforces data access restrictions on data displayed in the dashboard based on the setups available in Oracle EBS that may be applicable to different business dashboards.
        * ECC allows configuration of custom security that is applied on the existing security handler. 

        ![Security Handler](../images/security_handler.png "Security Handler")



7.	At the time of creating the dataset, the security handler and privilege details are mandatory. We have pre-created the Security Handler and Privilege for you to directly use in this task, there is a separate task towards the end of the Lab which details the steps needed to create both Security Handler and Privilege from scratch.


7.	Click on “Security Rule” tab and provide below details:
    *	Security Handler Name: 
            ```
  	    <copy>XX_PO_PCC_DATASECURITY_PKG_PUB.GetFilterAttributeValuesPO</copy>
            ```
    *   Privilege(1): 
             ```
  	    <copy>XX_PO_PCC_ECC_LOCAL_AGREEMENTS</copy>
            ```
        

9.	Click on "Save" button. The new dataset has been created successfully.
        ![Create Dataset](../images/a111.png "Create Dataset") 
## Task 2:	Create metadata attributes

**Attribute Metadata**
</br>
Attribute metadata section helps you define an attribute's characteristics, including:

* Attribute Key and type.

* Display name.

* Configuration parameters. For example, whether an attribute is searchable.

* Navigability settings. For example, whether to show record counts for available refinements, whether to enable multi-select and how to sort refinements.




1.	In ECC Developer page, go to “Metadata” menu under “Data Designer” section
2.	Choose the dataset from the dropdown as “XX PCC Local Agreements”
        ![Create Dataset](../images/d5.png "Create Dataset") 
    *	You will be on the “Attributes” tab
    *   Click on the “Import” button
        *	Connection: ebsdb
        *   Type: Describe
        ![Create Metadata](../images/d6.png "Create Metadata") 

        *   SQL:  ```
  	         <copy>SELECT ecc_spec_id, agreement, agreement_number, agr_revision, status, supplier, supplier_site, agr_supplier_contact, agr_agreed_amount, agr_amount_limit, agr_amount_released, functional_currency_code, currency, buyer_name, effective_from, effective_to, creation_date, approval_date, submit_date, agr_payment_term, org_id, operating_unit, received_amount, invoiced_amount, shipped_amount, language, group_status, sub_status, next_action_type, reservation_status, creation_year, creation_month, agreements_to_watch, expiring_agreements, agr_style, amount_agreed_func, released_amount_func, authorization_status, document_type, utilization_percentage, doc_authorized_user_ids, security_level_code, type_lookup_code, supplier_id, agreement_line, line_number, line_type, item, item_description, category, uom, unit_price, line_status, lead_time, no_price_breaks, negotiation, order_num, released_quantity, shipped_quantity, received_quantity, rejected_quantity, invoiced_quantity, line_released_amount, line_received_amount, line_invoiced_amount, line_shipped_amount, agreement_status_code, supplier_item_num, cancel_flag, acceptance_required_flag, po_lineloc_id, release_number, po_shipment_num, po_ship_ordered_quantity, po_ship_to_location, shipment_amount, po_ship_received_quantity, po_ship_rejected_quantity, po_ship_invoiced_quantity, po_ship_cancelled_quantity, po_ship_shipped_quantity, po_ship_ordered_amount, po_ship_shipped_amount, po_ship_received_amount, po_ship_rejected_amount, po_ship_invoiced_amount, po_unit_price, po_need_by_date, po_promised_date, overdue_flag, need_by_date_open_shipment 
FROM ecc_proc_local_agreements</copy>
            ```

3.	Click on the “Import” button to create metadata attributes
        ![Create Metadata](../images/a112.png "Create Metadata") 


4. Perform the below changes in the metadata attributes section
    *   Review the profile for all the attributes
    *	Change the profile of the below attributes:
        * Doc Authorized User Ids to “strings”
        * Order Num to “strings”

        ![Update profile](../images/a113.png "Update profile") 


    * Enable “Show in Guided Discovery?” checkbox for below attributes:
        * Agreement
        * Status
        * Buyer Name
        * Effective From
        * Effective To
    * Click on "Save" 

**Attribute Groups** </br>
Attribute Groups are logical groupings of attributes for display purposes based on functional/business meaning. They reduce clutter on Available Refinements and Results Table components.

Attribute Groups are defined at the data set level, where each data set can have zero or more attribute groups, and each group can have zero or more attributes. Groups can be designed at design time in the Administration UI or during runtime in metadata load phase.

5.	Define the below “Attribute Groups” and add attributes as listed below:
    * Navigate to “Attribute Groups” tab
    * Click on the “Add” button to create a new group
    * Provide below details:
        * Sequence #: 1
        * Group Key: PO_RELEASE
        * Group Name: Releases
    * Attributes:
        * Po Unit Price
        * Po Need By Date
        * Po Promised Date
        * Po Ship To Location
        * Po Ship Ordered Quantity

        ![Add Group](../images/a1133.png "Add Group")

    * Click on “Save” button

**Associations** </br>
Associations allow explicit connection between two data sets by defining a link between a common attribute across the data sets. Oracle Enterprise Command Center Framework utilizes this information to enforce associative filtering of data in one destination data set based on refinement state in a source data set.

Additionally, Oracle Enterprise Command Center Framework establishes an implicit relationship between two different data sets that are both associated with a shared data set but not directly linked with each other. This advanced capability allows for advanced refinement state inheritance between data sets that are not directly associated with each other.

6.	Define the below “Associations”:
    * Navigate to “Associations” tab
    * Click on the “Add” button
    * Provide the below details to add association with “PCC Purchase Orders” dataset
        * Source Dataset: XX PCC Local Agreements
        * Source Attribute: Agreement
        * Target Dataset: PCC Purchase Orders
        * Target Attribute: SOURCE\_HEADER\_ID
        * Click on the “Save” button

            ![Associations](../images/a1131.png "Associations")


## Task 3:	Assign data set to an application and execute data load

1. Go to ECC Developer home page
2. Search for “Procurement” application
3. Click on the edit icon for the application
4. Assign the dataset “XX PCC Local Agreements” to the application
                                                                    ```
  	    <copy>XX PCC Local Agreements</copy>
            ```
5. Click on the “Save” button
        ![Assign Dataset reference](../images/a114.png "Assign Dataset reference") 

6. Execute data loads for this new dataset
    * Navigate to “Data Load Submission” menu under “Administration” section
    * Select the below details to submit “Query load”
        * Application Name: Procurement
        * Dataset: XX PCC Local Agreements
        * Load Type: Query Load
        * Connection: ebsdb
        * SQL Query: ```
  	         <copy>SELECT ecc_spec_id, agreement, agreement_number, agr_revision, status, supplier, supplier_site, agr_supplier_contact, agr_agreed_amount, agr_amount_limit, agr_amount_released, functional_currency_code, currency, buyer_name, effective_from, effective_to, creation_date, approval_date, submit_date, agr_payment_term, org_id, operating_unit, received_amount, invoiced_amount, shipped_amount, language, group_status, sub_status, next_action_type, reservation_status, creation_year, creation_month, agreements_to_watch, expiring_agreements, agr_style, amount_agreed_func, released_amount_func, authorization_status, document_type, utilization_percentage, doc_authorized_user_ids, security_level_code, type_lookup_code, supplier_id, agreement_line, line_number, line_type, item, item_description, category, uom, unit_price, line_status, lead_time, no_price_breaks, negotiation, order_num, released_quantity, shipped_quantity, received_quantity, rejected_quantity, invoiced_quantity, line_released_amount, line_received_amount, line_invoiced_amount, line_shipped_amount, agreement_status_code, supplier_item_num, cancel_flag, acceptance_required_flag, po_lineloc_id, release_number, po_shipment_num, po_ship_ordered_quantity, po_ship_to_location, shipment_amount, po_ship_received_quantity, po_ship_rejected_quantity, po_ship_invoiced_quantity, po_ship_cancelled_quantity, po_ship_shipped_quantity, po_ship_ordered_amount, po_ship_shipped_amount, po_ship_received_amount, po_ship_rejected_amount, po_ship_invoiced_amount, po_unit_price, po_need_by_date, po_promised_date, overdue_flag, need_by_date_open_shipment 
FROM ecc_proc_local_agreements</copy>
               ```         
        * Data Upload: Select “Dataset Reset”
        </br>
        **Note:** Data set reset would wipe away any prior data set with the same name and start fresh whereas an extend existing data set option would use the same existing data set and ingest data on top of it
        * Click on the “Submit” button
        ![Execute Dataloads](../images/a115.png "Execute Dataloads") 
    * Once the data load has been submitted, a "Run ID" will be generated
        ![Request ID](../images/request_id_data_load.png "Request ID")

    * Upon clicking on the "Run ID" link displayed in the above image, user will be navigated to the  data load tracking page 
6.	You can also manually navigate to the data load tracking page from menu under “Administration” section
    * Refine using the request ID which is generated when data load is submitted
    * Click on the “Filter” button
        ![Data Load Tracking](../images/a1114.png "Data Load Tracking")

7. Once the data load request is completed, the status of the data load will change from “RUNNING” to “SUCCESS”
        ![Data Load Tracking](../images/a1115.png "Data Load Tracking")

8. Click on the “Query Details” link to view more details:
    * **SQL Time:** This refers to the time spent for SQL per dataset
    * **Elapsed Time:** Total time for ingesting data into ECC (including SQL Time)
    * **Processed Rows:** Number of rows/records which are processed by ECC framework to start ingesting into ECC
    * **Successful Rows:** Number of rows/records which are successfully ingested into ECC
    * **Failed Rows:** Number of rows/records which are failed to ingest into ECC

        ![SQL Query Details](../images/a1117.png "SQL Query Details")








## Task 4:	Extend existing dashboard

1. Navigate to ECC Developer home page
2. Search for “Procurement” application
3. Click on “Copy” option for “Agreements” dashboard
        ![Copy Page](../images/a116.png "Copy Page") 

4.	A new copied page is created as “Agreements(1)”
5.	For the copied page, change the details as mentioned below:
    * Page Short Name: 
                 ```
  	    <copy>xx-pcc-local-agreements</copy>
            ```
    * Page Name: 
                     ```
  	    <copy>XX Local Agreements</copy>
            ```
    * Click on the “Save” button
        ![Edit Page](../images/a117.png "Edit Page") 
6. Search for "Procurement" application and open "XX Local Agreements dashboard"
6.	In “XX Local Agreements” dashboard, replace the dataset from “PCC Agreements” to “XX PCC Local Agreements” in the configuration for
    * Search
    * Available Refinements
    * Selected Refinements
    * Summarization Bar (All Items)
    * Charts
        ![Edit Configuration](../images/a118.png "Edit Configuration") 

8.	In “XX Local Agreements” dashboard, remove the entire tab layout component which contains the result tables
        ![Remove Tab Layout](../images/a119.png "Remove Tab Layout") 

9.	Create a new tab layout with an empty title and configure 2 tabs:
    * Agreements
    * Releases
        ![Create Tab Layout](../images/a1110.png "Create Tab Layout") 

10.	Under “Agreement” tab, add a “Result Table” component and configure as mentioned below:
    * Title: (leave this empty)
    * Dataset: 
                         ```
  	    <copy>XX PCC Local Agreements</copy>
            ```
    * Record Identifier: 
                         ```
  	    <copy>Agreement Number</copy>
            ```
    * Attributes:
        * Agreement
        * Document type
        * Supplier
        * Supplier Site
        * Status
        * Group Status
        * Sub Status
        * Agr Amount Limit
        * Agr Supplier Contact

11.	Click on the “Save” button to save the configuration
        ![Add Agreement Table](../images/a1111.png "Add Agreement Table") 

11.	Under “Releases” tab, add a “Result Table” component and configure as mentioned below:
    * Title: (leave this empty)
    * Dataset: 
                             ```
  	    <copy>XX PCC Local Agreements</copy>
            ```

    * Attributes:
        * Enable “Display Attribute Groups” checkbox

        * Add below attributes (under Persistent Attributes section):
            * Agreement Number
            * Agreement Line
            * Release Number
            * Po Shipment Num

        * Add below group (under Interchangeable Attributes section):
            * Releases

12. You will see the below image:
        ![Add Releases Table](../images/a1112.png "Add Releases Table")

13.	We have successfully created the dashboard for local agreements.
        ![Local Agreements Dashboard](../images/a1113.png "Local Agreements Dashboard")

## Task 5:	Create data load package

**Data Load Process:**
</br>
As mentioned earlier, ECC uses PL/SQL packages to run the data load process. Here the process to create the data load package for “FULL LOAD” is explained below:

1. Create data load package to run Full Load for Local Agreements custom dataset:

    * The user need to create a PL/SQL package (specification and its respective body) with a procedure, which is required to execute FULL LOAD for xx-po-pcc-local-agreements dataset
    * Sample PL/SQL package files are provided in the Lab Files section
        * Specification: XX\_PO\_PCC\_LOC\_AGR\_UTIL\_PVT.pls
                ![Package Specification](../images/a1118.png "Package Specification")

        * Body: XX\_PO\_PCC\_LOC\_AGR\_UTIL\_PVT.plb
                ![Package Body](../images/a1120.png "Package Body")


2.	The procedure used for the data load must have below IN and OUT parameters:


<!DOCTYPE html>
<html>
<head>
<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
style="white-space:pre-wrap; word-wrap:break-word"
</style>
</head>
<body>


<table>
  <tr>
    <th>Parameter Type</th>
    <th>Parameter Name</th>
    <th>Details</th>
  </tr>

  <tr>
    <td>IN</td>
    <td>p_dataset_key</td>
    <td>Represents the data sets for which the data load is being run</td>
  </tr>
    
  <tr>
    <td>IN</td>
    <td>p_load_type</td>
    <td>Signifies which type of data load is being run</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>p_ds_last_success_run</td>
    <td>Signifies the last time the data load got ran successfully</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>p_languages</td>
    <td>Specifies the languages for which the dataload is going to be run</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>p_addl_params</td>
    <td>A parameter via which additional details can be passed to the procedure</td>

  </tr>
  <tr>
    <td>OUT</td>
    <td>x_ecc_ds_meta_rec</td>
    <td>Contains the final data load query that will be executed by ECC</td>
  </tr>
  <tr>
    <td>OUT</td>
    <td>x_return_status</td>
    <td>Returns the status of the load</td>
  </tr>


</table>
</body>
</html>


3.	Compile the package using following steps:
    * Go back to the Terminal window
 
    * Source the EBS edition using below command:
                                         ```
  	    <copy>source /u01/install/APPS/EBSapps.env run</copy>
            ```
    * The package specification is where you declare the public items like procedures, functions etc
                                         ```
  	    <copy>vi /u01/live_labs/11470/lab_files/lab5/task5/XX_PO_PCC_LOC_AGR_UTIL_PVT.pls</copy>
            ```
    * The package body has the definition of every cursor or subprogram like procedures, functions etc. which are declared in the package specification
                                         ```
  	    <copy>vi /u01/live_labs/11470/lab_files/lab5/task5/XX_PO_PCC_LOC_AGR_UTIL_PVT.plb</copy>
            ```
    * Connect to EBS Database using below command:
                                         ```
  	    <copy>sqlplus apps/apps</copy>
            ```

    * The package specification and body files are present under “/u01/live_labs/11470/lab_files/lab5/task5”  directory

    * Compile the package using below commands:
                                                 ```
  	    <copy>@/u01/live_labs/11470/lab_files/lab5/task5/XX_PO_PCC_LOC_AGR_UTIL_PVT.pls</copy>
            ```
                                                         ```
  	    <copy>@/u01/live_labs/11470/lab_files/lab5/task5/XX_PO_PCC_LOC_AGR_UTIL_PVT.plb</copy>
            ```
    ![Compile Package](../images/a1130.png "Compile Package")

4.	Once the package specification and the body are compiled successfully, then the user need to configure the data load rules for the respective dataset
    * Navigate to ECC Developer page
    * Go to “Datasets” menu under “Data Designer” section
    * Search for the local agreements dataset 
                                                             ```
  	    <copy>xx-po-pcc-local-agreements</copy>
            ```
    * Click on the Edit icon
    * Click on the “Load Rules” tab and add below details to configure FULL LOAD
        * Load Type: Full Load
        * Package Name: 
                                                                     ```
  	    <copy>XX_PO_PCC_LOC_AGR_UTIL_PVT</copy>
            ```
        * Procedure Name: 
                                                                             ```
  	    <copy>get_ecc_data_load_info</copy>
            ```
        * Connection Name: ebsdb
            ![Configure Load Rules](../images/a1122.png "Configure Load Rules")
    * Click on the “Save” button
    * Navigate to “Data Load Submission” menu
    * Provide the below details to submit a full load for the local agreements dataset
        *	Application Name: Procurement
        *   Dataset: 
                                                                                     ```
  	    <copy>XX PCC Local Agreements</copy>
            ```
        *	Load Type: Full Load
        *	Click on the “Submit” button

            ![Data Load Submission](../images/a1123.png "Data Load Submission")

    * This will submit a “Full Load” for the custom dataset and inturn uses the created PL/SQL package
    * Click on the Request ID to track the submitted data load job
            ![Data Load Tracking](../images/a1124.png "Data Load Tracking")
    * Once the data load is successful, click on the “Query Details” link to view more details
            ![Data Load Tracking](../images/a1127.png "Data Load Tracking")
    * The number of successful rows will match the successful row count of Query Upload
    * Navigate to the Local Agreements dashboard (ECC Developer -> Procurement -> XX Local Agreements)
            ![Local Agreements Dashboard](../images/a1113.png "Local Agreements Dashboard")


## Task 6:	Create security handler 

**Security Rules:** 
</br>
* At the time of creating the dataset, the security handler and privilege details are mandatory. So, the user has provided the names of the packages/privileges, which will be created at later point.

* Security handler also uses PL/SQL package to get the security identifiers which will be applied to the dataset to get the required subset of data – which the user is allowed to see.

* Here, the process to create the security rules for xx-po-pcc-local-agreements dataset is explained below:

    * Create a PL/SQL package with a procedure, which is required to add security filters based on the logged in user and organization.
    * Sample PL/SQL package files are provided in the Lab Files section
        * Specification: XX\_PO\_PCC\_DATASECURITY\_PKG\_PUB.pls
            ![Package Specification](../images/a1126.png "Package Specification")

    * Body: XX\_PO\_PCC\_DATASECURITY\_PKG\_PUB.plb
            ![Package Body](../images/a1125.png "Package Body")

    * This security handler procedure contains below security rules:
        * ORG\_ID in (ORG\_ID1, ORG\_ID2, ORG\_ID3…) for that specific user
        * DOC\_AUTHORIZED\_USER\_IDS = Logged\_In\_User\_ID
        * If the logged in user is a “Buyer”, then SECURITY\_LEVEL\_CODE in ('PUBLIC', 'PURCHASING'), or else, then SECURITY\_LEVEL\_CODE = 'PUBLIC'

* The final security filter which will be generated and returned to ECC will be:
ORG_ID in (ORG\_ID1, ORG\_ID2, ORG\_ID3…) 
AND 
(SECURITY\_LEVEL\_CODE = 'PUBLIC' OR DOC\_AUTHORIZED\_USER\_IDS = Logged\_In\_User\_ID)

* This security filter will be applied on top of the dataset so that the user will be able to see the designated subset of data only.

    * The procedure used for the data load have below IN and OUT parameters:




    <!DOCTYPE html>
<html>
<head>
<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
style="white-space:pre-wrap; word-wrap:break-word"
</style>
</head>
<body>


<table>
  <tr>
    <th>Parameter Type</th>
    <th>Parameter Name</th>
    <th>Details</th>
  </tr>

  <tr>
    <td>IN</td>
    <td>x_dataset_key</td>
    <td>Represents the data set that the dashboard is using</td>
  </tr>
    
  <tr>
    <td>IN</td>
    <td>x_user_id</td>
    <td>Logged in User ID</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>x_org_id</td>
    <td>Organization ID which is used to access the dataset</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>x_resp_id</td>
    <td>Responsibility ID which is used to access the dataset</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>x_resp_add_id</td>
    <td>Application ID to which the responsibility belongs</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>x_sec_group_id</td>
    <td>ID of the security group</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>x_params</td>
    <td>Additional parameters</td>
  </tr>
  <tr>
    <td>OUT</td>
    <td>x_return_status</td>
    <td>status of the data security execution</td>
  </tr>
  <tr>
    <td>IN</td>
    <td>x_return_message</td>
    <td>x_return_message would contain return the error message in case the x_return_status is 'UNEXPECTED ERROR' or 'EXPECTED ERROR'</td>
  </tr>
    <td>OUT</td>
    <td>x_sec_filter</td>
    <td>x_sec_filter would have the final filter as a json string which be a return value of the call to the methods in ecc_datasecurity_pkg</td>
  </tr>
</table>
</body>
</html>

* Once the changes are completed, compile the package using following steps:
    * Go back to the Terminal window
        * Connect to the environment using SSH (Details are mentioned in “Get Started -> Appendix: Connect Remotely Using SSH section”) 
        * Source the EBS edition using below command:
                                                                                     ```
  	    <copy>source /u01/install/APPS/EBSapps.env run</copy>
            ```
        * Connect to EBS Database using below command:

  	    <copy>sqlplus apps/apps</copy>

        * The package specification and body files are present under “/u01/live\_labs/11470/lab\_files/lab5/task6”  directory

    * Compile the package using below commands:
                                                                                     ```
  	    <copy>@/u01/live_labs/11470/lab_files/lab5/task6/XX_PO_PCC_DATASECURITY_PKG_PUB.pls</copy>
            ```
                                                                                     ```
  	    <copy>@/u01/live_labs/11470/lab_files/lab5/task6/XX_PO_PCC_DATASECURITY_PKG_PUB.plb</copy>
            ```

        ![Compile Package](../images/a1129.png "Compile Package")

* Once the package specification and the body are compiled successfully, then the user need to configure the data load rules for the respective dataset
    * Navigate to ECC Developer page
    * Go to “Datasets” menu under “Data Designer” section
    * Search for the local agreements dataset 
                                                                                         ```
  	    <copy>xx-po-pcc-local-agreements</copy>
            ```
    * Click on the Edit icon
    * Click on the “Security Rule” tab
    * Enable the “Enabled” checkbox. This will ensure that the security rules are applied before accessing the data.

        ![Configure Load Rules](../images/a1128.png "Configure Load Rules")
    * Click on the “Save” button
    * Navigate to the XX Local Agreements dashboard
        * The dashboard will error out stating that the user is not authorized to access the dataset using the logged in responsibility
        * This is because, we have added Privilege to the dataset that only the users accessing the dashboard using XX\_PO\_PCC\_ECC\_LOCAL\_AGREEMENTS page, can access the dataset

        ![Not Authorized](../images/a1135.png "Not Authorized")

* If any user accesses the local agreements dashboard using the allowed responsibility/page, then the user will be able to view only the designated subset of data. Hence ensuring data security.
        ![Operations User](../images/a1136.png "Operations User")

## Task 7:	New Dashboard RBAC Setup
In the previous task we extended the existing Agreements dashboard to include Local agreements, but this new dashboard is not accessible for end users.
There are two ways to provide access of Local Agreements dashboard to the users:
 
1. Replace the shipped "Agreements" dashboard with the custom "Local Agreements" dashboard using EBS OA Personalization
2. Create a new menu under Procurement Command Center to navigate to an OA Page where Local Agreements dashboard is displayed

In this task, we will replace the shipped "Agreements" dashboard with the custom "Local Agreements" dashboard.

1. Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials
    ```
  	 Username: sysadmin
Password: welcome1
    ```
2.	Create a new FND Function for Local Agreements Dashboard:
    * Navigate to Functional Administrator -> Core Services -> Function
    * Search with Code as: 
                ```
  	    <copy>PO_PCC_ECC_AGREEMENTS</copy>
            ```
    * Click on the “Duplicate” icon displayed for PO\_PCC\_ECC\_AGREEMENTS
        ![Duplicate Function](../images/a11s1.png "Duplicate Function")

    * Change the details in the duplicate function page as mentioned below:
        * Name: 
                        ```
  	    <copy>PO PCC ECC Local Agreements Page</copy>
            ```
        * Code: 
                                ```
  	    <copy>XX_PO_PCC_ECC_LOCAL_AGREEMENTS</copy>
            ```
        ![Duplicate Function](../images/a11s2.png "Duplicate Function")

    * Click on the “Continue” button
    * Change the value for HTML Call to 
                                    ```
  	    <copy>GWY.jsp?targetAppType=ECC&targetPage=web/eccapp/po_pcc/xx-pcc-local-agreements</copy>
            ```
    * Click on the “Submit” button
        ![Create Function](../images/a11s3.png "Create Function") 

3.	Add the new FND Function to Procurement Command Center Menu:
    * Navigate to Functional Administrator Responsibility -> Core Services -> Menus
    * Search with code as 
                                        ```
  	    <copy>PO_PCC_MAIN</copy>
            ```
    * Click on “Update” button for “Procurement Command Center” menu
    * In the menu manager section, click on “+” icon to add below menu entry details
        * Function: 
                                                        ```
  	    <copy>PO PCC ECC Local Agreements Page</copy>
            ```
        * Click on “Apply” button to save the menu
        ![Add Function to Menu](../images/arbac1.png "Add Function to Menu")

4. Clear Application Cache:
    * Navigate to Functional Administrator -> Core Services -> Caching Framework -> Global Configuration
    * Click on “Clear All Cache” button and then click on "Yes"
        ![Clear Cache](../images/ss110.png "Clear Cache")

## Task 8:	EBS OA Personalization

1. Login to EBS apps (From the browser URL navigate to http://apps.example.com:8000) with below credentials

    ```
  	 Username: operations
Password: welcome1
    ```
2.	Navigate to Purchasing, Vision Operations (USA) -> Procurement Command Center -> Procurement Operations
          ![Procurement Operations](../images/arbac2.png "Procurement Operations")

3.	Within "Procurement Operations", navigate to "Agreements" dashboard
          ![Agreements](../images/arbac3.png "Agreements")

4.  Click on EBS Settings icon
          ![EBS Settings](../images/arbac5.png "EBS Settings")

5.	Click on “Personalize Page” option
          ![Personalize Page](../images/arbac4.png "Personalize Page")

5. Personalize the Rich Container:
          ![Personalize Rich Container](../images/arbac6.png "Personalize Rich Container")

5.	Update the below details and click on the “Apply” button
     * Destination Function: 
                                                      ```
  	    <copy>XX_PO_PCC_ECC_LOCAL_AGREEMENTS</copy>
            ```
          ![Update Rich Container Details](../images/arbac7.png "Update Rich Container Details")

6. Click on “Return to Application” to access the dashboard
          ![Return to Application](../images/arbac8.png "Return to Application")
          ![Local Agreements Dashboard](../images/arbac9.png "Local Agreements Dashboard")

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

* **Contributors**-  Muhannad Obeidat, Nashwa Ghazaly, Mikhail Ibraheem, Rahul Burnwal, Manikanta Kumar and Mohammed Khan

* **Last Updated By/Date**- Mohammed Khan, August 2023

