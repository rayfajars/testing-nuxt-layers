# Example: Using TDM Design System Layer

This is an example of how to consume the TDM Design System in a Nuxt project.

## Project Structure

```
my-app/
├── nuxt.config.ts
├── package.json
├── app.vue
└── pages/
    └── index.vue
```

## Installation

### 1. Install the Layer

Choose one of the following methods:

**Via npm:**

```bash
pnpm add @tdm/design-system-web
```

**Via GitHub:**

```bash
pnpm add github:your-org/design-system-web
```

**Via Local Path (for development):**

```bash
pnpm add file:../design-system-web
```

### 2. Configure Your Nuxt App

**nuxt.config.ts:**

```typescript
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],

  modules: [
    // Your other modules
  ],
});
```

### 3. Use Components

**pages/index.vue:**

```vue
<template>
  <div class="container mx-auto p-8">
    <h1 class="text-3xl font-bold mb-6">Welcome to My App</h1>

    <!-- Button Component -->
    <div class="space-x-2 mb-4">
      <Button variant="default">Default Button</Button>
      <Button variant="destructive">Delete</Button>
      <Button variant="outline">Outline</Button>
    </div>

    <!-- Form Example -->
    <div class="max-w-md">
      <form @submit.prevent="handleSubmit">
        <div class="space-y-4">
          <div>
            <Label for="name">Name</Label>
            <Input
              id="name"
              v-model="form.name"
              placeholder="Enter your name"
            />
          </div>

          <div>
            <Label for="email">Email</Label>
            <Input
              id="email"
              v-model="form.email"
              type="email"
              placeholder="Enter your email"
            />
          </div>

          <div>
            <Label for="message">Message</Label>
            <Textarea
              id="message"
              v-model="form.message"
              placeholder="Enter your message"
            />
          </div>

          <div class="flex items-center space-x-2">
            <Checkbox id="terms" v-model:checked="form.terms" />
            <Label for="terms">Accept terms and conditions</Label>
          </div>

          <Button type="submit" class="w-full"> Submit </Button>
        </div>
      </form>
    </div>

    <!-- Dialog Example -->
    <div class="mt-8">
      <Dialog>
        <DialogTrigger as-child>
          <Button variant="outline">Open Dialog</Button>
        </DialogTrigger>
        <DialogContent>
          <DialogHeader>
            <DialogTitle>Confirmation</DialogTitle>
            <DialogDescription>
              Are you sure you want to proceed?
            </DialogDescription>
          </DialogHeader>
          <DialogFooter>
            <Button variant="outline">Cancel</Button>
            <Button>Confirm</Button>
          </DialogFooter>
        </DialogContent>
      </Dialog>
    </div>

    <!-- Table Example -->
    <div class="mt-8">
      <Table>
        <TableHeader>
          <TableRow>
            <TableHead>Name</TableHead>
            <TableHead>Status</TableHead>
            <TableHead>Action</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <TableRow v-for="item in items" :key="item.id">
            <TableCell>{{ item.name }}</TableCell>
            <TableCell>
              <Badge
                :variant="item.status === 'active' ? 'default' : 'secondary'"
              >
                {{ item.status }}
              </Badge>
            </TableCell>
            <TableCell>
              <Button variant="ghost" size="sm">Edit</Button>
            </TableCell>
          </TableRow>
        </TableBody>
      </Table>
    </div>
  </div>
</template>

<script setup lang="ts">
// Components and utilities are auto-imported
// No need to import Button, Input, etc.

const form = reactive({
  name: "",
  email: "",
  message: "",
  terms: false,
});

const items = ref([
  { id: 1, name: "Item 1", status: "active" },
  { id: 2, name: "Item 2", status: "inactive" },
  { id: 3, name: "Item 3", status: "active" },
]);

function handleSubmit() {
  console.log("Form submitted:", form);
}
</script>
```

### 4. Use Design Tokens

The CSS variables are automatically available:

```vue
<template>
  <div class="bg-primary text-white p-4">
    <h2 class="text-2xl font-monteserrat">Primary Background</h2>
    <p class="text-text-white">This uses TDM design tokens</p>
  </div>

  <div class="bg-container-high p-4 mt-4">
    <p class="text-text-high">High emphasis text</p>
    <p class="text-text-medium">Medium emphasis text</p>
    <p class="text-text-low">Low emphasis text</p>
  </div>

  <div class="space-x-2 mt-4">
    <span class="bg-success text-white px-3 py-1 rounded">Success</span>
    <span class="bg-warning text-white px-3 py-1 rounded">Warning</span>
    <span class="bg-info text-white px-3 py-1 rounded">Info</span>
  </div>
</template>
```

### 5. Use Utilities

```vue
<script setup lang="ts">
// The cn utility is auto-imported
const buttonClass = computed(() =>
  cn(
    "base-button-class",
    isActive.value && "active-class",
    isDisabled.value && "disabled-class"
  )
);

// Other utilities from the design system
const isActive = ref(false);
const isDisabled = ref(false);
</script>
```

## Advanced Usage

### Custom Theming

You can override design tokens in your app's CSS:

```css
/* app.vue or global CSS */
:root {
  --tdm-primary: #your-color;
  --tdm-secondary: #your-secondary-color;
}
```

### Extending Components

You can create custom components that extend the design system components:

```vue
<!-- components/MyCustomButton.vue -->
<template>
  <Button v-bind="$attrs" :class="customClass">
    <slot />
  </Button>
</template>

<script setup lang="ts">
const customClass = computed(() =>
  cn(
    "my-custom-styles"
    // Add your custom classes
  )
);
</script>
```

## Troubleshooting

### Components not auto-importing

Make sure your `nuxt.config.ts` has the layer in the `extends` array:

```typescript
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],
});
```

### Styles not loading

The CSS should be automatically imported. If not, try adding it explicitly:

```typescript
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],
  css: ["@tdm/design-system-web/assets/css/tailwind.css"],
});
```

### TypeScript errors

Make sure your TypeScript is configured to recognize the layer types. Restart your Nuxt dev server and VS Code if needed.
