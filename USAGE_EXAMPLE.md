# TDM Design System - Usage Guide & Examples

Complete guide for using the TDM Design System Nuxt Layer in your projects.

## 📚 Table of Contents

- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Installation](#-installation)
- [Component Examples](#-component-examples)
- [Design Tokens](#-design-tokens)
- [Utilities & Composables](#-utilities--composables)
- [Advanced Usage](#-advanced-usage)
- [Troubleshooting](#-troubleshooting)

## ⚡ Prerequisites

Before using the TDM Design System, make sure you have:

- **Node.js** 18+ or 20+
- **Package Manager**: npm, pnpm, yarn, or bun
- **TypeScript** 5.0+ (required for type resolution in Vue SFC)

### Installing TypeScript

If your project doesn't have TypeScript:

```bash
# pnpm
pnpm add -D typescript

# npm
npm install -D typescript

# yarn
yarn add -D typescript

# bun
bun add -D typescript
```

## 🚀 Quick Start

### In Your Consumer App

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  extends: ["../design-system-web"], // Local path
  // OR
  extends: ["@tdm/design-system-web"], // npm package
});
```

That's it! All components, utilities, and design tokens are now available in your app.

## 📦 Installation

### Method 1: Via npm (Recommended)

```bash
# Install the design system
pnpm add @tdm/design-system-web

# Install peer dependencies (if not already installed)
pnpm add -D typescript
```

### Method 2: Via GitHub

```bash
pnpm add github:your-org/design-system-web
pnpm add -D typescript
```

Or add to `package.json`:

```json
{
  "dependencies": {
    "@tdm/design-system-web": "github:your-org/design-system-web#main"
  },
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
```

### Method 3: Via Local Path (Development)

```bash
pnpm add file:../design-system-web
pnpm add -D typescript
```

### Configure Your Nuxt App

**nuxt.config.ts:**

```typescript
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],

  // Your other configuration
  modules: [
    // Your modules
  ],
});
```

## 📦 Component Examples

All components are **auto-imported** - no need to import them manually!

### Button

```vue
<template>
  <div class="space-x-2">
    <Button variant="default">Default</Button>
    <Button variant="destructive">Delete</Button>
    <Button variant="outline">Outline</Button>
    <Button variant="ghost">Ghost</Button>
    <Button variant="secondary">Secondary</Button>

    <!-- Sizes -->
    <Button size="sm">Small</Button>
    <Button size="default">Default</Button>
    <Button size="lg">Large</Button>

    <!-- With loading state -->
    <Button :loading="isLoading">Submit</Button>
  </div>
</template>

<script setup lang="ts">
const isLoading = ref(false);
</script>
```

### Input & Form

```vue
<template>
  <form @submit.prevent="onSubmit">
    <div class="space-y-4 max-w-md">
      <div>
        <Label for="name">Name</Label>
        <Input id="name" v-model="form.name" placeholder="Enter your name" />
      </div>

      <div>
        <Label for="email">Email</Label>
        <Input
          id="email"
          type="email"
          v-model="form.email"
          placeholder="your@email.com"
        />
      </div>

      <div>
        <Label for="message">Message</Label>
        <Textarea
          id="message"
          v-model="form.message"
          placeholder="Your message..."
        />
      </div>

      <div class="flex items-center space-x-2">
        <Checkbox id="terms" v-model:checked="form.terms" />
        <Label for="terms">Accept terms and conditions</Label>
      </div>

      <Button type="submit" class="w-full">Submit</Button>
    </div>
  </form>
</template>

<script setup lang="ts">
const form = reactive({
  name: "",
  email: "",
  message: "",
  terms: false,
});

const onSubmit = () => {
  console.log("Form submitted:", form);
};
</script>
```

### Form Validation (vee-validate + zod)

```vue
<template>
  <form @submit="onSubmit">
    <FormField v-slot="{ componentField }" name="email">
      <FormItem>
        <FormLabel>Email</FormLabel>
        <FormControl>
          <Input
            type="email"
            placeholder="your@email.com"
            v-bind="componentField"
          />
        </FormControl>
        <FormDescription>We'll never share your email.</FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <FormField v-slot="{ componentField }" name="password">
      <FormItem>
        <FormLabel>Password</FormLabel>
        <FormControl>
          <Input type="password" v-bind="componentField" />
        </FormControl>
        <FormMessage />
      </FormItem>
    </FormField>

    <Button type="submit" class="w-full">Login</Button>
  </form>
</template>

<script setup lang="ts">
import { z } from "zod";
import { useForm } from "vee-validate";
import { toTypedSchema } from "@vee-validate/zod";

const schema = z.object({
  email: z.string().email("Invalid email address"),
  password: z.string().min(8, "Password must be at least 8 characters"),
});

const { handleSubmit } = useForm({
  validationSchema: toTypedSchema(schema),
});

const onSubmit = handleSubmit((values) => {
  console.log("Valid form:", values);
});
</script>
```

### Dialog

```vue
<template>
  <Dialog v-model:open="isOpen">
    <DialogTrigger as-child>
      <Button>Open Dialog</Button>
    </DialogTrigger>
    <DialogContent>
      <DialogHeader>
        <DialogTitle>Confirmation</DialogTitle>
        <DialogDescription>
          Are you sure you want to proceed with this action?
        </DialogDescription>
      </DialogHeader>

      <div class="py-4">
        <p>This action cannot be undone.</p>
      </div>

      <DialogFooter>
        <Button variant="outline" @click="isOpen = false">Cancel</Button>
        <Button @click="handleConfirm">Confirm</Button>
      </DialogFooter>
    </DialogContent>
  </Dialog>
</template>

<script setup lang="ts">
const isOpen = ref(false);

const handleConfirm = () => {
  console.log("Confirmed!");
  isOpen.value = false;
};
</script>
```

### More Component Examples

For brevity, here are quick examples of other commonly used components:

#### Card

```vue
<Card class="max-w-md">
  <CardHeader>
    <CardTitle>Card Title</CardTitle>
    <CardDescription>Description</CardDescription>
  </CardHeader>
  <CardContent>
    <p>Content goes here</p>
  </CardContent>
  <CardFooter>
    <Button>Action</Button>
  </CardFooter>
</Card>
```

#### Select

```vue
<Select v-model="value">
  <SelectTrigger>
    <SelectValue placeholder="Select..." />
  </SelectTrigger>
  <SelectContent>
    <SelectItem value="1">Option 1</SelectItem>
    <SelectItem value="2">Option 2</SelectItem>
  </SelectContent>
</Select>
```

#### Alert

```vue
<Alert variant="default">
  <AlertTitle>Info</AlertTitle>
  <AlertDescription>This is an alert</AlertDescription>
</Alert>
```

#### Table

```vue
<Table>
  <TableHeader>
    <TableRow>
      <TableHead>Name</TableHead>
      <TableHead>Email</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    <TableRow v-for="item in items" :key="item.id">
      <TableCell>{{ item.name }}</TableCell>
      <TableCell>{{ item.email }}</TableCell>
    </TableRow>
  </TableBody>
</Table>
```

#### Badge & Tabs

```vue
<!-- Badges -->
<Badge>Default</Badge>
<Badge variant="destructive">Error</Badge>

<!-- Tabs -->
<Tabs default-value="tab1">
  <TabsList>
    <TabsTrigger value="tab1">Tab 1</TabsTrigger>
    <TabsTrigger value="tab2">Tab 2</TabsTrigger>
  </TabsList>
  <TabsContent value="tab1">Content 1</TabsContent>
  <TabsContent value="tab2">Content 2</TabsContent>
</Tabs>
```

## 🎨 Design Tokens

The design system includes comprehensive design tokens automatically available as Tailwind classes.

### Colors

```vue
<template>
  <!-- Primary & Secondary -->
  <div class="bg-primary text-white p-4">Primary</div>
  <div class="bg-secondary text-white p-4">Secondary</div>

  <!-- Opacity Variants -->
  <div class="bg-primary-50 p-4">Primary 50% opacity</div>
  <div class="bg-primary-10 p-4">Primary 10% opacity</div>

  <!-- Grayscale -->
  <div class="bg-gray-500 text-white p-4">Gray 500</div>

  <!-- Semantic Colors -->
  <span class="text-success">Success</span>
  <span class="text-warning">Warning</span>
  <span class="text-info">Info</span>

  <!-- Text Emphasis -->
  <p class="text-text-high">High emphasis</p>
  <p class="text-text-medium">Medium emphasis</p>
  <p class="text-text-low">Low emphasis</p>
</template>
```

### Typography

```vue
<template>
  <!-- Fonts -->
  <h1 class="font-monteserrat">Montserrat Font</h1>
  <p class="font-opensans">Open Sans Font</p>

  <!-- Sizes -->
  <p class="text-sm">Small (14px)</p>
  <p class="text-base">Base (16px)</p>
  <p class="text-lg">Large (18px)</p>
  <p class="text-xl">XL (20px)</p>
</template>
```

### Shadows & Spacing

```vue
<template>
  <!-- Shadows -->
  <div class="shadow-sm">Small shadow</div>
  <div class="shadow-md">Medium shadow</div>
  <div class="shadow-lg">Large shadow</div>

  <!-- Spacing -->
  <div class="p-4">Padding 1rem</div>
  <div class="m-8">Margin 2rem</div>
</template>
```

## 🛠️ Utilities & Composables

### cn() - Class Names Merger

Auto-imported utility for conditional classes:

```vue
<template>
  <button :class="buttonClass">Dynamic Button</button>
</template>

<script setup lang="ts">
const isActive = ref(false);
const isDisabled = ref(false);

const buttonClass = computed(() =>
  cn(
    "px-4 py-2 rounded",
    isActive.value && "bg-primary text-white",
    isDisabled.value && "opacity-50 cursor-not-allowed"
  )
);
</script>
```

## 🌙 Dark Mode

Built-in dark mode support:

```vue
<template>
  <div :class="{ dark: isDark }">
    <Button @click="isDark = !isDark">Toggle Dark</Button>
    <Card class="mt-4">
      <CardHeader>
        <CardTitle>Dark Mode Card</CardTitle>
      </CardHeader>
      <CardContent>
        <p class="text-text-medium">Adapts to dark mode!</p>
      </CardContent>
    </Card>
  </div>
</template>

<script setup lang="ts">
const isDark = ref(false);
</script>
```

## 🚀 Advanced Usage

### Custom Theming

Override design tokens:

```css
/* app.css or app.vue <style> */
:root {
  --tdm-primary: #1e40af;
  --tdm-secondary: #3730a3;
}
```

### Extending Components

```vue
<!-- components/MyButton.vue -->
<template>
  <Button v-bind="$attrs" :class="customClass">
    <Icon v-if="icon" :name="icon" class="mr-2" />
    <slot />
  </Button>
</template>

<script setup lang="ts">
interface Props {
  icon?: string;
  gradient?: boolean;
}

const props = defineProps<Props>();

const customClass = computed(() =>
  cn(props.gradient && "bg-gradient-to-r from-primary to-secondary")
);
</script>
```

## 🚨 Troubleshooting

### TypeScript Error: "Failed to load TypeScript"

**Solution**: Install TypeScript in your project:

```bash
pnpm add -D typescript
```

Then restart your dev server:

```bash
pnpm run dev
```

### Components Not Found?

```bash
pnpm run dev:prepare
```

### Styles Not Applying?

Clear cache:

```bash
rm -rf .nuxt node_modules/.cache node_modules/.vite
pnpm run dev
```

### Import Resolution Errors

Clear Vite cache and restart:

```bash
rm -rf .nuxt node_modules/.cache node_modules/.vite
pnpm run dev
```

### Hydration Errors

Wrap problematic components in `<ClientOnly>`:

```vue
<ClientOnly>
  <DatePicker v-model="date" />
</ClientOnly>
```

## 📚 Additional Resources

- [Layer Setup Guide](./LAYER_SETUP_GUIDE.md) - Technical layer configuration
- [README](./README.md) - Project overview
- [Storybook](http://localhost:6006) - Component docs (`pnpm storybook`)
- [shadcn-vue Docs](https://www.shadcn-vue.com/) - Component reference

---

**Happy Coding! 🎉**
