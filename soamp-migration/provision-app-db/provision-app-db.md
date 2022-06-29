# Provision the Application Database on OCI with DBaaS

## Introduction

This lab with guide you through provisioning a Application Database

Estimated Lab Time: 30 to 35 minutes including 25 to 30 minutes provisioning time.

### Objectives

In this lab you will:

- Provision the application database as a Database Virtual Machine.
- Create a security list with proper ports open.


## Task 1: Provision the Database System

1. Go to **Database -> Bare Metal, VM and Exadata**.

  ![](./images/provision-db-10.png)

2. Click **Create DB System**.

  ![](./images/provision-db-11.png)

3. Make sure you are in the **SOAMPCompartment** and select a name for your database system.

  ![](/images/provision-db-12.png)

4. Select an availability domain or keep the default. Use **Virtual Machine** and select a **Shape** that is available.

  ![](./images/provision-db-13-ad-shape.png)

5. Keep the defaults for **Total node count** and **Database Edition**.

  ![](./images/provision-db-14.png)

6. Select **Logical Volume Manager**.

  ![](./images/db-lvm.png)

7. Keep the default for **Storage**.

  ![](./images/provision-db-16-storage.png)

8. Add your **SSH public key**.

  ![](./images/provision-db-17-ssh.png)

9. Keep the default of **License Included**.

  ![](./images/provision-db-18-license.png)

10. Select the `SOAMP1VCN` **Virtual cloud network**, the `Private Subnet-SOAMP1VCN(regional)` **Client subnet** and set `soamp2db` as the **Hostname prefix**.

  ![](./images/db-network.png)

11. Click **Next**.

12. Use `SOAMP2DB` for the database name.

  ![](./images/db-name.png)

13. Select `19c` as the **Database version**.

  ![](./images/db-version.png)

14. Use `PDB1` as the **PDB** name.

  ![](./images/db-pdbname.png)


15. Enter and confirm the **SYS Database password**.

    You can create your own password or use the following (used in further steps):

    ```
    <copy>
    WELcome##123
    </copy>
    ```

  ![](./images/db-password.png)

16. Keep the default **Transaction Processing** option for **Workload type** and for **Backup**.

17. Optionally you can select **Enable automatic backups** for the period of `60 days` and scheduling `Anytime`.

  ![](./images/provision-db-21.png)

18. Click **Create DB System**.

  This will usually take up to 40 minutes to provision.

  ![](./images/provision-db-22.png)

## Task 2: Check the Status of the Database Provisioning

Before you can proceed to the next lab, you need to check that the database has been fully provisioned.

1. Go to **Oracle Databases -> BM, VM, Exadata**.

2. Make sure you are in the correct Compartment.

3. Check the status of the database is `Available` or wait until it is before proceeding.

  ![](./images/db-available.png)

You may proceed to the next lab.

## Acknowledgements

 - **Author** - Akshay Saxena, September 2020
 - **Last Updated By/Date** - Akshay Saxena, September 2020
