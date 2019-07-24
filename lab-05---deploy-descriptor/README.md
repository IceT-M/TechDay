# Lab 05 - Deploy Descriptor

Control-M Automation API enables you to use Deploy Descriptor to change job definition properties in JSON format before building, deploying, or running the JSON file.

Using the Deploy Descriptor enables you to streamline your code across different environments (for example, between Development, Test, or Production). Since each Control-M environment has different properties, the Deploy Descriptor enables you to programmatically manipulate these properties.

## Step 1 - Define a transformation

In this exercise, we will use example file [example-flow.json](example-flow.json). However, this time we will not change it. This is our immutable artifact. We are going to define a Deploy Descriptor to tranform this generic example so it will run under our user.

Open [deploy-descriptor.json](deploy-descriptor.json). First step is to update to set the run as user with your own given user id.

```
{
	"DeployDescriptor": [
		{
			"Property": "RunAs",
			"Assign": "<REPLACE WITH YOUR USER NAME>"
		}
	]
}
```

If we apply this deploy descriptor, the RusAs value will be set to your user name. 

- Like a job flow, we can use the build service to validate our deploy descriptor file
- Open the terminal and type ```ctm deploy``` 
Look for the transform option and examine the usage. 

- Now let's apply the transformation by typing ```ctm deploy transform example-flow.json deploy-descriptor.json```
- The output shows the example-flow.json with the assigned value for RunAs.

Now our flow still contains <USER> at several places. Let's add the following to the deploy descriptor file. Replace <REPLACE WITH YOUR USER NAME> with your given user name. Note we are adding the suffix ```_PROD``` to mimic a promotion to a production environment.


```
		{
			"Comment": "Changes the name of all folders to match the production standard",
			"Property": "@",
			"ApplyOn": {
				"Type": "Folder"
			},
			"Replace": [
				{
					"<USER>(.*)": "<REPLACE WITH YOUR USER NAME>$1_PROD"
				}
			]
		}
``` 

Now we still have the <USER> string at in the [example-flow.json](example-flow.json) file. Please visit the deoploy descriptor documentation page [here](https://docs.bmc.com/docs/automation-api/9182/deploy-descriptor-808125682.html) and try to add a transformation to replace <USER> with your user name for Apllication and SubApplication.

Transform the [example-flow.json](example-flow.json) to test the result.

## Step 2 - Deploy a flow using Deploy Descriptor

Now your deploy descriptor file transforms the [example-flow.json](example-flow.json) file in a suitable format, we can deploy the flow using the deploy service.

Open a terminal and type the following command to deploy your flow using the deploy descriptor file. 

```
ctm deploy example-flow.json deploy-descriptor
``` 

We can also directly deploy and run using the following command:

```
ctm run example-flow.json deploy-descriptor
``` 

Did your flow ran successful?

Try to include an extra option in your Eclipse to run and deploy using the deploy descriptor file 


## Step 3 - Export jobs from an existing environment

At some point, you might want to extract files from your current Control-M environment and move them to your repository. You can export jobs in json by running the following command:

```
ctm deploy jobs::get -s "ctm=*&folder=<USER>*" > ProdDefinitions.json
```

## Step 4 - Explorer in mode detail

Visit the Deploy Descriptor documentation page to explorer this in more detail. 

https://docs.bmc.com/docs/automation-api/9182/deploy-descriptor-808125682.html 