:original_name: asm_productdesc_0006.html

.. _asm_productdesc_0006:

Recommended Node Specifications
===============================

Recommended Specifications for Exclusive Nodes:
-----------------------------------------------

The performance of ASM is closely related to the cluster control plane (master nodes). Select appropriate node specifications based on your service requirements.

+---------------------------------+--------------------------+---------------------------+
| Total QPS (requests per second) | 0-20,000                 | 20,000-60,000             |
+---------------------------------+--------------------------+---------------------------+
| Specifications                  | 8 vCPUs and 16 GB memory | 16 vCPUs and 32 GB memory |
+---------------------------------+--------------------------+---------------------------+

.. note::

   -  The total QPS is the sum of requests of all services in all applications per second in a cluster.
   -  The function of recommending a proper amount of memory resources on the control plane based on the number of application service instances is coming soon.

ingressgateway Resource Consumption Reference
---------------------------------------------

The resource consumed by each ingressgateway pod is affected by the connection type, number of connections, and QPS. For details, see the following tables:

.. table:: **Table 1** Memory consumption of persistent connections

   =========== =================
   Connections Memory Usage (MB)
   =========== =================
   1           0.055
   1,000       55
   10,000      550
   =========== =================

.. table:: **Table 2** CPU and memory usage of short connections

   ====== ============= =================
   QPS    CPU Usage (m) Memory Usage (MB)
   ====== ============= =================
   100    30            100
   1,000  300           100
   10,000 3,000         150
   ====== ============= =================

The preceding data is for reference only. The actual resource consumption depends on the actual service model.
