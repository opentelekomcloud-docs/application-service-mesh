:original_name: asm_01_0035.html

.. _asm_01_0035:

Grayscale Release Overview
==========================

When switching between old and new services, you may be challenged in ensuring the system service continuity. If a new service version is directly released to all users at a time, it can be risky because once an online accident or bug occurs, the impact on users is great. It could take a long time to fix the issue. Sometimes, the version has to be rolled back, which severely affects user experience.

Several release policies are developed for service upgrade: canary release, blue-green deployment, A/B testing, rolling upgrade, and batch suspension of release. Traffic loss or service unavailability caused by releases can be avoided as much as possible. Currently, ASM supports canary release and blue-green deployment.

Canary Release
--------------

Canary release is also called grayscale release. It is a smooth iteration mode for version upgrade. During the upgrade, some users use the new version, while other users continue to use the old version. After the new version is stable and ready, it gradually takes over all the live traffic. In this way, service risks brought by the release of the new version can be minimized, the impact of faults can be reduced, and quick rollback is supported.


.. figure:: /_static/images/en-us_image_0000001254994475.png
   :alt: **Figure 1** Canary release process

   **Figure 1** Canary release process

Blue-Green Deployment
---------------------

Blue-green deployment provides a zero-downtime, predictable manner for releasing applications to reduce service interruption during the release. A new version is deployed while the old version is retained. The two versions are online at the same time. The new and old versions work in hot backup mode. The route weight is switched (0 or 100) to enable different versions to go online or offline. If a problem occurs, the version can be quickly rolled back.


.. figure:: /_static/images/en-us_image_0000001210274518.png
   :alt: **Figure 2** Blue-green deployment process

   **Figure 2** Blue-green deployment process
