# Practical Unit Testing for Existing Codebases
## K. Devin McIntyre
- @kdevinmcintyre
- https://speakerdeck.com/miyasudokoro
-
- https://github.com/miyasudokobo/unit-test-demo

## Notes
- Every time I've started developing, I've been given an existing or legacy code base. My team is essentially a "clean-up" team.

### Overview
- Blocker: time
  - Urgency of feautures has left quality cut short
  - Team or individual process is too tightly scheduled
- Blocker: Practical knowledge
  - Poor/nonexistent training in unit testing
- Blocker: Existing Codebase
  - What should be prioritized
  - How to refactor safely
- Examples - based on a real untested app
- Blocker: team & management buy-in

### Time
- Example of a unit-test-free process
  - 1. Prototype/first draft
    - QA has nothing to do
  - 2. Trial and error
    - Trial: run the app
    - error: see a defect
    - code: fix the defect
  - 3. Confirmation/QA
    - QA finishes the automated system tests
    - Manual tests still exist but should be fewer
- Here's what to do instead:
  - 1. Prototype/first draft
    - QA *starts writing automated system tests*
  - 2. Trial and error
    - Trial: *Write some unit tests and run the full suite*
    - Error *test failure*
    - Code: *fix test failure*
  - 3. QA
    - QAs finish automated system tests

Why use Test-During?
  - Productivity increases beacuse unit tests are faster than manual runs
  - You gain experience in unit tests

Differences of Test-During vs Test-Driven?
  - Throw out the first draft code
  - Trial and error has much shorter increments
  - Trials write one unit test for mission functionality

Starting Test-Driven Development
1. Decide you want to. It's a design method, not a test method
2. Gain experience with unit testing bad practices
   1. Poorly written unit tests lock in the bad rather than uncovering it
3. Understand how unit tests and code reflect each other
4. Mentally prepare for continuous refactoring, redesign, and failure.
5. Try it with defects first

### Practical Knowledge
- Getting started
- Choosing a test framework
  - What are other people using for apps similar to yours?
    - Most frameworks hae one or more recommended setups
    - "Misuse" of framework features may make this difficult without refactoring
    -
- Unit tests in browsers? Maybe not
  - Tests can stop running due to browser updates
  - Node is faster due to browser startup time
  - Considerations:
    - Do you have good functional/system tests against the UI?
    - Does your code handle its own cross-browser support?
    - Did you roll your own UI framework?
  - If you want to do it, you may need to experiment with test frameworks
  ? How do you do UI testing if you don't test against the browser?

- Testing UI Code in Node
  - Mimic the UI environment with JSDOM
    - Pro: provides a fake DOM that is good enough
    - Pro: can load your UI files directly into mock windows
    - Con: not enough documentation
    - Con: too many outdated posts
  - Support Node natively, then convert files during build process
  - Use functional/system tests of UI to complete your test coverage

- What to Unit Test
  - Contracts of public functions
    - If X goes into function A, the output willn be Y
    - Given we are in X state, if we call function A, the state will change to Y
  - Logic branches
    - If-else, switch, try-catch
    - Various paths going through private methods
  - "Public" = functions called by code not defined in this file

- What NOT to unit test
  - Every possible combination of parameters, logic etc
  - Third-party anything
    - trust frameworks, API's dependencies, etc to handle themselves
  - Theoretical ways things could be used byt probably never will be
    - Do test boundary conditions
  - The "contracts" of a private method

- Structure
  - One "setup" file to set up global state
    - If you're in Node, set up the global Window object or something similar
  - One "spec" file per each source code file
  - One "describe" block per state of app
    - Complex states -> nested describes
  - One "it" block per call of a function under test
  - Assert/expect choices
    - One "assert/expect" statement per "it"
    - Use enough "assert/expect" statements to fully query the end state or output

- State control
  - Don't let state bleed between individual tests
  - Must restore to previous state after each "describe" or "it" finishes
  - Avoid pollution of global objects
  - Memory leaks will break your tests; you must truly discard everything

- Stubs and mocks
  - Mock: a whole object pretending to be another object
  - Stub/spy: temporarily replacing an object's method

