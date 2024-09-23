:original_name: asm_productdesc_0011.html

.. _asm_productdesc_0011:

Grayscale Release
=================

Application Scenarios
---------------------

In traditional iterations, a new service version is directly released to all users at a time. This is risky, because once an online accident or bug occurs, the impact on users is great. It could take a long time to fix the issue. Sometimes, the version has to be rolled back, which severely affects user experience.

Grayscale release is a smooth iteration mode for version upgrade. During the upgrade, some users use the new version, while other users continue to use the old version. After the new version is stable and ready, it gradually takes over all the live traffic.

Product Benefits
----------------

ASM provides multiple grayscale release functions for application governance. It allows you to detect and fix issues at the early stage and ensure that the iteration goes smoothly and efficiently.

Product Advantages
------------------

-  **Built-in grayscale release process**: Multiple typical grayscale release processes are provided based on fine-grained distribution rules. A grayscale release wizard is provided for you to conveniently perform grayscale release practices. When a service version processes traffic, you can create a grayscale version. After the grayscale version is rolled out successfully, you can configure grayscale policies and diverge live traffic to the grayscale version.
-  **Flexible grayscale policies**: You can set grayscale policies based on traffic ratio or request content, such as the OS, browser, cookie, and header information in an HTTP request. After configuring grayscale policies, you can view the running status and access information on multiple online versions in real time. You can select a stable version and switch all live traffic to this version in one click.
