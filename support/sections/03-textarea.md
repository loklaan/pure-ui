## Textarea

A multi-line text input field. Displays a resizable textarea with support for sizes, controlled state, disabled state, and auto-sizing via `field-sizing-content`.

Built on `@base-ui/react/field` (uses `Field.Control` with the `render` prop).

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/textarea"
```

#### Manual

1. Install dependencies:

```bash
npm install @base-ui/react clsx tailwind-merge
pnpm add @base-ui/react clsx tailwind-merge
yarn add @base-ui/react clsx tailwind-merge
bun add @base-ui/react clsx tailwind-merge
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/textarea.tsx`.

### Anatomy

```tsx
import { Textarea } from "@/components/ui/textarea";

<Textarea />
```

### Props

#### Textarea

Accepts all standard `React.ComponentProps<"textarea">` props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | "sm" \| "default" \| "lg" \| number | "default" | Height and padding preset |

### Usage

#### Basic

```tsx
import { Textarea } from "@/components/ui/textarea";

export function TextareaBasic() {
  return <Textarea placeholder="Type your message here" />;
}
```

#### Small Size

```tsx
import { Textarea } from "@/components/ui/textarea";

export function TextareaSmallSize() {
  return <Textarea size="sm" placeholder="Type your message here" />;
}
```

#### Large Size

```tsx
import { Textarea } from "@/components/ui/textarea";

export function TextareaLargeSize() {
  return <Textarea size="lg" placeholder="Type your message here" />;
}
```

#### Controlled

Use `value` and `onChange` to control the textarea state.

```tsx
"use client";

import { useState } from "react";
import { Textarea } from "@/components/ui/textarea";

export function TextareaControlled() {
  const [value, setValue] = useState("Type your message here");

  return (
    <div className="flex flex-col gap-2">
      <Textarea
        aria-label="Message"
        placeholder="Type your message here"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <span className="text-muted-foreground px-1 text-sm">Value: {value}</span>
    </div>
  );
}
```

#### Disabled

```tsx
import { Textarea } from "@/components/ui/textarea";

export function TextareaDisabled() {
  return <Textarea placeholder="Can't type here" disabled />;
}
```

### Notes

- The textarea uses `field-sizing-content` CSS, which causes it to auto-size based on its content. The `min-h-*` classes set the minimum height.
- The `aria-invalid` attribute triggers destructive border and ring styling for form validation.
- `className` is merged via `cn()`, so Tailwind classes can be appended or overridden.
- Wraps in `Field.Control` from Base UI with the `render` prop, enabling integration with Base UI's field validation system.
