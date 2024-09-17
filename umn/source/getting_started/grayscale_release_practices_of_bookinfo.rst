:original_name: asm_qs_0001_0.html

.. _asm_qs_0001_0:

Grayscale Release Practices of Bookinfo
=======================================

Application Service Mesh (ASM) is a service mesh platform developed based on Istio and seamlessly interconnects with Cloud Container Engine (CCE). With better usability, reliability, and visualization, ASM provides you with out-of-the-box features and enhanced user experience.

Introduction
------------

Grayscale releases enable smooth iteration of software products in production environments. This section takes Bookinfo as an example to illustrate Istio-based service governance using ASM.

The grayscale release process of Bookinfo is as follows.


.. figure:: /_static/images/en-us_image_0000001202041610.png
   :alt: **Figure 1** Grayscale release process of Bookinfo

   **Figure 1** Grayscale release process of Bookinfo

Architecture Analysis of Bookinfo
---------------------------------

Bookinfo is an application that functions as an online bookstore that displays each book with its description, details (such as pages), and reviews.

Bookinfo consists of four independent services developed in different languages. These services demonstrate the features of a typical service mesh. They are described as follows:

-  productpage: calls the details and reviews services to generate a page.
-  details: contains book information.
-  reviews: contains book reviews and calls the ratings service.
-  ratings: contains book rating information based on reviews.

The reviews service has three versions:

-  The v1 (1.5.0) version does not call the ratings service.
-  The v2 (1.5.1) version calls the ratings service and uses one to five black stars to show ratings.
-  The v3 (1.5.2) version calls the ratings service and uses one to five red stars to show ratings.

.. note::

   To demonstrate traffic switching between versions, this section takes 1.5.1 (rating with black stars) and 1.5.2 (rating with red stars) of the reviews service as examples.


.. figure:: /_static/images/en-us_image_0000001440024745.png
   :alt: **Figure 2** End-to-end architecture of Bookinfo

   **Figure 2** End-to-end architecture of Bookinfo

Running Bookinfo with ASM does not require any changes on the application itself. Simply configure and run the services in the ASM environment, that is, inject an Envoy sidecar into each service. :ref:`Figure 3 <asm_qs_0001_0__fig1239019461376>` shows the final deployment.

.. _asm_qs_0001_0__fig1239019461376:

.. figure:: /_static/images/en-us_image_0000001389665636.png
   :alt: **Figure 3** Bookinfo with Envoy sidecars injected

   **Figure 3** Bookinfo with Envoy sidecars injected

All services are integrated with Envoy sidecars. All inbound and outbound traffic of the integrated services is intercepted by sidecars. In this way, ASM can provide service routing, telemetry data collection, and policy implementation for Bookinfo.

Preparations
------------

Perform the following operations:

#. .. _asm_qs_0001_0__li14222135210592:

   Create a VPC and subnet.

   Virtual Private Cloud (VPC) provides a logically isolated, configurable, and manageable virtual network environment, improving resource security and simplifying network deployment.

   a. Log in to the VPC console.
   b. Click Create VPC in the upper right corner.
   c. Configure the parameters as prompted and click Create Now.

#. .. _asm_qs_0001_0__li8805135016420:

   (Optional) Create a key pair.

   To log in to a cluster node using a key pair, create a key pair in advance.

   a. Log in to the Elastic Cloud Server (ECS) console.
   b. In the navigation pane, choose **Key Pair**. On the page displayed, click **Create Key Pair** in the upper right corner.
   c. Enter a key pair name and click **OK**.
   d. Manually or automatically download the private key file. The file name is the specified key pair name with a suffix of **.pem**. Securely store the private key file. In the dialog box displayed, click **OK**.

      .. note::

         For security purposes, a key pair can be downloaded only once. Keep it secure to ensure successful login.

#. Create a load balancer.

   A load balancer will be used as the external access entry of a service mesh, which will route the traffic to backend services.

   a. Log in to the Elastic Load Balance (ELB) console.
   b. Click Create Elastic Load Balancer in the upper right corner.
   c. **VPC** and **Subnet**: Select the VPC and subnet created in :ref:`1 <asm_qs_0001_0__li14222135210592>`, configure other parameters as prompted, and click Create Now.

#. .. _asm_qs_0001_0__li1024821518115:

   Create a cluster.

   a. Log in to the Cloud Container Engine (CCE) console.

   b. In the navigation pane, choose **Resource Management** > **Clusters**. Then, click **Create CCE Cluster** in the upper right corner.

   c. On the **Configure** page, configure the following parameters and retain the default values for other parameters.

      -  **Cluster Name**: Enter a cluster name, for example, **cce-asm**.
      -  **VPC** and **Subnet**: Select the VPC and subnet created in :ref:`1 <asm_qs_0001_0__li14222135210592>`.

   d. Click **Next: Create Node**, configure the following parameters, and retain the default values for other parameters.

      -  **Specifications**: 4 vCPUs and 8 GiB of memory.

         .. note::

            This is the minimum specifications for deploying Bookinfo.

      -  **Login Mode**: Select the key pair created in :ref:`2 <asm_qs_0001_0__li8805135016420>` for identity authentication upon remote node login.

   e. Click **Next: Install Add-on** and select the add-ons to be installed in the **Install Add-on** step.

      **System resource add-on** must be installed. **Advanced functional add-on** is optional.

   f. Click **Next: Confirm**. Read the product constraints and select **I am aware of the above limitations**. Review the configured parameters and specifications.

   g. Submit the order.

      It takes about 6 to 10 minutes to create a cluster. You can click **Back to Cluster List** to perform other operations on the cluster or click **Go to Cluster Events** to view the cluster details.