- Schools of thought
  - London/Mockist
    - Should mock outside resources **and usually** your dependent modules that are inside your app
  - Detroit/classical
    - Should mock outside resources **but not** dependent modules

### Existing Codebase
- Use the London School
  - Isolation of files lets you work on one thing at a time
  - Easier to control state
  - No need to understand 100% of the logic to write each test
  - No need to force every file in the system to conform to unit test structure
  - Clearer boundaries of what code has been tested vs covered
    - Code coverage tools only tell you whether lines of code are reached, not tested

- Basic London method
  - Stub/mock dependencies, outside or inside
    - prefer stubs over mocks
  - Always query your stubs to be sure they received the right parameters
    - It does no good if you stub something and don't check that you called it correctly
  - Add some cross-file "integration" tests sparingly

- Setup file
  - The test runner loads code files, your code does not.
  - Therefore, you can't test whatever gets your app loaded up
  - 1. Manually recreate the app-wide global state as it is before any of the code to be tested runs
  - 2. Start writing tests for app code; the next step can wait
  - 3. When ready, refactor as much of your initial load/configuration logic as possible into testable pieces, probably in separate file(s)

- Helper files
  - Used for difficult source code files
    - Spaghetti, ball of mud, etc.
  - MOve logic out of difficult file into this one
  - Write unit tests against helper file
  - Only the one difficult file uses the helper as a dependency
  - Intended as a **temporary** refactoring tool
    - Ideally, you refactor the difficult source code file and remove the helper

- Cleanup Code
  - Functions like "destroy" and "reset" that clear state at the end of the unit test
  - Need to remove listeners, clear timeouts, etc.
  - Added into your real source code
  - Benefit: prevention of memory leaks if you call them in real app execution

### Refactoring
- Refactoring catch-22
  - Few untested legacy systems are written in a testable manner, so they must be refactored so they can be unit tested
  - Refactoring legacy code could break it

- Refactoring a file for unit tests
  - 1. Strictly maintain all public contracts within the file
  - 2. Only add or move code; do not remove or change anything yet
  - 3. Focus on control of state, and siplitting code into smaller, testable pieces

- Be cautious
  - Don't rush to delete anything
  - Avoid "improving" the code until you have good coverage

### Prioritization
1. Canary test
  - If this test fails, you know you've broken your setup, failed to install something, etc.
```javascript
describe('canary', () => {
  if ('adds 2 + 2', () => {
    expect (2 + 2).toEqual(4)
  })
})
```

2. Easy file(s)
  - Pulling in one or two easy files lets you test whether you've set up the test environment correctly for your app
  - Indications of an easy file:
    - Other parts of your app calle this code, not the other way around
    - It cares very little about global state

3. Dependency tree roots
  - Files that are most dependend on should ideally gain test coverage first
  - Look at your dependents to figure out what test cases to write for it
  - Work your way gradually to files further along the tree, in order of "reach" or importance

4. Mission critical features
  - Wherever defect consequences are most severe
  - High-usage areas
  - Anything where money changes hands
  - Anything that would greatly embarrass the business

5. Defect areas
  - Add coverage for your worst (applicable) defect areas
  - As you fix new defects, add unit tests for them
  - If something is difficult to QA effectively, be proactive

6. Error handlers
  - If everything goes well, nothing will be hitting them. It's hard to make your tests actually hit them in typical cases
  - Those that are user-facing or otherwise important
  - Those that communicate with third parties
  - Not just those that log an error

### Real Code Example Time

### Gaining Buy In
- Be clear about both the costs and the benefits
- Discover everyone's concerns up front and discuss them seriously
  - Yes: "It seems you're concerned about X." Then listen!
  - No: "Don't worry about X." "Y will handle X." "Just trust the team."
- Do not assume "unit test" means the same thing to everyone
- Together, define a pla of action that ramps up gradually
- Read *Never Split the Difference* by Chris Voss

## Key Takeaways
- There are different schools of thought when it comes to mocks and stubs and how you should use them in relation to dependencies
- Mocks are mocking an entire dependency, whereas stubs are mocking one piece of functionality of a dependency
- You should prefer stubs where possible because they are easier to maintain and have more granular control over
