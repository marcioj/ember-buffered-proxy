# Ember-buffered-proxy [![Build Status](https://travis-ci.org/yapplabs/ember-buffered-proxy.svg)](https://travis-ci.org/yapplabs/ember-buffered-proxy)

An Ember Object Proxy (and mixin) the enables change buffering. Ever need to "hold back" property changes before they propogate? If so this may be the project for you.

## Usage

```sh
npm install --save-dev ember-buffered-proxy
```

```js
import BufferedProxy from 'ember-buffered-proxy/proxy';

var content = {
  firstName: 'stefan'
};

var buffer = BufferedProxy.create({
  content: content
});

buffer.get('firstName'); // => 'stefan'
buffer.set('firstName', 'Kris');

buffer.get('firstName'); // => 'Kris'
buffer.get('firstName.content'); // => 'stefan'

buffer.applyBufferedChanges();

buffer.get('firstName'); // => 'Kris'
buffer.get('firstName.content'); // => 'Kris'

buffer.set('firstName', 'Luke');
buffer.get('firstName'); // => 'Luke'
buffer.get('firstName.content'); // => 'Kris'

buffer.discardBufferedChanges();

buffer.get('firstName'); // => 'Kris'
buffer.get('firstName.content'); // => 'Kris'
```

Or you can grab the mixin directly

```js
import BufferedMixin from 'ember-buffered-proxy/mixin';

var content = {
  firstName: 'stefan'
};

var buffer = ObjectProxy.extend(BufferedMixin).create({
  content: content
});

// same as above
```


## development

## Installation

* `git clone` this repository
* `npm install`
* `bower install`

## Running

* `ember server`
* Visit your app at http://localhost:4200.

## Running Tests

* `ember test`
* `ember test --server`

## Building

* `ember build`

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
