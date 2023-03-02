# Tear Down

## Introduction

In this tutorial, we will tear down the infrastructure deployed on Oracle Cloud Infrastructure (OCI) as well as the local Docker environment.

Estimated Completion Time: 5 minutes.

### Objectives

In this tutorial, you will tear down and clean up resources.


## Task 1: Tear Down Resources

1. Go back to the **Resource Manager -> Stacks**:

2. Select the stack deployed earlier and click **Destroy**.

3. Sometimes destroy fails because the Load Balancer takes time to bring down. 
    If it fails, go back to the stack details, and click **Destroy** again.

4. When the job has ran successfully, you can delete the stack with **Other Actions** -> **Delete Stack**.

## Task 2: Tear Down the Local Docker Environment

1. Exit any container you may still be logged into:

    ```bash
    <copy>
    exit
    </copy>
    ```

2. Tear down the docker-compose environment:
    ```
    <copy>
    docker-compose down
    </copy>
    ```

3. Optionally you may also remove all the unused images and objects:

    > **Note:** This action removes any image not in use, so if you have other Docker images you want to keep, you may prefer to selectively delete the images of this workshop only.

    ```
    <copy>
    # Delete all images not in use
    docker rmi $(docker images -a -q)
    # clean up and reduce memory usage
    docker system prune
    </copy>
    ```

## Acknowledgements
 - **Author** - Subash Singh, Emmanuel Leroy, October 2020
 - **Last Updated By/Date** - Emmanuel Leroy, February 2023
