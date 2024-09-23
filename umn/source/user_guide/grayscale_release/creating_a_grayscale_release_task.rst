:original_name: asm_01_0036.html

.. _asm_01_0036:

Creating a Grayscale Release Task
=================================

Basic Concepts
--------------

-  Grayscale version

   Only one grayscale version can be released for a service. You can configure grayscale policies for the version.

-  Grayscale policy

   Before releasing a new service version in the production environment and letting it serve all the live traffic, you can add a grayscale version and configure grayscale policies to serve just a proportion of the traffic. After the grayscale version has run stably for a period, it can serve as the default version to take over all traffic in place of the original version in the production environment.


Creating a Grayscale Release Task
---------------------------------

#. Log in to the ASM console and go to the **Create a grayscale release task** page by one of the following ways:

   -  (Shortcut) In the upper right corner of an Enterprise mesh, click |image1|.
   -  (Shortcut) In the center of the target mesh, click **Create a grayscale release task**.
   -  Create a grayscale release task on the mesh details page.

      a. Click the target mesh and go to its details page, click **Grayscale Release** in the navigation pane on the left.
      b. If no grayscale task is running, click **Create Release Task** in the **Canary Release** or **Blue-Green Deployment** area. If there is an ongoing grayscale task, click **Grayscale Release** in the upper right corner.

#. Configure basic information of the grayscale release task.

   -  **Grayscale Release Form**

      Select **Canary Release** or **Blue-Green Deployment** as required. For details about the differences between the two forms, see :ref:`Grayscale Release Overview <asm_01_0035>`.

   -  **Task Name**

      Customize a grayscale release task name. Enter 4 to 63 characters, starting with a lowercase letter and ending with a letter or digit. Only lowercase letters, digits, and hyphens (-) are allowed.

   -  **Namespace**

      Select the namespace to which the service belongs.

   -  **Service**

      Select the service to be released from the drop-down list box. Services that are running grayscale tasks cannot be selected. They are automatically filtered out from the list.

   -  **Workload**

      Select the workload to which the service belongs.

   -  **Version**

      Current service version number, which cannot be changed.

#. Configure grayscale version information.

   -  **Cluster**

      Select the cluster on which the grayscale version of the service will be deployed.

   -  **Version**

      Enter the grayscale version number of the service.

   -  **Pods**

      Number of pods of the grayscale version. You can modify the number as required. Each pod of the grayscale version consists of containers deployed with the same image.

   -  **Image Name**

      The image of the service is selected by default.

   -  **Image Tag**

      Select the image tag of the grayscale version.

#. Click **Release**. Wait for the grayscale version to be created.

   Ensure that all pods of the grayscale version are running normally and configure the traffic policy when the startup progress reaches 100%. You can view the pod monitoring information, including **Start Logs** and **Performance Monitoring** on the **View Status** page.

#. (For canary release only) Click **Configure Traffic Policy** to configure a traffic policy.

   **Policy Type**: The value can be **Based on traffic ratio** or **Based on request content**.

   -  **Based on traffic ratio**

      A specified ratio of traffic will be directed to the grayscale version. For example, 75% of the traffic is directed to the original version, and 25% is directed to the grayscale version. In actual applications, you can gradually increase the traffic ratio of the grayscale version and deliver policies to monitor the performance of the grayscale version.


      .. figure:: /_static/images/en-us_image_0000001210438852.png
         :alt: **Figure 1** Based on traffic ratio

         **Figure 1** Based on traffic ratio

      **Traffic** **ratio**: You can set the traffic ratio for the original version and grayscale version. The system distributes traffic to the two versions based on the specific traffic ratio.

   -  **Based on request content**

      The grayscale version can be accessed only when the traffic meets the rules based on the cookies, custom headers, queries, operating systems, and browsers. For example, only HTTP requests whose cookies meet **User=Internal** can be forwarded to the grayscale version. Other requests are still received by the original version.


      .. figure:: /_static/images/en-us_image_0000001210119300.png
         :alt: **Figure 2** Based on request content

         **Figure 2** Based on request content

      -  **Cookie**

         **Regular expression**: When the cookie of a request matches the configured regular expression, the request will be distributed to the grayscale version.

      -  **Header**

         -  **Full match**: Only the URL that fully matches the values you set can be accessed. For example, if **Key** is set to **User** and **Value** is set to **Internal**, only requests whose headers contain **User** with the value **Internal** are responded by the service of the grayscale version.

         -  **Regular expression**: When the header of a request matches the configured regular expression, the request will be distributed to the grayscale version.

            You can customize the key and value for filtering. The value supports the full match and regular expression.

      -  **Query**

         -  **Full match**: Only the URL that fully matches the values you set can be accessed. For example, if **Key** is set to **User** and **Value** is set to **Internal**, only requests whose queries contain **User** with the value **Internal** are responded by the service of the grayscale version.

         -  **Regular expression**: When the query of a request matches the configured regular expression, the request will be distributed to the grayscale version.

            You can customize the key and value for filtering. The value supports the full match and regular expression.

      -  **Allowed OS**: Select OSs that can access the grayscale version, including iOS, Android, Windows, and macOS.

      -  **Allowed Browser**: Select browsers that can access the grayscale version, including Chrome and Internet Explorer.

      -  **Traffic management YAML**: The rule YAML is automatically generated based on the configured parameters.

   .. note::

      A traffic policy based on request content is valid only for the entry service that is directly accessed. If you want the traffic policy to be applied to all services, the header information of HTTP requests needs to be transferred in the service code.

      For example, if you configured a grayscale policy based on the request content for service **reviews** and did not transfer the HTTP request header information in the service code, the grayscale policy will not take effect when you send requests to service **productpage**.

      The reason is that when the **productpage** service calls the **reviews** service, the header information of the HTTP request you sent to **productpage** will be lost. As a result, the **reviews** service receives a request without the header information. The grayscale policy will not take effect.

#. Click **Deliver Policy**.

   It takes several seconds for a grayscale policy to take effect. You can view the traffic monitoring of the service and the health monitoring of the original version and grayscale version.

.. |image1| image:: /_static/images/en-us_image_0000001254994843.png
