# Blogr - A simple blogging API

To learn more about this project, check out this [article](https://blog.graph.cool/tutorial-building-a-graphql-server-with-graphql-yoga-6da86f346e68).

## Usage

### 1. Clone repository & deploy Prisma service

```sh
git clone git@github.com:nikolasburk/blogr.git
cd blogr
prisma deploy
```

When prompted where (i.e. to which _Prisma server_) you want to deploy your service, select the **Demo server**. For all subsequent questions you can simply choose the suggested values by hitting **Enter**. (Note that if you have Docker installed, you can also deploy locally.)

### 2. Set Prisma endpoint

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
      endpoint: 'https://eu1.prisma.sh/jane-doe/database/dev',
    }),
  }),
})
```

### 3. Start the server

Now, you can start the server:

```sh
node src/index.js
```

For more info, see [here](https://blog.graph.cool/tutorial-building-a-graphql-server-with-graphql-yoga-6da86f346e68).
