Javascript with graphql-request
=====================================

Install package "graphql" with :code:`npm install graphql --save`

Install package "graphql-request" with :code:`npm install graphql-request --save`

The following function takes in a pass template Id and creates a new pass.

.. code-block:: javascript

    const { GraphQLClient, gql } = require("graphql-request")
    const apikey = "YOUR API KEY HERE"
    const client = new GraphQLClient("https://api.passi.is/graphql", {
        headers: {
            "X-API-KEY": `${apikey}`
        },
    });

    async function createSmartPass(passTemplateId) {
        const variables = {
            data: {
                passTemplateId: passTemplateId,
                inputFieldValues: [
                    {
                        identifier: "name",
                        value: "John Smith"
                    }
            }
        }
        const mutation = gql`mutation UpsertPass($inputData: PassDataInput!) {
            upsertPass(data: $inputData) {
                distributionUrl
            }
        }`
        return await client.request(mutation, variables).catch((error) => console.error(error))
    }