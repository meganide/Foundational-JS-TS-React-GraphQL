# GraphQL

## What is GraphQL?
GraphQL is a query language and a server-side runtime for APIs that allows clients to request the exact data they need.

GraphQL solves the problem of over- or under-fetching, we get exactly what we ask for.

## Mutations vs Queries
- **Mutation:** Used to write or change data
- **Query:** Used to read data

## GraphQL Schema
Describes the types of data that can be queried and mutated, the relationships between these types, and the queries and mutations that are available.
It acts as a contract that specifies what information the client may reuqest and how the server will respond.

## Scalar types
Basic data types that represent single values: 
- String
- Int
- Float
- Boolean
- ID

## Resolvers
A resolver is a function that executes when we perform a specific query or mutation, it provides code execution on how to compute or retrieve data from the database.

## When is GraphQL useful?
- Apps that require efficient and precise data retrieval
- When we have multiple clients with different data requirements. For example in a micro-service architecture.
- To avoid doing multiple requests to get the data, with GraphQL we can get all the data we need in one request
- When we want to avoid over or under fetching data.

## Introspection
In GraphQL, introspection is a built-in feature that lets you query the GraphQL server about its own schema — like asking, “What types, fields, and queries do you support?”

It's like asking for the menu at a restaurant, to see what's available.

### Why it’s useful
- Developer tools like GraphiQL or Apollo Studio use it to give autocomplete and schema docs.
- Lets you generate type definitions for TypeScript or codegen clients.
- Helps with API exploration without reading separate documentation.

## Error handling
Errors are returned in the response alongside the data. GraphQL doesn't use the traditional HTTP status codes.

## ✅ Pros of GraphQL

1. **Client decides the data shape**  
   - Request exactly the fields needed, avoiding over-fetching and under-fetching.

2. **Single endpoint**  
   - All operations go through one `/graphql` endpoint instead of multiple REST routes.

3. **Strongly typed schema**  
   - Schema defines all types and relationships, enabling autocomplete, validation, and better tooling.

4. **Introspection & self-documentation**  
   - The schema describes itself, allowing auto-generated docs and type definitions.

5. **Efficient for complex UIs**  
   - Fetch related data in one request instead of multiple REST calls.

6. **Great for evolving APIs**  
   - Add new fields without breaking existing clients.


## ❌ Cons of GraphQL

1. **More complex server setup**  
   - Requires schema, resolvers, and tooling, which is more work upfront.

2. **Overhead for simple APIs**  
   - Can be overkill for basic CRUD APIs with fixed responses.

3. **Caching is harder**  
   - Standard HTTP caching is less effective; often needs specialized solutions.

4. **Performance pitfalls**  
   - Large or deeply nested queries can slow down responses; needs cost analysis and limits.

5. **Learning curve**  
   - Requires learning schema design, resolvers, and query syntax.

6. **Batching & N+1 issues**  
   - Poor resolver design can cause many database calls; tools like DataLoader help.