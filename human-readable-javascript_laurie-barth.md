# Human Readable JavaScript
## Laurie Barth
- @laurieontech
- Wrote "The Layers of JavaScript" on dev.to

## Notes
* I missed the first 10 minutes of this presentation because I left one that someone didn't show up to

### tl;dr JavaScript is hard to read
- a bunch of examples

### But not all JavaScript!

### Things have changed!
- You can make a full-stack JavaScript application because Node exists now! It is a standalone language

### Save JavaScript
- Not every brand new thing is the best thing ever simply because it is shiny

### Book recommendation
- Simplifying JavaScript by Joe Morgan

### ES2015+ is also known as ES6
- introduced a bunch of things that are considered essential for JavaScript now
- destructuring, JavaScript modules, spread operator, array methods, etc

### Live coding examples
- example of array.map
```javascript
let arr = [1,2,3,4];

// multiple examples:
let mapped = arr.map(e => e * 2);
let mapped = arr.map((e) => e * 2);
let mapped = arr.map((e) => return e * 2);
let mapped = arr.map(function(e) { return e * 2 })

let byTwo = function(e) { return e * 2; }
let mapped = arr.map(byTwo);
```

- Her opinion: An expert on a language is someone who can write vastly complex code in a language such that other people who write in different languages can understand what it is doing

- destructuring assignment example
```javascript
let arr = [1,2,3,4];

const first = arr[0];
console.log(first) // 1

const [first] = arr;
console.log(first) // 1

const [,,first] = arr;
console.log(first) // 3
```

  - part of readability is consistency. If you want to introduce a specific naming convention for dependencies, you can do that by aliasing imports.

- Spread operator. Why?
```javascript
let arr = [1,2,3,4];

let copy = [...arr];
console.log(copy) // [1, 2, 3, 4]

let merge = [...arr, ...copy];
console.log(merge); // [1, 2, 3, 4, 1, 2, 3, 4]

let merged = arr.concat(copy, copy); // what's wrong with this? Why is the spread operator better than this?

let obj = { key: 1 };
let copy = { ...obj, thing: 2, this: 3 };
console.log(copy); // { key: 1, thing: 2, this: 3 };
```

- New stuff
```javascript
// Array.flat
let arr = [1,2,[3,4, [5,6]]];

let flat = [].concat.apply(arr, [])
console.log(flat); // [1, 2, 3, 4, 5, 6]

let flat = arr.flat(1);
console.log(flat); // [1, 2, 3, 4, [5, 6]]

let flat = arr.flat(2);
console.log(flat); // [1, 2, 3, 4, 5, 6]

// map and flatmap
let arr = [1,2,3];
let mapped = arr.map(el => [el, el * 2]);
console.log(mapped); // [[1, 2], [2, 4], [3, 6]];

let flatMapped = arr.flatMap(el => [el, [el * 2]]);
console.log(flatMapped); // [1, 2, 2, 4, 3, 6]

// Object.entries
let obj = { a: 1, b: 2, c: 3 };
let arr = Object.entries(obj);
console.log(arr) [['a', 1], ['b', 2], ['c', 3]];

let mapped = arr.map(([key, value]) => return [key, value + 1]);
console.log(mapped); // [['a', 2], ['b', 3], ['c', 4]]
```

### Don't think that this means...
- Don't write 10 lines of code in every place that could've been two
- Simply make smart choices. Think about your audience and who is going to be looking at the code.

### More code examples for things that don't exist yet
- Null coalesce operator
```javascript
let obj = {
  thing: 0
};

let test = obj.thing || 2;
console.log(test); // 2 - we would want 2 to be the default when thing is null or undefined, not falsy.

let test = obj.thing ?? 2;
console.log(test); // 0;
```

- Optional chaining
```javascript
let obj = {
  thing: null
};

let test = obj.thing.that; // throws error: "Cannot read property 'that' of null"

let test = obj?.thing?.that ?? 2;
console.log(test); // 2
```

## Key Takeaways
- Just because you can do something in one line in a clever way doesn't mean you should. But the flipside is true too - you don't have to write 10 lines of code for something that can be done in two
- Use what makes sense for your audience. If you're writing code for NASA rockets, your code is probably going to look different than a CS student's Hello World!
- Just use common sense when writing code. No unnecessary abbreviations, no hard to read clever snippets, etc.
- Book recommendation: Simplifying Javascript by Joe Morgan