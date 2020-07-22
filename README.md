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
