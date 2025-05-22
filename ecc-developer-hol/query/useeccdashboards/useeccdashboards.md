# Use ECC Dashboards- Introduction to Information Discovery and User Preferences


### Introduction

This lab walks you through the a few demo flow scenarios that will help you learn the basics of Oracle Enterprise Command Center framework.

Estimated Time: 45 minutes

### Objectives
In this lab, you will:
* Learn about three different command centers and how you can do basic information discovery
* Learn 17 different ECC framework components and features 




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

<h2>Features demoed in this Lab:</h2>

<table>
  <tr>
    <th>Type</th>
    <th>Feature</th>
    
  </tr>

  <tr>
    <td>Visualization</td>
    <td> 
    1. Summarization bar: Flag<br/>
    2. Summarization bar: Metric<br/>
    3. Summarization bar: Filter Chip<br/>
    3. Chart Cascading<br/>
    4. Diagram: Pagination<br/>
    5. Diagram: Compare<br/>
    6. Diagram: Find similar<br/>
    7. Diagram: Actions<br/>
    
     
   
  </tr>
    <tr>
    <td>Navigation</td>
    <td> 
    1. Key Flexfields support <br/>
    2. Record Search<br/>
    3. Available refinements: Multi/single select from list<br/>
    4. Selected refinements: Breadcrumb<br/>
    5. Available refinements: Attribute Groups<br/>
    <tr>
    <td>End user personalization</td>
    <td> 
    1. Runtime options<br/>
    2. Runtime options: Charts<br/>
     
   
  </tr>
    <tr>
    <td>Detailed Insights</td>
    <td> 
    1. Row actions<br/>
    2. Results table: Actions<br/>
    
     
   
  </tr>

</table>
</body>
</html>

    
   



### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 

## Task 1: Open Your Workshop Guide

1. If the *Web* browser window(s) is(are) not already open side-by-side, double-click the *Get Started with your Workshop* icon from the remote desktop. This will launch one or two windows depending on the workshop.

    ![Get Started with your Workshop](../images/novnc-launch-get-started-1.png " ")

2. On the left window is your workshop guide and depending on your workshop, you may also have one or two browser tabs loaded with web apps. e.g. Weblogic console, Enterprise Manager Cloud Console, or a relevant application to your workshop such as SQL Developer, JDeveloper, etc.

    ![Workshop guide and sample webapp](../images/novnc-launch-get-started-2.png " ")

You may now **proceed to the next task**.

## Task 2: Validate integration of EBS and ECC 



1. Navigate to http://<VNC\_Public\_IP\>:8000 in the browser with below credentials 
   

    ```
  	 Username: SYSADMIN
Password: welcome1
    ```
  
    You should ideally see the below screen then
    ![Validate ECC](../images/val1.png "Validate ECC")
    If you encounter the below error we recommend to wait for 15 minutes 
    ![Validate ECC](../images/ecc.png "EBS ECC ERROR")

2. Navigate to ECC Developer, you should be able to see the applications as shown in the below image, if the integration is successful
    ![Validate integration of EBS and ECC](../images/val2.png "Validate integration")
3. Click on the "Activity audit" application.

    ![Activity audit](../images/activityaudit.png "Activity audit")

4. Click on the "Activity Tracker" page
    ![Activity audit](../images/activityaudit2.png "Activity audit")

5. The Activity Tracker dashboard is displayed. This validates the integration of EBS and ECC
    ![Activity audit](../images/activityaudit3.png "Activity audit")

## Task 3: Hands on demo of ECC Fixed Assets

**Goal:** Tune Business Operations and Improve Data Quality. 

