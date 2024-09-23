:original_name: asm_01_0031.html

.. _asm_01_0031:

Configuration Diagnosis
=======================

ASM diagnoses all services in a managed cluster. Traffic management and grayscale release are available only for normal services.

Constraints
-----------

-  If multiple services correspond to one deployment, these services cannot be added to the mesh. Otherwise, functions such as grayscale release or gateway access may fail.
-  If the workload of a service uses the host network mode (**hostNetwork: true** is configured for the pod), sidecars cannot be injected for the service.

Service Diagnosis
-----------------

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane, choose **Service Management**. The diagnosis results of services are displayed in the **Configuration Diagnosis Result** column.

   If a service is abnormal, click **Fix** to fix the issues. For details, see :ref:`Service Issue Fixing <asm_01_0031__section104191546916>`.

#. After the issues are fixed, you can click **Diagnose Again** to diagnose the service again.

.. _asm_01_0031__section104191546916:

Service Issue Fixing
--------------------

If a service is abnormal, you need to manually fix the abnormal items and then perform auto fix for left issues.

#. Click **Fix** in the row of the abnormal service. If there are issues to be fixed manually, click **View Solution** to see how to fix them.
#. Click **Next** to go to the auto fix page, and click **Auto Fix** to automatically fix left issues.

   .. note::

      -  If left issues cannot be fix automatically, click **View Solution** and fix them manually.
      -  Auto fix does not support Services which have configured gateways or have created grayscale release tasks.
      -  If the service is not displayed in the service list, check whether the corresponding workload exists.
