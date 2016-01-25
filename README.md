dustjs-helpers-extra  [![Build Status][travis-image]][travis-url] [![NPM version][npm-image]][npm-url]
====================

Dust.js [official](https://github.com/linkedin/dustjs-helpers) plus extra helpers.

# Extra Helpers


## Iterate
Iterates trough the key value pairs of an object.


- key - required - iteratee
- sort - Optional. If omitted, no sort is done. Values allowed:
     - sort="asc" - sort ascending (per JavaScript array sort rules)
     - sort="desc" - sort descending
     - sort="fname" - Look for fname object in global context,
       if found, treat it as a JavaScript array sort compare function.
       if not found, result is undefined.

*Additional context variable: ``{$parentKey}`` gives the parent key in a nested iteration.*

#### Example
For the context:

```
{
    "day":"4",
    "month":1,
    "year" : 2016
}
```
This template:
```
{@iterate key=obj}
    {$key} - {$value} of type {$type} {~n}
{/iterate}
```
Will output 
```
day - 4 of type String 
month - 1 of type Number
year - 2016 of type Number
```
## Some
The Dust.js `some` helper checks whether in a given array keys and values exist.

```
{@some arr=myObj key="myKey" value="myValue"}{/some}
```

- arr - *required* - the array containing the objects to be iterated 

- key - *required* - the key in the object

- value - *optional* - the value of the key to be checked, defaults to an existance check if absent. 


#### Examples

For the context:

```
{
  myArr: [
    {"name": "Steve"},
    {"name": "Diego"}
  ]
}
```

template #1:

```
{@some arr=myArr key="name" value="Steve" }
block
{/some}
```

renders to:

```
block
```

and template #2:

```
{@some arr=myArr key="name" value="John" }
block
{/some}
```

renders to empty string.




## All 
All the objects contained in the array must have the key (value) specified.
```
{@all arr=myObj key="myKey"}{/all}
{@all arr=myObj key="myKey" value="myValue"}{/all}
```

- arr - *required* - the array containing the objects to be iterated 
- key - *required* - the key in the object
- value - *optional* - the value of the key to be checked, defaults to an existance check if absent. 

#### Examples
For the context:

```
{
  myArr: [
    {"name": "Steve"},
    {"name": "Steve"}
  ]
}
```

template #1:

```
{@all arr=myArr key="name" value="Steve"}
block
{/all}
```

renders to:

```
block
```

and template #2:

```
{@all arr=myArr key="name" value="John"}
block
{/all}
```

renders to empty string.


## Contains

The Dust.js contains helper checks whether in a given array keys and values exist.
It delegates internally to `all` and `some` helpers.

```
{@contains arr=myObj key="myKey" value="myValue" scope="once/all"}{/contains}
```

- arr - *required* - the array containing the objects to be iterated 
- key - *required* - the key in the object
- value - *optional* - the value of the key to be checked.
- scope [`once` or `all`] - *optional* - 
    - 'once' checks whether there is at least one element in the array has the given key and value.
    - 'all' checks whether all elements in the array have the given key and value.


#### Examples

For the context:

```
{
  myArr: [
    {"name": "Steve"},
    {"name": "Steve"}
  ]
}
```

template #1:

```
{@contains arr=myArr key="name" value="Steve" scope="all"}
block
{/contains}
```

renders to:

```
block
```

and template #2:

```
{@contains arr=myArr key="name" value="John" scope="all"}
block
{/contains}
```

renders to empty string.



# Install

```
npm install dustjs-helpers-extra
```

# Requirements

* dustjs-helpers: ^1.5.0

# Test

Run ``grunt test``.

# History
* 1.0.0 - major refactoring, added some and all helpers
* 0.4.0 - change GIT repository to https://github.com/nikolaygit/dustjs-helpers-extra
* 0.3.1 - add travis CI.
* 0.3.0 - upgrades npm dependency ``dustjs-helpers`` from ``~1.3.0`` to ``~1.5.0``. See the [braking changes](https://github.com/linkedin/dustjs-helpers/wiki/Deprecated-Features) for your dustjs templates.
* 0.2.0 - new ``{@contains}`` helper and tests.
* 0.1.0 - iterate: new context variable ``{$parentKey}`` and tests.


[travis-image]: https://travis-ci.org/deddu/dustjs-helpers-extra.svg?branch=master
[travis-url]: https://travis-ci.org/deddu/dustjs-helpers-extra
[npm-url]:  https://npmjs.org/package/dustjs-helpers-extra
[npm-image]: http://img.shields.io/npm/v/dustjs-helpers-extra.svg?style=flat
