:original_name: asm_api_0018.html

.. _asm_api_0018:

Error Codes
===========

If an API fails to be called, no service data will be returned. You can identify the cause based on the error code of each API. If an error occurs in API calling, HTTP status code 4\ *xx* or 5\ *xx* will be returned. The response body contains the specific error code and information.

Error Response Body Format
--------------------------

If an error occurs during API calling, an error code and a message will be displayed. The following shows an error response body.

.. code-block::

   {
       "errorMsg": Modify the request body based on the returned message and the ASM API documentation, or contact technical support.
       "errorCode": "ASM.01400001"
   }

In the preceding information, **error_code** indicates an error code, and **error_msg** describes the error.

Error Code Description
----------------------

.. table:: **Table 1** Error codes

   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Status Code | Error Code   | Error Message                      | Description                                | Troubleshooting                                                                                                    |
   +=============+==============+====================================+============================================+====================================================================================================================+
   | 400         | ASM.01400001 | Invalid request.                   | The request body is invalid.               | Modify the request body based on the returned message and the ASM API documentation, or contact technical support. |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | 401         | ASM.01401001 | Authorization failed.              | The authentication failed.                 | See the returned message or contact technical support.                                                             |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | 403         | ASM.01403001 | Forbidden.                         | The access is denied.                      | See the returned message or contact technical support.                                                             |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | 404         | ASM.01404001 | Resource not found.                | The resource is not found.                 | Check whether the resource to be accessed has been deleted.                                                        |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | 409         | ASM.01409001 | The resource already exists.       | The resource already exists.               | Delete the resource and try again.                                                                                 |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | 429         | ASM.01429001 | Resource locked by other requests. | The resource is locked by another request. | See the returned message or contact technical support.                                                             |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | 500         | ASM.01500001 | Internal error.                    | An internal error occurred.                | See the returned message or contact technical support.                                                             |
   +-------------+--------------+------------------------------------+--------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
