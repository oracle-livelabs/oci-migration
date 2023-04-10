# Diagnose and monitor 


### Introduction

This lab walks you through the steps to general steps performed in diagnosing and monitoring Oracle Enterprise Command Center framework

Estimated Time: 10 minutes


### Objectives

In this lab, you will:
* Learn how to access Server, Application, OHS and OPMN Logs
* Learn how to access Log monitor
* Capture Loading Time for ECC Page
* Learn how to download HAR file
* Learn how to take advantage of Activity Audit

* Learn how to run ECC Analyzer
* Identify common issues

### Prerequisites 

This lab assumes you have:
* Completed all previous labs successfully 


##  

## Task 1: Diagnose and Monitor 
 <b> Location of Server Logs </b>
 
 Note the location of Server logs:

![Image alt text](images/serverlogs.png)
 <b> Location of Application Logs </b>

 Note the location of Application logs:

![Image alt text](images/applicationlogs.png)

 <b> Location of ohs Logs </b>

/u01/install/APPS/fs2/FMW\_Home/webtier/instances/EBS\_web\_OHS1/diagnostics/logs/OHS/EBS\_web

 <b> Location of opmn Logs </b>

/u01/install/APPS/fs2/FMW_Home/webtier/instances/EBS\_web\_OHS1/diagnostics/logs/OPMN/opmn

 <b> Log monitor </b>

Login to EBS as Admin user with eccadmin responsibility access

<pre><span class="hljs-attribute">
 Username: eccadmin
 Password: welcome1


</span></code></pre></li>



<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute"><div style="color:grey"> 


