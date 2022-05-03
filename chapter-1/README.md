# Amplify auth

Create a simple React application with the amplify ui react

## initialize amplify app
```
amplify init
```

## Add auth in the App
In the src/index.js
```
import Amplify from "aws-amplify";
import config from "./aws-exports";

Amplify.configure(config);
```

In the App.js
```
# replace all code 
import React from 'react';
import { Authenticator } from '@aws-amplify/ui-react';
import '@aws-amplify/ui-react/styles.css';

function App() {
  return (
    <Authenticator>
      {({ signOut, user }) => (
        <main>
          <h1>Hello {user.username}</h1>
          <button onClick={signOut}>Sign out</button>
        </main>
      )}
    </Authenticator>
  );
}

export default App;

```

## deploy new code into AWS
```
amplify add auth

amplify push
```