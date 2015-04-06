# test-driven-nodejs-development
test-driven-nodejs-development
**Table of Contents**
- [Introduction To Mocha](#Introduction-To-Mocha)
  - [Installation](#installation)
    - [NPM Install (npm)](#npm-install)
  - [Starting with mocha](#starting-with-mocha)
  
#Introduction To Mocha#
Mocha is a Javascript testing framework, which runs on nodejs and browser. It is mostly use to test synchronous and asynchronous Javascript code. Easy to use and it's also provides you simple test case results.

##Installation##
This library is available on **npm**. Install with **npm**:

###NPM Install(npm)###
```bash
$ npm install -g mocha
```
Above command will install mocha globally to your npm environment.

##Starting with mocha##
When you work on TDD(Test Driven Development), You need to take care of your project structure. Where you will put your test cases on all. I have basically created a test folder where i put all test cases.
```bash
$ mkdir test
```
Once you create a testing folder, Just create your first mocha test case. ie. **testing.js** It would be something like
```js
var assert = require("assert")
describe('String', function(){
    describe('#substring()', function(){
        it('should return -1 when the value is not present', function(){
            assert.equal(-1, 'True Developer!! Testing is hardest thing to do...'.indexOf('developer'));
        });
    });
});
```
Output would be:
String
    #substring()
      ✓ should return -1 when the value is not present

###Explaination of Previous Code###
**describe** is use to describe different level of block of your code. **it** is to specify the test case that you have created.

##Introduction to Assertion##
Mocha is very flexible to use any of the assertion library. If it throws error it will work with mocha. There are lots of assertion library available in cloud. I personally prefer shouldjs and chaijs. You can use native assertion module of node.

###Using NodeJs assert Module###
```js
var assert = require("assert");
describe('String', function(){
    describe('#substring()', function(){
        it('should return -1 when the value is not present', function(){
            assert.equal(-1, 'True Developer!! Testing is hardest thing to do...'.indexOf('developer'));
        });
    });
});
```
###Using ShouldJs###
```bash
$  npm install should --save-dev
```
```js
var should = require('should')
describe('Array', function(){
    describe('#indexOf()', function(){
        it('should return -1 when the value is not present', function(){
            [1,2,3].indexOf(5).should.equal(-1);
            [1,2,3].indexOf(0).should.equal(-1);
        })
    })
})
```

##Synchronous code Testing##
By default javascript environment is sync in nature(Not nodejs ;) ). When you don't callback to test cases, Mocha runs all test cases serially and sequentially.
```js
var should = require('should')
describe('Array', function () {
    describe('#indexOf()', function () {
        it('Test Case-1: should return -1 when the value is not present', function () {
            [1, 2, 3].indexOf(5).should.equal(-1);
            [1, 2, 3].indexOf(0).should.equal(-1);
        });
    });
});
describe('String', function () {
    describe('#substring()', function () {
        it('Test Case-2: should return -1 when the value is not present', function () {
            'True Developer!! Testing is hardest thing to do...'.indexOf('developer').should.equal(-1);
        });
    });
});
```
##ASynchronous code Testing##
Development environment like nodejs, is async in nature. Mocha provides you such design pattern where you can define callback function. Call it when you done with it.
```js
var should = require('should')
describe('Array', function () {
    describe('#indexOf()', function () {
        it('Test Case-1: should return -1 when the value is not present', function (done) {
            setTimeout(function () {
                [1, 2, 3].indexOf(5).should.equal(-1);
                [1, 2, 3].indexOf(0).should.equal(-1);
                done();
            }, 1000)
        });
    });
});
describe('String', function () {
    describe('#substring()', function () {
        it('Test Case-2: should return -1 when the value is not present', function (done) {
            setTimeout(function () {
                'True Developer!! Testing is hardest thing to do...'.indexOf('developer').should.equal(-1);
                done();
            }, 500);
        });
    });
});
```