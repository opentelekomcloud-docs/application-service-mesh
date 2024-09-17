:original_name: asm_bestpractice_3008.html

.. _asm_bestpractice_3008:

Service Discovery Model
=======================

Problems in the existing Dubbo model (summarized from the Dubbo community version 2.7.4):

-  In the microservice architecture, the Registry manages applications (services) instead of external service interfaces. However, the Dubbo Registry manages Dubbo service interfaces, contrary to the Spring Cloud or Cloud Native registration mode.
-  A Dubbo application (service) allows N Dubbo service interfaces to be registered. The more interfaces, the heavier the load of the Registry.

The existing Dubbo service model searches for service instances based on the Dubbo interface.

|image1|

The Dubbo Cloud Native service discovery model adds an app layer to search for instances.

|image2|

.. |image1| image:: /_static/images/en-us_image_0000001181759886.png
.. |image2| image:: /_static/images/en-us_image_0000001227360319.png
