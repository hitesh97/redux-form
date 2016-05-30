# `FieldArray`

The `FieldArray` component is how you render an array of fields. It works a lot like `Field`. 
With `Field`, you give a `name`, referring to the location of the field in the Redux state, and a 
`component` to render the field, which is given the props to connect the field to the Redux state.

With `FieldArray`, you provide a `name` just like with `Field`, but the `component` you give to 
`FieldArray` will be given a set of props to query, update, and iterate through the field array.

## Importing

```javascript
var FieldArray = require('redux-form').FieldArray;  // ES5
```
```javascript
import { FieldArray } from 'redux-form';  // ES6
```

## Props you can pass to `FieldArray`

#### `name : String` [required]

A string path, in dot-and-bracket notation, corresponding to a value in the form values. It may 
be as simple as `'firstName'` or as complicated as
`contact.billing.address[2].phones[1].areaCode`.

#### `component : Component|Function` [required]

A `Component` or stateless function to render the field array.

#### `withRef : boolean` [optional]

If `true`, the rendered component will be available with the `getRenderedComponent()` method.
Defaults to `false`. **Cannot be used if your component is a stateless function component.**

## Instance API

The following properties and methods are available on an instance of a `FieldArray` component.

#### `name : String`

> The `name` prop that you passed in.

#### `valid : boolean`

> `true` if this field passes validation, `false` otherwise.

#### `getRenderedComponent()`

> Returns the instance of the rendered component. For this to work, you must provide a 
`withRef` prop, and your component must not be a stateless function component.

## Props

These are props that `FieldArray` will pass to your wrapped component. As you can see, they are 
all under the `fields` key. Any additional props that you pass to `FieldArray` will be passed 
along, but will _not_ be under the `fields` key.

#### `fields.dirty : boolean`

> `true` if the any of the fields in the field array have changed from their initialized value. 
Opposite of `pristine`.

#### `fields.error : String` [optional]

> The error for this field array if its value is not passing validation. Both synchronous,
asynchronous, and submit validation errors will be reported here. Array-specific errors should be
returned from the validation function as an `_error` key on the array.

#### `fields.forEach(callback) : Function`

> A method to iterate over each value of the array. See the section on [Iteration](#iteration) 
for more details.

#### `fields.insert(index, value) : Function`

> A function to insert a new value into the array at any arbitrary index.

#### `fields.invalid : boolean`

> `true` if the field array value fails validation (has a validation error). Opposite of `valid`.

#### `fields.length : Number`

> The current length of the array.

#### `fields.map(callback) : Function`

> A method to iterate over each value of the array. Returns an array of the results of each call 
to the callback. See the section on [Iteration](#iteration) for more details.

#### `fields.pop() : Function`

> Removes an item from the end of the array. Returns the item removed.

#### `fields.pristine : boolean`

> `true` if the all of the fields in the field array are the same as their initialized 
value. Opposite of `dirty`.

#### `fields.push(value) : Function`

> Adds a value to the end of the array. Returns nothing.

#### `fields.remove(index) : Function`

> Removes an item from the array at an arbitrary index. Returns nothing.

#### `fields.shift() : Function`

> Removes an item from beginning of the array. Returns the item removed..

#### `fields.swap(indexA, indexB) : Function`

> Swaps two items in the array at the given indexes. Returns nothing.

#### `fields.unshift(value) : Function`

> Adds an item to the beginning of the array. Returns nothing.

#### `fields.valid : boolean`

> `true` if the field value passes validation (has no validation errors). Opposite of `invalid`.

## Iteration

When you iterate through a field array with either `forEach()` or `map()`, your callback will be 
passed two parameters:

#### `name : String`

> The name needed to give to `Field` to render the fields in this array. If the `name` prop you 
give to `FieldArray` is `'foo.bar'`, and there are three items in the array, your callback will 
be called three times, with `'foo.bar[0]'`, `'foo.bar[1]'`, and `'foo.bar[2]'`.

#### `index : Number`

> The index of the item in the array.