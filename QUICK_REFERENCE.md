# TDM Design System - Quick Reference

Quick reference for using the TDM Design System Nuxt Layer.

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

## 📦 Most Used Components

### Button

```vue
<Button variant="default">Default</Button>
<Button variant="destructive">Delete</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button size="sm">Small</Button>
<Button size="lg">Large</Button>
```

### Input & Form

```vue
<template>
  <form @submit="onSubmit">
    <div class="space-y-4">
      <div>
        <Label for="name">Name</Label>
        <Input id="name" v-model="name" placeholder="Enter name" />
      </div>

      <div>
        <Label for="email">Email</Label>
        <Input id="email" type="email" v-model="email" />
      </div>

      <Button type="submit">Submit</Button>
    </div>
  </form>
</template>

<script setup lang="ts">
const name = ref("");
const email = ref("");

const onSubmit = () => {
  console.log({ name: name.value, email: email.value });
};
</script>
```

### Dialog

```vue
<Dialog>
  <DialogTrigger as-child>
    <Button>Open Dialog</Button>
  </DialogTrigger>
  <DialogContent>
    <DialogHeader>
      <DialogTitle>Dialog Title</DialogTitle>
      <DialogDescription>
        Dialog description goes here
      </DialogDescription>
    </DialogHeader>
    <!-- Content -->
    <DialogFooter>
      <Button>Save</Button>
    </DialogFooter>
  </DialogContent>
</Dialog>
```

### Card

```vue
<Card>
  <CardHeader>
    <CardTitle>Card Title</CardTitle>
    <CardDescription>Card description</CardDescription>
  </CardHeader>
  <CardContent>
    <p>Card content goes here</p>
  </CardContent>
  <CardFooter>
    <Button>Action</Button>
  </CardFooter>
</Card>
```

### Select

```vue
<Select v-model="value">
  <SelectTrigger>
    <SelectValue placeholder="Select an option" />
  </SelectTrigger>
  <SelectContent>
    <SelectItem value="option1">Option 1</SelectItem>
    <SelectItem value="option2">Option 2</SelectItem>
    <SelectItem value="option3">Option 3</SelectItem>
  </SelectContent>
</Select>
```

### Alert

```vue
<Alert variant="default">
  <AlertTitle>Info</AlertTitle>
  <AlertDescription>This is an informational alert.</AlertDescription>
</Alert>

<Alert variant="destructive">
  <AlertTitle>Error</AlertTitle>
  <AlertDescription>Something went wrong.</AlertDescription>
</Alert>
```

### Table

```vue
<Table>
  <TableHeader>
    <TableRow>
      <TableHead>Name</TableHead>
      <TableHead>Email</TableHead>
      <TableHead>Role</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    <TableRow v-for="user in users" :key="user.id">
      <TableCell>{{ user.name }}</TableCell>
      <TableCell>{{ user.email }}</TableCell>
      <TableCell>{{ user.role }}</TableCell>
    </TableRow>
  </TableBody>
</Table>
```

### Badge

```vue
<Badge>Default</Badge>
<Badge variant="secondary">Secondary</Badge>
<Badge variant="destructive">Destructive</Badge>
<Badge variant="outline">Outline</Badge>
```

### Tabs

```vue
<Tabs default-value="tab1">
  <TabsList>
    <TabsTrigger value="tab1">Tab 1</TabsTrigger>
    <TabsTrigger value="tab2">Tab 2</TabsTrigger>
    <TabsTrigger value="tab3">Tab 3</TabsTrigger>
  </TabsList>
  <TabsContent value="tab1">Content for tab 1</TabsContent>
  <TabsContent value="tab2">Content for tab 2</TabsContent>
  <TabsContent value="tab3">Content for tab 3</TabsContent>
</Tabs>
```

## 🎨 Design Tokens

### Colors (Tailwind Classes)

```vue
<!-- Primary Colors -->
<div class="bg-primary text-white">Primary</div>
<div class="bg-secondary text-white">Secondary</div>

<!-- TDM Brand Colors -->
<div class="bg-primary-50">Primary 50% opacity</div>
<div class="bg-primary-10">Primary 10% opacity</div>

<!-- Gray Scale -->
<div class="bg-gray-100">Gray 100</div>
<div class="bg-gray-500">Gray 500</div>
<div class="bg-gray-900">Gray 900</div>

<!-- Semantic Colors -->
<div class="text-success">Success</div>
<div class="text-warning">Warning</div>
<div class="text-info">Info</div>

<!-- Text Colors -->
<div class="text-text-high">High emphasis</div>
<div class="text-text-medium">Medium emphasis</div>
<div class="text-text-low">Low emphasis</div>
```

### Typography

```vue
<!-- Fonts -->
<p class="font-monteserrat">Montserrat Font</p>
<p class="font-opensans">Open Sans Font</p>

<!-- Text Sizes (Tailwind defaults) -->
<p class="text-sm">Small text</p>
<p class="text-base">Base text</p>
<p class="text-lg">Large text</p>
<p class="text-xl">Extra large text</p>
```

### Spacing & Shadows

```vue
<!-- Spacing (Tailwind defaults) -->
<div class="p-4">Padding 1rem</div>
<div class="m-8">Margin 2rem</div>

<!-- Shadows -->
<div class="shadow-sm">Small shadow</div>
<div class="shadow-md">Medium shadow</div>
<div class="shadow-lg">Large shadow</div>
```

## 🛠️ Utilities

### cn() - Class Names Merger

```typescript
import { cn } from "@tdm/design-system-web/lib/utils";

const buttonClass = cn(
  "base-class",
  "another-class",
  isActive && "active-class",
  disabled && "disabled-class"
);
```

## 🌙 Dark Mode

The design system includes built-in dark mode support:

```vue
<template>
  <!-- Add dark class to enable dark mode -->
  <div :class="{ dark: isDark }">
    <Button>I respect dark mode</Button>
  </div>
</template>

<script setup lang="ts">
const isDark = ref(false);
</script>
```

## 📝 Form Validation

Using vee-validate and zod:

```vue
<template>
  <form @submit="onSubmit">
    <FormField v-slot="{ componentField }" name="email">
      <FormItem>
        <FormLabel>Email</FormLabel>
        <FormControl>
          <Input type="email" v-bind="componentField" />
        </FormControl>
        <FormMessage />
      </FormItem>
    </FormField>
    <Button type="submit">Submit</Button>
  </form>
</template>

<script setup lang="ts">
import { z } from "zod";
import { useForm } from "vee-validate";
import { toTypedSchema } from "@vee-validate/zod";

const schema = z.object({
  email: z.string().email("Invalid email"),
});

const { handleSubmit } = useForm({
  validationSchema: toTypedSchema(schema),
});

const onSubmit = handleSubmit((values) => {
  console.log(values);
});
</script>
```

## 🚨 Common Issues

### Components not found?

Run `nuxt prepare`:

```bash
pnpm run dev:prepare
```

### Styles not applying?

Make sure you've extended the layer in `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  extends: ["@tdm/design-system-web"],
});
```

### Hydration errors with DatePicker or Calendar?

Wrap in `<ClientOnly>`:

```vue
<ClientOnly>
  <DatePicker />
</ClientOnly>
```

## 📚 Resources

- [Full Layer Setup Guide](./LAYER_SETUP_GUIDE.md)
- [README](./README.md)
- [Usage Examples](./USAGE_EXAMPLE.md)
- [Storybook](http://localhost:6006) (when running `pnpm storybook`)

---

**Happy Coding! 🎉**
