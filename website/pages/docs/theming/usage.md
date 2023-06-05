---
title: Usage
description: There are various ways to consume Panda tokens depending on your need at that point in time.
---

# Using Tokens

There are various ways to consume Panda tokens depending on your need at that point in time.

## Usage in CSS function

This is the basic way to consume your tokens. You use them as attribute values in the `css` method exposed by css panda.

```js
import { css } from '../styled-system/css'

const className = css({
  color: 'green.400',
  background: 'grey.200',
  height: '4',
  borderRadius: 'md'
})
```

## Usage in Composite values

In CSS, composite values are values that combine two or more individual values into a single value. We can't tokenize
this values, so we provide a way to reference your design system tokens within these.

```js
import { css } from '../styled-system/css'

const className = css({ border: 'solid 1px token(colors.red.400)' })
```

You can also provide a fallback value.

```js
import { css } from '../styled-system/css'

const className = css({ border: 'solid 1px token(colors.red.400, red)' })
```

## Incremental adoption

You might not be ready to run your design system fully based on css panda. In such cases you can incrementally adopt it
by consuming the panda tokens via the style attribute or in existing `styled-components` or `emotion` project

```tsx
import { token } from '../styled-system/tokens'

return (
  <div
    style={{
      background: token('colors.blue.200')
    }}
  />
)
```

Each of your design tokens will be available in the generated `/tokens` folder. It looks like this:

```js
const tokens = {
  // ...
  'colors.blue.200': {
    value: '#bfdbfe',
    variable: 'var(--colors-blue-200)'
  }
  // ...
}
```

- The `token()` function returns the raw value of the token.
- The `token.var()` function returns the CSS custom property used to reference the token.

Both functions are typesafe and expect a known dot-separated token path, they also accept a fallback value as a second
argument.

Using the example above, `token('colors.blue.200')` would return `#bfdbfe` and `token.var('colors.blue.200')` would
return `var(--colors-blue-200)`.

### Usage in styled-components

```tsx
import styled from 'styled-components'

const Button = styled.button`
  background: ${token('colors.blue.200')};
`
```

### Usage in emotion

```tsx
import styled from '@emotion/styled'

const Button = styled.button`
  background: ${token('colors.blue.200')};
`
```