# sitequery
*An impractical reactive framework for asynchronous web crawling.*

## Overview
`sitequery` is a [reactive](http://en.wikipedia.org/wiki/Reactive_programming) webcrawling framework that enables web crawling through server-side execution of [jQuery selectors](http://api.jquery.com/category/selectors/).

## npm install
[sudo] npm install sitequery

## Features
`sitequery` models web crawls as an infinite streams using the rx.js and jsdom.

  - Any valid jQuery selector can be executed across an entire website (or crawl sequence)
  - Crawls can be paramerized to only go *n* levels deep
  - Site crawls have use a redis store to track visitation and insure a crawl is cycle-free
  - Supports the latest jQuery version

## Crawling a website using SiteCrawl
*(From: /examples/hello-crawl.js)*

Allows you to crawl to a depth of *n* into a website

```javascript
var SiteCrawl = require('./lib/sitecrawl').SiteCrawl;

// create a new SiteCrawl of depth 2 with a delay of 1s between next page
// Note: Webcrawling is delayed and will not be executed
// until Subscription
var siteCrawl = new SiteCrawl(query.url, query.depth, 1000);

// ask for the observable sequence and subscribe for the CrawlResult(s)
siteCrawl.toObservable().Subscribe(function(crawlResult) {                 
  console.log(crawlResult.body);
},
// on err
function(exn){
},
// on crawl complete
function(){
console.log('SiteCrawl complete');
});
```


