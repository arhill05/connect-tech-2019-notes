# Angular Team Ask-Me-Anything
## Minko Gechev

## Notes
Q: React has React Native, are there any plans for the Angular team to release something?
A: We're working closely with NativeScript and Ionic to provide these features.

Q: What kind of performance upgrades can we look forward to with Ivy?
A: It depends on the size of the application. If the app is small, you can get HUGE performance gains. If you have a large application, the performance gains will be smaller but still tangible.

Q: What is your biggest Angular app?
A: At Google it's Google Cloud. 5-7 million lines of code. An incremental build takes approximately 5 seconds because of caching, but if the cache is empty it'll take a few hours. You can use the local dist cache to be able to do this. Look into implementing remote cache for faster incremental builds - it simply applies the changes to a previous build instead of building everything from scratch

Q: With AngularJS hitting end of life in mid 2021, what can we expect for the Angular Upgrade module and supporting the upgrade of legacy applications?
A: ngUpgrade won't stop working even in later projects

Q: Is there any reason AngularJS would stop working even after LTS?
A: It will keep working. The prime goal for new standards are to make sure we have backwards compatibility

Q: Do you know percentage wise how many folks are using AngularJS vs Angular?
A: I don't have an answer to that right now

Q: What do you think about GraphQL?
A: In Google, we are not using it. We are using GRPC and other RPC inspired solutions. GraphQL doesn't give you typing, so I don't prefer it, but it is definitely a viable solution if it works for you.

Q: What is your official recommendation for sharing events and data between components since React now has it's Hooks API?
A: Services! We haven't discussed going in a direction because we don't think it is going to work well with Angular. Some people say they don't like that we have dependency injection, but really everyone uses it. Whether you are giving a component something as an input, via constructor parameters, or props, it is just another way of doing dependency injection

Q: Managing state properly in the services has been more than adequate, but the argument is "the more complex it gets, the more important it is to consider something like ngrx." What are your thoughts?
A: There are several alternatives to ngrx like ngx. You can do proper state management in services if you want, but you have to be careful to not mutate the state or store it in multiple places, or handle notifications for changes in sub-objects. It is doable, but there is definitely something to be careful with. There are well-established practices for ngrx

* look into differences of change detection strategies

* they're thinking about getting rid of NgModules??

Q: Are there any plans to make reactive forms strongly typed?
A: Yes. It's even higher priority than Angular elements

Q: Are there any projects in the community that you want to promote?
A: Yeah.
  - Angular-PreRender - a static site generator for Angular essentially
  - Someone implemented an Angular CLI builder to help you build Electron apps using it
  -

## Key Takeaways