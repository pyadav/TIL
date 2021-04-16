## TypeScript With react
Using these tips i just want to increase my developer experience

- Type checking for component props

### Type checking for component props 
```javascript
const defaultHeadingProps = {
  name: 'h1'
}

// composite types
type HeadingProps = {
  title: string;
} &  typeof defaultHeadingProps;

// declare a Function Component; return type is inferred.
const Heading = ({ title }: HeadingProps ) => {
  return <h1>{title}</h1>;
};
Heading.defaultProps = defaultHeadingProps;


/*
  React.FC<Props>
  adds a default children Props
*/

// react hooks
const [user, setUser] = React.useState<IUser | null>(null);

const initialState = { count: 0 };
type ACTIONTYPE =
  | { type: "increment"; payload: number }
  | { type: "decrement"; payload: string };
function reducer(state: typeof initialState, action: ACTIONTYPE) {}
const [state, dispatch] = React.useReducer(reducer, initialState);

`;
```

### References
- [React TypeScript Cheatsheets](https://react-typescript-cheatsheet.netlify.app/)