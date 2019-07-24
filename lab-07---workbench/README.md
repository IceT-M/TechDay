# Lab 07 - Workbench

Control-M Workbench is a self-service, standalone development environment that is launched in minutes, giving you the autonomy to code, debug, and test jobs the same way that any other coding activity is performed.

Workbench is availible for both Oracle Virtual Box and VMWare. If you have one of them, please continue to step 2. Else you can install Oracle Virtual Box in step 1. 

## Step 1 - Install Oracle Virtual Box

Download your preferred platform package from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) and follow the provided instructions to install Oracle VirtualBox on your computer.


## Step 2 - Download and Install Control-M Workbench

- Download the Control-M Workbench appliance to your computer. You can download [Workbench for Oracle Virtual Box](https://s3-us-west-2.amazonaws.com/controlm-appdev/release/v9.18.3/workbench_oracle_virtual_box_ova-9.0.18.300-20190218.133426-1.ova) or [Download Workbench for VMWare](https://s3-us-west-2.amazonaws.com/controlm-appdev/release/v9.18.3/workbench_vmware_ova-9.0.18.300-20190218.132300-1.ova) 
- For the Oracle VM VirtualBox Manager, go to File > Import Appliance and select the workbench.ova file that you downloaded to your computer and wait for the import process to complete.
- From the left pane, select workbench and click Start to run the appliance. 
- After workbench is up and running, click [https://localhost:8443/automation-api/startHere.html](https://localhost:8443/automation-api/startHere.html) to get started.
 
## Step 2 - Configure your Automation API to point to workbench
 
Add a workbench environment with the following end-point: https://localhost:8443/automation-api

## Step 3 - Run a job

Switch the Automation API CLI to the Workbench environment:

```
ctm environment set workbench
```

Now execute [workbench-flow.json](workbench-flow.json)

Did it run?