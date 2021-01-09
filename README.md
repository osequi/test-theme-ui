# test-theme-ui

Playing with Theme UI, **The Design Graph Framework**

See:

- https://github.com/system-ui/theme-ui
- Design Graph: https://jxnblk.com/blog/design-graph/

## Scales

Are limited collections of raw values that map to specific style properties. For example, values for font-size are stored in the fontSizes scale.

### Colors

- https://theme-ui.com/theming/#colors
- All these color aliases has to be defined,
- Then other aliases can be added

```
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

```js
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

## Components

Are elements that have styles constrained by scales.

## Variants

Are partial styles that map to specific components. For example, a button might have primary and secondary variants, or large and small variants.

## Themes

Are collections of scales (and possibly variants) that encapsulate a particular visual design language. Ideally, themes follow a common interface (or schema) and can be swapped out in different implementations.
