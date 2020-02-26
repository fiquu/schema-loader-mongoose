# @fiquu/schema-loader-mongoose

[![Build Status](https://travis-ci.org/fiquu/schema-loader-mongoose.svg?branch=master)](https://travis-ci.org/fiquu/schema-loader-mongoose)
![GitHub](https://img.shields.io/github/license/fiquu/schema-loader-mongoose)
![GitHub last commit](https://img.shields.io/github/last-commit/fiquu/schema-loader-mongoose)
![npm (scoped)](https://img.shields.io/npm/v/@fiquu/schema-loader-mongoose)
![npm](https://img.shields.io/npm/dw/@fiquu/schema-loader-mongoose)

Schema loader for Mongoose connections.

## Installation

```sh
npm i @fiquu/schema-loader-mongoose
```

## Usage

Use it to load your schemas into any Mongoose connection.

`./configs/schemas.ts`:
```ts
import { SchemasMap, SchemaLoaderOptions } from '@fiquu/schema-loader-mongoose';

// You could move the schema map to another sub-module...
import profile from '../schemas/profile';
import user from '../schemas/user';

const schemas: SchemasMap = new Map();

schemas.set('profile', profile);
schemas.set('user', user);

const options: SchemaLoaderOptions = {
  replace: false,
  clone: true
};

export default {
  schemas,
  options
}
```

`./components/schemas.ts`:
```ts
import { createSchemaLoader, SchemaLoader } from '@fiquu/schema-loader-mongoose';
import { Connection } from 'mongoose';

import { options, schemas } from '../configs/schemas';
import db from '../components/database';

const conn: Connection = db.connection('default');
const loader: SchemaLoader = createSchemaLoader(conn, options);

loader.loadAll(schemas);

export default loader;
```

## Documentation

Please visit https://fiquu.github.io/schema-loader-mongoose/ for more info and options.
