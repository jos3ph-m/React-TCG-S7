# Section 7 - Diving Deeper into Components & React Internals

## Class-based vs Functional Components

#### Class-based

> Class XY extends Component
> Access to State
> Lifecycle Hooks
> Access State and Props via "this" - this.state.XY & this.props.XY
> Use if you need to manage State or access Lifecycle hooks and you don't want to use React hooks

#### Functional

> const XY = props => {...}
> Access to State (useState())
> No Lifecycle Hooks
> Access props via "props" - props.XY
> Use in all other cases (opposed to class-based point above)

---

## Component Lifecycle

#### Only available in Class-based Components

> Constructor()
> getDerivedStateFromProps()
> shouldComponentUpdate()
> getSnapshotBeforeUpdate()
> componentDidUpdate()
> componentDidCatch()
> componentDidMount()
> componentWillUnmount()
> render()

#### Component Lifecycle-Creation

The naming can be confusing, but "Lifecycle hooks" have nothing to do with "React hooks".

- constructor(props)
  **DO:** Set up state
  **DON'T:** Cause Side-Effects
- getDerivedStateFromProps(pros, state)
  **DO:** Sync state
  **DON'T:** Cause Side-Effects
- render() - Prepare & Structure your JSX code
- Render Child Components
- componentDidMount()
  **DO:** Cause Side-Effects
  **DON'T:** Update State (it triggers a re-render)

#### Component Lifecycle-Update

When props or state change, the two triggers for a component to be reevaluated by React, then we go to the update lifecycle.

- getDerivedStateFromProps(props, state) - very rarely needed
  **DO:** Sync state to props
  **DON'T:** Cause side-effects
- shouldComponetUpdate(nextProps, nextState)
  **DO:** decide whether to continue or not
  **DON'T:** cause side effects
- render()
- Update child component props
- getSnapshotBeforeUpdate(prevProps, prevState)
  **DO:** Last-minute DOM ops
  **DON'T** Cause side effects
- componentDidUpdate()
  **DO:** cause side-effects
  **DON'T:** update state (triggers re-render)

---

## useEffect() in Functional Components

useEffect covers all the needed class based lifecycle hooks in one React hook. The React hooks are not lifecycle hooks. It can be added anywhere in the functional component body.

useEffect takes a function that will run for every render cycle.

---

## How React Updates The DOM

render() is called

---

## Setting State Correctly

When old state is needed, we'll want to use prevState to set state:

```javascript
nameChangedHandler = (e, id) => {
  const personIndex = this.state.persons.findIndex((p) => {
    return p.id === id;
  });

  const person = {
    ...this.state.persons[personIndex],
  };

  // Alternative method to that just above
  // const person = Object.assign({}, this.state.persons[personIndex])

  person.name = e.target.value;

  const persons = [...this.state.persons];
  persons[personIndex] = person;

  this.setState((prevState, props) => {
    return {
      persons: persons,
      changeCounter: prevState.changeCounter + 1,
    };
  });
};
```

---

## Using PropTypes

To install:

```console
npm install --save prop-types
```

Import:

```javascript
import PropTypes from "prop-types";
```

Use - here we check prop types on a few props we passed into our class based component:

```javascript
Person.propTypes = {
  click: PropTypes.func,
  name: PropTypes.string,
  age: PropTypes.number,
  changed: PropTypes.func,
};
```
