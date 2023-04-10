#  Create ECC schema and Install Weblogic Server


This lab walks you through the steps to create ECC schema and to install weblogic server so that you can set up Oracle Enterprise Command Center Framework



Estimated Time: 30 minutes

### Objectives
In this lab, you will:
* Create ECC schema and install Weblogic Server


### Prerequisites

This lab assumes you have:
* Completed the previous section successfully 

##  


## Task 1: Extract quickInstall 

* Open terminal and navigate to /u01 directory by using below command

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">cd /u01

</span></code></pre></li>

* .bsx files are downloaded in /u01 directory. Extract the .bsx files by running the below command from /u01 directory 




<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">for f in *.bsx; do sh $f; done

</span></code></pre></li>

![Image alt text](images/quickinstall.png)

* This process will take a few minutes. After extraction is completed, navigate to cd /u01/Oracle/quickInstall

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">cd /u01/Oracle/quickInstall

</span></code></pre></li>


<b>Note: </b>In this directory (Oracle/quickInstall) there is a file called "EccConfig.properties", which has all the parameters predefined for this Hands-on-lab. You don't have to change any parameters but described below are some important parameters you should keep in mind. 


<b>ECC_BASE</b> - The root directory where you extracted the .bsx files. This property is set to the value /u01 by default.

<b>ECC\_CONFIG\_LOC</b> - You can optionally set this property to the location of a custom ecc-config.properties file. Oracle Enterprise Command Center Framework will then use the properties file in this location instead of the standard ecc-config.properties file created in the $ECC_BASE/Oracle/quickInstall/env/ecc directory.

<b>ECC\_LOG\_DIR</b> - The directory where the Oracle Enterprise Command Center Framework administration application log files should be generated. For cluster setup, this directory must be shared between all nodes. All nodes must have read and write access to this shared directory.

<b>EBS\_MIDDLETIER\_HOST\_FQDN</b> - The fully qualified domain name (FQDN) for the Oracle E-Business Suite application tier. If the Oracle E-Business Suite instance uses a proxy or load balancer, use the FQDN for the web entry point instead.

<b>EBS\_MIDDLETIER\_PORT</b> - The Oracle E-Business Suite application tier port. If the Oracle E-Business Suite instance uses a proxy or load balancer, use the port for the web entry point instead. If you plan to enable TLS for communication between Oracle E-Business Suite and the Oracle Enterprise Command Center Framework installation, then you should use port 4443 here. See Enabling TLS for Oracle Enterprise Command Center Framework, Release 12.2, My Oracle Support Knowledge Document 2496445.1.

<b>EBS\_MIDDLETIER\_PROTOCOL</b> - The Oracle E-Business Suite application tier protocol, either http or https. If the Oracle E-Business Suite instance uses a proxy or load balancer, use the protocol for the web entry point instead. If you plan to enable TLS for communication between Oracle E-Business Suite and the Oracle Enterprise Command Center Framework installation, then you must set the protocol to https here. See Enabling TLS for Oracle Enterprise Command Center Framework, Release 12.2, My Oracle Support Knowledge Document 2496445.1.

<b>EBS\_MIDDLETIER\_INTERNAL\_HOSTS</b>- The host name of the Oracle E-Business Suite instances. If there is more than one Oracle E-Business Suite instance behind a load balancer, specify all the Oracle E-Business Suite host names separated by a comma.

For further information please refer to section 4.3.1 of the following document
[Installing Oracle Enterprise Command Center Framework](https://mosemp.us.oracle.com/epmos/faces/ui/km/DocumentDisplay.jspx?_afrLoop=263547950196438&id=2495053.1&_afrWindowMode=0&_adf.ctrl-state=1can4pxb6b_4#schemabackup)



## Task 2: Create ECC Schema

* From the terminal navigate to /u01/Oracle/quickInstall using below command

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">cd /u01/Oracle/quickInstall

</span></code></pre></li>

* Execute the below script and when prompted choose <b>Option 1</b> to create ECC schema. 

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute"> ./envSetup.sh
</span></code></pre></li>


![Image alt text](images/selectoption.png)




* This step creates the ECC schema and provides an option to use the existing ECC user created in the ECC database:

<pre style=""><code class="hljs ini">Selected ECC DB is jdbc:oracle:thin:@ebs.org:1521:ebsdb
Is the user <ECC_DB_USERNAME> existing in ECC database [y/n]?<password>

</code></pre>


* If you choose option “y”, you are prompted for ECC user credentials to create the ECC schema. If you choose the option “n”, you are prompted to enter ECC database system user credentials to create the ECC user and later create the ECC schema.

* For this demo type <b>  "n" </b>

* When prompted provide the database system user details, mentioned below:
 <pre><span class="hljs-attribute">
Database system username: <b>system</b>
Database system password: <b>manager</b>
Password for ECC DB User: <b>welcome1</b>


</span></code></pre></li>


![Image alt text](images/eccschema0.png)


* <b>Option 1</b> should be completed successfully. You can verify the logs in $ECC_BASE/Oracle/quickInstall/logs/setup.log

* Enter <b>Option 6 </b>  to exit and then execute following commands to validate  successful ECC schema creation:


<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">source env/ecc.env


</span></code></pre></li>

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">
source /u01/install/APPS/19.0.0/ebscdb_apps.env


</span></code></pre></li>

* Execute the following command with the credentials mentioned:

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute">
sqlplus $ECC_DB_USER@"(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=$ECC_HOST_NAME)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=$EBS_DS_NAME)))"</span></code></pre></li>

 <pre><span class="hljs-attribute">
Password: <b>welcome1</b>


</span></code></pre></li>


![Image alt text](images/systemmanager1.png)

* If you are able to log in to SQL and receive a SQL> prompt, then the ECC DB connection is available to use. 

* Exit from the SQL prompt by typing <b>exit;</b>

## Task 3: Install Weblogic Server

* Make sure you are in the  /u01/Oracle/quickInstall directory 

* Run the ./envSetup.sh script again and when prompted choose <b>Option 2</b> to Install Weblogic Server 

<pre><button class="copy-button" title="Copy text to clipboard">Copy</button><code class="hljs apache"><span class="copy-code"><span class="hljs-attribute"> ./envSetup.sh
</span></code></pre></li>



![Image alt text](images/selectoption.png)

![Image alt text](images/weblogic0.png)
![Image alt text](images/weblogic.png)


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

