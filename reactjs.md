# React.js
- [Complementary Tools](https://github.com/facebook/react/wiki/Complementary-Tools)

### [React-router](https://github.com/rackt/react-router)
- Use `IndexLink` to avoid index always active: [code](https://github.com/rackt/react-router/blob/master/examples/active-links/app.js#L17)
- How to pass data from parent route to children: see [my comment](https://github.com/rackt/react-router/issues/1857#issuecomment-174080760)

### Render if
Use this template, or see this issue [Discuss Conditional JSX Expression](https://github.com/reactjs/react-future/issues/35).

```js
<div>
  {condition ?
    <span></span>
  : null}
</div>
```