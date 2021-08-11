Generating new API keys
=============================

To generate a new API key navigate to the User settings page. You can find it by clicking your user in the top right corner of the page. When you are in the user setup page navigate to the API keys tab. 

To create a new API key click the *create new API key* button then go ahead, give it a descriptive name and hit save. You should now be forwarded to your new API key. Please keep your new API key a secret as it gives whomever has the key access to read and manipulate your data on the platform.

The API-key can be used instead of the user cookie to authenticate requests to the GraphQL server. To authenticate via the API key simply add a header to your request with the key as "X-API-KEY" and the value as your new API-key. With the header in place you should now be authorized to make requests.

Now that your API-key is ready. You can go ahead and checkout our guide on :ref:`how to write your first request <Making a simple request>` and get your feet wet in minutes.

Note: Currently API keys are published via users and they will inherit the same rights as the user has. This is subject to change in the future and the rights will have to be applied key level instead. When this happens the currently existing keys will inherit the user rights at the time of migration.

Second note: There are plans on the roadmap for a new type of 3rd party authentication method that enables better security than the API-Key provides. But a release date has not been decided on. The old key will not be made obsolete.