# Power User Personalization


## Introduction


In ECC, Power users can modify a dashboard to tailor it based on their business requirements. This lab walks you through the steps to Personalize an existing dashboard to suit it to your business requirement with an example. 


A Power User has:

*	Same designer experience as admin
*	Enabled at the user level using the profile option “FND: ECC Power User Enabled”
*	All personalizations are saved without any deployment. 
*	No access to ECC Admin UI

A Power user can/can't do the following:
<div>

<table id="huyh">


  <tr>
    <th>Can</th>
    <th>Cannot</th>
  </tr>
  <tr>
    <td>Adding a new component</td>
    <td>Create a new data set</td>
  </tr>
  <tr>
    <td>Modify existing component</td>
    <td>Create a new dashboard</td>
  </tr>
  <tr>
    <td>Delete component</td>
    <td>Configure a component from a data set that is not part of the application datasets</td>
  </tr>
  <tr>
    <td>Change dashboard layout</td>
    <td>Create public save search</td>
  </tr>

  </tr>
</table>
<style>
#huyh caption {
 display: none;
}
</style>
</div>

Estimated Time: 20 minutes

### Objectives

In this lab, you will:
* Personalize the Supplier Balance dashboard to track cash outflow for invoice payments per bank account so that you can analyze payment trends
* Personalize the Account Analysis dashboard to maintain the accuracy of financial records


### Prerequisites 

This lab assumes you have:
* Completed all previous labs successfully 



## Task 1: Personalize Supplier Balance dashboard 

**Goal**: As a Payables Accountant, I want to track  cash outflow for invoice payments per bank account so that I can analyze payment trends 


1. Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials
    ```
  	 Username: eccuser
Password: welcome1
    ```



2. You will see the below screen:
   ![EBS home screen](../images/gl100.png "EBS home screen")

3. From "Payables Manager", navigate to "Payables Command Center"
   ![Payables Manager responsibility](../images/pl1.png "Payables Manager responsibility")



4. From Supplier Balance dashboard, Enable Personalization Mode by clicking on the "i" icon (on the top left of the page, beside the share icon) to edit the dashboard as a Power User

   ![Enable Personalization Mode](../images/jda1.png "Enable Personalization Mode")
5. The personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon

   ![Enable Personalization Mode](../images/jda2.png "Enable Personalization Mode")

6. Remove existing Tag cloud by clicking on Tag cloud's "x" icon 



   ![Delete Tag cloud](../images/jda3.png "Delete Tag cloud")

7. Add a chart (Pie chart) that replaces the deleted Tag cloud. You can do this by going to the bottom of the page and clicking the "Open components list" icon
   ![Open components list](../images/opencomponentlist.png "Open components list")

8. Go to the top of the page and drag  chart component into the dashboard

9. Now edit the configuration of the chart. 

    - Data set: Installaments 
    - Chart type: Pie (Default is Pie, keep it as is)
    - Dimension: Validation status
    - Metric: Atrribute (Invoice) and Aggregation (count distinct) 
10. Click "Preview" and then click "Save"

   ![Configure chart component](../images/jda5.png "Configure chart component")

11. Add a new Tab in the existing Tab component. To do this you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. Name this tab "Bank Balance"

   ![Configure Tab layout](../images/jda6.png "Configure Tab layout")

   ![Enter Tab title](../images/jda7.png "Enter Tab title")

12. Click "Preview" and then click "Save"
   ![Save Tab component](../images/jda8.png "Save Tab component")

13. Add a chart component inside the new tab "Bank Balance" to highlight paid amount per bank account

    - Data set: Payments 
    - Chart type: Bar
    - Dimension: Bank Account (series dimension)
    - Metric: Attribute (Paid amount) and Aggregation (Sum) 

14. Click preview 

   ![Click preview](../images/jda9.png "Click preview")
15. This gives cash outflow across all currencies, now add additional dimension to split the chart per currency.

16. Add "Currency" as Trellis column dimension
17. Click "Preview" and then click "Save"

   ![Add Trellis column](../images/jda10.png "Add Trellis column")
   ![Save trellis chart](../images/jda11.png "Save trellis chart")


18. In addition of viewing detailed payments add a Pivot view

19. Add New Component- Aggregate Table (Pivot view is an alternate visualization of the Aggregate Table component)
    - Data set: Payments
    - Attributes:
          - Supplier name
          - Supplier site
          - Currency name (This will become a column when Pivot visualization is enabled)
    - Metric:
          - Attribute (Paid amount) and Aggregation (Sum)
