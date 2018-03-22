
# @kohlmannj/css-to-object

Convert flat CSS rules to JavaScript style objects

Useful for css-in-js libraries

```sh
npm i css-to-object
```

```js
const cssToObject = require('css-to-object')

const style = cssToObject(`
  color: tomato;
  padding: 16px;
  @media (min-width: 40em) {
    paddingLeft: 32px;
    paddingRight: 32px;
  }
  &:hover: {
    color: black;
  }
  & h1 {
    font-size: 48px;
  }
`, {
  camelCase: true,
  numbers: true
})

// {
//   color: 'tomato',
//   padding: 16,
//   '@media (min-width: 40em)': {
//     paddingLeft: 32,
//     paddingRight: 32,
//   },
//   ':hover': {
//     color: 'black'
//   },
//   h1: {
//     fontSize: 48
//   }
// }
```

## Options

- `ampersands`: preserves `&` in nested selectors
  - For use with JSS / [jss-nested](http://cssinjs.org/jss-nested/?v=v6.0.1) and other CSS-in-JS solutions that support the `&` reference selector
- `numbers`: Converts px values to numbers
- `camelCase`: converts CSS properties to camelCased keys

## Differences from the Original
This is a fork of [jxnblk/css-to-object](https://github.com/jxnblk/css-to-object) / [`css-to-object` on NPM](https://www.npmjs.com/package/css-to-object) with the following changes:

- Add `ampersands` option (see above)
- Import [`css.parse()`](https://github.com/reworkcss/css#cssparsecode-options) directly, thereby enabling **usage in web browsers**
  - The [`css` module]() exports both its `parse()` and `stringify()` methods
  - `css.stringify()`'s [source map support](https://github.com/reworkcss/css/blob/master/lib/stringify/source-map-support.js) depends on [Node `fs`](https://www.nodejs.org/api/fs.html) module, which can't be used in-browser
  - Therefore, despite only using `css.parse()`, the original `css-to-object` module cannot be bundled with Webpack or used client-side
- Incorporate @meyer's shorthand bugfix ([jxnblk/css-to-object#3](https://github.com/jxnblk/css-to-object/pull/3))

[MIT License](LICENSE.md)
