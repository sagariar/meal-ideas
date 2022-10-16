---
layout: default
---
## Migration from 749 to 753 SAPinst

### Summary

| **SAPinst version**,<br /> **features** | **JVM Patch**  | **External?** | **SWPM SP** | **XPath groups** | **Linux PPC64 BE** | **RHEL 9** |
|---|:---:|:---:|:---:|---|:---:|:---:|
| [749.0.94](https://jira.tools.sap/issues/?jql=project%20%3D%20TIPCORELMCROSSITCLINST%20AND%20fixVersion%20%3D%20%22SAPinst%20749.0.94%22)  | 81 | :white_check_mark: | SP 35 | not restricted | **:white_check_mark:** | :x: |
| [749.0.95](https://jira.tools.sap/issues/?jql=project+%3D+TIPCORELMCROSSITCLINST+AND+fixVersion+%3D+%22SAPinst+749.0.95%22)  | 88 | :x: | :x: | restricted | :white_check_mark: | :white_check_mark: |
| [753.0.2](https://jira.tools.sap/issues/?jql=project%20%3D%20TIPCORELMCROSSITCLINST%20AND%20fixVersion%20%3D%20%22SAPinst%20753.0.2%22)   | 88 | :white_check_mark: | SP36 (initial) | restricted <br /> (packages.xml adapted) | :white_check_mark: | :white_check_mark: |
| [753.0.3](https://jira.tools.sap/issues/?jql=project%20%3D%20TIPCORELMCROSSITCLINST%20AND%20fixVersion%20%3D%20%22SAPinst%20753.0.3%22)   | 90 | :white_check_mark:  | SP36 (patch) | not restricted | :x: | :white_check_mark: |

### Remarks

1. SAP JVM:

   1. Patch 88 implements security patch for XPath expressions via jdk.xml.xpathExprGrpLimit property;
      this affects product.xml files for SWPM SP 35;
      fix will come with SAPinst 753.0.3
   2. Patch 89 has restricted PAM;
      besides support end of PPC64 big endian CPUs, further OS versions are not maintained any more;
      Message for PPC64 big endian in JVM patch 88 (from smoketest)

      ```
      WARNING    2022-09-19 16:16:57.073 (sapsrc30/shadow) (startInstallation) [CSiManagerInterfaces.cpp:158]
      Java executable:
      Path:              /sapmnt/ls3896/a/753_COR/bc_753_COR/linuxppc64/genoptU/_out/jre/bin/java
      Version:           1.8.0_333
      Runtime Version:   8.1.088
      Platform Support : Support for SAP JVM on SUSE Linux Enterprise Server 11 ends March 31st, 2022. See SAP note 2998013.
      ```
2. Besides showing different versions, SAPinst 749.0.95 and 753.0.2 are build on an equal source code base;
   both of them contain SAP JVM patch 88;
   Kernel codeline is different which does not impact the functionality of SAPinst.

### SAP Notes
| SAP Note | Title |
|:--:|--|
| [2393060](https://launchpad.support.sap.com/#/notes/2393060) | Release SAPinst Framework 749 Central Note
| [3207613](https://launchpad.support.sap.com/#/notes/3207613) | Release SAPinst Framework 753 Central Note 
| [929929](https://launchpad.support.sap.com/#/notes/929929) | Latest SAPinst Patch 
| [2998013](https://launchpad.support.sap.com/#/notes/2998013) | SAP JVM 8.1 As Runtime for SAP Tools 
| [2754340](https://launchpad.support.sap.com/#/notes/2754340) | Start SAPinst 749 and higher with external SAP JVM binaries 
| [1680045](https://launchpad.support.sap.com/#/notes/1680045) | Release Note for Software Provisioning Manager 1.0 (recommended: SWPM 1.0 SP35) 
| [2568783](https://launchpad.support.sap.com/#/notes/2568783) | Release Note for Software Provisioning Manager 2.0 (recommended: SWPM 2.0 SP12) 

### SWPM

1. SWPM in Development was changed to 753_COR within https://jira.tools.sap/browse/TIPCORELMCROSSITCLINST-2752
2. SWPM 1.0 SP35/SWPM 2.0 SP12

   1. SAPinst 749.0.94 is included
   2. In order to not impact these SWPMs (security patch for XPath expressions)
      - 749.0.95 will not be consumed by these SWPMs
      - SAPinst 749.0.95 will be available only internally via patch-inbox-external
      - Currently there is no open customer ticket for any 749.0.95 feature;
        if something comes up, we may release this SAPinst version later; probability is low due to EoM in Dec 2022
3. SWPM 1.0 SP36/SWPM 2.0 SP13

   1. Initially SAPinst 753.0.2 will be included
      - XPath restriction is solved by adapting packages.xml
      - Linux PPC64 BE is still working
   2. SAPinst 753.0.3 patch will be available after SWPM RTC
      - XPath restriction is solved within SAPinst
      - Linux PPC64 BE platform is not available any more
