---
layout: default
---
### Access to Azure Registry "sapclmiftregistry" (without setting up a Cluster)

📝 NOTE: Use this documentation if you only need access to a registry from your PC, for example if you only need to copy or transfer artifacts to a registry, without installing a container-based system. This documentation does not describe how to set up a complete K8S cluster.
If you want to set up a complete K8S cluster including a jump host with access to a container registry, go to [How to set up a Cluster on Azure AKS](https://wiki.one.int.sap/wiki/display/SLCB/How+to+set+up+a+Cluster+on+Azure+AKS) .

```
az login
```

* Log on to the Azure AKS Console:  https://portal.azure.com/#home
* Install the Azure CLI: https://docs.microsoft.com/de-de/cli/azure/install-azure-cli
* Make sure that you have Docker running on your PC. If you have not Docker on your PC, install Docker Desktop.
* Open a command prompt and execute the following:

You should now see command line output like the following:

```
C:\WINDOWS\system32>az login
The default web browser has been opened at https://login.microsoftonline.com/common/oauth2/authorize. Please continue the login in the web browser.
If no web browser is available or if the web browser fails to open, use device code flow with az login --use-device-code.
You have logged in. Now let us find all the subscriptions to which you have access...
The following tenants require Multi-Factor Authentication (MFA).
Use 'az login --tenant TENANT_ID' to explicitly login to a tenant.
69b863e3-480a-4ee9-8bd0-20a8adb6909b 'SAP Shared Tenant'
[
{
"cloudName": "AzureCloud",
"homeTenantId": "42f7676c-f455-423c-82f6-dc2d99791af7",
"id": "3a9986fa-8e53-4d17-98fc-3ddf4042818b",
"isDefault": true,
"managedByTenants": [],
"name": "sap-clm-azr-inst-framework",
"state": "Enabled",
"tenantId": "42f7676c-f455-423c-82f6-dc2d99791af7",
"user": {
"name": "klaus.billig@sap.com",
"type": "user"
}
}
]
```

Now enter the following command:

```
az acr login --name sapclmiftregistry
```

In case of success, you should now see command line output like the following:

```
C:\WINDOWS\system32>az acr login --name sapclmiftregistry

```

Login Succeeded

open the Azure Registry page and check access keys:
[https://portal.azure.com/#@sap.onmicrosoft.com/resource/subscriptions/3a9986fa-8e53-4d17-98fc-3ddf4042818b/resourceGroups/sapclmift/providers/Microsoft.ContainerRegistry/registries/sapclmiftregistry/accessKey]()
You should see now the following information. The values required for you to log on to sapclmiftregistry are marked with red frames:

`<img src="{{ site.baseurl }}/images/azure-registry-login.png" />`

Use the Login server, the Username and password to logon with slcb to the Azure registry.
To test that this works, try out the following from the same command prompt you used to log in to the sapclmiftregistry before:

Keep in mind that you cannot log on directly to sapclmiftregistry.azurecr.io . When entering the value for "Address of the Container Image Repository" you must specify a subfolder with your user id: sapclmiftregistry.azurecr.io/`<your user id>`. Example: sapclmiftregistry.azurecr.io/d035521

If you only enter sapclmiftregistry.azurecr.io without specifying a subfolder, you get an error like the following:
Error: Get "https://sapclmiftregistry/v2/": dial tcp: lookup sapclmiftregistry: no such host

slcb copy --onlyBridgebase --SAP_REPO_STAGE val

Example Output in case of success:

C:\Users\D035521\Downloads>slcb copy --onlyBridgebase --SAP_REPO_STAGE val

'slcb' executable information
Executable: slcb
Build date: 2021-06-23 11:08:40 UTC
Git branch: fa/rel-1.1
Git revision: d8971d2f5c68c039a6ee7e29dfcf85b13dc8bcc5
Platform: windows
Architecture: amd64
Version: 1.1.65
SL Core version: 1.0.0
SLUI version: 2.6.67
Arguments: copy --onlyBridgebase --SAP_REPO_STAGE val
Working dir: C:\Users\D035521\Downloads
Schemata: 0.0.65, 1.14.65

Explanation of supported shortcuts:
`<F1>`: Display help for input value.
`<ENTER>` or `<Ctrl-N>`: Confirm and continue to next input value.
`<Ctrl-C>`: Abort current processing and return to the Welcome dialog.
Ctrl-C is not explicitly shown as an option in the command line prompt but you can always use it.
`<F12>` or `<Ctrl-B>`: Go back to previous input value.

`<r>`: Retry current step.
`<e>`: Edit a multi-line input value.
`<Tab>`: Completion of input values.
In dialogs that accept only a restricted set of values (like files, directories etc)
use the `<Tab>` key to cycle through the values or for completion of incomplete input.

Copy bridgebase images only

Starting step "Download Bridge Images"

---

* Product Bridge Image Repository *

---

Enter the address of your private container image repository used to store the bridge images.
You require read and write permissions for this repository.
Choose action `<F12>` for Back/`<F1>` for help
Address of the Container Image Repository: sapclmiftregistry.azurecr.io/d035521

---

* Image Registry User *

---

The user name used to logon to "sapclmiftregistry.azurecr.io". For user name enter the application (client) ID. For password enter the client secret. Identity token generated with "az acr
login" is not used.
Choose action `<F12>` for Back/`<F1>` for help
Image registry user name: sapclmiftregistry
Choose action `<F12>` for Back/`<F1>` for help
Image registry password:

---

* Enter Logon Information *

---

You require S-User credentials to log on to the SAP Registry ("rhapi.repositories.cloud.sap") for product version "SL TOOLSET 1.0" (01200615320900005323)
Choose action `<F12>` for Back/`<F1>` for help
S-User Name: D035521
Choose action `<F12>` for Back/`<F1>` for help
Password:

Copying image slcb://01200615320900005323.val.dockersrv.repositories.sapcdn.io/com.sap.sl.cbpod/slcbridgebase:1.1.65 to "sapclmiftregistry.azurecr.io/d035521"
Copying image slcb://01200615320900005323.val.dockersrv.repositories.sapcdn.io/com.sap.sl.cbpod/nginx-sidecar:1.1.65 to "sapclmiftregistry.azurecr.io/d035521"
Successfully replicated all images

C:\Users\D035521\Downloads>
