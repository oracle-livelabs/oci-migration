# Power User Personalization

### Introduction


This lab walks you through the steps to personalize Oracle Enterprise Command Center dashboards as a Power user.

Estimated Time: 30 minutes

### Objectives
In this lab, you will:
* Learn about ECC component categorization and ECC configuration model
* Personalize ECC Payables command center as a Power User
* Personalize ECC General Ledger command center as a Power User



### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 

##  

## Task 1: ECC Component walkthroughs

**Categorization of components**

Oracle Enterprise Command Center Framework UI components are grouped into four main groups:
   * Navigation:
      * Search Box
      * Selected Refinements (breadcrumb)
      * Available Refinements
   * Visualization: 
      * Summarization Bar
      * Chart
      * Tag Cloud
      * Aggregated Table
      * Diagram
      * Aggregated Grid
   * Detailed insights:    
      * Results Table
      * Results Grid
   * Layout:
      * Tabbed component container

   All Oracle Enterprise Command Center Framework components come with a unified configuration model that enhances the configuration experience. Also, many components share a subset of user-facing options. 


**Configuration model**


   The Oracle Enterprise Command Center Framework configuration model uses a familiar structure that follows that of a SQL query. No coding or custom expressions are required to configure any Oracle Enterprise Command Center Framework component.
   For the sake of explaining different configuration options of Oracle Enterprise Command Center Framework components, we will use a SQL query structure to introduce the relevant concept in the Oracle Enterprise Command Center Framework configuration template. Please note that Oracle Enterprise Command Center Framework does not execute a SQL query to display data in a component.


   For example, given the SQL query:

      SELECT
      SUM(ASSET_COST), MAJOR_CATEGORY

   The metric can be added under "Metrics" with the Attribute of "Asset Cost" and Aggregation "Sum".
    ![Configuration model](../images/conf1.png "Configuration model")
   
   If the SQL statement is:

      FROM
      fa-asset
   The Oracle Enterprise Command Center Framework Configuration would show
   fa_asset as the selected data set.
    ![Configuration model](../images/conf2.png "Configuration model")

   If the SQL statement is:
      WHERE
      ASSET\_TYPE = 'CAPITALIZED'
   The Oracle Enterprise Command Center Framework Configuration would have the condition with Asset Type Code for Attribute, = for Operator, and CAPITALIZED for Value.
    ![Configuration model](../images/conf3.png "Configuration model")
   If the SQL statement is:
      GROUP BY MAJOR\_CATEGORY
   The Oracle Enterprise Command Center Framework Configuration would have
   The category listed under Dimensions
    ![Configuration model](../images/conf4.png "Configuration model")
   If the SQL statement is:
      HAVING
      SUM(ASSET\_COST) > 10000
   The Oracle Enterprise Command Center Framework Configuration would have Asset Cost (SUM) for Attribute, >= for Operator, and 10000 for Value under Aggregate Conditions.
    ![Configuration model](../images/conf5.png "Configuration model")


   Based on the above example, the following chart will be displayed:
    ![Configuration model](../images/conf6.png "Configuration model")
   Likewise a Results Table, which is a flat list of rows, displaying Batch name, Journal name, Account type, Source, Category from  attributes would be similar to a translate to 
      Select Batch name, Journal name, Account type, Source, Category from table name



## Task 2: Personalize Supplier Balance Dashboard

**Goal**: As a Payables Accountant, I want to track  cash outflow for invoice payments per bank account so that I can analyze payment trends 


