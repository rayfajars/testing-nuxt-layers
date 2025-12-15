# Using TDM Design System from GitHub

Quick guide to consume the TDM Design System Nuxt Layer directly from GitHub.

## 📦 Installation from GitHub

### Method 1: Direct Install (Recommended)

```bash
# Install the layer from GitHub
pnpm add github:rayfajars/testing-nuxt-layers

# Install required peer dependency
pnpm add -D typescript
```

### Method 2: Via package.json

Add to your `package.json`:

```json
{
  "dependencies": {
    "@tdm/design-system-web": "github:rayfajars/testing-nuxt-layers#main"
  },
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
```

Then install:

```bash
pnpm install
```

### Method 3: Specific Branch or Tag

Install from a specific branch:

```bash
pnpm add github:rayfajars/testing-nuxt-layers#develop
```

Install from a specific tag/release:

```bash
pnpm add github:rayfajars/testing-nuxt-layers#v1.0.0
```

Install from a specific commit:

```bash
pnpm add github:rayfajars/testing-nuxt-layers#567da27
```

## ⚙️ Configuration

Once installed, configure your Nuxt app:

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],

  // Your other configuration
});
```

## 🚀 Usage

All components are auto-imported:

```vue
<template>
  <div>
    <Button>Hello from GitHub!</Button>
    <Card>
      <CardHeader>
        <CardTitle>Using TDM Design System</CardTitle>
      </CardHeader>
      <CardContent>
        <p>Installed directly from GitHub repository!</p>
      </CardContent>
    </Card>
  </div>
</template>
```

## 🔄 Updating the Layer

To update to the latest version:

```bash
# Remove the current version
pnpm remove @tdm/design-system-web

# Install the latest from GitHub
pnpm add github:rayfajars/testing-nuxt-layers

# or simply
pnpm update @tdm/design-system-web
```

## 🌐 Repository Information

- **Repository**: https://github.com/rayfajars/testing-nuxt-layers
- **Main Branch**: `main`
- **Installation**: `github:rayfajars/testing-nuxt-layers`

## 📝 Important Notes

### 1. TypeScript is Required

Make sure TypeScript is installed in your project:

```bash
pnpm add -D typescript
```

### 2. Authentication for Private Repos

If the repository is private, you'll need GitHub authentication:

```bash
# Using SSH
pnpm add git+ssh://git@github.com:rayfajars/testing-nuxt-layers.git

# Using Personal Access Token
pnpm add https://<TOKEN>@github.com/rayfajars/testing-nuxt-layers.git
```

### 3. Clear Cache After Updates

After updating the layer:

```bash
rm -rf .nuxt node_modules/.cache node_modules/.vite
pnpm run dev
```

## 🆚 GitHub vs npm vs Local

| Method     | Best For             | Pros                          | Cons                   |
| ---------- | -------------------- | ----------------------------- | ---------------------- |
| **GitHub** | Development, Testing | Always latest, Easy updates   | Requires Git access    |
| **npm**    | Production           | Stable versions, Fast install | Need to publish        |
| **Local**  | Layer Development    | Instant changes               | Manual path management |

## 🔗 See Also

- [README.md](./README.md) - Full project documentation
- [USAGE_EXAMPLE.md](./USAGE_EXAMPLE.md) - Usage examples
- [LAYER_SETUP_GUIDE.md](./LAYER_SETUP_GUIDE.md) - Technical setup guide

---

**Repository**: [rayfajars/testing-nuxt-layers](https://github.com/rayfajars/testing-nuxt-layers)
