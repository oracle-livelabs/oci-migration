# Set Up the demo SOA 'on-premises' environment

## Introduction

For this migration workshop, we need an environment to migrate *from*.

We're offering 2 ways to provision this environment:

- Using a demo Marketplace image for this workshop
- Installing required Apps locally on your development machine

The first path provide a pre-packaged 'on-premises' simulated environment, which includes SOA Suite 12.2.1.3 and quick start SOA Suite 12.2.1.4 (Jdeveloper 12.2.1.4)

The Marketplace image deployment is simpler and faster, while the provisioning local environment provides a way to more realistically simulate an 'on-premises' environment as it runs on your local machine. 

### Objectives

In this workshop, you will:

- Choose a path to create a demo environment to use as the 'on-premises' environment.

### Prerequisites

*Depending on the path you choose, there are different requirements:*

- For the Marketplace environment, you will need:
    - One bare metal compute instance with at least 4 OCPU (8 preferred) available in your tenancy. 
    
    >Note: The workshop will run on a VM instance but will be very very slow, so it is not recommended.  

- For the local machine environment, you will need:
    - A machine with at least 12GB of memory
    - At least 4 CPUs, 
    - At least 25GB of disk space to download and install the VM image
    - VirtualBox with extension

## Task 1: Choose a path

Choose the option that best suits your needs:

A. [Set Up the on-premises Environment using Marketplace image (15min)](?lab=lab-1-option-setup-on-premises-environment)

B. [Set Up the on-premises Environment Locally with VirtualBox (60min+)](?lab=lab-1-option-b-setup-local-(on-premises))

You may proceed to the next lab.

### Disclaimer

> Note that this is a demo environment pre-packaged with a SOA WebLogic Domain, demo applications, and a database inside a single VM. This is for demo/training purpose only and is not production-ready.

## Acknowledgements

 - **Author** - Akshay Saxena, September 2020
 - **Last Updated By/Date** - Akshay Saxena, September 2020
