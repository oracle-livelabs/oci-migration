# Tear Down the Workshop

## Introduction

In this lab, we will tear down the infrastructure deployed on OCI as well as the local Docker environment.

Estimated Lab Time: 5 minutes

### Objectives

In this lab, you will tear down and clean up resources.


## Task 1: Tear Down Terraform Resources

1. Simply run the terraform destroy command:

    ```
    <copy>
    terraform destroy
    </copy>
    ```

    You will be prompted to type `yes` to confirm.

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

3. Optionally you may also remove all the unused images and objects.

    Attention: this removes anything not in use, so if you have other Docker images you want to keep, you may prefer to selectively delete the images of this workshop only.

    ```
    <copy>
    # Delete all images not in use
    docker rmi $(docker images -a -q)
    # clean up and reduce memory usage
    docker system prune
    </copy>
    ```

## Task 3: Delete the Database Dump and Storage Bucket

1. In the Oracle Cloud Console go to Object Storage

2. Find the bucket you created earlier

3. Select all files and click **Delete**

4. When done, delete the bucket.


## Acknowledgements
 - **Author** - Subash Singh, Emmanuel Leroy
 - **Last Updated By/Date** - Emmanuel Leroy, May 2021
