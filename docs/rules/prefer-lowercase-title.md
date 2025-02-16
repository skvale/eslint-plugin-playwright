# Enforce lowercase test names (`prefer-lowercase-title`)

## Rule details

Enforce `test` and `test.describe` to have descriptions that begin with a
lowercase letter. This provides more readable test failures. This rule is not
enabled by default.

The following pattern is considered a warning:

```javascript
test('Adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

The following pattern is **not** considered a warning:

```javascript
test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

## Options

```json
{
  "playwright/prefer-lowercase-title": [
    "error",
    {
      "allowedPrefixes": ["GET", "POST"],
      "ignore": ["test.describe", "test"],
      "ignoreTopLevelDescribe": true
    }
  ]
}
```

### `ignore`

This array option controls which Playwright functions are checked by this rule.
There are two possible values:

- `"test.describe"`
- `"test"`

By default, none of these options are enabled (the equivalent of
`{ "ignore": [] }`).

Example of **correct** code for the `{ "ignore": ["test.describe"] }` option:

```javascript
test.describe('Uppercase description');
```

Example of **correct** code for the `{ "ignore": ["test"] }` option:

```javascript
test('Uppercase description');
```

### `allowedPrefixes`

This array option allows specifying prefixes, which contain capitals that titles
can start with. This can be useful when writing tests for API endpoints, where
you'd like to prefix with the HTTP method.

By default, nothing is allowed (the equivalent of `{ "allowedPrefixes": [] }`).

Example of **correct** code for the `{ "allowedPrefixes": ["GET"] }` option:

```javascript
test.describe('GET /live');
```

### `ignoreTopLevelDescribe`

This option can be set to allow only the top-level `test.describe` blocks to
have a title starting with an upper-case letter.

Example of **correct** code for the `{ "ignoreTopLevelDescribe": true }` option:

```javascript
test.describe('MyClass', () => {
  test.describe('#myMethod', () => {
    test('does things', () => {});
  });
});
```
