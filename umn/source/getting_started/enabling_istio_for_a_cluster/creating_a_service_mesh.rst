:original_name: asm_qs_0010.html

.. _asm_qs_0010:

Creating a Service Mesh
=======================

ASM allows you to create a service mesh of the Basic edition, which is a standard service mesh available for commercial use.

Procedure
---------

#. Log in to the ASM console and click **Create Mesh**.

#. Configure the following parameters and retain the default values for other parameters.

   -  **Mesh Edition**

      The default value is **Basic edition**.

   -  **Mesh Name**

      Enter the service mesh name.

   -  **Istio Version**

      Select the Istio version supported by the service mesh.

   -  **Cluster**

      Select the cluster created in :ref:`Creating a Cluster <asm_qs_0004__section19395823191819>`.

   -  **Mesh Control Plane Node**

      To achieve HA, select two or more nodes from different AZs.

#. Review the service mesh configuration in **Configuration List** on the right of the page and click **Submit**.

   It takes about 1 to 3 minutes to create a service mesh. If the service mesh status changes from **Installing** to **Running**, the service mesh is successfully created.
