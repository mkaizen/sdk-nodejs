[![Build Status](https://travis-ci.org/PopSugar/shopstyle-sdk-nodejs.svg?branch=master)](https://travis-ci.org/PopSugar/shopstyle-sdk-nodejs)
[![codecov](https://codecov.io/gh/PopSugar/shopstyle-sdk-nodejs/branch/master/graph/badge.svg)](https://codecov.io/gh/PopSugar/shopstyle-sdk-nodejs)

# shopstyle-sdk-nodejs

A lightweight, caching wrapper for the ShopStyle API.

```
npm install -S shopstyle-sdk
```


To use:
```
const ShopStyle = require('shopstyle-sdk');
const ss = new ShopStyle('test');
ss.product(359131344).then(result => console.log(response.name));

> Matthew Williamson Jungle Whispers Gown

// passing arguments to the api
const options = {
  fts: 'red dress',
  offset: 2,
  limit: 1,
  fl: ['b171', 'b28080', 'c7', 'd0', 'p31:40', 's85', 's87', 's89', 't0'],
  sort: 'PriceLoHi',
};
ss.products(options).then(response => console.log(response));

> { metadata:
   { offset: 2,
     limit: 1,
     total: 4,
     category:
      { id: 'dresses',
        name: 'Dresses',
        shortName: 'Dresses',
...
```

Caching:
```
// override the default 12 hour cache to a one hour cache:
const ss = new ShopStyle('test', 'US', { stdTTL: 3600});
// disable the cache
const ss = new ShopStyle('test', 'US', false);
```

Selecting a locale:
```
const ss = new ShopStyle('test', 'JP');
ss.categories({ depth: 1 }).then(result => console.log(result.categories[0].name));

> レディース　ファッション
```

The sdk default to the US locale. You can instantiate the ShopStyle object with another supported locale.
See the official ShopsStyle [API documentation](https://www.shopstylecollective.com/api/overview) for details on using the API.




## Caching:
shopstyle-sdk uses [node-cache](https://www.npmjs.com/package/node-cache) to cache results from the api.  The default ttl is twelve hours.  All options for configuring the cache can be passed through to node-cache.  The cache can also be disabled by passing ``false`` as the cache options during construction of the ShopStyle object.

## Supported Locales:
The locale can be selected when constructing the ShopStyle object.  The following locales are supported:
- Australia (AU)
- Canada (CA)
- France (FR)
- Germany (DE)
- Japan (JP)
- United Kingdom (UK)
- United States (US)

## Node Support:
This library uses features of node 6+.  For support on older versions see [Shopsense API nodejs client](https://www.npmjs.com/package/shopsense)

