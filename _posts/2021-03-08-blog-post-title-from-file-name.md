# What is Salesforce GraphQL API

The Salesforce GraphQL API introduces a novel approach to data exchange, allowing clients to precisely specify the fields they need in the response. This addresses the common challenges associated with traditional REST APIs, such as under fetching (receiving insufficient data) and over fetching (receiving more data than necessary).

This API allows developers to interact with the Salesforce platform through GraphQL, a new API standard that enables declarative data fetching where a client can specify exactly what data it needs from an API.

Instead of multiple endpoints that return fixed data structures, a GraphQL server only exposes a single endpoint and responds with precisely the data a client asked for.

## Benefits of GraphQL

**Better Performance**: Apps that call GraphQL are more performant than those that use traditional REST APIs. This is because they are able to reduce roundtrips to the server through retrieval of all needed data in one request.

**More efficient data fetching**: GraphQL allows you to specify exactly the data you need. This ensures you don't get more data than you need (overfetching) or you don't get less data than you need (underfetching).

**Strong Type system**: GraphQL relies on a strongly-typed schema, which serves as a contract between the client and server. This schema defines the types of data that can be queried, ensuring increased predictability in API interactions. By enforcing strict typing, GraphQL minimizes errors, such as attempting to access non-existent fields or deserializing data into mismatched types, providing a more robust and reliable development experience.

**More flexibility**: GraphQL is more flexible to interact with APIs. You can request data from multiple sources in a single query. This can be used for building complex applications.

## How to Query using GraphQL

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

The example above shows how to use GraphQL to query the Account object.

The query above is similar to the SOQL query `SELECT ID, NAME FROM ACCOUNT`.

Here are some of the keywords used in the above example and what they represent:

- `query` - This is used to indicate that this is a query operation.
- `uiapi` - This is used to indicate that we are using the Salesforce UIAPI to query Salesforce data. The UI API is a Salesforce API that provides access to the same data and functionality as the Salesforce user interface.
- The second `query` - This field is used to specify the SOQL query that we want to execute. The SOQL query in this case is `SELECT Id, Name FROM Account`. This query will retrieve all account records in Salesforce.
- `edges` field - This field contains the results of the query. Each edge contains a `node` field, which contains the data for each individual account record.
- `node` field - This field contains the data for each individual account record. In this case, the only fields that we are requesting are `Id` and `Name` fields.

## Response

The response to the query will be a JSON object that contains the data that was requested. The data will be nested in a `data` field, and the account data will be nested in a `uiapi` field.

Here is an example of a response to the query:

```json
{
  "data": {
    "uiapi": {
      "query": {
        "edges": [
          {
            "node": {
              "Id": "0010X0000074153AAE",
              "Name": {
                "value": "Acme Corporation"
              }
            }
          },
          {
            "node": {
              "Id": "0010X0000074154AAE",
              "Name": {
                "value": "XYZ Corporation"
              }
            }
          }
        ]
      }
    }
  }
}
```
