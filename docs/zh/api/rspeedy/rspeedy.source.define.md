<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@lynx-js/rspeedy](./rspeedy.md) &gt; [Source](./rspeedy.source.md) &gt; [define](./rspeedy.source.define.md)

## Source.define property

The `define` options is used to define some values or expressions at compile time.

**Signature:**

```typescript
define?: Record<string, string | number | boolean | undefined | Record<string, unknown>> | undefined;
```

## Remarks

- If the value provided is a string, it will be utilized as a code fragment.

- If the value provided is an object, all its keys will be defined in the same manner.

- If the value isn't a string, it will be stringified, with functions included.

- Notably, if a `typeof` prefix is attached to the key, it will be exclusively defined for `typeof` calls."

## Example 1

Using `define` for environment variables.

```js
import { defineConfig } from '@lynx-js/rspeedy'
export default defineConfig({
  source: {
    define: {
      BUILD_VERSION: JSON.stringify(process.env.BUILD_VERSION ?? 'unknown_version'),
      'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV),
    },
  },
})
```
Expressions will be replaced with the corresponding code fragments:

```js
const version = BUILD_VERSION;
if (process.env.NODE_ENV === 'development') {}

// ⬇️ Turn into being...
const version = "unknown_version";
if ("development" === 'development') {}
```

## Example 2

Using `define` for `typeof`<!-- -->.

```js
import { defineConfig } from '@lynx-js/rspeedy'
export default defineConfig({
  source: {
    define: {
      'typeof window': JSON.stringify("undefined"),
    },
  },
})
```
The `typeof` expressions will be replaced with the corresponding code fragments:

```js
if (typeof window !== 'undefined') {}

// ⬇️ Turn into being...
if ("undefined" !== 'undefined') {}
```

## Example 3

Using `define` with objects.

```js
import { defineConfig } from '@lynx-js/rspeedy'
export default defineConfig({
  source: {
    define: {
      'import.meta': {
        foo: JSON.stringify('foo'),
        bar: { baz: 0 },
      },
    },
  },
})
```
Expressions will be replaced with the corresponding code fragments:

```js
console.log(import.meta)

// ⬇️ Turn into being...
console.log({ foo: "foo", bar: { baz: 0 } })
```