#. Prepare the images required by Bookinfo (as shown in :ref:`Table 1 <asm_qs_0001_0__table428162913363>`), push them to SWR and set their **Type** to **Public**.

   .. caution::

      The image name and tag of each service must be the same as those in :ref:`Table 1 <asm_qs_0001_0__table428162913363>`. Otherwise, the experience task may fail.

   .. _asm_qs_0001_0__table428162913363:

   .. table:: **Table 1** Image list

      =========== ================================ ==========
      Service     Image Name                       Image Tag
      =========== ================================ ==========
      productpage examples-bookinfo-productpage-v1 1.5.0
      details     examples-bookinfo-details-v1     1.5.01.5.0
      ratings     examples-bookinfo-ratings-v1     1.5.01.5.0
      reviews     examples-bookinfo-reviews-v1     1.5.1
      \           examples-bookinfo-reviews-v1     1.5.2
      =========== ================================ ==========

   The following uses Bookinfo images as an example:

   a. Prepare a computer that can access the Internet and has Docker 1.11.2 or later installed.

   b. .. _asm_qs_0001_0__li15857121914118:

      Run the following commands in sequence to download the images required by Bookinfo:

      **docker pull docker.io/istio/examples-bookinfo-productpage-v1:1.5.0**

      **docker pull docker.io/istio/examples-bookinfo-details-v1:1.5.0**

      **docker pull docker.io/istio/examples-bookinfo-ratings-v1:1.5.0**

      **docker pull docker.io/istio/examples-bookinfo-reviews-v2:1.5.0**

      **docker pull docker.io/istio/examples-bookinfo-reviews-v3:1.5.0**

   c. Connect to SWR.

   d. Label the images pulled in :ref:`5.b <asm_qs_0001_0__li15857121914118>`. Ensure that the image names and tags are the same as those in :ref:`Table 1 <asm_qs_0001_0__table428162913363>`.

      **docker tag docker.io/istio/examples-bookinfo-productpage-v1:1.5.0** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-productpage-v1:1.5.0**

      **docker tag docker.io/istio/examples-bookinfo-details-v1:1.5.0** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-details-v1:1.5.0**

      **docker tag docker.io/istio/examples-bookinfo-ratings-v1:1.5.0** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-ratings-v1:1.5.0**

      **docker tag docker.io/istio/examples-bookinfo-reviews-v2:1.5.0** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-reviews-v1:1.5.1**

      **docker tag docker.io/istio/examples-bookinfo-reviews-v3:1.5.0** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-reviews-v1:1.5.2**

      *swr.xxxxxxxxx.* indicates the image repository address, and *group* indicates the organization name. Replace them with the actual values.

   e. Push the images to the SWR.

      **docker push** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-productpage-v1:1.5.0**

      **docker push** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-details-v1:1.5.0**

      **docker push** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-ratings-v1:1.5.0**

      **docker push** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-reviews-v1:1.5.1**

      **docker push** *swr.xxxxxxxxx.*\ **/**\ *group*\ **/examples-bookinfo-reviews-v1:1..5.2**

   f. Change the image type to **Public**.

Creating a Mesh
---------------

#. Log in to the ASM console.

#. Click **Create Mesh** in the upper right corner.

#. Configure the following parameters and retain the default values for other parameters.

   -  **Mesh Edition**

      The default value is **Basic edition**.

   -  **Mesh Name**

      Enter the mesh name.

   -  **Istio Version**

      Select the Istio version supported by the mesh.

   -  **Cluster**

      Select the cluster created in :ref:`4 <asm_qs_0001_0__li1024821518115>`.

   -  **Mesh Control Plane Node**

      To achieve HA, select two or more nodes from different AZs.

#. Review the service mesh configuration in **Configuration List** on the right of the page and click **Submit**.

   It takes about 1 to 3 minutes to create a service mesh. If the service mesh status changes from **Installing** to **Running**, the service mesh is successfully created.

Deploying Bookinfo in One Click
-------------------------------

After the service mesh is enabled for the cluster, you can quickly create a Bookinfo demo.

#. Log in to the ASM console.
#. Click the name of the service mesh to access its details page.
#. In the navigation pane, choose **Experience Tasks** and click **Try Now** in the Bookinfo task.
#. On the right of the page, set **Cluster** to the cluster where Bookinfo resides, set **Load Balancer** to a load balancer that is in the same VPC and subnet as the selected cluster, set an external port, and click **Install**.
#. Wait until Bookinfo is created. Click **Service Management** and ensure that the value in the **Configuration Diagnosis Result** column is **Normal**. The Bookinfo contains the productpage, details, reviews, and ratings services.

