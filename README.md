# styled-create-react-app-easy-debug-guide

Scaffold a project with react, typescript, styled and debug tools

1. yarn create react-app mycoolapp --template typescript
> (or alternatively: npx create-react-app mycoolapp --template typescript)
2. yarn add styled-components
3. yarn add @types/styled-components react-app-rewired customize-cra babel-plugin-styled-components --dev
4. update package.json to use react-app-rewired
```
"start": "react-app-rewired start",
"build": "react-app-rewired build",
"test": "react-app-rewired test",
```
5. Create config-override.js in the root of the project with the following content:
```
const { override, addBabelPlugin } = require("customize-cra");

module.exports = override(
  addBabelPlugin([
    "babel-plugin-styled-components",
    {
      displayName: true,
      // any extra config from babel-plugin-styled-components
    },
  ])
);
```

6. To test if it works, create an AppStyle.ts file:
```
import styled, { css } from "styled-components";

interface ButtonProps {
  primary: boolean;
}

const Button = styled.a<ButtonProps>`
  /* This renders the buttons above... Edit me! */
  display: inline-block;
  border-radius: 3px;
  padding: 0.5rem 0;
  margin: 0.5rem 1rem;
  width: 11rem;
  background: purple;
  color: green;
  border: 2px solid black;

  /* The GitHub button is a primary button
   * edit this to target it specifically! */
  ${(props) =>
    props.primary &&
    css`
      background: purple;
      color: black;
    `}
`;

export { Button };
```

7. Update App.tsx to match:
```
import { Button } from "./AppStyle";

function App() {
  return <Button primary={false}>Hallo</Button>;
}

export default App;
```

#### Reference
1. https://dev.to/stanleysathler/enabling-styled-components-debugging-options-in-your-cra-app-without-ejecting-16c1
2. https://stackoverflow.com/questions/47077210/using-styled-components-with-props-and-typescript
