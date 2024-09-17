:original_name: asm_qs_0004.html

.. _asm_qs_0004:

Preparations
============

Before enabling Istio for a cluster, perform the following operations.

.. _asm_qs_0004__section1956152937:

Creating a VPC
--------------

Virtual Private Cloud (VPC) provides a logically isolated, configurable, and manageable virtual network environment, improving resource security and simplifying network deployment.

#. Log in to the VPC console.
#. Click **Create VPC** in the upper right corner.
#. Configure the parameters as prompted and click Create Now.

Creating a Key Pair
-------------------

Create a key pair for identity authentication upon remote node login.

#. Log in to the Elastic Cloud Server (ECS) console.
#. In the navigation pane, choose **Key Pair**. On the page displayed, click **Create Key Pair** in the upper right corner.
#. Enter a key pair name and click **OK**.
#. Manually or automatically download the private key file. The file name is the specified key pair name with a suffix of **.pem**. Securely store the private key file. In the dialog box displayed, click **OK**.

   .. note::

      For security purposes, a key pair can be downloaded only once. Keep it secure to ensure successful login.

Creating a Load Balancer
------------------------

A load balancer will be used as the external access entry of a service mesh, which will route the traffic to backend services.

#. Log in to the Elastic Load Balance (ELB) console.
#. Click Create Elastic Load Balancer in the upper right corner.
#. **VPC** and **Subnet**: Select the VPC and subnet created in :ref:`Creating a VPC <asm_qs_0004__section1956152937>`, configure other parameters as prompted, and click Create Now.

.. _asm_qs_0004__section19395823191819:

Creating a Cluster
------------------

#. Log in to the CCE console.

#. Then, click **Create CCE Cluster** in the upper right corner.

#. Configure the following parameters:

   -  **Cluster Name**: Enter a cluster name, for example, **cluster-test**.
   -  **VPC** and **Subnet**: Select the VPC and subnet created in :ref:`Creating a VPC <asm_qs_0004__section1956152937>`.

   Retain the default settings of other parameters.

#. Click **Next: Select Add-on**.

#. Click **Next: Confirm**. Read the product constraints and select **I am aware of the above limitations**. Review the configured parameters and specifications.

#. **Submit** the order.

   It takes about 6 to 10 minutes to create a cluster. You can click **Back to Cluster List** to perform other operations on the cluster or click **Go to Cluster Events** to view the cluster details.

(Optional) Creating a Namespace
-------------------------------

#. Log in to the CCE console and click the cluster name to access the cluster console.
#. In the navigation pane on the left, choose **Namespaces**. In the upper right corner, click **Create Namespace**.
#. Enter a namespace name and click **OK**.

Creating a Workload and a Service
---------------------------------

#. Log in to the CCE console and click the cluster name to access the cluster console.
#. Choose **Workloads** > **Deployments**. In the the upper right corner, click **Create Workload**.
#. Create a workload and a Service by referring to *CCE User Guide*.
