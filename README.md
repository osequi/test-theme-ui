# test-theme-ui

Playing with Theme UI, **The Design Graph Framework**

See:

- https://github.com/system-ui/theme-ui
- Design Graph: https://jxnblk.com/blog/design-graph/
- Spec: https://theme-ui.com/theme-spec

## Summary

- MDX / Gatsby origins (Purpose)
- Not completed. ~50% of the token docs are missing.
- Highly opinionated.
- Not all cases covered, like responsive tokens

### Tokens

- Lots of mandatory data to be defined.
- Ambiguous naming conventions. (`Scales`, `styles`)
- Tokens (`styles`) doesn't support responsive declarations.
- Some tokens (`styles`) are required to use a special component (`Styled`) to be accessible outside MDX.

### Composition

- Uses a [Beat-like](https://github.com/metamn/gust/blob/master/code/framework/design/typography/text-style/text-style.json) recursive JS / JSON.
- The syntax is much cleaner. No `mixins`, `properties`, `responsive`. But in the same time less powerful.

### Usage

- `sx` is like Emotion's `css` + built-in support for accessing tokens (theme aware)
- Supports responsive value arrays
- They work via a pragma
- Variants can be accessed both from `sx` and components (`<Button variant='small'>`)

## Scales

Are limited collections of raw values that map to specific style properties. For example, values for font-size are stored in the fontSizes scale.

### Colors

- https://theme-ui.com/theming/#colors
- All these aliases has to be defined,
- Then other aliases can be added

```text
text	body color
background	body background color
primary	primary button and link color
secondary	secondary color - can be used for hover states
accent	a contrast color for emphasizing UI
highlight	a background color for highlighting text
muted
```

#### Cons

- `primary`, `secondary`, `accent`, `highlight`, `muted` are very subjective

#### Takeways

- `text`, `background` can be used as is
- In Somenage's color theory we can use `highlight` and `muted`.

### Color Modes

- https://theme-ui.com/theming/#color-modes
- They match the shape of Colors

```
// example colors with dark mode
colors: {
  text: '#000',
  background: '#fff',
  primary: '#07c',
  modes: {
    dark: {
      text: '#fff',
      background: '#000',
      primary: '#0cf',
    }
  }
```

#### Cons

- Color values are repeating, they are not canonical: `#000` is defined at least in two places.

#### Takeways

- `Color Modes` is a good naming convention

### Typography

- https://theme-ui.com/theme-spec#typography
- All these aliases has to be defined,
- Then other aliases can be added

```text
fonts
	body: default body font family
	heading: default heading font family
	monospace: default monospace font family for <pre>, <code>, etc.
fontWeights
	body: body font weight
	heading: default heading font weight
	bold: default bold font weight
lineHeights
	body: body line height
	heading: default heading line height
```

```
// example theme object
{
  colors,
  fonts: {
    body: 'system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", sans-serif',
    heading: 'Georgia, serif',
    monospace: 'Menlo, monospace',
  },
  fontSizes: [
    12, 14, 16, 20, 24, 32, 48, 64
  ],
  fontWeights: {
    body: 400,
    heading: 700,
    bold: 700,
  },
  lineHeights: {
    body: 1.5,
    heading: 1.125,
  },
  letterSpacings: {
    body: 'normal',
    caps: '0.2em',
  },
}
```

#### Cons

- `fontSizes` are in `px` and freely added vs using a [scale](https://github.com/modularscale/modularscale-js).

#### Takeways

- The granularity

### Breakpoints

- https://theme-ui.com/theming/#breakpoints

```
// example custom breakpoints
{
  breakpoints: [
    '40em', '56em', '64em',
  ],
}
```

#### Cons

- The names `mobile`, `tablet` can be better remembered than these values.

#### Takeways

- They use the `min-width` aka mobile-first approach, like Somenage

### Styles / Compositions

- https://theme-ui.com/theming#styles
- Adding other styles like for `<body>`, `<h1>`, '<a>' etc.
- They re-use the scales above, aka Beat like compositions.

```
styles: {
  h1: {
	fontSize: 32,
	fontFamily: 'heading',
	fontWeight: 'heading',
	color: 'primary',
	mt: 4,
	mb: 2,
  },
}
```

#### Cons

- How `H1` is made responsive?

## Variants

Are partial styles that map to specific components. For example, a button might have primary and secondary variants, or large and small variants.

- https://theme-ui.com/theme-spec#variants
- Define custom groups of styles
- Can be accessed in `sx`

```
// example typographic style variants
{
  colors: {...},
  fonts: {...},
  fontWeights: {...},
  lineHeights: {...},
  // variants can use custom, user-defined names
  text: {
    heading: {
      fontFamily: 'heading',
      lineHeight: 'heading',
      fontWeight: 'heading',
    },
    caps: {
      textTransform: 'uppercase',
      letterSpacing: '0.1em',
    },
  },
  // variants for buttons
  buttons: {
    primary: {
      // you can reference other values defined in the theme
      color: 'white',
      bg: 'primary',
    },
    secondary: {
      color: 'text',
      bg: 'secondary',
    },
  }
}
```

```
// example using variants
<h1
  sx={{
    variant: 'text.heading',
  }}>
  Hello
</h1>
<button
  sx={{
    variant: 'buttons.primary',
  }}>
  Beep
</button>
```

## Components

Are elements that have styles constrained by scales.

## Themes

Are collections of scales (and possibly variants) that encapsulate a particular visual design language. Ideally, themes follow a common interface (or schema) and can be swapped out in different implementations.
