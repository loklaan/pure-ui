## Input

A form input field. Displays a single-line text input with support for multiple HTML input types, sizes, controlled state, and validation styling.

Built on `@base-ui/react/input`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/input"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge @base-ui/react
pnpm add clsx tailwind-merge @base-ui/react
yarn add clsx tailwind-merge @base-ui/react
bun add clsx tailwind-merge @base-ui/react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/input.tsx`.

### Anatomy

```tsx
import { Input } from "@/components/ui/input";

<Input />
```

### Props

#### Input

Accepts all props from `@base-ui/react/input`, except that `size` is overridden with a custom type.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | "sm" \| "default" \| "lg" \| number | "default" | Height preset; a numeric value is passed through to the HTML `size` attribute |
| type | string | -- | HTML input type; `"search"` and `"file"` receive specific styling |

### Usage

#### Basic

```tsx
import { Input } from "@/components/ui/input";

export function InputBasic() {
  return <Input type="text" placeholder="Enter text" aria-label="Enter text" />;
}
```

#### Input Types

Use the standard HTML `type` attribute to render email, number, password, and other input types.

```tsx
import { Input } from "@/components/ui/input";

export function InputTypesExample() {
  return (
    <div className="flex flex-col gap-4">
      <div className="flex flex-col gap-1">
        <label htmlFor="input-email" className="text-sm text-muted-foreground">
          Email
        </label>
        <Input id="input-email" placeholder="jane@example.com" type="email" />
      </div>
      <div className="flex flex-col gap-1">
        <label htmlFor="input-number" className="text-sm text-muted-foreground">
          Age
        </label>
        <Input id="input-number" min={0} placeholder="30" type="number" />
      </div>
      <div className="flex flex-col gap-1">
        <label htmlFor="input-password" className="text-sm text-muted-foreground">
          Password
        </label>
        <Input id="input-password" placeholder="••••••••" type="password" />
      </div>
    </div>
  );
}
```

#### Small Size

```tsx
import { Input } from "@/components/ui/input";

export function InputSmall() {
  return <Input type="text" size="sm" placeholder="Enter text" aria-label="Enter text" />;
}
```

#### Large Size

```tsx
import { Input } from "@/components/ui/input";

export function InputLarge() {
  return <Input type="text" size="lg" placeholder="Enter text" aria-label="Enter text" />;
}
```

#### Controlled

Use `value` and `onValueChange` to control the input state.

```tsx
"use client";

import { Input } from "@/components/ui/input";
import React from "react";

export function InputControlled() {
  const [value, setValue] = React.useState("base-ui.com");

  return (
    <div className="flex flex-col gap-2">
      <Input
        aria-label="Domain"
        placeholder="domain"
        value={value}
        onValueChange={(value) => setValue(value)}
      />
      <span className="text-muted-foreground px-1 text-sm">
        https://{value || "your-domain"}
      </span>
    </div>
  );
}
```

#### Disabled

```tsx
import { Input } from "@/components/ui/input";

export function InputDisabled() {
  return <Input type="text" placeholder="Disabled" disabled aria-label="Disabled" />;
}
```

#### File Type

Set `type="file"` to render a file picker. The component applies specific styling for the file input button.

```tsx
import { Input } from "@/components/ui/input";

export function InputFile() {
  return <Input type="file" aria-label="File" />;
}
```

### Notes

- The `size` prop controls the component height preset (`"sm"`, `"default"`, `"lg"`). Pass a number to set the HTML `size` attribute on the underlying input element instead.
- `type="search"` hides the browser default search cancel button and decoration icons.
- `type="file"` applies styling to the native file button text.
- The `aria-invalid` attribute triggers destructive border and ring styling for form validation.
- `className` is merged via `cn()`, so Tailwind classes can be appended or overridden.
- The `render` prop from Base UI can be used to render the input as a different element.
