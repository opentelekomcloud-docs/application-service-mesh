:original_name: asm_qs_0009.html

.. _asm_qs_0009:

Grayscale Release
=================

Creating a Grayscale Release Task
---------------------------------

#. Log in to the ASM console and click |image1| in the **asmtest** mesh.

#. Set **Task Name** to **test** and select **servicetest** created in :ref:`Creating a Workload and a Service <asm_qs_0008__section496120305565>` for **Service**. (**Workload** is automatically set to **deptest**.) Configure other basic information and grayscale version information and click **Release**.

   .. note::

      If you cannot select **servicetest**, check whether the service is normal. If the service is abnormal, fix the issues and try again.

#. Click **Configure Traffic Policy**, set the policy type to **Based on traffic ratio**, and set the **traffic ratio** of v2 to 80%.

#. Click **Deliver Policy**.

   It takes several seconds for the traffic policy to take effect. You can view the running of the grayscale version on the **View Status** page.

Switching All Traffic to the Grayscale Version
----------------------------------------------

Check whether the number of resources in v2 matches that in v1. After confirming that v2 is able to serve all the traffic of v1, switch all the traffic from v1 to v2.

#. On the **Grayscale Release** page, click **test** and then click **Monitor and Manage Traffic**.
#. Click **Take Over All Traffic** next to v2.
#. Click **OK**. A message is displayed in the upper right corner, indicating that the traffic is taken over successfully.

Bringing the Original Version Offline
-------------------------------------

After v2 takes over all the traffic from v1, bring v1 offline to release its resources.

#. On the **Grayscale Release** page, click **test** and then click **Monitor and Manage Traffic**.

#. On the displayed page, when the traffic percentage of v2 is **100%**, v2 has taken over all traffic of v1. Click **Terminate Task**.

#. Click **OK**.

   The v1 version is brought offline and the test grayscale task is deleted.

.. |image1| image:: /_static/images/en-us_image_0000001247200741.png
