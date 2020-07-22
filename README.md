# Section 7 - Diving Deeper into Components & React Internals

## Class-based vs Functional Components

#### class-based

> Class XY extends Component
> Access to State
> Lifecycle Hooks
> Access State and Props via "this" - this.state.XY & this.props.XY
> Use if you need to manage State or access Lifecycle hooks and you don't want to use React hooks

#### functional

> const XY = props => {...}
> Access to State (useState())
> No Lifecycle Hooks
> Access props via "props" - props.XY
> Use in all other cases (opposed to class-based point above)
