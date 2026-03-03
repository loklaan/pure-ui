## Switch

A toggle switch component for alternating between checked and unchecked states.

Built on `@base-ui/react/switch`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/switch"
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

3. Copy the component source into your project at `components/ui/switch.tsx`.

### Anatomy

```tsx
import { Switch } from "@/components/ui/switch";

<Switch />
```

The Switch renders the Base UI `Switch.Root` and `Switch.Thumb` internally as a single component. There are no separate sub-component exports.

### Props

Accepts all props from `@base-ui/react/switch` (`Switch.Root`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | "sm" \| "md" \| "lg" | "md" | Size of the switch |
| isInteractive | boolean | false | Enables a press-to-stretch animation on the thumb |
| reduceMotion | boolean | false | Disables all transition animations |
| checked | boolean | -- | Controlled checked state |
| defaultChecked | boolean | -- | Initial checked state for uncontrolled usage |
| onCheckedChange | (checked: boolean) => void | -- | Callback fired when checked state changes |
| disabled | boolean | false | Disables the switch |

### Variants

#### size

Values: `"sm"` | `"md"` | `"lg"`
Default: `"md"`

```tsx
<Switch size="sm" />
<Switch size="md" />
<Switch size="lg" />
```

### Usage

#### Basic

```tsx
import { Switch } from "@/components/ui/switch";

export function SwitchExample() {
  return <Switch />;
}
```

#### With Label

Wrap the Switch and a text element inside a Label component for accessible labelling.

```tsx
import { Switch } from "@/components/ui/switch";
import { Label } from "@/components/ui/label";

export function SwitchWithLabel() {
  return (
    <Label className="cursor-pointer">
      <Switch />
      <span>Enable notifications</span>
    </Label>
  );
}
```

#### Interactive

By default the switch has no press animation. Set `isInteractive` to enable a stretch effect on the thumb when pressed.

```tsx
import { Switch } from "@/components/ui/switch";
import { Label } from "@/components/ui/label";

export function SwitchInteractiveExample() {
  return (
    <Label className="cursor-pointer">
      <Switch isInteractive />
      <span>Enable notifications</span>
    </Label>
  );
}
```

#### Controlled

Use the `checked` and `onCheckedChange` props to control the switch state.

```tsx
"use client";

import { useState } from "react";
import { Switch } from "@/components/ui/switch";
import { Label } from "@/components/ui/label";

export function SwitchControlledExample() {
  const [checked, setChecked] = useState(false);

  return (
    <div className="flex flex-col gap-3">
      <Label className="cursor-pointer">
        <Switch isInteractive checked={checked} onCheckedChange={setChecked} />
        <span>Airplane Mode</span>
      </Label>

      <div className="flex items-center gap-2 text-sm text-muted-foreground">
        <span>Checked: {checked ? "Yes" : "No"}</span>
      </div>
    </div>
  );
}
```

#### Disabled

```tsx
import { Switch } from "@/components/ui/switch";

export function SwitchDisabledExample() {
  return <Switch disabled />;
}
```

#### Sizes

```tsx
import { Switch } from "@/components/ui/switch";
import { Label } from "@/components/ui/label";

export function SwitchSizesExample() {
  const sizes = ["sm", "md", "lg"] as const;

  return (
    <div className="flex flex-col gap-4">
      {sizes.map((size) => (
        <Label key={size} className="cursor-pointer">
          <Switch size={size} />
          <span>Enable Polar Payments</span>
        </Label>
      ))}
    </div>
  );
}
```

#### Reduce Motion

Set `reduceMotion` to disable all transition animations on the switch and thumb.

```tsx
import { Switch } from "@/components/ui/switch";

export function SwitchReduceMotionExample() {
  return <Switch reduceMotion />;
}
```

#### Custom Card Style

The switch can be composed with other elements for custom layouts. This example renders a card-style toggle using Label and className overrides.

```tsx
import { cn } from "@/lib/classes";
import { Switch } from "@/components/ui/switch";
import { Label } from "@/components/ui/label";

export function CustomSwitchCardStyleExample() {
  return (
    <Label
      htmlFor="custom-switch-card"
      className="flex items-center gap-6 rounded-lg border-2 p-3 bg-card hover:bg-accent/50 has-data-checked:border-primary/88 has-data-checked:bg-accent/50 cursor-pointer"
    >
      <div className="flex flex-col gap-1">
        <p className="text-sm leading-4">Enable notifications</p>
        <p className="text-xs text-muted-foreground">
          You can enable or disable notifications at any time.
        </p>
      </div>
      <Switch
        id="custom-switch-card"
        defaultChecked
        isInteractive
      />
    </Label>
  );
}
```

### Notes

- The thumb element is rendered inline within the Switch component. It is not exported as a separate sub-component.
- The `isInteractive` prop adds a press animation that stretches the thumb width on click. This is purely visual and does not affect functionality.
- The `render` prop from Base UI can be used to render the switch root as a different element.
