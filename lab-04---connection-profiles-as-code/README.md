# Lab 04 - Connection Profiles as-code

Connection profiles are used to define access methods and security credentials for a specific application. They can be referenced by multiple jobs. To do this, you must deploy the connection profile definition before running the relevant jobs.

In chapter, we will only cover a basic connection profile for a FTP job. A more detailed documentation on connection profiles can be found [here](https://docs.bmc.com/docs/display/ctmapi9182/Code+Reference#CodeReference-ConnectionProfile)

## Step 1 - Deploy a connection profile

Open [ftp-connection-profile.json](ftp-connection-profile.json). Replace every occurrence of <USER> with your given user name. Explore the different options.

Once your adjusted file is ready, you can use ```ctm deploy ftp-connection-profile.json``` to deploy them. You can also use the imported run configuration.

## Step 2 - Define an FTP job

Open [file-transfer-job-flow.json](file-transfer-job-flow.json). Replace every occurrence of <USER> with your given user name. Explore the example job and run it.

## Step 3 - Using the vault

The config service allows you to add, delete, or update named secrets in the Control-M vault. The Control-M vault is a secured collection of name and value pairs of secrets.

The full documentation can be found [here](https://docs.bmc.com/docs/automation-api/9182/services-808125681.html#Services-ConfigSecrets)

The command for adding secrets is 
```
ctm config secret::add <name> <value>
```

Configure the following secrets. Update the USER prefix with your user names.


| Name                  | Value          |
|-----------------------|----------------|
| USER_FTP_User       | Anonymous      |
| USER_FTP_Password   | Anonymous      |
| USER_LOCAL_User     | YOUR USER NAME |
| USER_LOCAL_Password | YOUR USER NAME |


Now open [ftp-connection-profile.json](ftp-connection-profile.json) again and replace the user names and passwords with the secret by inserting 
```
{"Secret": "SECRET_NAME"}
```

More information on how to use secrets in code can be found [here](https://docs.bmc.com/docs/automation-api/9182/code-reference-808125680.html#CodeReference-secrets_in_code)
