# Prepare Your Tenancy for Oracle E-Business Suite

## Introduction
In this exercise, you will prepare your Oracle E-Business Suite (EBS) environment by setting up Oracle E-Business Suite Cloud Manager authentication.

Estimated Lab Time: 30 minutes
<!--
Watch this short video to preview how to prepare your tenancy for Oracle E-Business Suite.

[](youtube:kWBDCZ-r0zQ)

-->
### **Objectives**
* Register Oracle E-Business Suite Cloud Manager as a confidential application.

### **Prerequisites**
* This step is to be performed by the tenancy administrator.

## Task 1: Sign in to the Oracle Cloud Infrastructure Console

Use the tenancy administrator credentials to sign in to Oracle Cloud Infrastructure console.

1. Reference your ``key-data.txt`` file and locate the tenancy administrator credentials.

2. Sign in to the Oracle Cloud Infrastructure console using the following:

    * **User name**: ``Tenancy Admin User``
    * **Password**: ``Tenancy Admin Password``

## Task 2: Register Cloud Manager as a Confidential Application in Tenancies Using IAM with Identity Domains

1. Open the navigation menu and click **Identity & Security**. Under **Identity**, click **Domains**.

    ![This screenshot shows the console navigation menu and depicts the navigation to the Domains page.](./images/domains-navigation.png " ")

2. Select the root compartment in the **Compartment** drop-down list.

3. Within the list of domains, click the link for the "Default" domain.

    ![This screenshot shows the Domains page.](./images/domains-listing.png " ")

4. Click **Applications** in the menu on the left.

    ![This screenshot shows the Applications page and highlights the Add application button within the user interface.](./images/applications-menu.png " ")

5. Click **Add application**.

6. Select **Confidential Application**. 

    ![This screenshot shows the Add application window and highlights the Confidential Application option.](./images/confidential-application.png " ")

7. Click **Launch Workflow**. This takes you to the Add Confidential Application page.

8. Under Add application details, enter the following:
    - **Name**: ``Oracle E-Business Suite Cloud Manager``
    - **Description**: Enter a description.

9. Click **Next**.

10. Under Configure OAuth:

    a. Click **Configure this application as a client now**.
    
    b. Under Allowed Grant Types, select the following options:
    - Client Credentials
    - Refresh Token
    - Authorization Code

    c. Now, we are going to set our Cloud Manager URL. For this lab, use the following example URL: ``https://myebscm.ebshol.org:443``

    Save your Cloud Manager URL in your ``key-data.txt`` file as ``Cloud_Manager_URL``.

    Using the Cloud Manager URL you have just saved, append that URL with the following values as shown to enter your Redirect URL.

    d. **Redirect URL**: ``<Cloud Manager URL>/cm/auth/callback``
    
    For example: ``https://myebscm.ebshol.org:443/cm/auth/callback``

    e. **Post-Logout Redirect URL**: ``<Cloud Manager Balancer URL>/cm/ui/index.html?root=login``
    
    For example: ``https://myebscm.ebshol.org:443/cm/ui/index.html?root=login``

    f. **Logout URL**: Leave this field empty.

    ![This screenshot shows the Configure OAuth section when adding an application. It shows the Configure this application as a client now radio button which must be selected. It highlights the Client credentials, Refresh token, and Authorization code options which must be selected. It also highlights the Redirect URL and Post-logout redirect URL which must be entered. Note that it is required that the Logout URL field is left empty.](./images/client-configuration-1.png " ")

    g. Under Client Type, ensure that the **Confidential** radio button is selected.

    h. Select the **Introspect** option for Allowed Operations.

    ![This screenshot shows the Configure OAuth section when adding an application. It highlights the Confidential radio button that must be selected as well as the Introspect check box which must be checked.](./images/client-configuration-2.png " ")

    i. Under Token Issuance Policy, select the **Add app roles** check box.

     1. Click **Add roles**.
        ![This screenshot shows the Configure OAuth section when adding an application and highlights the Add app roles check box which must be selected and the Add roles button in the user interface.](./images/client-configuration-3.png " ")
     2. Select **Authenticator Client** and **Me**. Then click **Add**.
        ![This screenshot shows the Add app roles section and highlights the Me and Authenticator Client check boxes to be selected. It also points out the Add button on the user interface.](./images/add-app-roles.png " ")
    
    3. Click **Next**.
    
11. Under Configure policy, click **Finish**.

    ![This screenshot shows the Finish button within the user interface in the Configure policy section.](./images/configure-policy.png " ")

12. Make a note of the following values under General Information in your ``key-data.txt`` (under ``Client_ID`` and ``Client_Secret``, respectively):

    • Client ID

    • Client secret (In order to view, click Show secret.)

    ![This screenshot shows the confidential application information page.](./images/client-id-and-secret.png " ")

13. Click **Activate** and confirm to activate the confidential application.

    ![This screenshot highlights the Activate button within the user interface and displays the Activate application pop-up window to activate your application.](./images/activate-application.png " ")

14. Record your Oracle Identity Cloud Service Client Tenant value as ``Client_Tenant`` in the ``key-data.txt``. This is found in the Overview of the default domain under the Domain Information section. It is seen as part of the URL found in Domain URL, after the "//" and before ".identity.oraclecloud.com". It begins with the characters "idcs-", followed by a string of numbers and letters in the format ``idcs-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx``

    For Example: ``idcs-6572bfeb183b4becad9e649bfa14a488``.
    
    ![This screenshot shows the Domain information tab and highlights the Oracle Identity Cloud Service Client Tenant information you must record in your key-data.txt file.](./images/client-tenant.png " ")

You may now proceed to the next lab.

## Acknowledgements

* **Authors:** 
  * Santiago Bastidas, Product Management Director
  * Vijay Kumar Vudari Satyanarayana, Principal Cloud Architect
  * Danish Ansari, Principal Cloud Architect
* **Contributors:** 
  - William Masdon, Cloud Engineering
  - Mitsu Mehta, Cloud Engineering
  - Chris Wegenek, Cloud Engineering
* **Last Updated By/Date:** Tiffany Romero, EBS Documentation, December 2023


