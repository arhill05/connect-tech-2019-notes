# AHA Programming

## Avoid Hasty Abstractions - Being intentional and mindful

## Kent C. Dodds

- https://github.com/kentcdodds/aha-programming-slides
- kentcdodds.com
- @kentcdodds

* how many developers does it take to make microphones work correctly?

## What is AHA programming?

- similar concept to WET or DRY programming, AHA programming is just another one of these approaches

## What is this presentation?

- A live coded demonstration of the lifecycle of an abstraction

- Example:

```javascript
const phil = {
  name: { honorific: 'Dr.', first: 'Philip', last: 'Rodriquez' },
  username: 'philipr'
};

// navigation.js
// ...
const navDisplayName = `${phil.name.first} ${phil.name.lest}`;
console.log(navDisplayName);
// ...

// profile.js
// ...
const profileDisplayName = `${phil.name.first} ${phil.name.lest}`;
console.log(profileDisplayName);
// ...

// user-card.js
// ...
const cardDisplayName = `${phil.name.first} ${phil.name.lest}`;
console.log(cardDisplayName);
// ...
```

- The aboe example has `${phil.name.first} ${phil.name.lest}` duplicated and it also has a typo. The DRY principle says you should remove this duplication and put it into an abstraction. So let's fix it like that:

```javascript
function getDisplayName(user) {
  return `${user.name.first} ${user.name.last}`;
}

const phil = {
  name: { honorific: 'Dr.', first: 'Philip', last: 'Rodriquez' },
  username: 'philipr'
};

// navigation.js
// ...
const navDisplayName = getDisplayName(phil);
console.log(navDisplayName);
// ...

// profile.js
// ...
const profileDisplayName = getDisplayName(phil);
console.log(profileDisplayName);
// ...

// user-card.js
// ...
const cardDisplayName = getDisplayName(phil);
console.log(cardDisplayName);
// ...
```

- Now the project manager says "hey we need to make a change. We want to include "the honorable" in some cases. Great! Let's add it to the abstraction:

```javascript
function getDisplayName(user, { includeHonorific = false } = {}) {
  let displayName = `${user.name.first} ${user.name.last}`;
  if (includeHonorific) {
    displayName = `${user.honorific} ${displayName}`;
  }

  return displayName;
}

const phil = {
  name: { honorific: 'Dr.', first: 'Philip', last: 'Rodriquez' },
  username: 'philipr'
};

// navigation.js
// ...
const navDisplayName = getDisplayName(phil);
console.log(navDisplayName);
// ...

// profile.js
// ...
const profileDisplayName = getDisplayName(phil, { includeHonorific: true });
console.log(profileDisplayName);
// ...

// user-card.js
// ...
const cardDisplayName = getDisplayName(phil);
console.log(cardDisplayName);
// ...
```

- Now another change comes down that says "we want the user name to be in parenthesis on the user-card.js. Okay... add another thing to the abstraction And another use case, and another use case... you get the point. Example below

```javascript
function getDisplayName(
  user,
  {
    includeHonorific = false,
    includeUsername = false,
    firstInitial = false,
    onlyUsername = false
  } = {}
) {
  let first = user.name.first;
  if (firstInitial) {
    // get first initial
  }
  let displayName = `${user.name.first} ${user.name.last}`;
  if (includeHonorific) {
    displayName = `${user.honorific} ${displayName}`;
  }
  if (includeUsername) {
    displayName = `(${user.userName}) ${displayName}`;
  }
  if (onlyUsername) {
    return user.username;
  }

  return displayName;
}

const phil = {
  name: { honorific: 'Dr.', first: 'Philip', last: 'Rodriquez' },
  username: 'philipr'
};

// navigation.js
// ...
const navDisplayName = getDisplayName(phil);
console.log(navDisplayName);
// ...

// profile.js
// ...
const profileDisplayName = getDisplayName(phil, { includeHonorific: true });
console.log(profileDisplayName);
// ...

// user-card.js
// ...
const cardDisplayName = getDisplayName(phil, { onlyUsername: true });
console.log(cardDisplayName);
// ...
```

- And then add another... and another... you get the point. You'll get to the point that the abstraction no longer does the thing it was originally doing, defeating the purpose of the abstraction.
- When abstractions get so big, they almost demand that you use them. They get way too hairy to maintain and understand.
- What if you want to remove the Honorific? Okay, great - remove the option from the getDisplayName call. You're no longer using the honorific, but now you have completely unused code that no one knows about. The feature wasn't removed from the abstraction.
- Developers become afraid of removing things from this monstrous abstraction, so they tend to leave it like it is.

- Now what do we do?
- "The quickest way forward at this point is backwards." Remove the abstraction.
```javascript
const navDisplayName = `${phil.name.first.slice(0,1)}. ${phil.name.last}`;
console.log(navDisplayName);

const profileDisplayName = `${phil.name.first} ${phil.name.last}`
console.log(profileDisplayName);

const cardDisplayName = phil.username;
console.log(cardDisplayName);
```
- Don't fall victim to the sunk cost fallacy. The work has already been done, you are not losing work by undoing something you've already done.
- The abstraction is gone in the above code, but if it's absolutely necessary to add an abstraction for something (maybe the profileDisplayName case), do it, but **be careful** not to add a bunch of crazy functionality and features to the new abstraction.

## Takeaways
- DRY is not necessarily a bad thing. Thoughtless abstraction *is* a bad thing.
- You cannot predict the future: optimize for change
- Duplication is far cheaper than the wrong abstraction, so prefer duplication over the wrong abstraction - Sandi Metz
- Wait for the commonalities in duplicate code to scream at you for abstraction.
- If you have "Shared code" with lots of branches, then resist the urge to add more conditionals to it. Refactor it first.

