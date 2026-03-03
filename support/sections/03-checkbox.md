## Checkbox

A toggle control that allows the user to switch between checked, unchecked, and indeterminate states. Provides a convenience wrapper (`Checkbox`) for simple use and individual sub-components (`CheckboxRoot`, `CheckboxIndicator`) for custom compositions.

Built on `@base-ui/react` (Checkbox).

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/checkbox"
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

3. Copy the component source into your project at `components/ui/checkbox.tsx`.

### Anatomy

The component offers two usage modes.

**Simple** -- use the `Checkbox` wrapper, which combines root and indicator:

```tsx
import { Checkbox } from "@/components/ui/checkbox";

<Checkbox />
```

**Composable** -- use `CheckboxRoot` and `CheckboxIndicator` separately for full control:

```tsx
import { CheckboxRoot, CheckboxIndicator } from "@/components/ui/checkbox";

<CheckboxRoot>
  <CheckboxIndicator />
</CheckboxRoot>
```

### Props

#### Checkbox

Convenience component that renders `CheckboxRoot` with a `CheckboxIndicator` inside. Accepts all props from `CheckboxRoot`. Pass `children` to replace the default check icon inside the indicator.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| checked | boolean | -- | Controlled checked state |
| defaultChecked | boolean | false | Initial checked state (uncontrolled) |
| onCheckedChange | (checked: boolean, event: Event) => void | -- | Called when the checked state changes |
| indeterminate | boolean | -- | Puts the checkbox in an indeterminate (mixed) state |
| size | "sm" \| "default" \| "lg" | "default" | Size of the checkbox |
| radius | "none" \| "sm" \| "default" \| "lg" \| "full" | "default" | Border radius preset |
| reduceMotion | boolean | false | Disables all transition animations |
| disabled | boolean | false | Disables the checkbox |

#### CheckboxRoot

Root element that wraps the Base UI `Checkbox.Root` and provides `CheckboxContext` to descendant components. Accepts the same props as `Checkbox` above.

#### CheckboxIndicator

Visual indicator rendered inside `CheckboxRoot`. Must be a descendant of `CheckboxRoot`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| icon | ReactNode \| (props: CheckboxIconProps) => ReactNode | CheckboxIcon | Custom icon to render instead of the default animated checkmark |

Pass `children` to `CheckboxIndicator` to fully replace the indicator content.

### Variants

#### size

Values: `"sm"` | `"default"` | `"lg"`
Default: `"default"`

```tsx
<Checkbox size="sm" />
<Checkbox size="default" />
<Checkbox size="lg" />
```

#### radius

Values: `"none"` | `"sm"` | `"default"` | `"lg"` | `"full"`
Default: `"default"`

```tsx
<Checkbox radius="none" />
<Checkbox radius="full" />
```

### Usage

#### Basic

```tsx
import { Checkbox } from "@/components/ui/checkbox";

export function CheckboxDemo() {
  return (
    <label className="flex items-center gap-2 cursor-pointer">
      <Checkbox />
      <span>Enable Notifications</span>
    </label>
  );
}
```

#### Sizes

```tsx
import { Checkbox } from "@/components/ui/checkbox";

export function CheckboxSizesDemo() {
  return (
    <div className="flex flex-col gap-5">
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox size="sm" />
        <span>Make a choice</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox size="default" />
        <span>Make a choice</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox size="lg" />
        <span>Make a choice</span>
      </label>
    </div>
  );
}
```

#### Radius

```tsx
import { Checkbox } from "@/components/ui/checkbox";

export function CheckboxRadiusDemo() {
  return (
    <div className="flex flex-col gap-5">
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox radius="none" />
        <span>Sharp Corners</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox radius="sm" />
        <span>Subtle Rounding</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox radius="default" />
        <span>Standard Appearance</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox radius="lg" />
        <span>Softer Edges</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox radius="full" />
        <span>Completely Rounded</span>
      </label>
    </div>
  );
}
```

#### Custom Icons

Pass `children` to `Checkbox` to replace the default animated checkmark with any icon.

```tsx
import { Checkbox } from "@/components/ui/checkbox";
import { CheckIcon, Map, Settings } from "lucide-react";

export function CheckboxIconsDemo() {
  return (
    <div className="flex flex-col gap-5">
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox size="lg">
          <CheckIcon />
        </Checkbox>
        <span>Make a choice</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox size="lg">
          <Map />
        </Checkbox>
        <span>Would you like to visit?</span>
      </label>
      <label className="flex items-center gap-2 cursor-pointer">
        <Checkbox size="lg">
          <Settings />
        </Checkbox>
        <span>Would you like to configure?</span>
      </label>
    </div>
  );
}
```

#### Disabled

```tsx
import { Checkbox } from "@/components/ui/checkbox";

export function CheckboxDisabledDemo() {
  return (
    <label className="flex items-center gap-2 cursor-pointer">
      <Checkbox disabled />
    </label>
  );
}
```

#### Composable Usage

Use `CheckboxRoot` and `CheckboxIndicator` separately when you need to insert additional content or customise the indicator placement.

```tsx
import { CheckboxRoot, CheckboxIndicator } from "@/components/ui/checkbox";

export function CheckboxComposableDemo() {
  return (
    <CheckboxRoot size="lg" radius="full">
      <CheckboxIndicator />
    </CheckboxRoot>
  );
}
```

### Notes

- The default check icon uses an animated `stroke-dashoffset` SVG for a draw-on effect. Set `reduceMotion` to disable this animation.
- When `indeterminate` is `true`, the indicator displays a horizontal line instead of a checkmark. The checkbox will not toggle on click unless an `onCheckedChange` handler is provided.
- Wrap the checkbox in a `label` element to associate it with descriptive text and improve accessibility.
- Base UI's `render` prop is the equivalent of Radix UI's `asChild` for polymorphic rendering.
