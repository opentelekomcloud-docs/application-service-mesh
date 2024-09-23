:original_name: asm_01_0041.html

.. _asm_01_0041:

Sidecar Management
==================

On the **Sidecar Management** page, you can view information about all workloads injected with sidecars, perform sidecar injection, and configure sidecar resource limits.

.. _asm_01_0041__section65931513505:

Injecting a Sidecar
-------------------

You can view the namespace and cluster to which the injected sidecar belongs. If no sidecar has been injected or you need to inject sidecar for more namespaces, perform the following operations:

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.
#. In the navigation pane, choose **Mesh Configuration**. Then click the **Sidecar Management** tab.
#. Click **Sidecar Management**, select a namespace, determine whether to restart the existing services, and click **OK**.

   -  **Namespace**: Select one or more namespaces. The system labels the namespaces with **istio-injection=enabled**.

   -  **Restart Existing Services**

      |image1|: Pods of the existing services in the namespace will be restarted, which will temporarily interrupt your services. The **istio-proxy** sidecar is automatically injected into the pods of the existing services.

      |image2|: The **istio-proxy** sidecar cannot be automatically injected into the pods of the existing services. You need to manually restart the workloads on the CCE console to inject the sidecar. Whether to restart existing services affects only existing services. If the namespaces are labeled with **istio-injection=enabled**, sidecars will be automatically injected into new pods.

   -  **Traffic Interception Settings**

      .. note::

         By default, sidecars intercept all inbound and outbound traffic of pods. You can modify the default traffic rules in **Traffic Interception Settings**.

      **Inbound Ports**: Inbound ports separated by commas (,). You can use this field to specify the ports that will be included or excluded for inbound traffic redirection.

      -  **Include only specified ports** means that the traffic to services in a service mesh over specified ports will be redirected to the sidecar.

      -  **Exclude only specified ports** means that the traffic to services in a service mesh over the ports except the specified ports will be redirected to the sidecar.

      **Outbound Ports**: Outbound ports separated by commas (,). You can use this field to specify the ports that will be included or excluded for outbound traffic redirection.

      -  **Include only specified ports** means that the traffic from services in a service mesh over specified ports will be redirected to the sidecar.

      -  **Exclude only specified ports** means that the traffic from services in a service mesh over the ports except the specified ports will be redirected to the sidecar.

      **Outbound IP Ranges**: IP address ranges separated by commas (,) in CIDR format. You can use this field to specify the IP ranges that will be excluded from redirection to the sidecar.

      -  **Include only specified IP ranges** means that the traffic from specified IP ranges will be redirected to the sidecar.

      -  **Exclude only specified IP ranges** means that the traffic from IP ranges except the specified IP ranges will be redirected to the sidecar.

   .. note::

      -  If the system displays a message indicating that modification of namespace injection is not enabled in the following clusters, you need to run the **kubectl** command to enable namespace injection. For details, see :ref:`How Do I Enable Namespace Injection for a Cluster? <asm_faq_0036>`.
      -  After sidecar injection is enabled for a namespace of a cluster, sidecars are automatically injected for pods of all workloads in the namespace. If you do not want to inject sidecars for some workloads, see :ref:`How Do I Disable Sidecar Injection for Workloads? <asm_faq_0037>`.

Viewing Workload Details
------------------------

The list displays all workloads created in the clusters managed by a mesh. You can view the workload name, cluster to which the workload belongs, service, and sidecar information of the workload, including the sidecar name, version, status, CPU usage, and memory usage. The procedure is as follows:

#. In the drop-down list and search box in the upper right corner of the workload list, select a cluster and namespace, and enter the target workload name.

#. Click |image3| in front of the workload to view the sidecar information of the workload.

   If the system displays a message indicating that there is no sidecar in the workload, no sidecar has been injected into the namespace to which the workload belongs. In this case, you can inject one into the namespace. For details, see :ref:`Injecting a Sidecar <asm_01_0041__section65931513505>`.

Configuring Sidecar Resource Limits
-----------------------------------

You can configure the upper and lower limits of CPU and memory resources for sidecars (istio-proxy container). If the upper and lower resource limits are not set for a workload, a resource leak of this workload will make resources unavailable for other workloads deployed on the same node. In addition, workloads that do not have upper and lower resource limits cannot be accurately monitored.

The default upper and lower limits of sidecar resources are as follows:

-  CPU (core): 0.1 to 2 (included)
-  MEM (MiB): 128 to 1,024 (included)

To change the value, perform the following operations:

#. Click **Set Resource Limit** in the **Operation** column of the target workload. You can also select multiple workloads and click **Set Resource Limit** in the upper left corner of the workload list to configure sidecar resource limits in batches.

   -  Minimum CPU: CPU request, the minimum number of CPU cores required by a container. Resources are scheduled for the container based on this value. The container can be scheduled to a node only when the total available CPU on the node is greater than or equal to the number of CPU cores applied for the container.
   -  Maximum CPU: CPU limit, the maximum number of CPU cores required by a container.
   -  Minimum memory: memory request, the minimum amount of memory required by a container. Resources are scheduled for the container based on this value. The container can be scheduled to this node only when the total available memory on the node is greater than or equal to the requested container memory.
   -  Maximum memory: memory limit, the maximum amount of memory required by a container. When the memory usage exceeds the specified memory limit, the pod may be restarted, which affects the normal use of the workload.

.. |image1| image:: /_static/images/en-us_image_0000001930216052.png
.. |image2| image:: /_static/images/en-us_image_0000001256463368.png
.. |image3| image:: /_static/images/en-us_image_0000001200574170.png
