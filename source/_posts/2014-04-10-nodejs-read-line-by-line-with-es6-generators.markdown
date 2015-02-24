---
layout: post
title: "Nodejs read line by line with ES6 generators"
date: 2014-04-10 00:07:55 +0200
comments: true
categories: ["javascript", "nodejs", "ecmascript-6"]
description: Nodejs read file line by line synchronously with ECMA-6 generators
---

For many languages it’s a simple operation no one even need to ask about it just read the docs, but in 
nodejs it’s a different story u have [SO question currently with 87 upvotes](http://stackoverflow.com/questions/6156501/read-a-file-one-line-at-a-time-in-node-js) 
& [many](https://github.com/nickewing/line-reader) [different](https://github.com/jahewson/node-byline) libraries to deal with it!

The problem is actually not with reading lines from small files as u can simply do

``` javascript
var fs = require('fs')

fs.readFile('test.txt', {encoding: 'utf8'}, function (err, data) {
    var lines = data.split('\n')

    console.info(lines)
})
```

Which load the whole file into memory but that won’t be efficient with large files, that’s the reason 
behind the question & many libs.

With ES6 becoming more and more common I decided to use a cool feature of it called generators to have 
a nice & clean solution. [here’s the gist](https://gist.github.com/Basemm/9700229)

>Please note that the script is sync, If you want async/lazy loading solution, have a look at [lazy.js](https://github.com/dtao/lazy.js)

How it’s used:

``` javascript
readLineSync = require('./readLineSync')

for(var line of readLineSync('test.txt')) {
    console.info(line)
}

//========================================
//or with while loop

file = readLineSync('test.txt')

next = file.next()

while(!next.done) {
    console.info(next.value)
    next = file.next()
}
```

After calling ‘readLineSync’ with the target file you are able to read lines by calling “file.next()” 
& process the line and when ready get next line or for simplicity use the generator with 
"for of" loop as in the first example 

Note that you need to use node >= 0.11 & run your script with flag "--harmony", ex:

```
node --harmony testscript
```

It benefit from generators feature that allow saving function state between “.next()” calls, 
allowing the function to keep track of current position in the file.

**So when to use it** 

As it run synchronously it won't be of great benefit for public websites as it won't benefit much 
from node main feature which is async calls "the main reason behind node speed". It could be used for ex in 
a script automating a task on your machine that it's operation depend on reading large files line by line to 
process it, so reading the file sync or async dosn't matter as you will be waiting/doing nothing in both cases
until the line is read to process it and you would have a clean code without async callbacks!


**Note** that it blocks execution only while getting a new line as we are not reading the whole file all 
at once also not all calls to “next()” would need disk access due to use of a buffer.
