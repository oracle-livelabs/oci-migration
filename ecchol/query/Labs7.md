# Power User Personalization

In ECC, Power users can modify a dashboard to tailor it based on their business requirements. This lab walks you through the steps to Personalize an existing dashboard to suit it to your business requirement with an example. 

Estimated Time: 20 minutes


A Power User has:

*	Same designer experience as admin
*	Enabled at the user level using the profile option “FND: ECC Power User Enabled”
*	All personalizations are saved without any deployment. 
*	No access to ECC Admin UI

<h2> A Power user can/can't do the following: </h2>
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


### Objectives

In this lab, you will:
* Personalize the Supplier Balance dashboard to track cash outflow for invoice payments per bank account so that you can analyze payment trends
* Personalize the Account Analysis dashboard to maintain the accuracy of financial records


### Prerequisites 

This lab assumes you have:
* Completed all previous labs successfully 

##  

## Task 1: Personalize Supplier Balance dashboard 

<b>Goal</b>: As a Payables Accountant, I want to track  cash outflow for invoice payments per bank account so that I can analyze payment trends 


* Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials


 <pre><span class="hljs-attribute">
 Username: eccuser
 Password: welcome1


</span></code></pre></li>
* You will see the below screen:
  ![Image alt text](images/gl100.png)

* From "Payables Manager", navigate to "Payables Command Center"
  ![Image alt text](images/pl1.png)



* From Supplier Balance dashboard, Enable Personalization Mode by clicking on the "i" icon (on the top left of the page, beside the share icon) to edit the dashboard as a Power User

  ![Image alt text](images/jda1.png)
* The personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon

  ![Image alt text](images/jda2.png)

* Remove existing Tag cloud by clicking on Tag cloud's "x" icon and then replace Tag cloud with a Pie chart (Pie is the default visualization in Chart component)

* Delete the Tag cloud component  


  ![Image alt text](images/jda3.png)

* Add a chart (Pie chart) that replaces the deleted Tag cloud. You can do this by going to the bottom of the page and clicking the "Open components list" icon
  ![Image alt text](images/opencomponentlist.png)

* Go to the top of the page and drag  chart component into the dashboard

* Now edit the configuration of the chart. 

    1. Data set: Installaments 
    2. Chart type: Pie (Default is Pie, keep it as is)
    3. Dimension: Validation status
    4. Metric: Invoice with Aggregation as (count distinct) 
* Click preview and then Save

  ![Image alt text](images/jda5.png)

* Add a new Tab in the existing Tab component. To do this you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. Name this tab "Bank Balance"

  ![Image alt text](images/jda6.png)

  ![Image alt text](images/jda7.png)

* Click preview and then Save
  ![Image alt text](images/jda8.png)

* Add a chart component inside the new tab "Bank Balance" to highlight paid amount per bank account

    1. Data set: Payments 
    2. Chart type: Bar
    3. Dimension: Bank Account
    4. Metric: Paid amount with Aggregation as (Sum) 

* Click preview 

  ![Image alt text](images/jda9.png)
* This gives cash outflow across all currencies, now add additional dimension to split the chart per currency.

* Add "Currency" as Trellis dimension
* Click preview and then Save

  ![Image alt text](images/jda10.png)
  ![Image alt text](images/jda11.png)


* In addition of viewing detailed payments add a Pivot view

* Add New Component- Aggregate Table (Pivot view is an alternate visualization of the Aggregate Table component)
    * Data set: Payments
    * Dimensions:
         * Supplier name
         * Supplier site
         * Currency name (This will become the Column when Pivot visualization is selected)
    * Metric:
         * Paid amount with Aggregation as (Sum)
* Click preview 

* This gives Per supplier, per supplier site totals of invoice paid amount.

  ![Image alt text](images/jda13.png)
* Enable Pivot view and Sub summary and then click preview

  ![Image alt text](images/jda14.png)

* Save the configuration


  ![Image alt text](images/jda15.png)


## Task 2: Run dataload for General Ledger Command Center

You have already run dataload for Payables command center. The steps are similar here.

* Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials


 <pre><span class="hljs-attribute">
 Username: eccuser
 Password: welcome1
 Responsibility: General Ledger Super User


</span></code></pre></li>


