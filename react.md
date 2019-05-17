# Caveats

Typescript?
Global state (a registry of object).
No Model, you have to [choose](https://reactjs.org/community/model-management.html),
[maybe](https://hackernoon.com/introducing-react-axiom-84bf37a50adb)?

# Source tree layout

As React doesn't enforce any structure, there is choice to be made. That's a big annoying topic,
and there's no definitive answer. Here are some interesting pieces about it:

- [1](https://medium.com/@alexmngn/how-to-better-organize-your-react-applications-2fd3ea1920f1)
- [2](https://hackernoon.com/the-100-correct-way-to-structure-a-react-app-or-why-theres-no-such-thing-3ede534ef1ed)
- [3](https://daveceddia.com/react-project-structure/)
- [4](https://marmelab.com/blog/2015/12/17/react-directory-structure.html)
- [5](https://blog.bitsrc.io/structuring-a-react-project-a-definitive-guide-ac9a754df5eb)

# Install

See machine.git

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

## Debug tool

https://reactjs.org/blog/2015/09/02/new-react-developer-tools.html#installation


# React packages

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

export function simpleView(props: any): JSX.Element
{
    return <div>Some content</div>;
}

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
