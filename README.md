# 从零开始开发一个 React

这个是从零开始开发一个 React 系列的第五篇。

## 先行知识

学习这个课程之前呢，需要各位了解 React 的 api，以及做了什么事情。

如果完全不了解的话，不建议您继续往下看。

如果你已经具备了相关 React 的知识，那么就让我们开始吧。

## 本章要实现的效果

本章主要实现 react 的声明周期。

我们先来介绍一下 react 的声明周期（V16.4.1）

### Mounting

- constructor(props)

- static getDerivedStateFromProps(props, state)

- render(props, state)

- componentDidMount()

### Updating

- static getDerivedStateFromProps(props, state)

- shouldComponentUpdate(nextProps, nextState)

- render(props, state)

- getSnapshotBeforeUpdate(props, state)

// (snapshot here is the value returned from getSnapshotBeforeUpdate)

- componentDidUpdate(props, state, snapshot)

### Unmounting

- componentWillUnmount()

### Error Handling

- componentDidCatch(error, info)

> later

最终实现效果

```js
class LifeCycleDemo extends React.Component {
  constructor(props) {
    super(props);
    console.log("constructor with props: ", props);
  }
  shouldComponentUpdate(props, state) {
    console.log(
      "next props: ",
      props,
      "currentProps:",
      this.props,
      "nextState:",
      state,
      "currentState:",
      this.state
    );
  }
  getSnapshotBeforeUpdate(props, state) {
    console.log("getSnapshotBeforeUpdate with props: ", props, "state:", state);
  }
  componentDidUpdate(props, state, snapshot) {
    console.log(
      "componentDidUpdate with props: ",
      props,
      "state:",
      state,
      "snapshot:",
      snapshot
    );
  }
  componentDidMount() {
    console.log("componentDidMount");
  }
  componentWillUnmount() {
    console.log("componentWillUnmount");
  }
  // render函数和react的render略有不同
  // 这里借鉴了preact的思想，将props和state通过参数传到render函数中去
  render(props, state) {
    console.log("render with props: ", props, "render with state:", state);
    return <div>Hello {props.name}</div>;
  }
}

// render to dom
ReactDOM.render(
  <LifeCycleDemo name="Taylor" />,
  document.getElementById("root")
);
```
