# rollup-plugin-hypothetical [![npm][npm-image]][npm-url] [![Dependency Status][david-image]][david-url] [![Build Status][travis-image]][travis-url]
This allows [Rollup] modules to import hypothetical files passed in as options
to the plugin. It's intended to make it easier to write tests for other Rollup
plugins.

## Installation
```bash
npm install --save-dev rollup-plugin-hypothetical
```

## Usage
```js
// rollup.config.js
import hypothetical from 'rollup-plugin-hypothetical';

export default {
  entry: './dir/a.js',
  plugins: [hypothetical({
    files: {
      './dir/a.js': `
        import foo from './b.js';
        foo();
      `,
      './dir/b.js': `
        export default function foo() {
          console.log("Hello, world!");
        }
      `
    }
  })]
};
```


## Options
### options.files
An object whose keys are paths, either relative to the current working directory
or absolute, and whose values are the code within the hypothetical files at
those paths.

### options.allowRealFiles
Set this to `true` to allow mixing of hypothetical and actual files. "Actual"
files can be files accessed by Rollup or produced by plugins further down the
chain.

### options.allowExternalModules
Set this to `false` to forbid importing of external modules.

### options.leaveIdsAlone
When this is set to `true`, the IDs in `import` statements won't be treated as
paths and will instead be looked up directly in the `files` object. There will
be no relative importing, path normalization, or restrictions on the contents
of IDs.


## License
MIT


[npm-url]: https://npmjs.org/package/rollup-plugin-hypothetical
[npm-image]: https://img.shields.io/npm/v/rollup-plugin-hypothetical.svg
[david-url]:   https://david-dm.org/Permutatrix/rollup-plugin-hypothetical
[david-image]: https://img.shields.io/david/Permutatrix/rollup-plugin-hypothetical/master.svg
[travis-url]: https://travis-ci.org/Permutatrix/rollup-plugin-hypothetical
[travis-image]: https://img.shields.io/travis/Permutatrix/rollup-plugin-hypothetical/master.svg

[Rollup]:    https://www.npmjs.com/package/rollup
