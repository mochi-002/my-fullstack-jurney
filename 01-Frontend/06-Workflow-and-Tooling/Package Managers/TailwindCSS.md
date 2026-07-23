## What is it?
A utility-first CSS framework that lets you build designs using utility classes directly in HTML.

## Install

```bash
npm install -D tailwindcss @tailwindcss/cli
```

## Run

```bash
npx tailwindcss -i ./src/input.css -o ./build/css/style.css --watch
```

## package.json

```json
{
  "scripts": {
    "tailwind": "npx tailwindcss -i ./src/input.css -o ./build/css/style.css --watch"
  }
}
```

Run:

```bash
npm run tailwind
```

## Folder structure

```
src/
    input.css

build/
    css/
        style.css
```

## Common directives

```css
@import "tailwindcss";
```

## Useful commands

Build once

```bash
npx tailwindcss -i ./src/input.css -o ./build/css/style.css
```

Watch

```bash
npm run tailwind
```

Minify

```bash
npx tailwindcss -i ./src/input.css -o ./build/css/style.css --minify
```

## Notes

- Utility-first framework
- Mobile-first
- Can use arbitrary values
- Supports dark mode
- Very customizable