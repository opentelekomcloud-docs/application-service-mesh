:original_name: asm_bulletin_0003.html

.. _asm_bulletin_0003:

Istio Version Support Mechanism
===============================

Powered by Istio, ASM is a fully hosted service mesh infrastructure that features high performance, reliability, and usability. It enables you to monitor and manage service traffic, ensure access security, and perform diverse forms of grayscale releases. As the Istio community periodically releases Istio versions, ASM will release corresponding Istio versions accordingly. This section describes the Istio version policies of ASM.

.. table:: **Table 1** Version lifecycle of Istio in ASM

   +---------+-------------------+------------------------+------------------+---------------------+------------------+
   | Version | Status            | Community Release Time | Version OBT Time | Commercial Use Time | Version EOS Time |
   +=========+===================+========================+==================+=====================+==================+
   | v1.18   | In commercial use | June 2023              | December 2023    | June 2024           | June 2027        |
   +---------+-------------------+------------------------+------------------+---------------------+------------------+
   | v1.15   | In commercial use | August 2022            | April 2023       | October 2023        | October 2026     |
   +---------+-------------------+------------------------+------------------+---------------------+------------------+
   | v1.13   | EOS               | February 2022          | June 2022        | January 2023        | January 2026     |
   +---------+-------------------+------------------------+------------------+---------------------+------------------+
   | v1.8    | EOS               | May 2021               | July 2021        | January 2022        | April 2024       |
   +---------+-------------------+------------------------+------------------+---------------------+------------------+
   | v1.6    | EOS               | May 2020               | September 2020   | May 2021            | April 2024       |
   +---------+-------------------+------------------------+------------------+---------------------+------------------+
   | v1.3    | EOS               | September 2019         | December 2019    | March 2020          | April 2024       |
   +---------+-------------------+------------------------+------------------+---------------------+------------------+

Version Phases of Istio in ASM
------------------------------

-  OBT: You can experience the latest features from the Istio OBT version. However, the stability of this version has not been completely verified.
-  Commercial use: The commercial version has been fully verified and is stable and reliable.
-  Version EOS: After an Istio version reaches its EOS, ASM no longer supports the creation of service meshes of this Istio version and does not provide technical support, including new feature updates, vulnerability or issue fixes, new patches, service ticket guidance, and online checks.

Version Description of Istio in ASM
-----------------------------------

Istio versions evolve iteratively based on the community versions, so Istio versions are in the format of **v**\ *X.Y.Z*\ **-r**\ *N*, which consists of the community version and patch version, for example, v1.18.2-r0.

-  A community Istio version is in the format of *X.Y.Z*, which inherits the community version policy. The major version is represented by *X*, the minor version is represented by *Y*, and the patch version is represented by *Z*.
-  An example patch version is v1.18.2-r\ *N*. New patches are released on an irregular basis for the community Istio versions that are still in the maintenance period. If a new patch version provides new features, bug fixes, vulnerability fixes, or scenario optimizations compared to the previous version, the *N* version number increases.

Upgrading Istio in ASM
----------------------

To ensure you have access to new features and avoid any known vulnerabilities or issues, it is recommended that you regularly upgrade Istio to a secure, stable, reliable version. Once an Istio version reaches EOS, technical support is no longer available. Therefore, it is important to upgrade your Istio version promptly. After a mesh is upgraded, it cannot be rolled back to the source version.

Compatibility Between Istio Versions in ASM and CCE Cluster Versions
--------------------------------------------------------------------

This section describes the Istio version support mechanism of Application Service Mesh (ASM).

.. table:: **Table 2** Compatibility between Istio versions and CCE cluster versions

   +---------------+---------------------------------------------------------------+
   | Istio Version | CCE Cluster Version                                           |
   +===============+===============================================================+
   | v1.18         | v1.25, v1.27, v1.28, v1.29, v1.30, v1.31, v1.32, v1.33, v1.34 |
   +---------------+---------------------------------------------------------------+
   | v1.15         | v1.21, v1.23, v1.25, v1.27, or v1.28                          |
   +---------------+---------------------------------------------------------------+
   | v1.13         | v1.21 or v1.23                                                |
   +---------------+---------------------------------------------------------------+
   | v1.8          | v1.15, v1.17, v1.19, or v1.21                                 |
   +---------------+---------------------------------------------------------------+
   | v1.6          | v1.15 or v1.17                                                |
   +---------------+---------------------------------------------------------------+
   | v1.3          | v1.13, v1.15, v1.17, or v1.19                                 |
   +---------------+---------------------------------------------------------------+
