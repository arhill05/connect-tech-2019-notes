# Observables and Monadic Streams
- Powerful Composition: Building pipelines to tame complex data flows over time
## Jeff Barczewski
- @jeffbski
- jeff@codewinds.com
- https://codewinds.com/connect-rxjs-most
- Married, father, Catholic
- Developing for about 30 years
- Worked for USAF, RGA, MasterCard, etc.

## Notes
### Modern Developer Challenges
- events - inputs, environmental, IoT, etc.
- async I/O
  - Always talking to servers all over the world
- state
- concurrency
- cloud services - latency, concurrent limits, network failures
- dependencies
- cancellation

### What is an observable?
- Lazy push collection of multiple values
- It can emit 0 to N values and can be cancelled
- They are designed to do multiple events and cancellation whereas promises are not. Cancellation wasn't in the original spec, but they're trying to add it.

### RxJS demo in StackBlitz
 - Auto Search using RxJS AJAX with debouncing and cancellation: https://stackblitz.com/edit/react-pdjjaj
 - Drag and Drop using RxJS: https://stackblitz.com/edit/react-gaceaj

### Observable.create
- Tons of different ways to create observables. Observable.create lets you create one and have explicit control over the different pieces of the lifecycle.
- Many functions from rxjs to create observables from other things

### mergeMap, concatMap, switchMap
- Do something asynchronous and turn the result into another observable
- mergeMap - order of results is based on response that returns first
- concatMap - order is preserved, requests are started serially
- switchMap - only last request is delivered, previous is cancelled

### More live RxJS demos

### retryWhen
- Complete control over retry logic in RxJS pipes

### Most.js
- High performance reactive event stream programming that powers Most.js
- Differences from Observables
  - High performance, 2-100x faster depending on operations
  - Smaller feature set
  - Scheduler clock for app, time is passed with the event
  - Less popularity and contributers
  - runEffects and run vs subscribe

## Key Takeaways
- Observables and RxJS is very powerful and can do a ton of stuff with the functional style of programming
- Most.js can be more performant than RxJS
- This was just a bunch of code examples, I didn't really like this presentation.