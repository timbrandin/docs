---
title: Meteor integration
order: 112
description: Specifics about using Apollo in your Meteor application.
---

The Apollo client and server tools are published on NPM, which makes them available to all JavaScript applications, including those written with Meteor 1.3 and above. When using Meteor with Apollo, there are a few things to keep in mind to have a smooth integration between the client and server.

You can see all of these in action in the [Apollo Meteor starter kit](https://github.com/apollostack/meteor-starter-kit).

```
meteor add apollo
meteor npm add --save apollo-client apollo-server express
```

## Client

```js
import ApolloClient from 'apollo-client';
import { createMeteorNetworkInterface } from 'meteor/apollo';

const client = new ApolloClient({
  networkInterface: createMeteorNetworkInterface()
});
```

## Server

```js
import { createApolloServer } from 'meteor/apollo';

import schema from '/imports/api/schema';
import resolvers from '/imports/api/resolvers';

createApolloServer({
  graphiql: true,
  pretty: true,
  schema,
  resolvers,
});
```

Now, you can use `context.user` from your resolvers:

```js
user(root, args, context) {
  // Only return data if the fetched id matches the current user, for security
  if (context.user._id === args.id) {
    return context.user;
  }
}
```
