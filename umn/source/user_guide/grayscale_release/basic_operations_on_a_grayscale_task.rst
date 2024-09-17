:original_name: asm_01_0037.html

.. _asm_01_0037:

Basic Operations on a Grayscale Task
====================================

Description
-----------

Basic operations on a grayscale version are performed by modifying the configuration of the DestinationRule and VirtualService resources of Istio. After the modification is complete, wait for about 10 seconds for the new policy to take effect.

Modifying the Traffic Policy of a Grayscale Version
---------------------------------------------------

**Modifying a grayscale policy that is based on traffic ratio**

For such a grayscale policy that is based on traffic ratio, you can gradually increase the traffic ratio of the grayscale version to avoid service risks caused by direct traffic switchover. To change the traffic ratio, perform the following steps:

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane, choose **Grayscale Release**. Then click the target canary release task.

#. On the **Configure Traffic Policy** page, set the traffic ratio of the grayscale version.

   If the traffic ratio of the grayscale version is set to **x**, the traffic ratio of the original version is automatically adjusted to **100-x**.

#. Click **Deliver Policy**.

**Modifying a grayscale policy that is based on request content**

With such a policy, a grayscale version can be accessed only when the traffic meets the rules based on Cookies, Headers, Queries, Allowed Operating Systems, and Allowed Browsers. In real-world use cases, rules may be modified for multiple times to fully verify the performance of the grayscale version.

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.
#. In the navigation pane on the left, choose **Grayscale Release** and click the target canary release task.
#. On the **Configure Traffic Policy** page, reconfigure **Cookie**, **Header**, **Query**, **Allowed OS**, and **Allowed Browser**.
#. Click **Deliver Policy**.

Switching the Grayscale Policy Type
-----------------------------------

You can change the type of a grayscale policy from **based on request content** to **based on traffic ratio** and vice versa. After this operation is complete, all configured rules become invalid and all traffic is redistributed based on the new policy.

.. important::

   Grayscale policies can be changed only for running tasks. After a grayscale version is released (that is, the new version completely takes over the traffic and the old version has been brought offline), its grayscale policy cannot be reconfigured.

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.
#. In the navigation pane on the left, choose **Grayscale Release** and click the target canary release task.
#. On the **Configure Traffic Policy** page, change the policy type.
#. Click **Deliver Policy**.

Taking Over All Traffic
-----------------------

After you click **Take Over All Traffic**, the original version or grayscale version takes over all traffic.

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.
#. In the navigation pane on the left, choose **Grayscale Release** and click the target grayscale release task.
#. On the **Monitor and Manage Traffic** page, click **Take Over All Traffic** next to the target version.
#. In the displayed dialog box, click **OK**.

Terminating a Grayscale Release Task
------------------------------------

After the grayscale version takes over all traffic, you can terminate the grayscale task. After the grayscale task is canceled, the original version will be brought offline, and all workloads and Istio configuration resources will be deleted.

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane on the left, choose **Grayscale Release** and click the target grayscale release task.

#. On the **Monitor and Manage Traffic** page, click **Take Over All Traffic** next to the grayscale version.

#. Click **Terminate Task** in the lower right corner.

#. In the displayed dialog box, click **OK**.

   You can go to the **Terminated Tasks** tab page to view the finished grayscale task. The **Release Result** is **Released successfully**.

Canceling a Grayscale Release Task
----------------------------------

After the original version takes over all traffic, you can cancel the grayscale task.

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane on the left, choose **Grayscale Release** and click the target grayscale release task.

#. On the **Monitor and Manage Traffic** page, click **Take Over All Traffic** next to the original version.

#. Click **Cancel Task** in the lower right corner. You can also click |image1| in the upper right corner of a task in the grayscale task list.

#. In the displayed dialog box, click **OK**.

   You can go to the **Terminated Tasks** tab page to view the finished grayscale task. The **Release Result** is **Released canceled**.

Viewing Terminated Grayscale Release Tasks
------------------------------------------

You can view canceled and finished grayscale tasks on the **Terminated Tasks** tab page.

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane on the left, choose **Grayscale Release** and click the **Terminated Tasks** tab page.

   You can view the release task name, release result, service, and release time, and delete a terminated task.

.. |image1| image:: /_static/images/en-us_image_0000001209978068.png
