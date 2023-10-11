# Migrate the Tomcat Application

## Introduction

In this tutorial, we will migrate the application to the Tomcat cluster on Oracle Cloud Infrastructure (OCI).

Estimated Completion Time: 10 minutes.

### Objectives

In this tutorial, you will:
* Move the application over to the Tomcat cluster on OCI
* Configure the datasource used by the application to point to the Oracle Autonomous Database

### Prerequisites

For this tutorial, you need to have provisioned the Tomcat cluster on OCI.

## Task 1: Move the Application WAR File to the Tomcat Cluster on Oracle Cloud Infrastructure

1. Gather the Tomcat servers IP addresses from the output of the stack deployment.

2. Get into the Tomcat Docker container:

    If you were previously inside the database container, exit with:

    ```
    <copy>
    exit
    </copy>
    ```

    Then get in the Tomcat container with:

    ```
    <copy>
    docker exec -it tomcat-to-oci-tomcat-1 /bin/bash
    </copy>
    ```

2. Copy the application WAR file over to each Tomcat server:

    ```bash
    <copy>
    # Set the PUBLIC IP of the bastion
    export BASTION_IP=<Bastion_public_IP>
    </copy>
    ```

    ```
    <copy>
    export TOMCAT_IP=<Tomcat Private IP>
    </copy>
    ```

    Then run:

    ```bash
    <copy>
    cd /usr/local/tomcat/webapps/
    scp -o ProxyCommand="ssh -W %h:%p opc@${BASTION_IP}" SimpleDB.war opc@${TOMCAT_IP}:~/
    </copy>
    ```

3. SSH to the Tomcat server:

    ```bash
    <copy>
    ssh -o ProxyCommand="ssh -W %h:%p opc@${BASTION_IP}" opc@${TOMCAT_IP}
    </copy>
    ```

4. Copy the file to the deployment folder:

    The folder will depend on the version of Tomcat deployed.


    ```bash
    <copy>
    sudo cp SimpleDB.war /u01/apache-tomcat-9.0.45/webapps
    sudo chown tomcat:tomcat /u01/apache-tomcat-9.0.45/webapps/SimpleDB.war
    </copy>
    ```

5. Check the deployment happened as expected:

    ```bash
    <copy>
    cd /u01/apache-tomcat-9.0.45/webapps
    ls -lh
    </copy>
    ```

    If the war file was deployed, you should find a folder called `SimpleDB` in this folder.

    It may take several seconds to deploy, so if you don't see the folder at first, try the `ls -lh` command again.

## Task 2: Configure the Data Source

1. Open the `context.xml` file in the tomcat home folder for editing:

    ```bash
    <copy>
    sudo nano /u01/apache-tomcat-9.0.45/conf/context.xml
    </copy>
    ```

2. Add the following section within the existing `<Context>` section:

    ```xml
    <copy>
     <Resource name="jdbc/JDBCConnectionDS"
          global="jdbc/JDBCConnectionDS"
          auth="Container"
          type="javax.sql.DataSource"
          username="riders"
          password="Nge29v2rv#1YtSIS#"
          driverClassName="oracle.jdbc.OracleDriver"
          description="RIDERS's database"
          url="jdbc:oracle:thin:@tomcatatp_high?TNS_ADMIN=/usr/lib/oracle/19.10/client64/lib/network/admin/"
          maxActive="15"
          maxIdle="3"/>
    </copy>
    ```

    Make sure to replace the `tomcatatp` name with your information if you didn't use the name `tomcatatp`.

3. Type `CTRL+x`, then `y` to save the file.

## Task 3: Install the Oracle JDBC driver

1. As the tomcat user:

    ```
    <copy>
    sudo su - tomcat
    </copy>
    ```

2. Download and extract the driver:

    ```
    <copy>
    wget -c https://download.oracle.com/otn-pub/otn_software/jdbc/1918/ojdbc8-full.tar.gz -O - | tar -x -C /u01/apache-tomcat-9.0.45/webapps/SimpleDB/WEB-INF/lib/
    </copy>
    ```

3. Restart Tomcat:

    ```bash
    <copy>
    sudo systemctl restart tomcat
    </copy>
    ```

5. Test the servlet is working using curl:

    ```
    <copy>
    curl http://localhost:8080/SimpleDB/dbservlet
    </copy>
    ```

    You should see the JSON payload returned by the servlet

6. Exit the Tomcat VM


## Task 3: Repeat for Each Tomcat Server

1. Repeat the steps in the "Move the Application WAR File to the Tomcat Cluster on Oracle Cloud Infrastructure" section and "Configure the Datasource" section for each server on the Tomcat cluster if you had more than one.

## Task 4: Check the Application Served Via the Load Balancer

1. Get the load balancer public IP from the Stack deployment output.

2. In your browser, go to http://*LOAD_BALANCER_IP*/SimpleDB/.

3. Check that you see the application being served.

    !["application output"](./images/lb-simpledb-app.png "application")


## Acknowledgements
 - **Author** - Subash Singh, Emmanuel Leroy, October 2020
 - **Last Updated By/Date** - Emmanuel Leroy, February 2023
