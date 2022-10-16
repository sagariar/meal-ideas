---
layout: default
---
We need to provide necessary security scan reports to the Sofia Team before Release Decision meeting which takes place two weeks after dev close. Dayana always sends an email stating the date when we need to provide the results.

Security reports needs to be collected for the following projects:

1. Image replication service
2. Diag Util
3. ELM bridge

Whitesource [https://sap.whitesourcesoftware.com/Wss/WSS.html#!home](https://sap.whitesourcesoftware.com/Wss/WSS.html#!home){:target="_blank"}

1. DIST - CTNR ELM REPLICATION SVC 1.0

You can find the reports in the build artifacts of the respective master build job in Jenkins [image Replication Service - master](https://edgelm.jaas-gcp.cloud.sap.corp/job/edgelm/job/image-replication-service/job/master/){:target="_blank"}

<img src="{{ site.baseurl }}/images/whitesource-irs1.png"/>

Aletrnatively,

To generate the report do the following:

1. Open[Whitesource UI](https://sap.whitesourcesoftware.com/Wss/WSS.html#!home){:target="_blank"}
2. Select Reports from the Menu
3. Click on Risk from the drop down
4. Then Select the Products and corresponding Project as seen in the screenshot below

<img src="{{ site.baseurl }}/images/whitesource-irs2.png" />

Similarly do for other projects:

1. DIST - CTNR SL K8S DIAGNOSTICS 1.0

* [Jenkins job](https://edgelm.jaas-gcp.cloud.sap.corp/job/edgelm/job/diagutil/job/master/){:target="_blank"}
* [Whitesource ](https://sap.whitesourcesoftware.com/Wss/WSS.html#!product;id=1531944;orgToken=74cbbb27-f32c-474e-bb6b-d99fbffddee4){:target="_blank"}

2. DIST - ELM BRIDGE 1.0

* [Jenkins job](https://iftjenkins.jaas-gcp.cloud.sap.corp/job/ElmBridge/job/elm-bridge/job/master/){:target="_blank"}
* [Whitesource ](https://sap.whitesourcesoftware.com/Wss/WSS.html#!project;id=2581396;orgToken=74cbbb27-f32c-474e-bb6b-d99fbffddee4){:target="_blank"}
