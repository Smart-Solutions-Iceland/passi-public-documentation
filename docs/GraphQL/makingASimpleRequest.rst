Making a simple request
============================

This guide is intended to give an example on how to make your first query and mutation on the platform. We will use the provided playground on `api.passi.is/playground <https://api.passi.is/playground>`_ to try our the requests to the graphQL server.

We will assume that you have already have made your first pass template and wish to add new passes to it. We will also use the cookie provided from the UI to make the test request but there will be an example on how to use the api key in code examples. To generate a cookie to use, simply log on to `passi.is <https://passi.is>`_.

What we first want to do is get the Id of the passtemplate we want to create the new pass with. To do this we will query the passTemplates to get a list of the passtemplates we have. 

Because the list is paged, the data we are looking for will be returned under data. We only really need to find the Id here but because we might need something to distinguish between the templates if we have multiple, so we fetch the name as well.

.. code-block::

    query passTemplateQuery {
        passTemplates {
            data {
                id
                name
            }
        }
    }


*Note that passtemplates accept a option of specifying how many results we get per page, but we will leave it at the default for this example.*

When you have written the query into the playground you can hit the play button to execute the query. This should give us a reply which looks something like this.

.. code-block:: json

    {
        "data": {
            "passTemplates": {
                "data": [
                    {
                        "id": "d9d42dfa-6d58-4b2a-f173-85ec9100f077",
                        "name": "VIP club membership"
                    },
                    {
                        "id": "247851ef-88a6-4004-9312-1e0a2c3b94de",
                        "name": "no descirption test hehe"
                    }
                ]
            }
        }
    }

From there we can grab the ID we need and start creating passes.

To create a pass we have to use the upsertPass mutation and pass in the id as a parameter. To do this we write the following query.

.. code-block::

    mutation UpsertPass($inputData: PassDataInput!) {
        upsertPass(data: $inputData) {
            distributionUrl
        }
    }

But we also have to fill in the query variables below to pass in the variables to go on with it. The variables should be in json format.

We name the variable "inputData" to reference the variable $inputData that we stated in the query above. In the query we set inputData to be of the type PassDataInput which is a argument for the UpsertPass mutation. That means that here we can pass in any data here that exists in the PassDataInput type, for example you would add the custom inputValues here.

.. code-block:: json
    
    {
        "inputData":{
            "passTemplateId":"e5ad18f5-928d-40ce-8773-c0aaa4d27589"
        }
    }

*Note that when upserting a pass, passTemplateId is a required argument*

Go ahead and execute the query we just wrote. This should return to us the following results:

.. code-block:: json

    {
        "data": {
            "upsertPass": {
                "distributionUrl": "https://api.passi.is/distribution/pass/7f523440f-4436-4ab1-af7e-d30564b366e5/8029e3b7-8a5a-4d41-950f-6432b484af79"
            }
        }
    }

Now that we have created a new pass we have been returned the freshly generated distributionUrl. This URL contains the download links for the pass we just created.

In a more practical environment you would not want to open up the playground to run the tests but instead run them directly via code. We highly recommend that you find a graphQL client library that fits your platform to make things easier. We'll provide a few :ref:`code examples <Code examples>` to get you started.

