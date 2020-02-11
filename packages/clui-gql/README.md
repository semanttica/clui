# CLUI GraphQL

`@replit/clui-gql` is a small utility that transforms [GraphQL introspection](https://graphql.org/learn/introspection) data for a type into commands.


## Install

```sh
npm install @replit/clui-gql
```

## Usage

```js
import { toCommand } from '@replit/clui-gql';

const command = toCommand({
  // 'query' or 'mutation'
  operation: 'query',

  // GraphQL introspection data for type
  type: TypeInfo,

  // the path at wich the above type appears in the graph
  mountPath: ['cli', 'admin'],

  // Return a `run` function for given command
  runFn: (gqlOptions) => (runOptions) => doSomehtingWith({ gqlOptions, runOptions }),

  // Configure fields and fragments for GraphQL operation
  outputFn: () => ({
    fields: '...Output',
    fragments: `
      fragment Output on YourOutputTypes {
        ...on SuccessOutput {
          message
        }
        ...on ErrorOutput {
          error
        }
      }`,
  }),
});
```