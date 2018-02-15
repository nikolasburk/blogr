# Blogr - A simple bloggin API

To learn more about this project, check out this [article](https://blog.graph.cool/tutorial-building-a-graphql-server-with-graphql-yoga-6da86f346e68).

## Usage

Clone repository and deploy Prisma service:

```sh
git clone git@github.com:nikolasburk/blogr.git
cd blogr
prisma deploy
```

When prompted where (i.e. to which _cluster_) you want to deploy your service, choose any of the development clusters, e.g. `public-us1` or `public-eu1`. (If you have Docker installed, you can also deploy locally.)

From the output of the previous command, copy the `HTTP` endpoint and paste it into `src/index.js` where it's used to instantiate the `Prisma` binding. You need to replace the current placeholder `__PRISMA_ENDPOINT__`:

```js
const server = new GraphQLServer({
  typeDefs: './src/schema.graphql',
  resolvers,
  context: req => ({
    ...req,
    db: new Prisma({
      typeDefs: 'src/generated/prisma.graphql',
      endpoint: '__PRISMA_ENDPOINT__',
      secret: 'mysecret123',
    }),
  }),
})
```

For example:

```js
const server = new GraphQLServer({
  typeDefs: './src/schema.graphql',
  resolvers,
  context: req => ({
    ...req,
    db: new Prisma({
      typeDefs: 'src/generated/prisma.graphql',
      endpoint: 'https://eu1.prisma.sh/public-hillcloak-flier-942261/hackernews-graphql-js/dev',
      secret: 'mysecret123',
    }),
  }),
})
```