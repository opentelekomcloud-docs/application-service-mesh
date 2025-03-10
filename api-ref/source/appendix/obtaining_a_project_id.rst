:original_name: asm_api_0019.html

.. _asm_api_0019:

Obtaining a Project ID
======================

Obtaining a Project ID by Calling an API
----------------------------------------

A project ID can be obtained by calling a specific API. For details, see `Querying Project Information Based on the Specified Criteria <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845625.html>`__.

The API used to obtain a project ID is **GET https://**\ *{Endpoint}*\ **/v3/projects/**, where *{Endpoint}* indicates the IAM endpoint. You can obtain the IAM endpoint from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.

In the following example, **id** indicates the project ID.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "eu-de",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }

Obtaining a Project ID from the Console
---------------------------------------

A project ID is required for some URLs when an API is called. To obtain a project ID, perform the following operations:

#. Log in to the management console.
#. Click the username and select **My Credentials** from the drop-down list. On the **API Credentials** page, view the project ID in the project list.

If a project contains multiple sub-projects, click the plus (+) sign to view sub-project IDs.
