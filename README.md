# ApartmentRental App
## Working with Relationships and Inheritance

### Description

In this application we have three main types of things we are dealing with.

* `Person`
* `Building`
* `Unit`


#### Person

With `Person` we have two main subtypes:

* `Manager`
* `Tenant`

Both `Manager` and `Tenant` should *inherit* methods from `Person`, and implement any extra behavior they need to play their role in the App.

##### Relationships

* `Manager` has many `buildings`
* `Tenant` has a many `references` that are just `Person` instances with contact info. 

#### Building

A `Building` should always have a `Manager` before `tenants` can move in. All `Tenants` should have `two` references before moving in.

##### Relationships

* `Building` has many `Unit`s.

#### `Unit`

* A `Unit` belongs to one `Building` and has one `Tenant`.

## Getting Started


### Run tests

in project folder, run:
	
	npm test
	
They should all fail! 

Your first assignment is is to make them all pass!


### Playing In Console

* Open the node REPL and `require('./src/app.js')`

```
$ node
> var app = require('./src/app.js')
```

* Create a few objects and inspect them.

```
> var person = app.Person();
> var building = app.Building();
> var manager = app.Manager();
```

not much here, the objects are *empty*.

============

* Next start implementing inheritance for a `manager`


You could do the following:

```
var person = require("./person");

function Manager(name, contact) {
  this.name = name;
  this.contact = contact;
  this.properties = [];
}

// Inheriting
Manager.prototype = new Person();
Manager.prototype.constructor = Manager;

```
But the following makes use of a cool `call` method you can use with functions that avoids a bunch extra work.

```
var person = require("./person");

function Manager(name, contact) {

  // Note here the use of "call"
  //  which will run the method 
  //  with a context.
  Person.call(this, name, contact);
  this.properties = [];
}

// Inheriting
Manager.prototype = new Person();
Manager.prototype.constructor = Manager;

```

* Note you might want to think about writing an `inherits` function as follows:

`src/inherits`

```
// write the following
var inherits = function(Child, Parent) {
  Child.prototype = new Parent();
  Child.prototype.constructor = Child;
};

module.exports = inherits;
```

you can then require the `inherits` module in each file that require inheritance.


## Writing AppartentRental app

We will use this as part of review opportunity for testing, so try to write as some tests for this project.

There are some `test` stubs for `test/people/`,  `test/property_types/`, and `test/unit.js`. To run these tests run the following in terminal.

* `mocha test/` to run the files in the `test/folder`, i.e. `unit_test.js` 
* `mocha test/people/` to test the `people` subfolder
* `mocha test/property_types/` to test the `property_types` subfolder


