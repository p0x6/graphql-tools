---
id: documents-loading
title: Loading GraphQL operation documents from different sources
sidebar_label: Documents loading
---

Similar to schema loading - but meant to use for GraphQL documents (query/mutation/subscription/fragment).

Any input provided as a source will be recognized by utils automatically.

It also extracts usages of `gql` from code files using [`@graphql-tools/graphql-tag-pluck`](/docs/graphql-tag-pluck).

## Usage

```ts
const { loadDocuments } = require('@graphql-tools/load');
const { GraphQLFileLoader } = require('@graphql-tools/graphql-file-loader');
const { CodeFileLoader } = require('@graphql-tools/code-file-loader');

const document1 = loadDocuments('query { f }'); // load from string

const document2 = loadDocuments('./users.query.graphql', {  // load from a single file
    loaders: [
        new GraphQLFileLoader()
    ]
});

const document3 = loadDocuments('./src/**/*.graphql', { // load from multiple files using glob
    loaders: [
        new GraphQLFileLoader()
    ]
});

const document4 = loadDocuments('./src/my-component.ts', {  // load from code file
    loaders: [
        new CodeFileLoader()
    ]
});


```

`loadDocuments` return an array of document sources and these source objects have the following structure;
```ts
interface DocumentSource {
  document: DocumentNode; // Object representation of GraphQL Content
  rawSDL: string; // SDL in text
  location: string; // Way to access to that source
}
```

> You can learn more about [loaders](/docs/loaders) to load documents from different sources.