1. Login to EBS apps (Navigate to http://<VNC\_Public\_IP\>:8000) with below credentials
    ```
  	 Username: eccuser
Password: welcome1
    ```

2. Navigate to Payables Manager responsibility -> Payables Command Center -> Supplier Balance Dashboard
   ![Payables Manager responsibility](../images/pl1.png "Payables Manager responsibility")

4. From Supplier Balance dashboard, click on the Ledgers flag and select "Vision Operations (USA)" Ledger from the pop up.

   ![Supplier Balance dashboard](../images/sup1.png "Supplier Balance dashboard")
   ![Supplier Balance dashboard](../images/sup20.png "Supplier Balance dashboard")


5. Enable Personalization Mode by clicking on the "i" icon (on the top left of the page, beside the share icon) and then click on "Personalize" button.

   ![Enable Personalization Mode](../images/sup3.png "Enable Personalization Mode")  
   ![Enable Personalization Mode](../images/sup4.png "Enable Personalization Mode")

6. The "Personalize" button is now disabled and the personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon

   ![Enable Personalization Mode](../images/sup5.png "Enable Personalization Mode")


7. Add a new Tab in the existing Tab component. To do this you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. Name this tab "Bank Balance"

   ![Configure Tab layout](../images/sup9.png "Configure Tab layout")

8. Click "Preview" and then click "Save"
   ![Add Bank Balance Tab](../images/addbankbalancetab.png "Add Bank Balance Tab")
   ![Save Tab component](../images/sup10.png "Save Tab component")

9. Add a chart component inside the new tab "Bank Balance", by dragging and dropping the chart component within the tab layout, to highlight paid amount per bank account

    - Data set: Payments 
    - Chart type: Bar
    - Dimension: Bank Account (series dimension)
    - Metric: Paid amount (Attribute) and Sum (Aggregation) 

10. Click preview 
11. This gives cash outflow across all currencies, now add additional dimension to split the chart per currency.

12. Add "Currency" as Trellis column dimension
13. Click "Preview" and then click "Save"

   ![Add Trellis column](../images/sup120.png "Add Trellis column")
   ![Save trellis chart](../images/sup13.png "Save trellis chart")


14. In addition of viewing detailed payments add a Pivot view under "Bank Balances" tab.

15. Add New Component- Aggregate Table (Pivot view is an alternate visualization of the Aggregate Table component)
    - Data set: Payments
    - Attributes:
          - Supplier name
          - Supplier site
          - Currency name (This will become a column when Pivot visualization is enabled)
    - Metric:
          - Paid amount (Attribute) and Sum (Aggregation)
16. Click preview. This gives per supplier, per supplier site totals of invoice paid amount.

    ![Aggregate table configuration](../images/sup140.png "Aggregate table configuration")

17. Save the configuration

    ![Save Aggregate table configuration](../images/sup160.png "Save Aggregate table configuration")

18. Now, lets convert the Aggregate table to a Pivot view. Click on the configuration, click on "Enable Pivot view" from the "Visualization" accordion, click on "Preview" and then click on "Save".
    ![Pivot view](../images/switch1.png "Pivot view")
19. Switch to Pivot view from Aggregate Table view by clicking on the Pivot view icon [The Pivot View allows users to perform comparisons and identify trends across several cross-sections of data. The values in the header rows and columns represent every possible grouping of the selected attributes. Each body cell contains a metric value corresponding to the values in the heading rows and columns.].
    ![Pivot view](../images/switch.png "Pivot view")
    ![Pivot view](../images/switch77.png "Pivot view")


    ![Pivot view](../images/switch2.png "Pivot view")

20. Finally, click on the "i" icon and then the "Exit" button to disable Personalization mode.
   ![Exit Personalization](../images/exitpersonalizationsuppbalance.png "Exit Personalization")

## Task 3: Personalize Account Analysis dashboard

**Goal**: Investigate and act to maintain the accuracy of financial records


1. Login to EBS apps (Navigate to http://<VNC\_Public\_IP\>:8000) with below credentials

    ```
  	 Username: eccuser
Password: welcome1
    ```


2. You will see the below screen,  From **General Ledger Super User** responsibility navigate to **General Ledger Command Center**

   ![EBS home screen](../images/genz100.png "EBS home screen")


3. You will see the Account Analysis dashboard. If you see any existing filters in the Selected refinements, please remove them and then enable personalization from "i" icon 
   ![Personalize dashboard](../images/genz2000.png "Personalize dashboard")

4. Click on the search bar to find the previously saved search [in Lab 2 - Task 2]
   ![Personalize dashboard](../images/genz3000.png "Personalize dashboard")

5. Click on the saved search to start our investigation from there
   ![Personalize dashboard](../images/genz4000.png "Personalize dashboard")


8. Add a new Tab in the existing Tab component, the one below the chart. To do this you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. Add Tab Title as "Period Activities by Department and Parent Account". Click "Preview" and then click "Save".
   ![Tab](../images/genz500.png "Tab")
 
9. Add a new bar chart  inside this new tab

   ![Tab](../images/genz600.png "Tab")

10. Configure the chart with the below details:

    - Dataset: GL Account Analysis
    - Chart type: Bar
    - Group dimension: Cost Center
    - Series dimension: Parent account 1
    - Trellis column: Period Name
    - Metric: Period Activity (Attribute) and no Aggregation, since this is a calculated attribute.

10. Click "Preview" 

   ![Click Preview](../images/f1000.png "Click Preview")
11. Save the configuration. You will be able to see a combined view of account segment and hierarchy
   ![combined view of account segment and hierarchy](../images/f2000.png "Combined view of account segment and hierarchy")





## Learn More
* [Enterprise Command Center- User Guide](https://docs.oracle.com/cd/E26401_01/doc.122/e22956/T27641T671922.htm)
* [Enterprise Command Center- Administration Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f34732/toc.htm)
* [Enterprise Command Center- Extending Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f21671/T673609T673618.htm)
* [Enterprise Command Center- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)
* [Enterprise Command Center- Direct from Development videos](https://learn.oracle.com/ols/course/ebs-enterprise-command-centers-direct-from-development/50662/60350)
* [Enterprise Command Center for E-Business Suite- Technical details and Implementation](https://mylearn.oracle.com/ou/component/-/117416)

## Acknowledgements

* **Author**- Muhannad Obeidat, VP

* **Contributors**-  Muhannad Obeidat, Nashwa Ghazaly, Mikhail Ibraheem, Rahul Burnwal, Manikanta Kumar and Mohammed Khan

* **Last Updated By/Date**- Mohammed Khan, August 2023

