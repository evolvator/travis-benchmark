# travis-benchmark

Generate json results for [benchmark.js](https://github.com/bestiejs/benchmark.js).

[![NPM](https://img.shields.io/npm/v/travis-benchmark.svg)](https://www.npmjs.com/package/travis-benchmark)

## About

- Dont work outside the travis environment.
- Write results to `buildId.json` file of `process.env.RESULTS_BRANCH` branch in current or `process.env.RESULTS_REPO_SLUG` git repository. Create file if not exists. 

## Example

```js
var Benchmark = require('benchmark');
var tb = require('travis-benchmark');

var suite = new Benchmark.Suite('suiteName');
suite.add('benchmarkName', function() {})
.on('complete', function(event) {
  tb.saveSuite(
    tb.parseSuite(event),
    function(error) {}
  );
})
.run({ 'async': true });
```

## Environment

We recommended to configure this package from bash env. This will allow the js code to focus exclusively on tests.

- `RESULTS_AUTH` required, can be `token` or pair `login:password`
- `RESULTS_BRANCH` optional name of results branch, default value `results`
- `RESULTS_REPO_SLUG` optional repo in githab, default value is equal with `TRAVIS_REPO_SLUG`
- `RESULTS_REPO` optional custom git link, default value `https://github.com/${process.env.RESULTS_REPO}.git`

## Config

You can configure everything from js.

```js
tb.saveSuite(
  parsedSuite,
  function(error) {},
  {
    auth: 'token', // equal to RESULTS_AUTH
    branch: 'results', // equal to RESULTS_BRANCH
    repo_slug: 'user/repo', // equal to RESULTS_REPO_SLUG
    repo: 'http://github.com/user/repo.git', // equal to RESULTS_REPO
  }
));
```