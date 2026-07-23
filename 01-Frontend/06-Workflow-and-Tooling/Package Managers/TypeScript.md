## What is it?

JavaScript with static typing.

---

## Setup

**Init npm**

```bash
npm init -y
```

**Install**

```bash
npm install -D typescript
```

**Initialize** (creates `tsconfig.json`)

```bash
npx tsc --init
```

**Compile**

```bash
npx tsc
```

**Watch mode**

```bash
npx tsc --watch
```

**package.json scripts**

```json
{
  "scripts": {
    "build": "tsc",
    "watch": "tsc --watch"
  }
}
```

**Important file:** `tsconfig.json`

---