Creating a Grayscale Release Task
---------------------------------

A new grayscale version of the **reviews** service of Bookinfo will be created. A grayscale policy will be configured to divert traffic of the default version to the new version.

The following steps will guide you to create a new version (v3) of the **reviews** service and divert 30% traffic of Bookinfo to this version.

**Deploying a grayscale version**

#. In the navigation pane, choose **Grayscale Release**. On the **Canary Release** area of the displayed page, click **Create Release Task**.
#. Configure basic information.

   -  **Task Name**: Enter a task name, for example, **reviews-v3**.
   -  **Namespace**: Select the namespace that the service belongs to.
   -  **Service**: Select **reviews** from the drop-down list box.
   -  **Workload**: Select the workload that the service belongs to.

#. Configure version information.

   -  **Cluster**: Select the cluster that the service belongs to.
   -  **Version**: Set this parameter to **v3**.
   -  **Pods**: Retain the default value.
   -  **Pod Configuration**: Set the image tag to **1.17.2** and retain the default values for other parameters.

#. Click **Release**. If the progress reaches 100%, the grayscale version is successfully released.

**Configuring a traffic policy**

Configure a grayscale policy for the grayscale version. A specified percentage of traffic will be diverted from the original version to the grayscale version.

#. After the grayscale version is deployed, click **Configure Traffic Policy**.

#. Configure a traffic policy.

   **Policy Type**: The value can be **Based on traffic ratio** or **Based on request content**.

   -  **Based on traffic ratio**: A specified percentage of traffic will be directed to the grayscale version. For example, 80% of the traffic is directed to the original version, and 20% is directed to the grayscale version.
   -  **Based on request content**: Only the traffic that meets specific conditions will be directed to the grayscale version. For example, only users on the Windows operating system can access the grayscale version.

   In this example, configure a traffic policy **Based on traffic ratio** and set the traffic percentage of v3 to **20%**.


   .. figure:: /_static/images/en-us_image_0000001202053160.png
      :alt: **Figure 4** Traffic policy

      **Figure 4** Traffic policy

#. Click **Deliver Policy**.

   It takes several seconds for the traffic policy to take effect. You need to enable APM to view the traffic monitoring data of the original version and grayscale version.

#. On the **Service List** page, click the **Access Address** of the productpage service. Frequently refresh the book information page. You can find that the **Book Reviews** area is switching between black stars (v1) and red stars (v3) and the ratio is nearly 4 to 1.


   .. figure:: /_static/images/en-us_image_0000001247893125.png
      :alt: **Figure 5** v1 page

      **Figure 5** v1 page


   .. figure:: /_static/images/en-us_image_0000001203053124.png
      :alt: **Figure 6** v3 page

      **Figure 6** v3 page

#. Run the following command on a server that has been connected to the public network to continuously access the productpage service:

   **while true;do wget -q -O- http://**\ *ip:port*\ **/productpage; done**

   Return to the **Monitor and Manage Traffic** page on the console and view the real-time traffic monitoring data of v1 and v3.


   .. figure:: /_static/images/en-us_image_0000001203333110.png
      :alt: **Figure 7** Traffic monitoring data

      **Figure 7** Traffic monitoring data

Switching All Traffic to the Grayscale Version
----------------------------------------------

Check whether the number of resources in v3 matches that in v1. After confirming that v3 is able to serve all the traffic of v1, switch all the traffic from v1 to v3.

#. On the **Monitor and Manage Traffic** page, click **Take Over All Traffic** next to v3.

#. Click **OK**.

   A message indicating that the traffic is successfully switched is displayed in the upper right corner. Frequently refresh the Bookinfo page. You can find that only red stars (v3) are used in the **Book Reviews** area.


   .. figure:: /_static/images/en-us_image_0000001203040696.png
      :alt: **Figure 8** v3 page

      **Figure 8** v3 page

Ending the Grayscale Release Task
---------------------------------

After v3 takes over all the traffic from v1, bring v1 offline to release its resources.

#. On the **Monitor and Manage Traffic** page, click **End Task**.

#. Click **OK** to end the task, bring the original version offline, and delete the task.

   Bringing a version offline will delete all its workloads and Istio configuration resources.

Clearing Resources
------------------

This is the end of the demo of performing the grayscale release using ASM. Delete applications and nodes in time to avoid unnecessary fees.

#. In the navigation pane, choose **Experience Tasks** and click **Uninstall** in the Bookinfo task.
#. Click **OK**. After the Bookinfo experience task is uninstalled, the productpage, details, reviews, and ratings services and related resources are automatically deleted.

   .. note::

      After an experience task is uninstalled, go to the CCE console and manually delete the workloads corresponding to the grayscale version of the service for which grayscale release has been completed.
