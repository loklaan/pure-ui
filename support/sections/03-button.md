## Button

A button triggers an action or event, such as submitting a form, opening a dialog, or sending a request. Supports multiple visual variants, sizes, border radii, and rendering as another element.

Built on `@base-ui/react/button`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/button"
```

#### Manual

1. Install dependencies:

```bash
npm install tailwind-variants clsx tailwind-merge @base-ui/react
pnpm add tailwind-variants clsx tailwind-merge @base-ui/react
yarn add tailwind-variants clsx tailwind-merge @base-ui/react
bun add tailwind-variants clsx tailwind-merge @base-ui/react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/button.tsx`.

### Anatomy

```tsx
import { Button } from "@/components/ui/button";

<Button>Click me</Button>
```

### Props

#### Button

Accepts all props from `@base-ui/react/button`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| variant | "default" \| "secondary" \| "outline" \| "ghost" \| "link" \| "destructive" | "default" | Visual style of the button |
| size | "default" \| "xs" \| "sm" \| "lg" \| "xl" \| "icon-sm" \| "icon" \| "icon-lg" \| "icon-xl" | "default" | Size preset; icon sizes render a square button |
| radius | "none" \| "sm" \| "default" \| "lg" \| "xl" \| "full" | "default" | Border radius preset |
| disabled | boolean | false | Disables the button |
| render | React.ReactElement | -- | Renders the button as another element while preserving button behaviour |
| nativeButton | boolean | true | Set to `false` when using `render` with a non-button element to preserve keyboard accessibility |
| focusableWhenDisabled | boolean | false | Keeps the button focusable when disabled, preventing focus loss |

### Variants

#### variant

Values: `"default"` | `"secondary"` | `"outline"` | `"ghost"` | `"link"` | `"destructive"`
Default: `"default"`

```tsx
<Button variant="default">Default</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="link">Link</Button>
<Button variant="destructive">Destructive</Button>
```

#### size

Values: `"default"` | `"xs"` | `"sm"` | `"lg"` | `"xl"` | `"icon-sm"` | `"icon"` | `"icon-lg"` | `"icon-xl"`
Default: `"default"`

The `"icon-sm"`, `"icon"`, `"icon-lg"`, and `"icon-xl"` sizes render a square button sized for icon-only content.

```tsx
<Button size="sm">Small</Button>
<Button size="lg">Large</Button>
<Button size="icon" aria-label="Upload">
  <ArrowUpIcon />
</Button>
```

#### radius

Values: `"none"` | `"sm"` | `"default"` | `"lg"` | `"xl"` | `"full"`
Default: `"default"`

```tsx
<Button radius="full">Pill Button</Button>
<Button radius="none">Sharp Button</Button>
```

### Exports

The component file exports two symbols:

- `Button` -- the button component.
- `buttonVariants` -- the `tailwind-variants` config object. Use this to apply button styling to non-button elements or to compose button styles in other components.

### Usage

#### Basic

```tsx
import { Button } from "@/components/ui/button";

export function ButtonBasic() {
  return <Button>Button</Button>;
}
```

#### With Icon

Place an SVG icon as a direct child alongside text. The button auto-sizes icons and adjusts padding.

```tsx
import { GitBranchIcon } from "lucide-react";
import { Button } from "@/components/ui/button";

export function ButtonWithIcon() {
  return (
    <Button variant="outline" size="sm">
      <GitBranchIcon />
      New Branch
    </Button>
  );
}
```

#### Icon Only

Use an icon size (`"icon-sm"`, `"icon"`, `"icon-lg"`, `"icon-xl"`) and provide an `aria-label`.

```tsx
import { CircleFadingArrowUpIcon } from "lucide-react";
import { Button } from "@/components/ui/button";

export function ButtonIconOnly() {
  return (
    <Button variant="outline" size="icon" aria-label="Upload">
      <CircleFadingArrowUpIcon />
    </Button>
  );
}
```

#### Disabled

```tsx
import { Button } from "@/components/ui/button";

export function ButtonDisabled() {
  return <Button disabled>Button</Button>;
}
```

#### Loading

Combine `disabled` with a `Spinner` to indicate a pending action.

```tsx
"use client";

import { useEffect, useState } from "react";
import { Button } from "@/components/ui/button";
import { Spinner } from "@/components/ui/spinner";

export function ButtonLoading() {
  const [isPending, setIsPending] = useState(false);

  useEffect(() => {
    isPending && setTimeout(() => setIsPending(false), 2000);
  }, [isPending]);

  return (
    <Button disabled={isPending} onClick={() => setIsPending(true)}>
      {isPending ? <Spinner size="sm" /> : null}
      {isPending ? "Submitting..." : "Submit"}
    </Button>
  );
}
```

#### Rendering as Another Element

Use the `render` prop to make another component look like a button. Set `nativeButton={false}` when the rendered element is not a native button to preserve keyboard accessibility.

```tsx
import Link from "next/link";
import { Button } from "@/components/ui/button";

export function LinkAsButton() {
  return (
    <Button
      render={<Link href="/login" />}
      nativeButton={false}
    >
      Login
    </Button>
  );
}
```

### Notes

- The `render` prop is Base UI's replacement for Radix UI's `asChild`. Pass a React element (e.g. `render={<Link href="/login" />}`) and set `nativeButton={false}` for non-button elements.
- `focusableWhenDisabled` keeps focus on the button when it becomes disabled. This prevents focus from being lost and preserves tab order.
- SVG children are automatically sized based on the `size` variant. Icons with an explicit `class` containing a `size-` utility are left unchanged.
- The button respects `prefers-reduced-motion` via `motion-reduce:transform-none`, disabling scale transitions when the user prefers reduced motion.
- `className` is merged via `cn()`, so Tailwind classes can be appended or overridden.
