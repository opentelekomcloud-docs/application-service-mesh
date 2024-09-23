:original_name: asm_bestpractice_0003.html

.. _asm_bestpractice_0003:

Upgrading Data Plane Sidecars Without Service Interruption
==========================================================

ASM enables you to manage the traffic of services added into a service mesh. Sidecars are important components in ASM data plane. The upgrade of sidecars involves the re-injection of sidecars into data plane service pods, which requires the pods to be updated.

This section describes how to avoid service interruption during sidecar upgrade.

Configuring the Number of Service Pods
--------------------------------------

Ensure that the number of service pods is greater than or equal to **2** and the upgrade policy is set to **RollingUpdate**.

Sample configurations:

**kubectl get deploy nginx -n** *namespace_name* **-oyaml \| grep strategy -a10**

|image1|

**Configuration description:**

-  Number of service pods: deployment.spec.replicas >= 2
-  Upgrade policy: deployment.spec.strategy.type == RollingUpdate
-  Minimum number of alive pods in rolling upgrade: deployment.spec.replicas - deployment.spec.strategy.maxUnavailable > 0

Adding a Readiness Probe
------------------------

Readiness probes help you ensure that new service pods take over traffic only when they are ready. This prevents access failures caused by unready new pods.

The configurations are as follows:

**kubectl get deploy nginx -n** *namespace_name* **-oyaml \| grep readinessProbe -a10**

|image2|

**Configuration description:**

Configuring a readiness probe: deployment.spec.template.spec.containers[i].readinessProbe

The configuration includes the initial check time, check interval, and timeout duration.

Setting the Service Ready Time
------------------------------

**minReadySeconds** is used to specify the minimum number of seconds for which a newly created pod should be ready without any of its containers crashing, for it to be considered available.

The configurations are as follows:

**kubectl get deploy nginx -n** *namespace_name* **-oyaml \| grep minReadySeconds -a1**

|image3|

**Configuration description:**

The service ready time: deployment.spec.minReadySeconds. Configure this parameter based on the live environment.

Configuring a Graceful Shutdown Time
------------------------------------

**terminationGracePeriodSeconds** is used to configure a graceful shutdown time. During a rolling upgrade, the endpoint of an old service pod is removed and the pod status is set to **Terminating**. A SIGTERM signal is then sent to the pod. After the graceful shutdown time you configured, the pod will be forcibly terminated. The graceful deletion time allows the pod to keep processing unfinished requests, if any, to avoid hard termination.

**kubectl get deploy nginx -n** *namespace_name* **-oyaml \| grep terminationGracePeriodSeconds -a1**

|image4|

**Configuration description:**

The graceful shutdown time: deployment.spec.template.spec.terminationGracePeriodSeconds. The default value is 30s. Configure this parameter based on the live environment.

Configuring the preStop
-----------------------

**preStop** enabled you to perform certain execution before a service pod is stopped. In this way, it helps you gracefully shut down a service pod. Configure this parameter based on service requirements. Nginx is used as an example here.

**kubectl get deploy nginx -n** *namespace_name* **-oyaml \| grep lifec -a10**

|image5|

In the **lifecycle.preStop** field, the **nginx -s quit; sleep 10** command is defined. This command first sends a graceful shutdown signal to the Nginx process and then the pod termination pauses for 10 seconds. In this way, Nginx has enough time to complete the ongoing requests and gracefully close the pod before it terminates.

**10** in **sleep 10** is an example value. You can change it based on the actual requirements and application performance. The key should be a proper value so that Nginx has enough time to gracefully shut down the process.

Alternatively, you can run custom commands or scripts to gracefully shut down your service process.

.. |image1| image:: /_static/images/en-us_image_0000001145684268.png
.. |image2| image:: /_static/images/en-us_image_0000001191764069.png
.. |image3| image:: /_static/images/en-us_image_0000001191923931.png
.. |image4| image:: /_static/images/en-us_image_0000001191923929.png
.. |image5| image:: /_static/images/en-us_image_0000001493677652.png
