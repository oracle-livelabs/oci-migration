# Create ECC Domain

### Introduction


This lab walks you through the steps to create and validate ECC domain so that you can set up Oracle Enterprise Command Center Framework

Estimated Time: 30 minutes

### Objectives
In this lab, you will:
* Create and validate ECC domain
* Validate ECC Release


### Prerequisites

This lab assumes you have:
* Completed all previous labs successfully 

##  

## Task 1: Create ECC Domain

1. After weblogic is installed you would be prompted to submit the next option in the installation steps in which case you should  select **Option 3** otherwise execute the ./envSetup.sh script again and then choose **Option 3** to Create ECC domain. 


    ```
  	 <copy>./envSetup.sh</copy>
    ```
    ![Select option 3](../images/selectoption.png "Select option 3")


2. As part of creation of ECC domain, following are the key tasks performed (no action required in this lab):
    ![These are the key tasks performed](../images/eccdomain.png "Key tasks performed")
    - Enter the password for ECC DB user as **welcome1** 
    - Set the password for ECC user weblogic as **welcome1**



    ![Create ECC domain by entering ECC dB user and weblogic passwords](../images/weblogic1000.png "Create ECC domain")

3. After completing successfully you will see the below screen

    ![Create ECC domain](../images/eccdomainsuccess.png "Create ECC domain")


## Task 2: Validate ECC Domain

1. From the browser navigate to the below URL 

    ```
  	 <copy>http://localhost:7776/ecc</copy>
    ```

**Note:** If you are not able to type in the remote desktop browser then please hit the command key


   * ECC Administrator UI should be accessible i.e., you should see the highlighted section in below  screen
   * Activity audit application should be imported i.e., you should see Activity audit application in home screen


    ![Validate ECC domain](../images/validateeccdomain6.png "Validate ECC domain")




## Task 3: Validate ECC Release


1. From the browser navigate to the below URL


    ```
  	 <copy>http://localhost:7776/ecc</copy>
    ```

2. ECC Administrator UI should be accessible.

   * In **About** page “Enterprise Command Centers:” should be shown as ‘V12’.

   * “Oracle JavaScript Extension Toolkit (JET) :” should be shown as 15.1.6

   * “SOLR” should be shown as 8.8.2

    ![Validate ECC release](../images/validateabout5.png "Validate ECC release")



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