(http://&lt;EBS_MIDDLETIER_HOST_FQDN&gt;:&lt;EBS_MIDDLETIER_PORT&gt;/ecc/monitor/logs)

</div>
</span></code></pre></li>




![Image alt text](images/logmonitor.png)

<b>Capture Loading Time for ECC Page</b>

* Open the Oracle E-Business Suite Enterprise Command Center application in the Google Chrome browser. 
* Log in and navigate to the page you want. Then open the Chrome tools by pressing the F12 button on the keyboard, or by pressing Ctrl+Shift+I. 
* The Development Tools window occupies the lower part of the page. Select the Network tab

![Image alt text](images/eccinspectelement.png)

<b>Download HAR file</b>


To analyze performance deeply download HAR file:

* Open browser developer tools via inspect element (in chrome)
* Navigate to "Network" tab
* Click on the download icon highlighted below
![Image alt text](images/harfile.png)


## Task 2: Learn about Activity Audit 

The Activity Audit dashboard gives full insight into the use of the Enterprise Command Center dashboards. It allows business analysts and administrators to know whether dashboards are being used or not, who uses them, and at what times and which dashboard is used more. It also helps generate valuable new insights into user searches.

Activity Audit provides the following benefits:

 * Capitalize on ECC investment

 * Track dashboard usage

 * Capture audit trail of user activities on dashboards

 * Tune deployment and tune extract, transform, and load (ETL) processes

 * Tune business operations

 * Monitor search activity

 * Identify and analyze user intents

 * Resolve issues as they arise

To access the dashboard, navigate to the Activity Audit section in the Administration UI.

![Image alt text](images/lab10_activityaudit.png)

<n>Tracking User Activity</n>
Nine types of user activity are tracked, as follows:

* Action Details: Refinements that are applied on the dashboard due to user action. Multiple values of an attribute are separated by '|'. Each filter is captured along with the corresponding data set.

* Filters Applied: Total filters in Selected Refinements. Multiple values of an attribute separated by '|'. Each filter is included along with the corresponding data set.

* Component Title: Title of the component where the user action has been performed.

* Component Type: Type of component where the user action has been performed.

* Number of Results: Total number of records in detailed insight components (Results Table and Grid) after the user action.

* Application Name: Name of application for the dashboard.

* Page Name: Name of dashboard.

* Data Set Name: Name of the data set for the user action.

<n>Enabling Activity Audit</n>
The following properties in the EccConfig.properties file control activity auditing. This feature can be enabled during installation by setting the properties in EccConfig.properties. For more details on installation, refer to Installing Oracle Enterprise Command Center Framework, My Oracle Support Knowledge Document 2495053.1.

* Set the property ecc.activity.audit.isenabled to true or false for enabling or disabling the feature respectively.

* Add the data sets to the property ecc.activity.audit.enabled.datasets = <data set 1>, <data set 2> for capturing user activities in the dashboards configured with these data sets. Each data set key must be separated by a comma (,). By default, no data set is specified.

<n>Note</n>: If the property is not set with any data set, the feature will be enabled to all the data sets. Dashboards (and corresponding data sets) with frequent usage where user activity needs to be captured for compliance or analytical purposes should be considered for activity audit.

* Set the property ecc.activity.audit.ingest.limit to define the limit on the number of user actions beyond which a Data Load is triggered to refresh the dashboard data. The default limit is 100. This can be updated to adjust the frequency of data loads based on the number of dashboards, users and the average activity.

<b>Capturing User Activity </b>

User activity is captured if Activity Audit application is available.

On Oracle Enterprise Command Center Framework server startup, the Activity Audit data is ingested to Oracle Enterprise Command Center Framework asynchronously by following the above procedure.

Users need not submit a data load separately. If a data load is submitted, it resets the data set and once the scheduled query load is triggered, the updated data is ingested into the Activity Audit data set.

<b>Application and Data Set Details </b>

* Dataset Name: Activity Audit

* Dataset Key: activity-audit

* Application Name: Activity Audit

* Application Short Name: activity-audit

* Page Name: Activity Tracker

* Page Short Name: activity-tracker

The Activity Audit dashboard is designed to support two use cases: tracking user activity and tracking search activity.
![Image alt text](images/lab10_activityaudit2.png)


For more information on Activity audit please refer to [Enterprise Command Centres- Admistration Guide](https://docs.oracle.com/cd/E26401_01/doc.122/f34732/T676250T676672.htm#8723752)

## Task 3: Learn about ECC Analyzer 
* The EBS Enterprise Command Center (ECC) Analyzer is a self-service health-check script that reviews Oracle Enterprise Command Center related data, analyses current configurations and settings for the environment and provides feedback and recommendations on best practices. 
* The Analyzer collects data using all the tables necessary to diagnose issues and provides solutions and recommended actions. 
![Image alt text](images/eccanalyzer1.png)

<b>NOTE</b>:  Analyzer does not perform any INSERTs, UPDATEs or DELETEs to your data; it just reports on it.


<b>ECC Analyzer: Technical Requirement</b>

* Requires Java 1.7+
* Available on Linux platforms only

<b>Verify java version</b>

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">$ java –version
</span></code></pre></li>

<b>Running Analyzer</b>
To run Analyzer as a java program follow below instruction. The java program will prompt for the WebLogic and APPS usernames and passwords.

![Image alt text](images/eccanalyzer2.png)


<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">  $ java -	Danalyzer="ecc_analyzer.xml" -jar HA.jar

</span></code></pre></li>

<b>ECC Analyzer: Sample Output</b>

* Analyzer generates a zip file containing all the script outputs and the analyser html report(ATGECCHA_<date>.html). 

* When running the analyzer as a java program
  EBS Enterprise Command Center (ECC) Analyzer output zip file is located in the same directory where it was run.  This location is also displayed in the window after execution. 

![Image alt text](images/eccanalyzer3.png)

Html page contains all the information about the ECC environment being analysed. Below are some of the sample outputs:

![Image alt text](images/eccanalyzer4.png)
![Image alt text](images/eccanalyzer5.png)
![Image alt text](images/eccanalyzer6.png)


## Task 4: Identify common issues 
* You will see the below screen if you are authenticated but not authorized to view the dashboard. You need to use the right responsibility to access the dashboard 

  ![Image alt text](images/auth.png)

* You will see the below screen if you are not authenticated/ or not logged in to EBS

  ![Image alt text](images/auth2.png)

* You will see the below screen if ECC isn’t integrated with EBS (ecc.conf is missing).
  ![Image alt text](images/ECCmissing.png)
* You will see the below screen if ECC is integrated with EBS but ECC is down.

  ![Image alt text](images/ECCdown.png)

You may now  **proceed to the next lab**

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

