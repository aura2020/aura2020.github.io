# How to Use Salesforce GraphQL API: `where`, `orderBy`, and `first` Clauses

Salesforce GraphQL API filters allow you to filter the results of your queries to return only the records that meet your specific criteria. This can be useful for reducing the amount of data that you need to process, or for finding specific records that you are looking for.

## Filter Operators

There are a number of different filter operators that you can use in Salesforce GraphQL API, including:

* `eq`: Equal to
* `ne`: Not equal to
* `gt`: Greater than
* `lt`: Less than
* `gte`: Greater than or equal to
* `lte`: Less than or equal to
* `in`: In a list of values
* `nin`: Not in a list of values
* `like`: Contains a string

You can also use Boolean operators such as `AND`, `OR`, and `NOT` to combine multiple filter criteria.

## How to Filter Results in Salesforce GraphQL API

To filter the results of your query, use the `where` argument. The `where` argument is an object that contains the filter criteria for your query.

### Example: Filtering Opportunities by Stage

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

The Salesforce object query language (SOQL) equivalent for the above query is:

```sql
SELECT Id,Name from opportunities where stageName = "Closed Won"
```

### Example: Filtering Opportunities by Related Account

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

The SOQL equivalent for the above query is:

```sql
SELECT Name, StageName FROM Opportunity WHERE Account.Name LIKE '%Edge%'
```

## Ordering Results in Salesforce GraphQL API

In addition to filtering the results of your query, you can also order the results and limit the number of results that are returned.

### Example: Ordering Opportunities by Close Date

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

The SOQL equivalent for the above query is:

```sql
SELECT Id, Name FROM Opportunity ORDER BY CloseDate ASC;
```

### Example: Limiting the Number of Results

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

The SOQL equivalent for the above query is:

```sql
SELECT Id , Name from opportunities limit 2
```

## Combining Multiple Filters, Order By Clauses, and First Clauses

You can also combine multiple filters, order by clauses, and first clauses in the same query.

### Example: Combining Multiple Filters and Order By Clauses

```graphql
query {
  uiapi {
    query {
      Opportunity(
        where: {
          StageName: { eq: "Closed Won" }
          Account: { Name: { like: "%Edge%" } }
        }

        orderBy: { CloseDate: { order: ASC } }

        first: 10
      ) {
        edges {
          node {
            Id

            Name {
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

The SOQL equivalent for the above query is:

```sql
SELECT Id,Name,CloseDate from opportunity where StageName = “closed Won” and Accoun.Name = %Edge% limit 10
```

## Exercise

Write a GraphQL query that will fetch 2 accounts whose name like “United”.

### Solution

```graphql
query {
  uiapi {
    query {
      Account(
        where: {
          Name: { like: "%United%" }
        }
        first: 2
      ) {
        edges {
          node {
            Id
            Name {
              value
            }
            Industry {
              value
            }
          }
        }
      }
    }
  }
}
```

The SOQL equivalent for the above query is:

```sql
Select Id,Name,Industry from Account where Name like '%United%' LIMIT 2
```
