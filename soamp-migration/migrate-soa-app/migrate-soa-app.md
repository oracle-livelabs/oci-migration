# Migrate the SOA Domain Application

## Introduction: 

Migrating a SOA domain is equivalent to re-deploying the applications and resources to a new domain and infrastructure.
Once source and target environments are ready for migration, you can transition your production system from the on-premises deployment to the OCI deployment.

We will use a manual process to migrate the domain from on-premises and re-deploy on OCI.

Estimated Lab Time: 45 minutes.

### About Product/Technologies

**Deploying, Undeploying, and Redeploying SOA Composite Applications**.

Oracle SOA Suite uses the SCA standard as a way to assemble service components into a SOA composite application. You can deploy, undeploy, and redeploy SOA composite applications.

SOA composite applications consist of the following:

Service components such as Oracle Mediator for routing, BPEL processes for orchestration, human tasks for workflow approvals, business rules for designing business decisions, and complex event processing for queries of event streams.

Binding components (services and references) for connecting SOA composite applications to external services, applications, and technologies.

These components are assembled together into a SOA composite application. This application is a single unit of deployment that greatly simplifies the management and lifecycle of SOA applications.

You can use Oracle Fusion Middleware Control, Oracle JDeveloper, or the command line to deploy, undeploy, or redeploy a SOA application.

The manual migration process consists of 3 steps:

- Convert the SOA code version from 12.2.1.3 to 12.2.1.4 by redeploying it in Oracle JDeveloper 12.2.1.4.

- Create the same directory structure used in the source SOA code on the target SOA server.

- Deploy the code on the SOA Suite version 12.2.1.4.

### Objectives

In this lab, you will:

- Discover the source SOA Suite environment and test the source code.
- Prepare your source for migration / side-by-side upgrade.
- Prepare your target environment.
- Transition from old deployment to new deployment.
- Check that the migration was successful.

### Prerequisites

To run this lab, you need to:

- Have setup the demo 'on-premises' environment as the source domain to migrate.
- Have deployed a SOA on OCI domain using the marketplace.

## Task 1: Discover the Source SOA Suite Environment

