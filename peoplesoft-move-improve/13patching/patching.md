# Patching an Environment

## Introduction
This lab walks you through the steps to patch an environment.

Estimated Lab Time: 10 minutes + 1-2 hours for downloading + 1 hour for patching

### Objectives
In this lab you will:
* Patch an existing environment

### Prerequisites
- Access to the Cloud Manager console.
- Environment up and running

## Task 1: Subscribe to Tools Channels

1.  Navigate to **Cloud Manager Dashboard** > **Repository**. 
    ![Navigate to Cloud Manager Dashboard and then Repository.](./images/repo.png "")

2.  On **Downloaded Subscriptions**, switch to **Unsubscribed**. Scroll down to find **Tools\_860\_Linux**, click the **V** arrow and then **Subscribe**
    ![On Downloaded Subscriptions, switch to Unsubscribed. Scroll down to find Tools_860_Linux, click the arrow and then Subscribe](./images/linsubscribe.png "")


3. Enter **11** for the minimum patch number, and click **OK**
    ![Enter 11 for the minimum patch number, and click OK](./images/linpatchnum.png "")

4. Repeat the same steps for **Tools\_860\_Windows**
    ![Repeat the same steps for Tools_860_Windows](./images/winsubscribe.png "")
    ![Repeat the same steps for Tools_860_Windows](./images/winpatchnum.png "")

## Task 2: Monitor Subscription Progress

1. To monitor progress, you can go to **Download History**, select **Tools\_860\_Linux** and **Tools\_860\_Windows** to see which packages are in progress and which have been completed.

    ![To monitor progress, you can go to Download History, select Tools_860_Linux and Tools_860_Windows to see which packages are in progress and which have been completed](./images/patchlist.png "")
2. You can also look at the **Logs**. Select the **Channel Name**, **Log File**, add **Number of Lines to Display**, and click **Fetch Logs**.
    ![You can also look at the Logs. Select the Channel Name, Log File, add Number of Lines to Display, and click Fetch Logs](./images/logs.png "")

3. Once you see this, you may apply the patches to your environment:
    ![Once you see this, you may apply the patches to your environment](./images/860Linuxdone.png "")
    ![Once you see this, you may apply the patches to your environment](./images/860Windowsdone.png "")
## Task 3: Apply Patch to Environment

1. Navigate to **Cloud Manger Dashboard** > **Environments**
    ![Navigate to Cloud Manger Dashboard and then Environments](./images/env.png "")
2. Find the environment you would like to patch, click **V** and **Details**
    ![Find the environment you would like to patch, click the arrow and then details](./images/details.png "")
<<<<<<< HEAD:peoplesoft-move-improve/peoplesoft-move-improve/13patching/patching.md
3. Navigate to **Apply PeopleTools Patch**. In the drop down, select the **8.60.08**, and then click **Update**
    ![Find the environment you would like to patch, click arrow and details](./images/patch60.png.png "")
=======
3. Navigate to **Apply PeopleTools Patch**. In the drop down, select the **8.58.11**, and then click **Update**
    ![Find the environment you would like to patch, click arrow and details](./images/patch58.png "")
>>>>>>> upstream/main:peoplesoft-move-improve/14patching/patching.md
    - Click **Yes**
    ![Navigate to Apply PeopleTools Patch. In the drop down, select the 8.58.11, and then click Update](./images/yes60.png "")
4. You can track the status below 
    ![You can track the status below](./images/status60.png "")

    ![You can track the status below](./images/status60additional.png "")
    - When it's done, it will say **Completed**
    ![When it's done, it will say Completed](./images/complete60.png "")
   
You may now **proceed to the next lab.**



## Acknowledgements
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect; Megha Gajbhiye, Principal Cloud Architect
<<<<<<< HEAD:peoplesoft-move-improve/peoplesoft-move-improve/13patching/patching.md
* **Last Updated By/Date** - Ziyad Choudhury, Principal Cloud Architect, August 2023
=======
* **Last Updated By/Date** - Deepak Kumar M, Principal Cloud Architect, March 2023
>>>>>>> upstream/main:peoplesoft-move-improve/14patching/patching.md
