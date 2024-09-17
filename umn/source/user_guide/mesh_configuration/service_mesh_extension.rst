:original_name: asm_01_0123.html

.. _asm_01_0123:

Service Mesh Extension
======================

Observability configuration includes access logs, application metrics, and traces of the current service mesh. You can enable application metric collection and access logging.

.. note::

   Tracing can be enabled only when a service mesh is created.

Constraints
-----------

Only Istio 1.18 or later can work with LTS to collect and store access logs. To enable access logging, install CCE Log-Agent on the **Add-ons** page in advance.

Enabling Application Metrics
----------------------------

#. Log in to the ASM console.
#. Click the name of the service mesh to go to its details page.
#. In the navigation pane, choose **Mesh Configuration**. Then click the tab for displaying service mesh extension.
#. Enable application metrics, select an AOM instance, and click **OK**.

Enabling Access Logging
-----------------------

#. Log in to the ASM console.
#. Click the name of the service mesh to go to its details page.
#. In the navigation pane, choose **Mesh Configuration**. Then click the tab for displaying service mesh extension.
#. Enable access logging, select the log group and log stream, and click **OK**.
