ColdFusion Coding Style Guide
=============================

**Author:** Adam Presley
**Revisions:**

|Date        |Author           |Revision
|------------|-----------------|----------------------------------------------|
|2015-05-28  |Adam Presley     |Initial creation                              |


1. Whitespace and Formatting
----------------------------

### 1.1 Indentation
* Use hard tabs set to three (3) spaces.
* Do not mix tabs and spaces.

### 1.2 Line Length
* Line length *must not* exceed 120 characters
* Lines *should not* exceed 80 characters

### 1.3 Spaces
* Use spaces after commas in arguments lists
* *Do not use spaces* before commas in argument lists

**Good**
```cfm
public void function sayHi(string name, numeric age) output="false" {

}
```

**Bad**
```cfm
public void function sayHi(string name , numeric age) output="false" {

}
```

* *Do not use spaces* before or after parenthesis when defining and calling
   functions
* *Do* put a space between a parenthesis and **if**, **while**
* *Do* put a space after a closing parenthesis and an open curly brace

**Good**
```cfm
local.sum = add(left=1, right=2);
if (local.sum > 10) {
   // Do stuff
}
```

**Bad**
```cfm
local.sum = add ( left=1, right=2 );
if(local.sum > 10){
   // Do stuff
}
```

* *Do* use spaces between operators and operands in expresions

**Good**
```cfm
local.sum = 1 + 4 + local.somethingElse;
```

**Bad**
```cfm
local.sum = 1+4+local.somethingElse;
```

* *Do not* use spaces around equal signs when calling functions using named
   arguments
* *Do not* use spaces around equal signs when defining default values for
   arguments in function declarations

**Good**
```cfm
public string function doStuff(string name="Adam") output="false" {

}

local.result = doStuff(name="Bob");
```

**Bad**
```cfm
public string function doStuff(string name = "Adam") output="false" {

}

local.result = doStuff(name = "Bob");
```

### 1.4 Curly and Square Braces
* All open curly braces for function declarations, try/catch blocks, while,
   if, and structure variable declarations go on the same line as the
   statement/expression they are attached to
* All closing curly braces go on the next line
* Open curly braces for structures defined inside an array may start on their
   own line
* All open square braces go on the same line as the statement/expression they
   are attached to

**Good**
```cfm
if (isValid) {
   // Do stuff
}

try {
   // dangerous code
} catch {
   // log me!
}

local.claim = {
   id=1,
   token="12345",
   associated=[1, 2, 3],
   nonAssociated=[
      4,
      5,
      6
   ]
};

local.people = [
   {
      name: "Adam",
      age: 36
   }
];
```

**Bad**
```cfm
if (isValid)
{
   // Do stuff
}

try
{
   // dangerous code
}
catch
{
   // log me!
}

local.claim =
{
   id=1,
   token="12345",
   associated=
   [
      1,
      2,
      3
   ],
   nonAssociated=
   [4,5,6]
};

local.people =
[{
   name: "Adam",
   age: 36
}];
```


2. Casing and Naming
--------------------

### Casing Definitions
* Lower case - All digits are lower cased. Example: ```mynamehere```
* Upper case - All digits are upper cased. Example: ```MYNAMEHERE```
* Pascal case - First letter of each word upper cased, starting with an upper
   case letter. Example: ```MyNameHere```
* Camel case - First letter of each word upper cased, starting with a lower
   case letter. Example: ```myNameHere```

### Variable Names
* All variable names *must be* in camel case

**Good**
```cfm
local.payPeriod = "Bi-weekly";
local.allCustomerSettings = [];
```

**Bad**
```cfm
local.PayPeriod = "Bi-weekly";
local.allcustomersettings = [];
```
