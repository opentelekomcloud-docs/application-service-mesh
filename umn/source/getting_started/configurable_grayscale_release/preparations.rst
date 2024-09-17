:original_name: asm_qs_0008.html

.. _asm_qs_0008:

Preparations
============

Before creating a grayscale release task, perform the following operations.

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

.. _asm_qs_0008__section4238161922215:

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

.. _asm_qs_0008__section496120305565:

Creating a Workload and a Service
---------------------------------

#. Log in to the CCE console and click the cluster name to access the cluster console.
#. Choose **Workloads** > **Deployments**. In the the upper right corner, click **Create Workload**.
#. Create a workload and a Service by referring to *CCE User Guide*.

Creating a Service Mesh
-----------------------

#. Log in to the ASM console and click **Create Mesh**.
#. Select the cluster named **cluster-test** created in :ref:`Creating a Cluster <asm_qs_0008__section4238161922215>` and select nodes on which the Istio control plane is installed. Two or more nodes in different AZs are recommended.
#. Configure observability parameters as required.
#. Click **Show Advanced Settings**. In **Namespace Injection Settings**, select the namespace named **default** and enable **Restart Existing Services**. Configure other parameters as required.

5. Review the service mesh configuration in **Configuration List** on the right of the page and click **Submit**.

   It takes about 1 to 3 minutes to create a service mesh. If the service mesh status changes from **Installing** to **Running**, the service mesh is successfully created.

Diagnosing Configurations
-------------------------

ASM diagnoses all services in a managed cluster. Grayscale release can be performed only for services that are diagnosed as normal.

#. Log in to the ASM console, click the service mesh named **asmtest** to access its details page.
#. In the navigation pane, choose **Service Management**, select **Namespace: default**, and view the configuration diagnosis result of **servicetest**.
#. If **Abnormal** is displayed, click **Fix** to fix the issue.
