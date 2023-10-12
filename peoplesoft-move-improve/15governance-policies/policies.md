# Setting up Governance Policies

## Introduction
Cloud Manger provides the ability to define and manage policies. Using the governance framework, administrators can manage life cycle activities of environments. Policies can be scheduled or executed real time by connecting through events.

Estimated Lab Time: 30 minutes + 15 minutes for environment starting/stopping

### Objectives
In this lab you will:
* Create a policy group
* Create policies
* Execute policies

### Prerequisites
- Access to the Cloud Manager console
- A PeopleSoft Environment up and running

## Task 1: Creating a Policy Group

Before creating any policies we will create a policy group. Policy groups are optional and are used to group policies together for display.

1.  Navigate to **Dashboard** > **Governance**. Click **Policy Groups** on the side menu and click the plus button to add a new policy group.
    ![Navigate to Dashboard > Governance. Click Policy Groups on the side menu and click the plus button to add a new policy group.](./images/policygroup.png "")

2.  Under name, enter the name of the PeopleSoft environment that this policy group is for. For demo purposes we will be using the **HCMFT** environment. Enter a description, then click save.
    ![For demo purposes we will be using the HCMFT environment. Enter a description, then click save.](./images/policysave.png "")

## Task 2: Creating Policies

1.  Navigate to **Dashboard** > **Governance**. Click **PolicyEditor** on the side menu then click **Add Policy**    
    ![Navigate to Dashboard, then Governance and  Click PolicyEditor on the side menu then click Add Policy](./images/policyadd.png "")

2.  First we will create a start policy for our environment. Type the information as shown below. If you are using an environment other than **HCMFT**, be sure to update **PolicyGroup** and **PolicyConditions** as appropriate.
    ![If you are using an environment other than HCMFT, be sure to update PolicyGroup and PolicyConditions as appropriate](./images/start.png "")

    Click **Schedule** and enter a time/date for when you want this policy to take effect. This can be changed later on, for now just put some time in the future. Click **Save** and then click **Save** on the main policy page.
    ![Click Schedule and enter a time/date for when you want this policy to take effect. This can be changed later on, for now just put some time in the future. Click Save and then click Save on the main policy page.](./images/schedule.png "")

    Next we will create a stop policy. Click **Add Policy** again and type the information as shown below:
    ![Next we will create a stop policy. Click Add Policy again and type the information as shown below](./images/stop.png "")

    Set a schedule then click **Save** and then **Save** again.

    Next we will create a scale-up policy. Click **Add Policy** again and type the information as shown below:
    ![Next we will create a scale-up policy. Click Add Policy again and type the information as shown below](./images/scaleup.png "")

    ![Policy Action Parameters. Policy actions ](./images/policyactionup.png "")

    Set a schedule then click **Save** and then **Save** again.

    Finally, we will create a scale-down policy. Click **Add Policy** again and type the information as shown below:
    ![Finally, we will create a scale-down policy. Click Add Policy again and type the information as shown below](./images/scaledown.png "")
    
    ![Policy Action Parameters. Policy actions ](./images/policyactiondown.png "")
    Set a schedule then click **Save** and then **Save** again.

    Expand **HCMFT** and now as you can see we have multiple policies mapped under a single policy group for easy reference.
    ![Expand HCMFT and now as you can see we have multiple policies mapped under a single policy group for easy reference.](./images/policyview.png "")

3.  You can also view all of these policies directly from your environment. Navigate to **Dashboard** > **Environments**. On **HCMFT** (or whichever environment you created the previous policies for) click the down arrow and then **Details**
    ![You can also view all of these policies directly from your environment.Click the down arrow and then Details](./images/workshopdetail.png "")

4.  On the side menu select **Policies**. Here you will be able to import all the policies we recently created for this environment.
    ![On the side menu select Policies. Here you will be able to see all the policies we recently created for this environment.](./images/addpolicy.png "")

## Task 3: Executing Policies

1.  Now we will execute our stop policy. If you want a policy to execute immediately you can set the start date for a time in the past. Navigate to **Dashboard** > **Governance**. Click **Policy Editor** on the side menu then click the arrow under **View/Edit** next to our **HCMFT Stop** policy.
    ![Click Policy Editor on the side menu then click the arrow under View/Edit next to our HCMFT Stop policy.](./images/stoppolicy.png "")

2.  Click **Schedule** then set a **Start Date** and **Start Time** that has occurred in the past. Click **Save** and then click **Save** on the main policy page.
    ![Click Schedule then set a Start Date and Start Time that has occurred in the past. Click Save and then click Save on the main policy page.](./images/pastdate.png "")

3.  Answer **Yes** when the popup asks you if you are sure you want to re-generate existing policy.
    ![Answer Yes when the popup asks you if you are sure you want to re-generate existing policy.](./images/pop.png "")

4.  Navigate to **Dashboard** > **Environments**. You will see that our environment is in the **Stopping** phase which means that our policy has been executed and has initiated the stop of the environment.    
    ![You will see that our environment is in the Stopping phase which means that our policy has been executed and has initiated the stop of the environment](./images/stopprocess.png "")

5.  To see the status of the policy which we just executed navigate to **Dashboard** > **Governance** and on the side menu click **PolicyMonitor**. Click the arrow under **Status** next to **HCMFT Stop**.
    ![To see the status of the policy which we just executed navigate to Dashboard > Governance and on the side menu click PolicyMonitor. Click the arrow under Status next to HCMFT Stop.](./images/monitorpolicy.png "")

    You will see that the status of the policy is **Running**.
    ![You will see that the status of the policy is Running.](./images/policystatus.png "")

    Once you see the status of your environment changed to **Stopped** the policy has successfully executed.
    ![Once you see the status of your environment changed to Stopped the policy has successfully executed](./images/stopped.png "")

6.  We can now execute our start policy to bring the environment back up. Navigate to **Dashboard** > **Governance**. Click **Policy Editor** on the side menu then click the arrow under **View/Edit** next to our **HCMFT Start** policy.
    ![We can now execute our start policy to bring the environment back up. Navigate to Dashboard > Governance. Click Policy Editor on the side menu then click the arrow under View/Edit next to our HCMFT Start policy.](./images/startback.png "")

7.  Click **Schedule** then set a **Start Date** and **Start Time** that has occurred in the past. Click **Save** and then click **Save** on the main policy page.
    ![Click Schedule then set a Start Date and Start Time that has occurred in the past. Click Save and then click Save on the main policy page.](./images/pastdate.png "")

8.  Answer **Yes** when the popup asks you if you are sure you want to re-generate existing policy.
    ![Answer Yes when the popup asks you if you are sure you want to re-generate existing policy](./images/pop2.png "")

9.  Navigate to **Dashboard** > **Environments**. You will see that our environment is in the **Starting** phase which means that our policy has been executed and has initiated the start of the environment.    
    ![Navigate to Dashboard > Environments. You will see that our environment is in the Starting phase which means that our policy has been executed and has initiated the start of the environment.](./images/startagain.png "")

You may now **proceed to the next lab.**

## Acknowledgements
* **Authors** - Deepak Kumar M, Principal Cloud Architect; Sara Lipowsky, Cloud Engineer
* **Contributors** - Edward Lawson, Master Principal Cloud Architect
* **Last Updated By/Date** - Ziyad Choudhury, Principal Cloud Architect, August 2023
