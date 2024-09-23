:original_name: asm_faq_0039.html

.. _asm_faq_0039:

What Can I Do If A Pod Cannot Be Started Due to Unready Sidecar
===============================================================

Description
-----------

Pods of services managed by a mesh may fail to be started and keep restarting. When the service container communicates with external systems, the traffic passes through the **istio-proxy** container. However, the service container is started earlier than the **istio-proxy** container. As a result, the communication with external systems fails and the pod keeps restarting.

Solution
--------

In Istio 1.7 and later versions, the community adds a switch named **HoldApplicationUntilProxyStarts** to the **istio-injector** injection logic. After the switch is enabled, the proxy is injected to the first container and the **istio-proxy** container is started earlier than the service container.

The switch can be configured globally or locally. The following describes two ways to enable the switch.

.. important::

   After this switch is enabled, the service container cannot be started until the sidecar is fully ready, which slows down pod startup and reduces scalability for burst traffic. You are advised to evaluate service scenarios and enable this switch only for required services.

-  **Global Configuration**

   #. Run the following command to edit the IOP CR resource:

      **kubectl edit iop private-data-plane -n istio-system**

      Add the following command to the **spec.values.global.proxy** field:

      .. code-block::

         holdApplicationUntilProxyStarts: true

      |image1|

   #. Run the following command to check whether the latest logs contain no error information:

      **kubectl logs -n istio-operator $(kubectl get po -n istio-operator \| awk '{print $1}' \| grep -v NAME)**

   #. Run the following command to check whether the IOP CR is normal:

      **kubectl get iop -n istio-system**

      |image2|

   #. Run the following command to upgrade the services in the mesh in a rolling manner:

      **kubectl rollout restart deployment** *nginx* **-n** *default*

      where, **nginx** is an example service, and **default** is the namespace. Replace them with the actual values.

   #. Run the following command to check whether the pod is restarted:

      **kubectl get pod -n** *default* **\| grep** *nginx*

      |image3|

   #. Run the following command to check whether **postStart lifecycle** is added to the pod and whether the **istio-proxy** container is placed in the first position:

      **kubectl edit pod** *nginx-7bc96f87b9-l4dbl*

      |image4|

-  **Local Configuration**

   For Istio 1.8 or later versions, you can label the pods for which this function needs to be enabled with **proxy.istio.io/config** and set **holdApplicationUntilProxyStarts** to true.

   The following uses the **nginx** service in the **default** namespace as an example. The operations for other services are similar.

   **kubectl edit deploy** *nginx* **-n** *default*

   Add the following commands to the **spec.template.metadata.annotations** field:

   .. code-block::

      proxy.istio.io/config: |
        holdApplicationUntilProxyStarts: true

   |image5|

.. |image1| image:: /_static/images/en-us_image_0000001416062808.png
.. |image2| image:: /_static/images/en-us_image_0000001416224808.png
.. |image3| image:: /_static/images/en-us_image_0000001416065480.png
.. |image4| image:: /_static/images/en-us_image_0000001466625829.png
.. |image5| image:: /_static/images/en-us_image_0000001416387696.png
