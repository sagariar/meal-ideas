---
layout: default
---
## Table of contents

---

* [Create a AWS cluster and run an elm installation on it](#create-aws-cluster-and-run-elm-installation)

<!--te-->
---

### Create a AWS cluster and run an elm installation on it

#### Create a cluster

Cluster creation on AWS is very complicated. For now, please ask Billig, Klaus to create a cluster for you.
He will provide the following information:
- Cluster name
- Jump host IP and username
- PPK file to access the jump host

#### Logon to the cluster

If you are using Windows and Putty it should be very easy to use the ".PPK" (Private Key) file to logon to the jump host with Putty.
If you are using a command line to logon via SSH, then you need to convert the file into a ".pem" format:
- Install putty-gen tools
- Run "puttygen <.ppk file from Klaus> -O private-openssh -o \<output filename>"
- Now logon with "ssh -i <.pem file> \<jump host ip> -l \<user>"

#### Switch to admin user

Only the admin user has access to the cluster and the kubernetes CLI (kubectl)
- Run sudo su -

To test the connection just run "kubectl get pods -A"

#### Register kubeconfig on ELMO
The path to the kubeconfig is /root/.kube/config and is only accessible with the root user.
- Open a new terminal
- Run scp \<user>@\<jump host-ip>:/root/.kube/config \<path to local file>

Now you can register the cluster via the elmo UI or you use our internal tool [elm-util](https://github.wdf.sap.corp/edgelm/elm-bridge-oq-util):
- Follow the instructions of the Readme.md to install the tool on your local machine.

You need an env json file to access the ELMO system.
- Ask a colleague to provide you the elmo-env.json for the "test" system.
- Place the file into following path: \<userfolder>/.ssh/elmo-env.json

Now you can register the Cluster:
- KUBECONFIG=\<configfilepath> elm-util -a registerCluster -p \<password for context>
- Now you need to decrypt the downloaded context: elm-util -a decryptContext -p \<same password> -c context.cfg

#### Prepare elm init run

Before you can run elm init, you need to edit the elmo-input.yaml file which is in the downloaded and decrypted context:
- Unzip the elmo-input.yaml file from the context archive.
- Open the file and comment out "KUBECONFIG=config"
- Put the edited file back into the context archive

Next you need an inifile.yml to specify the target registry.
Create a new infile.yml and add these two lines:
- ELM_TARGET_REGISTRY: "<123456789012>.dkr.ecr.\<region>.amazonaws.com/\<project>"
- ELM_TARGET_REGISTRY_TYPE: "Generic"

Now you have to upload the context archive and the inifile.yml to the jump host:
- Run "scp \<path to context archive> \<user>@\<jump host-ip>:/home/\<user>/context.zip"
- Run "scp \<path to inifile> \<user>@\<jump host-ip>:/home/\<user>/inifile.yml"

#### Run elm init

- Go back to the terminal window, where you have the ssh connection to the jump host
- Move to folder "/home/\<user>/"
- Run elm init with the context and the inifile.yml, which you uploaded before

#### Cleanup

Unregister cluster in elmo:
- Run elm-util -a getClusters
- Search for your cluster and remember the id
- Run elm-util -a deleteCluster --id \<id>

Last step:
- Ask Billig, Klaus to delete the Cluster again