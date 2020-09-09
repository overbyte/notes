# React Notes From The Edge of Sanity

## Introduction

## React Classes

Quick Setup

```
import React from 'react';

export default class MyComponent extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            name: 'overbyte'
        }
    }

    componentDidMount() {
        // runs once on mount
    }

    componentDidUpdate() {
        // runs after an update
    }

    componentWillUnmount() {
        // runs once before an unmount
    }

    render() {
        function getRenderedItem() {
            return <div>my rendered item</div>;
        }

        return (
            <div className={ this.props.classSetByParent }>
                <div className="some-other-class">
                    { this.state.name }
                </div>
            </div>
        );
    }
}
```

notes:

* `this.state` references the state
* `this.props` references the props
* `className` will be used for css class

### updating state

```
function updateTheState() {
    // get the existing state by duplicating it
    let name = this.state.name; // string passes by value

    // update the state
    name = 'overbitten';

    // reassign the state
    this.setState({ name });
}
```

## Functional React

Ordinarily, functional react components do not have any state - they're used as
views on the data passed as props

```
import React from 'react';

export default function MyComponent(props) {
    return (
        <div className="some-css-class">
            { props.label }
        </div>
    );
}
```

### React Hooks

React Hooks allow functional components to include extra features like state,
side effects, reducers etc.

### State

```
import React, { useState } from 'react';

export default function MyComponent({ label }) {
    const [myColour, setMyColour] = useState('#ff0000');
    return (
        <div className="some-css-class">
            { label }
        </div>
    );
}
```

### Reducers

State uses reducers behind the scenes. Reducers allow the state to be updated
using more complicated logic, generally found in a switch statement

```
import React, { useReducer } from 'react';

export default function MyComponent(props) {
    const initialState = {
        myVar: 'initial-value',
        myArray: [],
    };

    const reducer = (state, { type, extras }) => {
        switch (type) {
            case 'ACTION_TYPE_ADD' :
                // return duplicated state with extras added
                return {...state, myArray: [...state.myArray, extras]};
            case 'ACTION_TYPE_REMOVE' :
                // return duplicated state with extras removed
                return {...state, myArray: state.myArray.filter(item => item !== extras};
            case 'ACTION_TYPE_RESET' :
                // replace state with initialState
                return {...initialState};
            default :
                throw new Error(`Action type "${type}" not recognised`);
        }
    };

    const [state, dispatchState] = useReducer(reducer, initialState);
}
``` 

### Side Effects

Used to fire an effect when the state in the (dependency) array in the 2nd
argument changes. If a return function is specified, this will also be fired
when the current state is discarded. 

To reproduce the `componentDidMount()`, `componentWillUnmount()` lifecycle
hooks, the dependency array should be only filled with dependecies that don't
update (like the mutator `updateState` in `useState` here). The React docs say
to use an empty dependency array but this comes with some code smell and may
bark linter errors.

```
import React, { useEffect } from 'react';

export default function MyComponent(props) {
    const [state, updateState] = useState('initial value');

    // create a side effect every time the state value changes.
    useEffect(() => {
        // do something when the state updates
        document.title = state;
    }, [state]);

    // create a side effect that only fires once on mount and once on unmount
    useEffect(() => {
        // do stuff
        
        return () => {
            // undo stuff
        };
    }, []);
}
```

Links:

* https://stackoverflow.com/questions/62572454/limiting-addeventlistener-to-componentdidmount-using-useeffect-hook
* https://reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often
* https://stackoverflow.com/questions/55840294/how-to-fix-missing-dependency-warning-when-using-useeffect-react-hook
