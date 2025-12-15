# TDM Design System Web

A comprehensive Nuxt layer containing reusable UI components, utilities, and design tokens for TDM projects.

## Features

- 🎨 **Rich UI Components** - 30+ pre-built components based on Reka UI & Shadcn
- 🎯 **Design Tokens** - Consistent colors, spacing, and typography
- 🔧 **Utilities** - Helper functions and composables
- 📦 **Auto-imports** - Components and utilities automatically available
- 🌗 **Dark Mode** - Built-in dark mode support
- 📱 **Responsive** - Mobile-first responsive components
- ♿ **Accessible** - ARIA compliant components

## ⚠️ Important: TypeScript Requirement

**TypeScript is required** in your consumer project. The design system uses TypeScript for type resolution in Vue components.

```bash
# Install TypeScript in your project (if not already installed)
pnpm add -D typescript
```

> **Note**: If you see errors like `Failed to load TypeScript, which is required for resolving imported types`, make sure TypeScript is installed in your **consumer app** (not just in the layer).

## Installation

### Via npm (Recommended for published packages)

```bash
# npm
npm install @tdm/design-system-web

# pnpm
pnpm add @tdm/design-system-web

# yarn
yarn add @tdm/design-system-web
```

### Via GitHub (For development or unpublished versions)

Add to your `package.json`:

```json
{
  "dependencies": {
    "@tdm/design-system-web": "github:your-org/design-system-web#main"
  }
}
```

Or install directly:

```bash
# npm
npm install github:your-org/design-system-web

# pnpm
pnpm add github:your-org/design-system-web

# yarn
yarn add github:your-org/design-system-web
```

### Via Local Path (For local development)

```bash
# npm
npm install file:../design-system-web

# pnpm
pnpm add file:../design-system-web

# yarn
yarn add file:../design-system-web
```

## Usage

> 📖 **For complete examples and detailed usage guide, see [USAGE_EXAMPLE.md](./USAGE_EXAMPLE.md)**

### 1. Add Layer to Your Nuxt Config

In your `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],

  // Your project configuration
});
```

### 2. Use Components

Components are auto-imported and ready to use:

```vue
<template>
  <div>
    <Button variant="default" @click="handleClick"> Click me </Button>

    <Input v-model="name" placeholder="Enter your name" />

    <Dialog>
      <DialogTrigger as-child>
        <Button>Open Dialog</Button>
      </DialogTrigger>
      <DialogContent>
        <DialogHeader>
          <DialogTitle>Dialog Title</DialogTitle>
        </DialogHeader>
        <!-- Dialog content -->
      </DialogContent>
    </Dialog>
  </div>
</template>

<script setup lang="ts">
const name = ref("");

function handleClick() {
  console.log("Button clicked!");
}
</script>
```

### 3. Use Utilities

Utilities are also auto-imported:

```vue
<script setup lang="ts">
import { cn } from "@tdm/design-system-web/lib/utils";

const classes = cn(
  "base-class",
  "conditional-class",
  someCondition && "conditional-class-2"
);
</script>
```

### 4. Access Design Tokens

The design system's Tailwind configuration and CSS variables are automatically available:

```vue
<template>
  <div class="bg-primary text-white p-4 rounded-lg">
    <p class="text-text-high">High emphasis text</p>
    <p class="text-text-medium">Medium emphasis text</p>
  </div>
</template>
```

## Available Components

### Form Components

- `Button` - Button with variants and sizes
- `Input` - Text input field
- `Textarea` - Multi-line text input
- `Checkbox` - Checkbox input
- `RadioGroup` - Radio button group
- `Switch` - Toggle switch
- `Select` - Dropdown select
- `NativeSelect` - Native HTML select
- `Label` - Form label
- `Form` - Form components with validation

### Layout Components

- `Dialog` - Modal dialog
- `Popover` - Popover component
- `Tabs` - Tab navigation
- `Table` - Data table

### Feedback Components

- `Alert` - Alert messages
- `Badge` - Status badges
- `Loader` - Loading spinner
- `Sonner` - Toast notifications
- `Snackbar` - Snackbar notifications

### Advanced Components