1. Open the EM console in the Firefox browser at [http://localhost:7001/em](http://localhost:7001/em)
in the on-premises environment.

    - Username: `weblogic`
    - Password: `welcome1`

    ![](./images/3-open-console.png)

2. Click the menu **icon**.

    ![](./images/menu.png)

3. Now click on top right button and go to **SOA_Domain -> SOA -> SOA-Infra**.

    ![](./images/4-open-project.png)

4. Then click the **Deployed Composites** tab.

    ![](./images/deployed-composites.png)

5. Search for the composite **IWSProj3[1.0]** used for migration in this lab.

    ![](./images/5-deployed-composite.png)

    This application is a simple file transfer composite which moves a test XML file from the `/tmp/soa/out` folder to the `/tmp/soa/out1` folder.

    The XML needs to be a valid XML file.

## Task 2: Test the Application

For testing, we'll place a test XML file in the `/tmp/soa/out` folder, wait 5 to 10 seconds to see the file be removed from the `/tmp/soa/out/` folder and moved to the `/tmp/soa/out1` folder as `File_1.txt`.


1. Create the necessary folders:

    ```
    <copy>
    mkdir -p /tmp/soa/out
    mkdir -p /tmp/soa/out1
    chmod -R 777 /tmp/soa/
    </copy>
    ```

2. Copy the test file into the `/tmp/soa/out/` folder:

    ```
    <copy>
    cd /tmp/soa/out
    cp /u01/training/OrderSampleOSB.xml ./
    </copy>
    ```

3. Check the file is in the `/tmp/soa/out` folder:

    ```
    <copy>
    ls -lh
    </copy>
    ```

4. Wait 5 to 10sec and check the file is now gone:

    ```
    <copy>
    ls -lh
    </copy>
    ```

5. Check the file `File_1.xml` was created in the `/tmp/soa/out1` folder:

    ```
    <copy>
    cd /tmp/soa/out1
    ls -lah
    </copy>
    ```

    It should show:

    ```
    File_1.xml
    ```

## Task 2: Prepare Your Source for Migration (Side-by-Side Upgrade)

In this step we will migrate the application from 12.2.1.3 (current version) to 12.2.1.4 (target version).

In order to achieve this, you will need to:

* Open the application in Oracle JDeveloper 12.2.1.3.
* Deploy the application as a SAR file.
* Open Oracle JDeveloper 12.2.1.4.
* Create a new project in Oracle JDeveloper 12.2.1.4.
* Import the SAR file generated in Oracle JDeveloper 12.2.1.3.
* Let the import wizard migrate the code to 12.2.1.4.
* Deploy the application with Oracle JDeveloper 12.2.1.4 as a SAR file.

*If you used the local VirtualBox VM, you downloaded JDeveloper 12.2.1.4 as part of the SOA Suite Quickstart 12.2.1.4.*

*If you used the Markletplace demo image, both 12.2.1.3 and 1.2.2.14 JDeveloper version are available on the desktop*

    ![](./images/soa-local-rdp.png)

1. Open Oracle Jdeveloper 12.2.1.3 on the on-premises desktop.

    ![](./images/jdev12213.png)

2. In the **Application** tab, select **IWSApplication**.

    ![](./images/open-iwsapplication.png)

3. Right-click on the Project **IWSProj3**.

    ![](./images/iwsproj3.png)

4. Select **Deploy -> Deploy IWSProj3...**.

    ![](./images/deploy-iwsproj3a.png)

5. Select **Generate SAR File** and click **Next**.

    ![](./images/deploy-iwsproj3b.png)

6. Review and click **Next**.

    ![](./images/deploy-iwsproj3c.png)

7. Review and click **Finish**.

    ![](./images/deploy-iwsproj3d.png)

8. Let the code build successfully.

    ![](./images/compilecode12213.png)

9. Open Oracle Jdeveloper 12.2.1.4.

    If you used the marketplace environment, Oracle JDeveloper 12.2.1.4 is on the desktop, click the icon and click **Run** and **OK** to use the full dev suite.

    Otherwise, open Oracle JDeveloper 12.2.1.4 you installed locally as part of the SOA Quickstart 12.2.1.4.

10. Create a new SOA Application.

    ![](./images/j12214a.png)

11. Select **SOA Application** in the template list.

    ![](./images/j12214b.png)

12. Set **IWSApplication** for **Application Name**, and click **Next**.

    ![](./images/j12214c.png)

13. Keep the default project name, and click **Next**.

    ![](./images/j12214d.png)

14. Select **Empty Composite**, and click **Finish**.

    ![](./images/j12214e.png)

15. Select **File -> Import**.

    ![](./images/j12214f.png)

16. Select **SOA Archive Into SOA Project** and click **OK**.

    ![](./images/j12214g.png)

17. Name the project **IWSProj3** (the same as in the source environment) and click **Next**.

    ![](./images/j12214h.png)

18. Click **Browse**.

    ![](./images/j12214i.png)

19. Go to the location where you have deployed your Oracle Jdeveloper 12.2.1.3 project.

    - On the marketplace environment, it will be under `/u02/training/SOAJdevProjects/IWSApplication/IWSProj3/deploy`.

    - On your local machine it usually would be under `JDEVELOPER_FOLDER/mywork/IWSApplication/IWSProj3/deploy`.


20. Select the **sca_IWSProj3.jar** file and click **Open**.

    ![](./images/j12214j.png)

21. Review and click **Finish**.

    ![](./images/j12214k.png)

22. Let the 12.2.1.3 code migrate to version 12.2.1.4.

We can now deploy the upgraded project as a SAR file.

23. Right click the **IWSProj3** project.

    ![](./images/iwsproj3.png)

24. Select **Deploy -> Deploy IWSProj3...**.

    ![](./images/j12214l.png)

25. Select **Generate SAR file** and click **Finish**.

    ![](./images/j12214m.png)

26. Wait until the code compiles successfully.

    ![](./images/compilecode12214.png)

## Task 3: Prepare Your Target Environment

Prepare your target environment by importing or recreating all the configurations of your source. This will ensure successful deployment of the Oracle SOA Suite application on the target instance.

1. Connect to your SOA on OCI compute instance via the bastion host:

    In the terminal window where you opened the tunnel earlier (in the on-premises environment) use:

    ```
    <copy>
    ssh -o ProxyCommand="ssh -W %h:%p opc${BASTION_IP}" opc@${REMOTEHOST}
    </copy>
    ```

2. Once on the target server, create the folder structure needed by the application:

    ```
    <copy>
    mkdir -p /tmp/soa/out
    mkdir -p /tmp/soa/out1
    chmod -R 777 /tmp/soa/
    </copy>
    ```

## Task 4: Re-deploy the Upgraded Application on the Target SOA Domain

The tunnel opened earlier creates the connection to the target SOA server, the SOA admin server is accessible on port 7002 on localhost. 

1. Open the `SOA EM` console in the Firefox browser in the on-premises environment at [https://localhost:7002/em](https://localhost:7002/em) and provide the credentials.

2. You might see a browser warning because the SSL security is using a self-signed certificate. Go through the steps to confirm the exception:

    ![](./images/firefox-ssl1.png)

    ![](./images/firefox-ssl2.png)

    ![](./images/soamp-deployment-1.png)

3. Log in with the credentials from provisioning:

    - Username: `weblogic`
    - Password: `welcome1`

2. Click the menu icon.

    ![](./images/menu.png)

3. Now click on the top right button and go to **SOA_Domain -> SOA -> SOA-Infra**.

    ![](./images/nav-composite.png)

4. Then click the **Deployed Composites** tab.

    ![](./images/deployed-composites.png)

5. Click **Deploy**.

    ![](./images/deploy.png)

6. Select the **Archive is on the machine...** option.

    ![](./images/deploy2.png)

7. Click **Browse** and navigate to the folder location of the upgraded 12.2.14 application.

    - If you used the local VirtualBox VM, it would be in:
        `JDEVELOPER_FOLDER\mywork\IWSApplication\IWSProj3\deploy`.
        
    - If you used the marketplace environment, it is under `/u02/oracle/developer/mywork/IWSApplication/IWSProj3/deploy`.

    ![](./images/filepath.png)

8. Select the `sca_IWSProj3.jar` file then click on **Open**.

9. Click **Next**.

    ![](./images/deploy2.png)


10. Select **SOA Folder** as **default** and click **Next**.

    ![](./images/deploy4.png)

12. Review all the information and then click **Deploy**.

    ![](./images/deploy5.png)

8. You will see a **Deployment in progress** message. Wait until the message switches to **Deployment Succeeded** and click **Close**.

    ![](./images/deploy6.png)

9. Check the deployed project in **Dashboard**.

    ![](./images/soamp-deployment-9.png)


## Task 5: Check the Application on the Target SOA Domain

1. Get back in the terminal where you SSH'ed to the target instance.

2. Navigate to the folder `/tmp/soa/out`:

    ```
    <copy>
    cd /tmp/soa/out
    </copy>
    ```

3. We'll select an XML file from the target server to use as demo, and copy it into the `/tmp/soa/out/` folder:

    ```
    <copy>
    sudo cp /etc/firewalld/direct.xml /tmp/soa/out
    </copy>
    ```

4. Wait 5 to 10 seconds to check that the file disappeared from the folder as it has been polled by the service which you have deployed. 

    ```
    <copy>
    ls -l
    </copy>
    ```

5. Go to destination folder `/tmp/soa/out1` and observe that a new file with name `File_1.xml` was created by the soa service.

    ```
    <copy>
    cd /tmp/soa/out1
    ls -l
    </copy>
    ```

    ![](./images/success.png)

6. You can check the **Flow Instances** of the project has one new **FlowID**.

    ![](./images/soamp-testing-5.png)

5. Click on **FlowID** and see the **Audit Trail** and the relevant logs.

    ![](./images/soamp-testing-6.png)

You may proceed to the next lab.

## Acknowledgements

 - **Author** - Akshay Saxena, October 2020
 - **Last Updated By/Date** - Akshay Saxena, October 2020