20. Click preview. This gives Per supplier, per supplier site totals of invoice paid amount.

    ![Aggregate table configuration](../images/jda13.png "Aggregate table configuration")
21. Enable Pivot view and Sub summary and then click "Preview" 

    ![Click preview](../images/jda14.png "Click preview")

22. Save the configuration


    ![Save Aggregate table configuration](../images/jda15.png "Save Aggregate table configuration")


## Task 2: Run dataload for General Ledger Command Center

You have already run dataload for Payables command center. The steps are similar here.

1. Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials

    ```
  	 Username: eccuser
Password: welcome1
Responsibility: General Ledger Super User
    ```




2. Navigate to "General Ledger Command Center"

3. When the dashboard appears change the function id in the dashboard to **1011696** as done before in the Payables command center. 

    ![Change Function ID](../images/jda100.png "Change Function ID")


4. You will then see the below screen



    ![Schedule request](../images/jda101.png "Schedule request")

5. Choose "General Ledger Command Center Data Load" in the Program name by copying it from below and pasting in the Program Name

    ```
  	 <copy>General Ledger Command Center Data Load</copy>
    ```

6. You will see the below screen
    ![General Ledger Command Center Data Load](../images/jda102.png "General Ledger Command Center Data Load")

7. From "Parameters" tab choose the Load type as **FULL_LOAD**, Set Ledger ID as **1** and Set/Reset Data as **TRUE**, this will wipe out all the records in the dataset.
    ![Enter parameters](../images/jda103.png "Enter parameters")

8. Click on "Continue" and then click on "Submit"

    ![Click Submit](../images/jda104.png "Click Submit")
    ![Request scheduled](../images/b10.png "Request scheduled")

9. Track the data load progress
    ![Track Data load from EBS](../images/b11.png "Track Data load from EBS")

10. You can also track the dataload in ECC Dataload Tracking page by logging in (http://apps.example.com:8000/ecc) via below credentials, using the Concurrent Program ID:

    ```
  	 Username: eccadmin
Password: welcome1
    ```

11. You will see the below screen
    ![Track Data load from ECC](../images/gl3.png "Track Data load from ECC")

## Task 3 : Personalize Account Analysis dashboard 

1. Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials

    ```
  	 Username: eccuser
Password: welcome1
    ```


2. You will see the below screen,  From **General Ledger Super User** responsibility navigate to **General Ledger Command Center**

   ![EBS home screen](../images/gl100.png "EBS home screen")

**Goal**:: Investigate and Act To Maintain the Accuracy Of Financial Records

3. From General Ledger Super User navigate to General Ledger Command Center and then to Account analysis dashboard. Personalize the dashboard to view employee expenses by the parent account by clicking on the "i" icon to edit the dashboard as a Power User
   ![Personalize dashboard](../images/gl200.png "Personalize dashboard")

4. The personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon

   ![Personalize dashboard](../images/gl300.png "Personalize dashboard")

5. By default the dashboard is populated with the oldest period, Jan-07. Replace this period Jan-07 with Apr-23 in selected refinements to view latest data 
   ![Change period name](../images/home1.png "Change period name")

**Note:** If instead you see period Adj-07 then replace it with Apr-23.


6. Add another refinement Account type : "Expense", by clicking on expense from the charts


   ![Add refinement](../images/home56.png "Add refinement")

7. You will see that the chart automatically cascades to display different accounts because cascading is enabled and configured by admin
   ![Chart cascade](../images/home23.png "Chart cascade")

8. Add a new Tab in the existing Tab component. To do this you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. 

   ![Edit Tab configuration](../images/home5.png "Edit Tab configuration")
9. Add Tab Title as "Period Activities by Department and Parent Account"

   ![Add Tab title](../images/home33.png "Add Tab title")


10. Click "Preview" and then click "Save"
 
11. Add a new bar chart  inside the tab and configure the chart with the below details:

    - Dataset: GL Account Analysis
    - Chart type: Bar
    - Group dimension: Cost Center
    - Series dimension: Parent account 1
    - Trellis column: Period Name
    - Metric: Attribute (Period Activity) and no Aggregation, since this is a calculated attribute.

12. Click "Preview" 


   ![Click Preview](../images/home44.png "Click Preview")
13. Save the configuration. You will be able to see a combined view of account segment and hierarchy
   ![combined view of account segment and hierarchy](../images/home45.png "Combined view of account segment and hierarchy")

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

