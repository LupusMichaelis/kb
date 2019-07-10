# Caveats

Typescript?
Global state (a registry of object).
No Model, you have to [choose](https://reactjs.org/community/model-management.html),
[maybe](https://hackernoon.com/introducing-react-axiom-84bf37a50adb)?

# /!\ BEWARE! ACHTUNG! /!\

React.Component.setState doesn't set the state, it updates it!

```
let mange="c'est", mon="n'importe", caca="quoi";
assert(this.state === {});
this.setState({mange})
assert(this.state === {mange: "c'est"});
this.setState({mon})
assert(this.state === {mange: "c'est", mon: "n'importe"});
this.setState({caca})
assert(this.state === {mange: "c'est", mon: "n'importe", caca: "quoi"});
this.setState({mange: "c'était"})
assert(this.state === {mange: "c'était", mon: "n'importe", caca: "quoi"});
```
# Source tree layout

As React doesn't enforce any structure, there is choice to be made. That's a big annoying topic,
and there's no definitive answer. Here are some interesting pieces about it:

- [1](https://medium.com/@alexmngn/how-to-better-organize-your-react-applications-2fd3ea1920f1)
- [2](https://hackernoon.com/the-100-correct-way-to-structure-a-react-app-or-why-theres-no-such-thing-3ede534ef1ed)
- [3](https://daveceddia.com/react-project-structure/)
- [organize by domain](https://marmelab.com/blog/2015/12/17/react-directory-structure.html)
- [5](https://blog.bitsrc.io/structuring-a-react-project-a-definitive-guide-ac9a754df5eb)

# Install

See machine.git

Install Bulma:
```sh
npm i --save react-bulma-components
# npm i --save-dev @types/react-bulma-components
# Doesn't exist yet, but we can work around:
echo "declare module 'react-bulma-components'" \
    > node_modules/react-bulma-components/index.d.ts
echo "declare module 'react-bulma-components/full'" \
    > node_modules/react-bulma-components/full/index.d.ts
```

## Vim

```sh
git clone https://github.com/mxw/vim-jsx.git
cd vim-jsx
cp after/syntax/jsx.vim  ~/.vim/syntax/

git clone https://github.com/leafgarland/typescript-vim.git
cd typescript-vim/
cp syntax/typescript.vim ~/.vim/syntax/


cat >> ~/.vimrc
au BufRead,BufNewFile *.elm set filetype=elm
au BufRead,BufNewFile *.ts set filetype=typescript
au BufRead,BufNewFile *.jsx set filetype=javascript.jsx
au BufRead,BufNewFile *.tsx set filetype=typescript.jsx
```

# Testing

[Testing Library](https://testing-library.com/)


## Debug tool

https://reactjs.org/blog/2015/09/02/new-react-developer-tools.html#installation


# Noticeable React packages

Name | Description
--- | ---
react | Base package
react-dom | JSX/TSX support
react-router-dom | Routing through DOM
reactstrap | Provides Twitter Bootstrap framework elements

# Basics

```tsx
import React from 'react';
import * as Person from './Model';

import './Person.css';

interface State
{
}

// Would be a component
export function simpleView(props: any): JSX.Element
{
    return <div>Some content</div>;
}

// Would be a container
export class View
    extends React.Component<Entity.Props, State>
{
    public render(): JSX.Element
    {
        return <div>Some text</div>;
    }

    public componentDidMount():
    {
    }

    public componentWillUnmount():
    {
    }

    public componentDidUpdate():
    {
    }
}
```

# Resources

- [A throughful description of React logic](https://overreacted.io/react-as-a-ui-runtime/)
  It explains well why key attribute is required on elements part of an iterable.

## Hooks

- Describe how to use [React hooks](https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d)
  in a function first citizen TS React way to develop components. The [official React hook
  introductory page](https://reactjs.org/docs/hooks-intro.html).
- Linter for [React hooks](https://reactjs.org/docs/hooks-rules.html)
  `npm install eslint-plugin-react-hooks --save-dev`
- [FAQ](https://reactjs.org/docs/hooks-faq.html)
- use of effect to [fetch data](https://www.robinwieruch.de/react-hooks-fetch-data/)

# Tooling

## Tools within

Package | Description
--- | ---
jest | Unit test
redux | Management of app state
eslint | A code linter for TypeScript
storybook | An environment to test components and document them
enzyme | Test React component output (DOM, styles, etc)

## Tools without

Tool | Description
--- | ---
Selenium | In browser functional testing
React Developer tool | Plugin for FF or Google Chrome
Redux Developer tool |Plugin for FF or Google Chrome
