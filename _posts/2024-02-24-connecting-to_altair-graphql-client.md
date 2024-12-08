# Connecting to Altair GraphQL client

Altair is a feature-rich open-source GraphQL client that allows developers to create and execute GraphQL queries.

Altair provides a number of useful features including pretty printing your query, linting your query, providing autocomplete functionality and enables access to schema documentation via introspection.

To query the API, you need the base URL and an API access token.

## Prerequisites

1. Salesforce Developer Edition
2. Install Altair GraphQL Client based on your operating system.

## How to obtain an access token

If you don't already have an access token, head over to the following url that describes how to get an access token for your org.

## Send a request from Altair GraphQL client

Now that you have your access token, you're ready to send a GraphQL API request to Salesforce:

1. Open the GraphQL client you installed.
2. Next to the POST option, enter your endpoint using the format `https://{MyDomainName}.my.salesforce.com/services/data/v{version}/graphql`, for example `https://myorg-dev-ed.my.salesforce.com/services/data/v57.0/graphql`.
3. Edit the HTTP headers:
   - Click the Set Headers icon (`⚙️`) on the sidebar. The Headers prompt appears.
   - For the Header key field, enter `Authorization`.
   - For the Header value field, enter the access token you generated in step 1. The format is `Bearer access_token`. For example, `Bearer 00DRM000000LnTv!AREAQN.therestofyourtokenhere`.
   - Click Save.
4. Back in the main client window, enter your query. You can use your own query or this example:

   ```graphql
   query accounts {
       uiapi {
            query {
                Account {
                    edges {
                        node {
                            Id
                             Name {
                                value
                            }
                        }
                    }
                }
            }
       }
   }
   ```
5. Click Send Request or the `▶️` icon to run the GraphQL query. Alternatively, you can press `Ctrl + Enter` (Windows) or `Cmd + Enter` (Mac).

## Explore GraphQL schema

To explore a GraphQL schema in Altair GraphQL client, follow these steps:

1. Click on the "Docs" tab in the left-hand sidebar to access the schema explorer.
2. The schema explorer displays the entire schema of the GraphQL API, including all types, fields, and their descriptions.
3. Click on any type or field to view its description and other relevant information.
4. Use the search bar to quickly find a specific type or field in the schema.
5. Use the "Explorer" tab to build and execute queries against the schema. The "Explorer" tab provides an autocomplete feature that suggests fields and arguments based on the schema, making it easier to write queries, it also also provides a preview of the query response, allowing you to inspect the data returned by the API.

Altair GraphQL client provides a user-friendly interface for exploring and interacting with GraphQL APIs. The schema explorer in Altair allows developers to quickly understand the structure of the API and its available data, making it easier to build queries and test the API.
