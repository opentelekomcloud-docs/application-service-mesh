:original_name: asm_faq_0007.html

.. _asm_faq_0007:

Why Can't I Change the Image Used for the Grayscale Version When Performing Grayscale Release?
==============================================================================================

Description
-----------

When I perform grayscale release, the image used for the grayscale version cannot be changed.

Analysis
--------

When performing grayscale release on a service, you create a new version of the same service. Therefore, the image used by the service cannot be changed. Only image tags can be changed.

Solution
--------

Pack the required image into a different tag of the same image and push it to the image repository. Then, select the newly pushed image tag when you perform grayscale release on the service.