1. Login to EBS apps (From the browser URL navigate to http://<VNC\_Public\_IP\>:8000) with below credentials

    ```
  	 Username: aperkins
Password: welcome1
    ```
2. Navigate to Fixed Assets Manager -> Assets Command center and then to "Asset Location" dashboard
    ![Assets Location](../images/fix1.png "Assets Location")

3. Click on "Assets Book" Filter Chip to select a book [The Filter Chip feature, displays the count of the configured dimension. Users can make a selection at runtime from the pop up as demonstrated here]
    ![Assets Location](../images/fix21.png "Assets Location")
4. Click on "OPS CORP" Book Type Code from the "Assets Book" Filter Chip.
5. Click on "Unassigned Assets" metric in the summarization bar component to track the unassigned assets. [Metrics display the value of a specific metric, they can be configured to be either to navigate to a destination dashboard or tab and optionally invoke a refinement action or have no action at all].
    ![Assets Location](../images/fix3.png "Assets Location")
6. From the Tag cloud named "Unassigned Assets by Category", click on "Computer" to filter for "Computer" category [The tag cloud cascades to the next level defined by the designer. Any value clicked from a tag cloud would result in refinement and the entire page will be refined for that particular value].
    ![Assets Location](../images/fix4.png "Assets Location")
7. Drill down to sub-categories by clicking on "PC" from the "Unassigned Assets by Category" tag cloud
    ![Assets Location](../images/fix5.png "Assets Location")
8. From the Chart named "Units assigned by State/County", click on "California" location track assets by location flexfield segments [Key flexfield support for location segment. Locations are displayed with dynamic label].
    ![Assets Location](../images/fix6.png "Assets Location")
9. From the Chart named "Units assigned by City" [The chart title has changed after cascading as it is dynamic], click on "San Francisco" city to track assets by location flexfield segments
    ![Assets Location](../images/fix7.png "Assets Location")

10. In the search bar type "laptop", ignore the suggestion list and hit enter to search for Laptop Assets. [This is a record search which allow user to perform a keyword search against specific attribute values assigned to records. The resulting records that have matching attribute values are returned, along with any valid refinement values]

    ![Assets Location](../images/fix8.png "Assets Location")

11. From the "Assignment Details" Results table click on the "Asset Assignment" Row action for the Asset number "100640" to navigate to the Asset workbench [This feature is called "Row Actions" where in you can choose to configure an action that can either open in a new tab, drawer, pop up] .
    ![Assets Location](../images/fix9.png "Assets Location")
12. You will see the assignment form with selected asset, and assign asset to employee [As forms are not accessible in the environment provided, so you can skip this step]
    ![Assets Location](../images/fix10.png "Assets Location")



## Task 4: Hands on demo of ECC Procurement

**Goal:** Inspect individual order details. 

1. Login to EBS apps (From the browser URL navigate to http://<VNC\_Public\_IP\>:8000) with below credentials

    ```
  	 Username: operations
Password: welcome1
    ```

1. Navigate to Purchasing, Vision Operations (USA) -> Procurement Command Center and then to "Procurement Operations" dashboard
    ![Procurement Command Center](../images/pro1.png "Procurement Command Center")
2. Within "Procurement Operations", navigate to "Orders" dashboard.Click on the "i" icon, this displays all the data sets used in the dashboard along with the last or latest date of the updated time.
    ![Procurement Command Center](../images/p1000.png "Procurement Command Center")



7. Scroll to the bottom of the page to view the Results table, here click on the three horizontal dots (used to denote actions) and view the actions configured in this Results Table
    ![Procurement Command Center](../images/pro5.png "Procurement Command Center")
    * You can see two row actions: View and Order details.
    * Click on "Order details" (for the Order 9346, as this is the order we are interested in investigating), which is a hyperlink to a different ECC dashboard, we are now navigating from Orders page, which has details of all orders to a page which has details on only this particular order i.e., the order specified in this row.
11. As you can see we are navigated to the Order details page, with "Order" and "Operating Unit" already applied in Selected refinements. ECC allows you to configure what attributes you want to refine for, when you are navigating to the row action dashboard, in this case it is "Order" and "Operating Unit".
    ![Procurement Command Center](../images/pro6.png "Procurement Command Center")
12. From the selected refinements, you can click on the 
"Order" value refinement to either replace the "Order" or click on the attribute name "Order" to replace/add more orders to refine the page.
    ![Procurement Command Center](../images/pro7.png "Procurement Command Center")

13. Click on the side navigation panel on the top left to open the "Available refinements" section and from "Schedules Summary" Attribute group click on "Ship-To location" attribute [Attribute group is a grouped list of attributes with each group representing a functional or logical grouping for a set of attributes] and select "M-1 Seattle Mfg" value as this is the specific order line we want to investigate.
    ![Procurement Command Center](../images/pro8.png "Procurement Command Center")
14. We can view the individual order line for this particular order and conclude our analysis.
    ![Procurement Command Center](../images/ki.png "Procurement Command Center")

## Task 5: Hands on demo of ECC Inventory Management 

**Goal:** Investigate picks to find a common cause. 


1. Login to EBS apps (From the browser URL navigate to http://<VNC\_Public\_IP\>:8000) with below credentials

    ```
  	 Username: mfg
Password: welcome1
    ```
2. Navigate to Logistics Manager -> Command Center and then to "Track and Trace" dashboard
    ![Move Orders](../images/log1.png "Move Orders")

3. In the Track and Trace dashboard, click on the side navigation panel to open Available refinements
    ![Track and trace](../images/ju2.png "Track and trace")

4. Check the data set name. It has to be set to "Inventory Trace Sales Orders", if it is not then change it by clicking on the three vertical dots beside the name of the data set. 
    ![Track and trace](../images/invchangedataset.png "Track and trace")

5. Within this data set, under "Ship-To Location" attribute search for "Atlanta" as we are aware of issues originating from Atlanta [In Available refinements within a multi select list, you can search and select multiple values, and then click on filter to apply them in one go or you can choose to click on any one value and refine for that value immediately. Here we will do the latter].
    ![Track and trace](../images/ju1.png "Track and trace")

6. The diagram of orders from Atlanta will be displayed. Within this diagram we want to focus on three known problematic sales orders "66007", "66008" and "66014". Hold control key and select all three sales orders, now select "Highlight Path" from the pop up to highlight their paths [You can see at the bottom of the diagram there is a small but concise overview of the diagram, in this example we only have one diagram but the feature allows for multiple diagrams to be shown in a paginated manner if the refinement were to result in completely distinct diagrams].

    ![Track and trace](../images/ju3.png "Track and trace")
    ![Track and trace](../images/ju4.png "Track and trace")

7.  Expand Staging Location to see individual tasks, by clicking on the arrow icon highlighted in the below image [This feature consolidates all related items in one node]

    ![Track and trace](../images/ju5.png "Track and trace")

8. Investigate relevant tasks, hold control key and select the relevant picks and then click on "Compare"
["Compare" feature allows a user to compare multiple nodes in one go].
    ![Track and trace](../images/ju6.png "Track and trace")
9. We find they have different lot numbers, different sub inventory, different locator and different item. Let's investigate Pack transactions now
    ![Track and trace](../images/ju7.png "Track and trace")

10. Select and compare the relevant pack transactions by holding control key, selecting all the three relevant pack transactions and then clicking on "Compare"

    ![Track and trace](../images/ju9.png "Track and trace")


11. User "New Hire" packed all 3 ‘problem’ different items
    ![Track and trace](../images/ju10.png "Track and trace")

12. Select "New Hire" and then click on "Find Similar" to find other pack transactions by New Hire ["Find similar" feature allows you to investigate further using a particular attribute, in this case all sales orders handled by user "New Hire" will be refined].
    ![Track and trace](../images/ju11.png "Track and trace")
13. Page 1 has the 3 problem orders we already know about and a new, unrelated order is found on page 2 
    ![Track and trace](../images/ju12.png "Track and trace")
14. Click on the page 2 diagram to view it
    ![Track and trace](../images/ju13.png "Track and trace")
15.  You can find their status and prevent shipping by changing their inventory status from the material workbench.


We have reached the end of this lab, we covered 3 different demo flows and 17 different ECC framework features.


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




