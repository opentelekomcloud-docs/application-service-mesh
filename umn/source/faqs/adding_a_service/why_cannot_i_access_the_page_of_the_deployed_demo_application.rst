:original_name: asm_faq_0005.html

.. _asm_faq_0005:

Why Cannot I Access the Page of the Deployed Demo Application?
==============================================================

Symptom
-------

The page of the deployed demo application cannot be accessed.

Analysis
--------

The load balancer configured for the application does not listen to the port.

Solution
--------

Log in to the Elastic Load Balance console. Check whether the port listener has been created and whether the health status of the backend server is normal.