- `Calendar` - Date picker calendar
- `DatePicker` - Date selection
- `Upload` - File upload
- `Command` - Command palette
- `Pagination` - Pagination controls
- `Avatar` - User avatar
- `Chips` - Chip/tag component
- `Divider` - Visual divider

### Utility Components

- `Text` - Typography component
- `TableToolbar` - Table toolbar

## Design Tokens

The design system includes comprehensive design tokens:

### Colors

- **Primary**: `primary`, `primary-{0-90}` (opacity variants)
- **Semantic**: `success`, `warning`, `info`, `processing`
- **Grays**: `gray-{100-900}`
- **Status Colors**: `red-*`, `green-*`, `blue-*`, `orange-*`
- **Text**: `text-high`, `text-medium`, `text-low`, `text-very-low`
- **Container**: `container-white`, `container-black`, `container-high/medium/low`

### Typography

- **Fonts**: `font-monteserrat`, `font-opensans`

### Shadows

- `shadow-sm`, `shadow-md`, `shadow-lg`, `shadow-xl`, `shadow-2xl`

## Development

### Layer Setup

This project is configured as a Nuxt Layer following best practices. For detailed information on how the layer is configured and how to use it in your projects, see [LAYER_SETUP_GUIDE.md](./LAYER_SETUP_GUIDE.md).

### Setup

```bash
# Install dependencies
pnpm install

# Prepare Nuxt types
pnpm run dev:prepare

# Start development server (Layer mode)
pnpm dev

# Start playground for testing (Playground mode)
pnpm run dev:playground

# Run Storybook
pnpm storybook
```

### Build

```bash
# Build for production
pnpm build

# Build Storybook
pnpm build-storybook
```

### Development Modes

1. **Layer Mode** (`pnpm dev`): Runs the layer at the root directory, useful for developing the layer itself.
2. **Playground Mode** (`pnpm run dev:playground`): Runs the `.playground` folder to test the layer in isolation.
3. **Storybook** (`pnpm storybook`): View and develop components in Storybook.

## Troubleshooting

### ❌ Error: "Failed to load TypeScript"

**Full Error**:

```
[@vue/compiler-sfc] Failed to load TypeScript, which is required for resolving imported types.
Please make sure "TypeScript" is installed as a project dependency.
```

**Solution**: Install TypeScript in your **consumer app** (the app using this layer):

```bash
# In your consumer app directory
pnpm add -D typescript

# Then restart dev server
pnpm run dev
```

**Why**: The design system uses TypeScript types in Vue components. Your consumer app needs TypeScript to resolve these types.

### 🔧 Components Not Auto-Importing

If components are not being auto-imported:

1. Make sure the layer is extended in `nuxt.config.ts`:

   ```typescript
   export default defineNuxtConfig({
     extends: ["@tdm/design-system-web"],
   });
   ```

2. Run `nuxt prepare`:

   ```bash
   pnpm run dev:prepare
   ```

3. Restart your IDE/dev server

### 🎨 Styles Not Applying

If styles are not showing:

1. Clear cache and restart:

   ```bash
   rm -rf .nuxt node_modules/.cache node_modules/.vite
   pnpm run dev
   ```

2. Make sure you're not overriding the layer's CSS in your app

### 💥 Import Resolution Errors

If you see `Failed to resolve import "@/lib/utils"`:

```bash
# Clear all caches
rm -rf .nuxt node_modules/.cache node_modules/.vite
pnpm run dev
```

### 🌊 Hydration Errors

For components like DatePicker or Calendar, wrap in `<ClientOnly>`:

```vue
<ClientOnly>
  <DatePicker v-model="date" />
</ClientOnly>
```

### 📚 More Help

- See [USAGE_EXAMPLE.md](./USAGE_EXAMPLE.md) for detailed examples
- See [LAYER_SETUP_GUIDE.md](./LAYER_SETUP_GUIDE.md) for technical setup
- Check [Storybook](http://localhost:6006) for component docs (`pnpm storybook`)

## Contributing

Please ensure all components follow the established patterns and include proper TypeScript types.

## License

MIT

## Support

For issues and questions, please open an issue on GitHub.
