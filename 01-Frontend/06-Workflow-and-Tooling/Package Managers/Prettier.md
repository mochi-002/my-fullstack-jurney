## What is it?

Opinionated code formatter.

## Install

```bash
npm install -D prettier
```

## Format

```bash
npx prettier --write .
```

Format HTML only

```bash
npx prettier --write "**/*.html"
```

## package.json

```json
{
    "scripts": {
        "prettier": "npx prettier --write '**/*.html'"
    }
}
```

Run

```bash
npm run prettier
```

## Config

.prettierrc

```json
{
    "tabWidth": 4,
    "useTabs": false,
    "semi": true,
    "singleQuote": true
}
```

Ignore

```
node_modules
dist
build
```

## Notes

- Doesn't lint
- Just formats
- Can integrate with VS Code
- Works with many languages