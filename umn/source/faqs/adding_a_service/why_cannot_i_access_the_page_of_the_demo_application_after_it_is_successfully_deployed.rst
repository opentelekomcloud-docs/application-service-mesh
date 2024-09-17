:original_name: asm_faq_0005.html

.. _asm_faq_0005:

Why Cannot I Access the page of the Demo Application After It Is Successfully Deployed?
=======================================================================================

Symptom
-------

The page of the demo application cannot be accessed after the application is successfully deployed.

Analysis
--------

The load balancer configured for the application does not listen to the port.

Solution
--------

Log in to the Elastic Load Balance console. Check whether the port listener has been created and whether the health status of the backend server is normal.
