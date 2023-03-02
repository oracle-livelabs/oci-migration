# Upgrading an Environment

## Introduction
This lab walks you through the steps to upgrade an environment.

Estimated Lab Time: 10 minutes + 1-2 hours for downloading + 1 hour for upgrading

### Objectives
In this lab you will:
* Upgrade an existing environment

### Prerequisites
- Access to the Cloud Manager console.
- Environment up and running

## Task 1: Subscribe to Tools Channels

1.  Navigate to **Cloud Manager Dashboard** > **Repository**. 
    ![Navigate to Cloud Manager Dashboard and then Repository](./images/repo.png "")

2.  On **Downloaded Subscriptions**, switch to **Unsubscribed**. Scroll down to find **Tools\_859\_Linux**, click the **V** arrow and then **Subscribe**
    ![On Downloaded Subscriptions, switch to Unsubscribed. Scroll down to find Tools_859_Linux, click the arrow and then Subscribe](./images/lin59subscribe.png "")


3. Enter **01** for the minimum patch number, and click **OK**
    ![Enter 01 for the minimum patch number, and click OK](./images/lin59number.png "")

4. Repeat the same steps for **Tools\_859\_Windows**
    ![Repeat the same steps for Tools_859_Windows](./images/win59subscribe.png "")
    ![Repeat the same steps for Tools_859_Windows](./images/win59number.png "")

## Task 2: Monitor Subscription Progress

1. To monitor progress, you can go to **Download History**, select **Tools\_859\_Linux** and **Tools\_859\_Windows** to see which packages are in progress and which have been completed.

    ![To monitor progress, you can go to Download History, select Tools_859_Linux and Tools_859_Windows to see which packages are in progress and which have been completed.](./images/patchlist59.png "")
2. You can then look at each patch progress status under **Logs**. Select the **Channel Name**, **Log File**, add **Number of Lines to Display**, and click **Fetch Logs**.
    ![You can then look at each patch progress status under Logs. Select the Channel Name, Log File, add Number of Lines to Display, and click Fetch Logs.](./images/logs59.png "")

3. Once you see this, you may apply the patches to your environment:
    ![Once you see this, you may apply the patches to your environment](./images/859done.png "")

## Task 3: Apply Upgrade to Environment

1. Navigate to **Cloud Manger Dashboard** > **Environments**
    ![Navigate to Cloud Manger Dashboard and then Environments](./images/env.png "")

2. Find the environment you would like to patch, click **V** and **Details**
    ![Find the environment you would like to patch, click arrow and Details](./images/details.png "")
3. Navigate to **Upgrade PeopleTools**. In the drop down, select the **8.59.01**, and then click **Update**
    ![Navigate to Upgrade PeopleTools. In the drop down, select the 8.59.01, and then click Update](./images/upgrade59.png "")
    - Click **Yes**
    ![click yes to start the upgrade](./images/yes59.png "")
4. You can track the status below 
    ![You can track the status below](./images/status59.png "")

    - When it's done, it will say **Completed**


You may now **proceed to the next lab.**

## Acknowledgements
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect 
* **Last Updated By/Date** - Deepak Kumar M, Principal Cloud Architect, March 2023