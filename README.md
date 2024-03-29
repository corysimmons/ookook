# ookook

Ook is a dumb styling component for React. It's like [Rebass](https://rebassjs.org/), but the API is any camelCased CSS property and an elegant breakpoint pattern. It also uses styled-components@5 under the hood, so it looks really pretty in React Devtools (especially with the [experimental branch](https://react-devtools-experimental-chrome.now.sh/)).

Ook takes about 15 seconds to master.

## Installation

`npx install-peerdeps ookook`

## Simple Example

```js
import Ook, { OokConfig } from 'ookook'

export default () => (
  <OokConfig>
    <Ook background="tomato">Eek!</Ook>
  </OokConfig>
)
```

## Demo

https://codesandbox.io/s/cra-ook-tnxfi

## Example with Custom Breakpoints

```js
import Ook, { OokConfig } from 'ookook'

const Eek = () => (
  <OokConfig
    breakpoints={{
      default: '0',
      tablet: '600px',
      desktop: '1200px',
    }}
  >
    <Ook
      fontFamily="sans-serif"
      color="white"
      background={{
        default: 'tomato',
        tablet: 'dodgerblue',
        desktop: 'hotpink',
      }}
      padding={{
        default: '2rem',
        desktop: '4rem',
      }}
    >
      <Ook fontWeight="bold">Eek!</Ook>
    </Ook>
  </OokConfig>
)

export default Eek
```

## Props

#### By Default, Any camelCased CSS property

https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#Keyword_index

Vendor prefixed props need camelCased with a `_` in front instead of a `-`. E.g. `<Ook _webkitFontSmoothing="antialiased">`

#### cssProperties

There is an array of [1000+ CSS property names](https://www.npmjs.com/package/known-css-properties) _(most of which are never used in the real world)_ that are looped over for every `<Ook>` prop **by default**. It seems to perform fine, but it might not be fast enough for your needs. Feel free to pass your own array of kebab-cased CSS properties to `<OokConfig cssProperties={yourArrayOfCssProps}>...`. I'm starting/updating/maintaining one at [common-css-properties](https://github.com/corysimmons/common-css-properties) if you'd like to contribute any CSS properties you use.

#### active, hover, focus, visited (object)

Support for [pseudo classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes):

```js
<Ook
  background="tomato"
  color="white"
  hover={{
    background: 'dodgerblue',
    color: {
      tablet: 'springgreen'
    }
  }}
>
```

#### before, after (object)

Limited support for [pseudo elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements):

```js
<Ook
  position="relative"
  after={{
    content: '',
    display: 'block',
    background: 'tomato',
    width: '100px',
    height: '100px'
  }}
>
```

> **Note:** Pseudo classes (`hover`, etc.) and breakpoints within _pseudo elements_ aren't currently supported but they will be in the future.

#### css (string)

styled-components [`css` prop](https://medium.com/styled-components/announcing-native-support-for-the-css-prop-in-styled-components-245ca5252feb) support as an escape hatch. Possibly handy for things like the lobotomized owl technique. Supports nesting and pseudo-classes/elements.

#### el (string)

Any valid HTML element, or React component, to render the `<Ook>` as. Defaults to `div`.

#### {...props}

Additional props work as expected.

##### `el` and `css` and additional props Example:

```js
<Ook
  el="ul"
  background="hotpink"
  css={`
    > *:hover {
      background: springgreen;
    }
  `}
  onClick={() => console.log(123)}
>
  <li>a</li>
  <li>b</li>
  <li>c</li>
</Ook>
```

## Tips

- If you ever feel like you're looking at a mountain of `<Ook>`s, you should break your component down into smaller components with only a few `<Ook>`s and friendlier names. It sounds like cliche advice, but it's particularly applicable to Ook.

---

That's it. Have a banana for making it to the end. 🍌
