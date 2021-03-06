# ember-data-url-templates

[![Build Status](https://travis-ci.org/amiel/ember-data-url-templates.svg)](https://travis-ci.org/amiel/ember-data-url-templates)

ember-data-url-templates is an addon to allow building urls with url templates instead of
defining `buildURL` as described in [RFC #4](https://github.com/emberjs/rfcs/pull/4).

ember-data-url-templates is under early development. Feedback is welcome, and of course,
so are pull-requests.

Url templates are compiled with [geraintluff/uri-templates](https://github.com/geraintluff/uri-templates),
which fully implements [RFC 6570](http://tools.ietf.org/html/rfc6570).

## Usage

### Installation

```shell
ember install ember-data-url-templates
ember generate ember-data-url-templates
```

### Requirements

ember-data-url-templates makes use of a few features in ember-data
that are still in canary (1.0.0-beta.17+canary). Namely:

* findQuery passes query to `buildURL` (introduced in
  https://github.com/emberjs/data/commit/ab93c00571d62504cb997d3a7944aa430575856f)
* Pass requestType to `buildURL` (introduced in
  https://github.com/emberjs/data/commit/ff35ee78bfac058afb7a715a5dfc5760218cc05c)

### Synopsis

```javascript
// adapters/comment

import DS from "ember-data";
import UrlTemplates from "ember-data-url-templates";

extend default DS.RESTAdapter(UrlTemplates, {
  findUrlTemplate: '{+host}/comments/{id}',
  urlTemplate: '{+host}/posts/{postId}/comments{/id}'
});
```

### findQuery

The entire query from `findQuery` can be included in the url with `{?query*}`.

```javascript
findQueryUrlTemplate: '/posts{?query*}'
```

Or, selective keys from `findQuery` can be used in the url.

```javascript
findQueryUrlTemplate: '/blog/{category}{/year,month}'
```

## Contributing

### Installation

* `git clone` this repository
* `npm install`
* `bower install`

### Running Tests

* `ember test` or
* `ember test --server`

## TODO

Here is a short list of things I'd like to support:

* Optionally specify a template for each requestType
* Use a template provided by the API (like `links`)
* Use the query from `findQuery` to fill the template
