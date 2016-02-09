# React.js
- [Complementary Tools](https://github.com/facebook/react/wiki/Complementary-Tools)

### [React-router](https://github.com/rackt/react-router)
- Use `IndexLink` to avoid index always active: [code](https://github.com/rackt/react-router/blob/master/examples/active-links/app.js#L17)
- How to pass data from parent route to children: see [my comment](https://github.com/rackt/react-router/issues/1857#issuecomment-174080760)

### Render with condition (if)
Use this template, or see this issue [Discuss Conditional JSX Expression](https://github.com/reactjs/react-future/issues/35).

```js
<div>
  {condition ?
    <span></span>
  : null}
</div>
```

---

## Redux
- Designing a Redux app often begins by thinking about the application state data structure. This is what describes what's going on in your application at any given time.
- In Redux, the application state is all stored in **one single tree structure.**
- Think about the application state in isolation from the application's behavior