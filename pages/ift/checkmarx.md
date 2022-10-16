---
layout: default
---
We need to provide necessary security scan reports to the Sofia Team before Release Decision meeting which takes place two weeks after dev close. Dayana always sends an email stating the date when we need to provide the results.

Security reports needs to be collected for the following projects:

1. Image replication service
2. Diag Util
3. ELM bridge

Checkmarx [https://sap.whitesourcesoftware.com/Wss/WSS.html#!home](https://sap.whitesourcesoftware.com/Wss/WSS.html#!home){:target="_blank"}

1. CTNR ELM REPLICATION SRV 1.0

You can find the reports in the build artifacts of the respective master build job in Jenkins [image Replication Service - master](https://edgelm.jaas-gcp.cloud.sap.corp/job/edgelm/job/image-replication-service/job/master/){:target="_blank"}


Aletrnatively,

To generate the report do the following:

1. Open [Protecode UI](https://protecode.c.eu-de-2.cloud.sap/#/groups/1083){:target="_blank"}
2. Select the latest image/tar file with the latest version which is shipped
3. If there are any vulnerabilities, triage them before generating the report.
4. Click on the respective project
5. Click on the export dropdown on the right side and select Summary (CVSS v3) as PDF. See screenshot below


<img src="{{ site.baseurl }}/images/protecode-report.png" />

Similarly do for other projects:

1. DIST - CTNR SL K8S DIAGNOSTICS 1.0

* [Jenkins job](https://edgelm.jaas-gcp.cloud.sap.corp/job/edgelm/job/diagutil/job/master/){:target="_blank"}
* [Protecode](https://protecode.c.eu-de-2.cloud.sap/#/groups/1588){:target="_blank"}

2. DIST - ELM BRIDGE 1.0

* [Jenkins job](https://iftjenkins.jaas-gcp.cloud.sap.corp/job/ElmBridge/job/elm-bridge/job/master/){:target="_blank"}
* [Whitesource ](https://protecode.c.eu-de-2.cloud.sap/#/groups/1135){:target="_blank"}
