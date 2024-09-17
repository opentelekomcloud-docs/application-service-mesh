:original_name: asm_01_0050.html

.. _asm_01_0050:

Configuring a Traffic Policy
============================

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane, choose **Service Management**. In the upper right corner of the list, select the namespace that your services belong to.

#. Locate the target service and click **Manage Traffic** in the **Operation** column. In the window that slides out from the right, configure retry, timeout, connection pool, outlier detection, load balancing, HTTP header, and fault injection policies.

   **Retry**

   Auto retries upon service access failures improve the access quality and success rate.

   On the **Retry** tab, click **Configure now**. In the displayed dialog box, set the parameters listed in the table below.

   .. table:: **Table 1** Retry parameters

      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter         | Description                                                                                                                                                                                                                                                                                                                 | Value Range   |
      +===================+=============================================================================================================================================================================================================================================================================================================================+===============+
      | Retries           | Maximum number of retries allowed for a single request. The default retry interval is 25 ms. The actual number of retries depends on the configured timeout period and retry timeout period.                                                                                                                                | 1-2147483647  |
      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Retry Timeout (s) | Timeout period of an initial or retry request. The default value is the same as the timeout period configured in the **Timeout** area below.                                                                                                                                                                                | 0.001-2592000 |
      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Retry Condition   | Configure retry conditions. For details, see `Retry Policies <https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/router_filter#x-envoy-retry-on>`__ and `gRPC Retry Policies <https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/router_filter#x-envoy-retry-grpc-on>`__. | ``-``         |
      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   **Timeout**

   Auto processing and quickly failure return upon service access timeout eliminate resource locking and request freezing.

   On the **Timeout** tab, click **Configure now**. In the displayed dialog box, set the parameters listed in the table below.

   .. table:: **Table 2** Timeout parameters

      =========== ================================ =============
      Parameter   Description                      Value Range
      =========== ================================ =============
      Timeout (s) Timeout period for HTTP requests 0.001-2592000
      =========== ================================ =============

   **Connection Pool**

   Connections and requests that exceed the thresholds are cut off to protect target services. Connection pool settings are applied to each pod of the upstream service at the TCP and HTTP levels. For details, see `Circuit Breaker <https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/circuit_breaking>`__.

   On the **Connection Pool** tab, click **Configure now**. In the displayed dialog box, set the parameters listed in the tables below.

   .. table:: **Table 3** Parameters under TCP Settings

      +---------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                       | Description                                                                                                                                                                               | Value Range   |
      +=================================+===========================================================================================================================================================================================+===============+
      | Maximum Number of Connections   | Maximum number of HTTP/TCP connections to the target service. The default value is **4294967295**.                                                                                        | 1-2147483647  |
      +---------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Maximum Number of Non-responses | Maximum number of keepalive probes to be sent before the connection is determined to be invalid. By default, the OS-level configuration is used. (The default value is **9** for Linux.)  | 1-2147483647  |
      +---------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Health Check Interval (s)       | Time interval between two keepalive probes. By default, the OS-level configuration is used. (The default value is **75** for Linux.)                                                      | 0.001-2592000 |
      +---------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Connection Timeout (s)          | TCP connection timeout period. The default value is **10**.                                                                                                                               | 0.001-2592000 |
      +---------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Minimum Idle Period (s)         | Duration in which a connection remains idle before a keepalive probe is sent. By default, the OS-level configuration is used. (The default value is **7200** for Linux, namely, 2 hours.) | 0.001-2592000 |
      +---------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   .. table:: **Table 4** Parameters under HTTP Settings

      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                                 | Description                                                                                                                                                                                                                | Value Range   |
      +===========================================+============================================================================================================================================================================================================================+===============+
      | Maximum Number of Requests                | Maximum number of requests that can be forwarded to a single service pod. The default value is **4294967295**.                                                                                                             | 1-2147483647  |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Maximum Number of Pending Requests        | Maximum number of HTTP requests that can be forwarded to the target service for processing. The default value is **4294967295**.                                                                                           | 1-2147483647  |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Maximum Connection Idle Period (s)        | Timeout period of an idle upstream service connection. If there is no active request within this time period, the connection will be closed. The default value is **3600** (1 hour).                                       | 0.001-2592000 |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Maximum Retries                           | Maximum number of retries of all service pods within a specified period. The default value is **4294967295**.                                                                                                              | 1-2147483647  |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Maximum Number of Requests Per Connection | Maximum number of requests for each connection to the backend. If this parameter is set to **1**, the keepalive function is disabled. The default value is **0**, indicating infinite. The maximum value is **536870912**. | 1-536870912   |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   **Outlier Detection**

   Unhealthy pods are automatically isolated to improve the overall access success rate.

   The traffic status of service pods is traced to determine whether the pods are healthy. Unhealthy pods will be ejected from the connection pool to improve the overall access success rate. Outlier detection can be configured for HTTP and TCP services. For HTTP services, pods that continuously return 5xx errors are considered unhealthy. For TCP services, pods whose connections time out or fail are considered unhealthy. For details, see `Outlier Detection <https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/outlier>`__.

   On the **Outlier Detection** tab, click **Configure now**. In the displayed dialog box, set the parameters listed in the table below.

   .. table:: **Table 5** Outlier detection parameters

      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                              | Description                                                                                                                                                                                                                                                 | Value Range   |
      +========================================+=============================================================================================================================================================================================================================================================+===============+
      | Consecutive Errors                     | Number of consecutive errors in a specified time period. If the number of consecutive errors exceeds the parameter value, the pod will be ejected. The default value is **5**.                                                                              | 1-2147483647  |
      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Base Ejection Time (s)                 | Base ejection time of a service pod that meets the outlier detection conditions. The actual ejection time of a service pod = Base ejection time x Number of ejection times. The value must be greater than or equal to 0.001s. The default value is **30**. | 0.001-2592000 |
      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Inspection Interval (s)                | If the number of errors reaches the threshold within this time period, the pod will be ejected. The value must be greater than or equal to 0.001s. The default value is **10**.                                                                             | 0.001-2592000 |
      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Maximum Percentage of Ejected Pods (%) | Maximum percentage of ejected service pods. The default value is **10**.                                                                                                                                                                                    | 1-100         |
      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   **Load Balancing**

   You can customize a load balancing policy to target backend service pods.

   On the **Load Balancing** tab, click **Configure now**. In the displayed dialog box, select one of the following load balancing algorithms as required:

   -  **Round robin**: The default load balancing algorithm. Each service pod in the pool gets a request in turn.

   -  **Least connection**: Requests are forwarded to the pod with fewer connections among two randomly selected healthy pods.

   -  **Random**: Requests are forwarded to a randomly selected healthy pod.

   -  **Consistent hashing**: There are four types, as described in :ref:`Table 6 <asm_01_0050__table1878918125557>`.

      .. _asm_01_0050__table1878918125557:

      .. table:: **Table 6** Consistent hashing algorithm types

         +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Type                     | Description                                                                                                                                           |
         +==========================+=======================================================================================================================================================+
         | Based on HTTP header     | The hash value is calculated using the header of the HTTP request. Requests with the same hash value are forwarded to the same pod.                   |
         +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Based on cookie          | The hash value is calculated using the cookie key name of the HTTP request. Requests with the same hash value are forwarded to the same pod.          |
         +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Based on source IP       | The hash value is calculated using the IP address of the HTTP request. Requests with the same hash value are forwarded to the same pod.               |
         +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Based on query parameter | The hash value is calculated using the query parameter key name of the HTTP request. Requests with the same hash value are forwarded to the same pod. |
         +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

   **HTTP Header**

   You can flexibly add, modify, and delete specified HTTP headers to manage request contents in non-intrusive mode.

   On the **HTTP Header** tab, click **Configure now**. In the displayed dialog box, set the parameters listed in the tables below.

   .. table:: **Table 7** Operations on the HTTP headers before the request is forwarded to the destination service

      +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter               | Description                                                                                                                          |
      +=========================+======================================================================================================================================+
      | Add request headers.    | To add a request header, you need to set **key** and **value**. You can also click |image4| to add more request headers.             |
      +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
      | Edit request headers.   | To edit an existing request header, you need to set **key** and **value**. You can also click |image5| to edit more request headers. |
      +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
      | Remove request headers. | To remove an existing request header, you need to set **key**. You can also click |image6| to remove more request headers.           |
      +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------+

   .. table:: **Table 8** Operations on the HTTP headers before the response is returned to the client

      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                | Description                                                                                                                             |
      +==========================+=========================================================================================================================================+
      | Add response headers.    | To add a response header, you need to set **key** and **value**. You can also click |image10| to add more response headers.             |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
      | Edit response headers.   | To edit an existing response header, you need to set **key** and **value**. You can also click |image11| to edit more response headers. |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
      | Remove response headers. | To remove an existing response header, you need to set **key**. You can also click |image12| to remove more response headers.           |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

   **Fault Injection**

   You can inject faults into the system to check whether it can tolerate and recover from faults.

   On the **Fault Injection** tab, click **Configure now**. In the displayed dialog box, set the parameters listed in the table below.

   .. table:: **Table 9** Fault injection parameters

      +-----------------------+-------------------------------------------------------------------------------------+-------------------------+
      | Parameter             | Description                                                                         | Value Range             |
      +=======================+=====================================================================================+=========================+
      | Fault Type            | The options are **Delay** and **Abort**.                                            | **Delay** and **Abort** |
      |                       |                                                                                     |                         |
      |                       | -  **Delay**: Service requests are delayed.                                         |                         |
      |                       | -  **Abort**: A service is aborted and the preset status code is returned.          |                         |
      +-----------------------+-------------------------------------------------------------------------------------+-------------------------+
      | Delay (s)             | This parameter needs to be set when **Fault Type** is set to **Delay**.             | 0.001-2592000           |
      |                       |                                                                                     |                         |
      |                       | A request will be delayed for this period of time before it is forwarded.           |                         |
      +-----------------------+-------------------------------------------------------------------------------------+-------------------------+
      | HTTP Status Code      | This parameter needs to be set when **Fault Type** is set to **Abort**.             | 200-599                 |
      |                       |                                                                                     |                         |
      |                       | HTTP status code returned when an abort fault occurs. The default value is **500**. |                         |
      +-----------------------+-------------------------------------------------------------------------------------+-------------------------+
      | Fault Percentage (%)  | Percentage of requests for which the delay or abort fault is injected.              | 1-100                   |
      +-----------------------+-------------------------------------------------------------------------------------+-------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001234454572.png
.. |image2| image:: /_static/images/en-us_image_0000001234773776.png
.. |image3| image:: /_static/images/en-us_image_0000001278854949.png
.. |image4| image:: /_static/images/en-us_image_0000001234454572.png
.. |image5| image:: /_static/images/en-us_image_0000001234773776.png
.. |image6| image:: /_static/images/en-us_image_0000001278854949.png
.. |image7| image:: /_static/images/en-us_image_0000001279134173.png
.. |image8| image:: /_static/images/en-us_image_0000001234614480.png
.. |image9| image:: /_static/images/en-us_image_0000001234294620.png
.. |image10| image:: /_static/images/en-us_image_0000001279134173.png
.. |image11| image:: /_static/images/en-us_image_0000001234614480.png
.. |image12| image:: /_static/images/en-us_image_0000001234294620.png
