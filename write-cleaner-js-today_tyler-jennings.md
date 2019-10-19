# Write Cleaner JavaScript Today
## Tyler Jennings
- @jenningstcj
- Work for a consulting company called ResultStack that does anything and everything
- http://clean-js.tylerscode.com

## Notes
- Cognitive load
  - definition: The total amount of mental effort being used in the working memory
  - As developers, there are a lot of things that we have to hold in our head at any given time
  - A high cognitive load leads to mental fatigue. When you are really zeroed in on a certain problem, you become blind to some things that are staring you in the face
- "Always code as if the person maintaining your code is a violent psychopath that knows where you live."

### Maintenance programming
- The maintainer may not know the context the original code was written in
  - Why was the code written?
  - Under what circumstances?
  - What were the original use cases?
  - What was the original coder thinking at the time?
- The maintainer doesn't always have proper documentation to understand the original problem being solved
- The maintainer may only see people that have problems from the code
  - they only hear one side of the story
- Sometimes you are the maintainer and put yourself in this situation

### Writing cleaner code
- Descriptive code
- Shorter code
- Simple code
- ES2015+ concepts
- Function composition

### Code example time
- Array.map removes need to iterate over arrays manually
- Ternary operator makes if statements a bit easier to understand
- Template syntax lets you handle string concatenation in a much easier to read manner
- Arrow functions can turn functions into one liners
  - There's a gotcha here -  you must declare your function expressions before you use them. Hoisting doesn't work with function expressions
  - What if you want to console.log without adding curly brackets?
    - `const add = (num1, num2) => console.log(num1, num2) || num1 + num2;
      - console.log returns falsy, so it will log and then return the thing after the `or`
- Write functions that you call for collections for a single object instead to eliminate the necessity of complex logic inside map functions
- Destructuring lets you take an object and destructure it into new local variables with the same name
```javascript
const { firstName, lastName } = employee;
// is equivalent to
const firstName = employee.firstName;
const lastName = employee.lastName;
```

- You can combine destructuring with the spread operator
- You can use destructuring with arrays too.

- Minimize mapping
  - nest function calls to reduce the number of iterations

### Composition
Function composition is the ability to take a function that goes from A to B, and combine it with something that goes from B to C

### A few other techniques
- shorthand properties
- spread operator

### Object.assign vs spread operator
- Both do a shallow copy AND preserves the reference in memory. They reference the same exact thing
- Both use getters to read the data
- Spread defines new properties, but Object.assign sets them
  - Object.assign will try to use a setter if one exists

### Proposed pipe operator
- TC39 proposal has a pipe operator included in it
```javascript
const capitalize = str => str.toUpperCase();

const exclaim = str => `${str}!`;

const result = "hello"
  |> capitalize
  |> exclaim;

console.log(result); //=> HELLO!
```

## Key Takeaways
- ES6 is awesome and can provide many ways to make your javascript more readable
- functional programming helps a lot with this
- new proposal contains the pipe operator