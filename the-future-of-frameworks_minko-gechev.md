# Keynote: The Future of Frameworks
## Minko Gechev
- Senior Engineer on Core Angular team @ Google
- @mgechev
- blog.mgechev.com

## Notes
### Agenda
- Three pillars of the front-end frameworks of the future
  - Rehydration
  - Serving
  - Data
- Disclaimer: this is my personal opinion; does not reflect the future roadmap of Angular
- Not stating...
  - the "framework of the future" is (or is not) Angular, React, etc.
  - The language of the future is JavaScript

- The guiding principles for making a technology successful today are:
  - happy users
  - happy developers
  in this order.

### Rehydration
- Serving a web app in 2019
  - SSR enabled app diagram
  - Single page applications in this manner have some pros:
    - SSR - social media and SSO friendly
    - Once the app is loaded the user gets immediate experience
    - resources are downloaded and processed only once
  - Cons:
    - Stateful apps with complex state management
    - Not optimized for server-side rendering
    - Unresponsive apps before complete rehydration
- Let's go back to 2007
  - LAMP stack was popular
    - Browser made request to apache, server read data from DB, returned to browser. Browser made AJAX requests to server
  - The bootstrap step in the Client didn't exist.
  - This had pros
    - server-side rendered by default
    - immediately interactive
    - "rehydrates" without destroying the rendered UI
  - ...and cons
    - Does not provide immediate transitions across pages
    - Downloading/processing the same assets multiple times
- Let's look into the future
  - Rule #1: Happy user
    - optimize for UX
      - Load fast
      - app must be responsive
    - This means we should eliminate the bootstrap AND the fetch data step
  - Progressive rehydration
    - Rules:
      - component is loaded and bootstrapped on interaction
      - Component is loaded and bootstrapped when it receives new data
      - Each logical unit has its own bundle
        - This creates a series of waterfall downloads

### Serving
- Single HTTP request to get all resources needed for one route.
  - Route-level code splitting that we have today does not scale
- What scales better then?
  - Allow the client to specify what scripts it wants to download? Nope. Still doesn't scale better

### Data
- Reasoning about
  - *Features* of our application
  - *Features* of our users
  - "In machine learning and pattern recognition, a feature is an individual measureable system..."
  - "Adaptable, intelligent systems"
- We already have this in the recommender systems!
  - Recommender systems are not YET part of the front-end toolchain.
  - example: Predictive prefetching
    - We have an application usage report, which gives us a data analytics/ML model that we can provide to a web app with instant feedback in order to speed up fetching of different components
- Guess.js lets you do predictive prefetching in the client today

### What about making *developers* happy?
- The Angular team's mission is working on that now.
- This is a huge area that warrants its own presentation and that the entire industry needs to improve upon

## Key Takeaways
- progressive rehydration can speed up user interactions
- different ways of serving bundles can help you scale performant applications
- You can use data to build a faster, more specialized experience for each user
- Look up Guess.js