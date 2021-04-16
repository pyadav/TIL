## TypeScript With styled-components 
Using these tips i just want to increase my developer experience

- Theme variable suggestions
- Type checking for component props

### Theme variable suggestions  
Want to auto complete for theme variables

```javascript
// a general way to access theme in style-component
const TextComponent = styled.Text`
  color: ${(props) => props.theme.primaryColor};
`;

// or by object destructuring 
const TextComponent = styled.Text`
  color: ${({ theme }) => theme.primaryColor};
`;


/*
SOLUTION:
Typescript interface declaration merging to override the default theme
*/ 

import { DefaultTheme } from "styled-components/native";
declare module "styled-components" {
  export interface DefaultTheme {
    primaryColor: string;
    secondaryColor: string;
  }
}

// OR
declare module 'styled-components' {
  type Theme = typeof theme;
  export interface DefaultTheme extends Theme {}
}

export const lightTheme: DefaultTheme = {
	primaryColor: "#333",
	secondaryColor: "#666",
};

export const darkTheme: DefaultTheme = {
	primaryColor: "#fff",
	secondaryColor: "#cacaca",
};


// then use this theme with ThemeProvider
<ThemeProvider theme={lightTheme}>
</ThemeProvider>
```


### Type checking for custom Props
Use props for altering the style of the components

```javascript

/*
 pass custom props on runtime to adapt css like:
 change opacity of the button based on primary props
*/

type Props = {
  disabled: boolean;
};

const StartButton = ({ disabled }: Props) => {
  return (
    <Button disabled={disabled} primary>
      <ButtonText>Start counter</ButtonText>
    </Button>
  );
};

type ButtonProps = {
  primary: boolean;
};

const Button = styled.TouchableOpacity<ButtonProps>`
  opacity: ${(props) => (props.primary ? 0.5 : 1)};
`;

// Attaching additional props
const Input = styled.input.attrs(props => ({
  // we can define static props
  type: "text",

  // or we can define dynamic ones
  size: props.size || "1em",
}))`
  /* here we use the dynamically computed prop */
  margin: ${props => props.size};
  padding: ${props => props.size};
`;
```
