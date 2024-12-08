# How to use Salesforce GraphQL API: where, orderBy, and first clauses

Salesforce GraphQL API filters allow you to filter the results of your queries to return only the records that meet your specific criteria. This can be useful for reducing the amount of data that you need to process, or for finding specific records that you are looking for.

There are a number of different filter operators that you can use in Salesforce GraphQL API, including:

- `eq`: Equal to
- `ne`: Not equal to
- `gt`: Greater than
- `lt`: Less than
- `gte`: Greater than or equal to
- `lte`: Less than or equal to
- `in`: In a list of values
- `nin`: Not in a list of values
- `like`: Contains a string

You can also use Boolean operators such as `AND`, `OR`, and `NOT` to combine multiple filter criteria.

## How to filter results in Salesforce GraphQL API

To filter the results of your query, use the `where` argument. The `where` argument is an object that contains the filter criteria for your query.

For example, the following query filters the results to only include opportunities that are in the "Closed Won" stage:

```graphql
query closedwonopportunities {
  uiapi {
    query {
      opportunity(where: { StageName: { eq: "Closed Won" } }) {
        edges {
          node {
            Name {
              value
            }
            StageName {
              value
            }
          }
        }
      }
    }
  }
}
```

The Salesforce object query language (SOQL) equivalent for the above query is `SELECT Id,Name from opportunities where stageName = "Closed Won"`.

You can also use filters to filter related objects. For example, the following query filters the results to only include opportunities that have a related account with a name that contains the string "Edge":

```graphql
query edgeopportunities {
  uiapi {
    query {
      Opportunity(where: { Account: { Name: { like: "%Edge%" } } }) {
        edges {
          node {
            Name {
              value
            }
            StageName {
              value
            }
          }
        }
      }
    }
  }
}
```

The SOQL equivalent for the above query is: `SELECT Name, StageName FROM Opportunity WHERE Account.Name LIKE '%Edge%'`.

## Ordering results in Salesforce GraphQL API

In addition to filtering the results of your query, you can also order the results and limit the number of results that are returned.

To order the results of your query, use the `orderBy` argument. The `orderBy` argument is an array of objects that specify the fields to order by and the direction to order by.

For example, the following query orders the results by the `CloseDate` field in ascending order:

```graphql
query opportunities {
  uiapi {
    query {
      Opportunity(orderBy: { CloseDate: { order: ASC } }) {
        edges {
          node {
            Name {
              value
            }
            StageName {
              value
            }
            CloseDate {
              value
            }
          }
        }
      }
    }
  }
}
```

The SOQL equivalent for the above query is `SELECT Id, Name FROM Opportunity ORDER BY CloseDate ASC;`.

To limit the number of results that are returned, use the `first` argument. The `first` argument is an integer that specifies the number of results to return.

For example, the following query limits the results to the first 2 opportunities:

```graphql
query opportunities {
  uiapi {
    query {
      opportunity(first: 2) {
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

The SOQL equivalent for the above query is `SELECT Id , Name from opportunities limit 2`.

You can also combine multiple filters, order by clauses, and `first` clauses in the same query. For example, the following query filters the results to only include opportunities that are in the "Closed Won" stage and have a related account with a name that contains the string "Edge", and then orders the
