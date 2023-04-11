# Power User Personalisation

In ECC Power users can modify a dashboard to tailor it based on their business requirements. This lab walks you through the steps to Personalise an existing dashboard to suit it to your business requirement with an example. 

Estimated Time: 20 minutes


A Power User has:

*	Same designer experience as admin
*	Enabled at the user level using the profile option “FND: ECC Power User Enabled.”
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
* Personalize the Account Analysis dashboard to maintain the accuracy of financial records
* Personalize the Supplier Balance dashboard to track cash outflow for invoice payments per bank account so that you can analyze payment trends

### Prerequisites (Optional)

This lab assumes you have:
* An Oracle Cloud account
* All previous labs successfully completed
* Have run the respective dataloads needed for General Ledger Command Center and Payables Command Center




## Task 1: Personalize Supplier Balance dashboard 

<b>Goal</b>: As a Payables Accountant, I want to track  cash outflow for invoice payments per bank account so that I can analyze payment trends 

Personalize dashboard to reflect payments per supplier and supplier site. 

Login to EBS apps (VNC url and then in browser open localhost:8000) using

Username: Aperkins
Password: welcome
Responsibility: Payables Manager
![Image alt text](images/ebsapps.png)

* Click on Payables Manager and then on Payables Command center
![Image alt text](images/ebspayables.png)



* From Supplier Balance dashboard, Enable Personalization Mode by clicking on the i icon to edit the dashboard as a Power User

![Image alt text](images/Personalisation_AP_1.png)
* The personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon
![Image alt text](images/Personalisation_AP_2.png)

* Remove existing Tag cloud and replace it with a Pie chart

Delete the Tag cloud component  


![Image alt text](images/deletetag.png)

* Adda a Pie chart that replaces the deleted Tag cloud 

![Image alt text](images/pie.png)

* Add a new Tab in the existing Tab component 
![Image alt text](images/tab.png)


* Add a chart to highlight paid amount per bank account

![Image alt text](images/chart.png)
This gives cash outflow across all currencies, now add additional dimension to split the chart per currency.

Add "Currency" as Trellis dimension

![Image alt text](images/charttrellis.png)
![Image alt text](images/charttrellis2.png)


In addition of viewing detailed payments add a Pivot view

* Add New Component- Aggregate Table. This gives Per supplier, per supplier site totals of invoice paid amount.

![Image alt text](images/pivot1.png)
* Enable Pivot view and Sub summary
![Image alt text](images/pivot2.png)

![Image alt text](images/pivot3.png)




## Task 2 : Personalize Account Analysis dashboard 

Login to EBS apps (VNC url and then in browser open localhost:8000) using

Username: Aperkins
Password: welcome
Responsibility: General Ledger Super User
![Image alt text](images/ebsapps.png)

<b>Goal</b>:: Investigate and Act To Maintain the Accuracy Of Financial Records

* From Account analysis dashboard Personalize the dashboard to view employee expenses by the parent account by clicking on the i icon to edit the dashboard as a Power User

![Image alt text](images/AP1.png)
* The personalization icon changes to blue when the dashboard is in edit mode. All components in the dashboard will now have the configuration and delete icon
![Image alt text](images/AP2.png)

* Add a new tab inside the tab component

![Image alt text](images/ap4.png)
* Add Tab Title
![Image alt text](images/ap5.png)
* Add a new chart inside the tab and Configure the chart

![Image alt text](images/ap6.png)
* Add "Period Activity" in Metrics
![Image alt text](images/ap7.png)
* Have a combined view of account segment and hierarchy

![Image alt text](images/ap8.png)





## Learn More
* [Enterprise Command Centres- User Guide](https://docs.oracle.com/cd/E26401_01/doc.122/e22956/T27641T671922.htm)
* [Enterprise Command Centres- Admistration Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f34732/toc.htm)
* [Enterprise Command Centres- Extending Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f21671/T673609T673618.htm)
* [Enterprise Command Centres- Installation Guide](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=264801675930013&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1c6rxqpyoj_102)
* [Enterprise Command Centres- Direct from Development videos](https://learn.oracle.com/ols/course/ebs-enterprise-command-centers-direct-from-development/50662/60350)
* [Enterprise Command Centres for E-Business Suite- Technical details and Implementation](https://mylearn.oracle.com/ou/component/-/117416)

## Acknowledgements

* **Author** - Muhannad Obeidat, VP
* **Contributors** -  Muhannad Obeidat, Nashwa Ghazaly, Mikhail Ibraheem, Rahul Burnwal, Mohammed Khan
* **Last Updated By/Date** - Mohammed Khan, March 2023

