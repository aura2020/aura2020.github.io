# What is Salesforce GraphQL API

The Salesforce GraphQL API introduces a novel approach to data exchange, allowing clients to precisely specify the fields they need in the response. This addresses the common challenges associated with traditional REST APIs, such as under fetching (receiving insufficient data) and over fetching (receiving more data than necessary).

This API allows developers to interact with the Salesforce platform through GraphQL, a new API standard that enables declarative data fetching where a client can specify exactly what data it needs from an API.

Instead of multiple endpoints that return fixed data structures, a GraphQL server only exposes a single endpoint and responds with precisely the data a client asked for.

## Benefits of GraphQL

- **Better Performance**: Apps that call GraphQL are more performant than those that use traditional REST APIs. This is because they are able to reduce round trips to the server through retrieval of all needed data in one request.
  
- **More Efficient Data Fetching**: GraphQL allows you to specify exactly the data you need. This ensures you don't get more data than you need (overfetching) or you don't get less data than you need (underfetching).
  
- **Strong Type System**: GraphQL relies on a strongly-typed schema, which serves as a contract between the client and server. This schema defines the types of data that can be queried, ensuring increased predictability in API interactions. By enforcing strict typing, GraphQL minimizes errors, such as attempting to access non-existent fields or deserializing data into mismatched types, providing a more robust and reliable development experience.
  
- **More Flexibility**: GraphQL is more flexible to interact with APIs. You can request data from multiple sources in a single query. This can be used for building complex applications.

## How to Query Using GraphQL

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