* Navigate to "General Ledger Command Center"

* When the dashboard appears change the function id in the dashboard to <b>1011696</b> as done before in the Payables command center. 

   ![Image alt text](images/jda100.png)


* You will then see the below screen



   ![Image alt text](images/jda101.png)

* Choose "General Ledger Command Center Data Load" in the Program name by copying it from below and pasting in the Program Name
<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">General Ledger Command Center Data Load

</span></code></pre></li>
* You will see the below screen
   ![Image alt text](images/jda102.png)

* From "Parameters" tab choose the Load type as  <b>FULL_LOAD</b>, Set Ledger ID as <b>1</b> and Set/Reset Data as <b>TRUE</b>, this will wipe out all the records in the dataset.
   ![Image alt text](images/jda103.png)

* Click on "Submit"

   ![Image alt text](images/jda104.png)
   ![Image alt text](images/b10.png)

* Track the data load progress
   ![Image alt text](images/b11.png)

* You can also track the dataload in ECC Dataload Tracking page by logging in (http://apps.example.com:8000/ecc) via below credentials, using the Concurrent Program ID:

<pre><span class="hljs-attribute">
Username: eccadmin
Password: welcome1
</span></code></pre></li>

* You will see the below screen
   ![Image alt text](images/gl3.png)

## Task 3 : Personalize Account Analysis dashboard 

* Login to EBS apps (Navigate to http://apps.example.com:8000) with below credentials

 <pre><span class="hljs-attribute">
 Username: eccuser
 Password: welcome1
 </span></code></pre></li>

* You will see the below screen,  From <b>General Ledger Super User </b> responsibility navigate to <b>General Ledger Command Center</b>

  ![Image alt text](images/gl100.png)

   <b>Goal</b>:: Investigate and Act To Maintain the Accuracy Of Financial Records

* From General Ledger Super User navigate to General Ledger Command Center and then to Account analysis dashboard. Personalize the dashboard to view employee expenses by the parent account by clicking on the "i" icon to edit the dashboard as a Power User
  ![Image alt text](images/gl200.png)

* The personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon

  ![Image alt text](images/gl300.png)

* By default the dashboard is populated with the oldest period, Jan-07. Replace this period Jan-07 with Apr-23 in selected refinements to view latest data 
  ![Image alt text](images/home1.png)


* Add another refinement Account type : "Expense", by clicking on expense from the charts


  ![Image alt text](images/home56.png)

* You will see that the chart automatically cascades to display different accounts because cascading is enabled and configured by admin
  ![Image alt text](images/home23.png)

* Add a new Tab in the existing Tab component. To do this you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. 

  ![Image alt text](images/home5.png)
* Add Tab Title as "Period Activities by Department and Parent Account"

  ![Image alt text](images/home33.png)


* Click preview and then Save
 
* Add a new bar chart  inside the tab and configure the chart with the below details:

    1. Dataset: GL Account Analysis
    2. Chart type: Bar
    3. Group dimension: Cost Center
    4. Series dimension: Parent account 1
    5. Trellis column: Period Name
    6. Metric: Period Activity (no aggregation)

* Click preview 


  ![Image alt text](images/home44.png)
* Save the configuration. You will be able to see a combined view of account segment and hierarchy
  ![Image alt text](images/home45.png)






## Learn More
* [Enterprise Command Centres- User Guide](https://docs.oracle.com/cd/E26401_01/doc.122/e22956/T27641T671922.htm)
* [Enterprise Command Centres- Admistration Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f34732/toc.htm)
* [Enterprise Command Centres- Extending Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f21671/T673609T673618.htm)
* [Enterprise Command Centres- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)
* [Enterprise Command Centres- Direct from Development videos](https://learn.oracle.com/ols/course/ebs-enterprise-command-centers-direct-from-development/50662/60350)
* [Enterprise Command Centres for E-Business Suite- Technical details and Implementation](https://mylearn.oracle.com/ou/component/-/117416)

## Acknowledgements

* **Author** - Muhannad Obeidat, VP
* **Contributors** -  Muhannad Obeidat, Nashwa Ghazaly, Mikhail Ibraheem, Rahul Burnwal and Mohammed Khan
* **Last Updated By/Date** - Mohammed Khan, March 2023

