# React.js
- [Complementary Tools](https://github.com/facebook/react/wiki/Complementary-Tools)

### [React-router](https://github.com/rackt/react-router)
- Use `IndexLink` to avoid index always active: [code](https://github.com/rackt/react-router/blob/master/examples/active-links/app.js#L17)
- How to pass data from parent route to children: see [my comment](https://github.com/rackt/react-router/issues/1857#issuecomment-174080760)

## React Tips

#### Render with condition (if)
Use this template, or see this issue [Discuss Conditional JSX Expression](https://github.com/reactjs/react-future/issues/35).

```js
<div>
  {condition ?
    <span></span>
  : null}
</div>
```

#### Key
Remember that the key only has to be unique among its siblings, not globally unique.

#### User action to callback props in pure components
```js
<button key={entry} onClick={() => this.props.vote(entry)}>
```
This is generally how we'll manage user input and actions with pure components: The components don't try to do much about those actions themselves. They merely invoke callback props.

---

## Redux
- The big idea of react-redux is to take our pure components and wire them up into a Redux Store by doing two things:
    - Mapping the Store state into component input props.
    - Mapping actions into component output callback props.
    
    
- Designing a Redux app often begins by thinking about the application state data structure. This is what describes what's going on in your application at any given time.
- In Redux, the application state is all stored in **one single tree structure.**
- Think about the application state in isolation from the application's behavior

- It is generally a good idea in these state transformation functions to always morph the old state into the new one instead of building the new state completely from scratch.

- It's becomes the job of our **reducer** to pick apart the state so that it gives only the relevant part to the function. The main reducer function only hands parts of the state to lower-level reducer functions. We separate the job of finding the right location in the state tree from applying the update to that location.

- *Store* stores your applicaiton state over time, you can dispatch actions to it `store.dispatch({type: 'NEXT'});`
- `connect(mapStateToProps)(SomeComponent);`
    - It takes a mapping function as an argument and returns another function that takes a React component class
    - The role of the mapping function is to map the state from the Redux Store into an object of props.
    
    
### When will React refresh?
React: if I just update a part of itwizm, why it won't refresh? Is it because it's not component, or is it because it's not immutable?

http://teropa.info/blog/2015/09/10/full-stack-redux-tutorial.html
> If the props of a component are all immutable values, and the props keep pointing to the same values between renders, there can be no reason to re-render the component, and it can be skipped completely!

That means we'll jsut need to render props.
Check test/components/Voting_spec.jsx
It's REPLACEING the props, not just change someting inside of the props.


    
    
### Question:
If it's all functional and immutable, do I create helper methods for things like `hasError()`, or store the computed data in store?

