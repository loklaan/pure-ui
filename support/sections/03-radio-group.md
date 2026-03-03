## Radio Group

A set of checkable buttons where no more than one can be checked at a time. Use `RadioGroup` to wrap a set of `Radio` items, with optional labels for each option.

Built on `@base-ui/react/radio` and `@base-ui/react/radio-group`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/radio-group"
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

3. Copy the component source into your project at `components/ui/radio-group.tsx`.

### Anatomy

```tsx
import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";

<RadioGroup defaultValue="option-a">
  <Label>
    <Radio value="option-a" /> Option A
  </Label>
  <Label>
    <Radio value="option-b" /> Option B
  </Label>
</RadioGroup>
```

### Props

#### RadioGroup

Accepts all props from `@base-ui/react/radio-group`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| orientation | "horizontal" \| "vertical" | "vertical" | Layout direction of the radio items |
| defaultValue | any | -- | Initial selected value (uncontrolled) |
| value | any | -- | Controlled selected value |
| onValueChange | (value: any, event: Event) => void | -- | Called when the selected value changes |
| disabled | boolean | false | Disables all radio items in the group |

#### Radio

Accepts all props from `@base-ui/react/radio` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | any | -- | Value associated with this radio item |
| disabled | boolean | false | Disables this individual radio item |

The `Radio` component renders its own `RadioPrimitive.Indicator` inline. There is no separate indicator export.

### Variants

#### orientation

Values: `"horizontal"` | `"vertical"`
Default: `"vertical"`

```tsx
<RadioGroup orientation="horizontal">
  <Label><Radio value="a" /> A</Label>
  <Label><Radio value="b" /> B</Label>
</RadioGroup>
```

### Usage

#### Basic

```tsx
import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";

export function RadioGroupBasicDemo() {
  return (
    <RadioGroup defaultValue="light">
      <Label>
        <Radio value="light" /> Light Theme
      </Label>
      <Label>
        <Radio value="dark" /> Dark Theme
      </Label>
      <Label>
        <Radio value="system" /> System Default
      </Label>
    </RadioGroup>
  );
}
```

#### With Description

Compose a radio item with a description by placing the `Radio` and descriptive text inside a `Label`.

```tsx
import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";

export function RadioGroupWithDescriptionDemo() {
  return (
    <RadioGroup defaultValue="all">
      <Label className="flex items-start gap-2">
        <Radio value="all" />
        <div className="flex flex-col gap-1">
          <span className="font-medium">All Notifications</span>
          <span className="text-xs text-muted-foreground">
            Receive all notifications including system, marketing, and activity
            alerts.
          </span>
        </div>
      </Label>
      <Label className="flex items-start gap-2">
        <Radio value="mentions" />
        <div className="flex flex-col gap-1">
          <span className="font-medium">Only Mentions</span>
          <span className="text-xs text-muted-foreground">
            Get notified only when someone mentions you or replies to your
            posts.
          </span>
        </div>
      </Label>
      <Label className="flex items-start gap-2">
        <Radio value="none" />
        <div className="flex flex-col gap-1">
          <span className="font-medium">None</span>
          <span className="text-xs text-muted-foreground">
            Do not receive any notifications.
          </span>
        </div>
      </Label>
    </RadioGroup>
  );
}
```

#### Horizontal Orientation

Set `orientation="horizontal"` to lay out radio items in a row.

```tsx
import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";

export function RadioGroupOrientationDemo() {
  return (
    <div className="flex flex-col gap-4">
      <div className="text-sm font-medium">
        How would you rate your experience?
      </div>
      <RadioGroup orientation="horizontal">
        {[1, 2, 3, 4, 5].map((item) => (
          <Label key={item}>
            <Radio value={item} /> {item}
          </Label>
        ))}
      </RadioGroup>
    </div>
  );
}
```

#### Controlled

Use the `value` and `onValueChange` props to control the selected value.

```tsx
"use client";

import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";
import { useState } from "react";

export function RadioGroupControlledDemo() {
  const [value, setValue] = useState("virat");

  return (
    <div className="flex flex-col gap-4">
      <RadioGroup
        value={value}
        onValueChange={(value) => setValue(value as string)}
      >
        <div className="text-sm font-medium">
          Choose your favorite cricket player
        </div>
        <Label>
          <Radio value="virat" /> Virat Kohli
        </Label>
        <Label>
          <Radio value="rohit" /> Rohit Sharma
        </Label>
        <Label>
          <Radio value="sachin" /> Sachin Tendulkar
        </Label>
        <Label>
          <Radio value="dhoni" /> MS Dhoni
        </Label>
      </RadioGroup>

      <span className="text-muted-foreground px-1 text-sm">
        Selected Value: {value}
      </span>
    </div>
  );
}
```

#### Disabled

Disable individual radio items with the `disabled` prop on `Radio`. Disabled items cannot be selected and appear dimmed.

```tsx
import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";

export function RadioGroupDisabledDemo() {
  return (
    <RadioGroup defaultValue="dhoni">
      <div className="text-sm font-medium">
        Choose your favorite cricket player
      </div>
      <Label>
        <Radio value="virat" /> Virat Kohli
      </Label>
      <Label>
        <Radio value="rohit" disabled /> Rohit Sharma
      </Label>
      <Label>
        <Radio value="sachin" disabled /> Sachin Tendulkar
      </Label>
      <Label>
        <Radio value="dhoni" /> MS Dhoni
      </Label>
    </RadioGroup>
  );
}
```

#### Custom Layout

The `Radio` component can be positioned freely inside a `Label`. Combine it with card-style containers to build selection UIs.

```tsx
import { RadioGroup, Radio } from "@/components/ui/radio-group";
import { Label } from "@/components/ui/label";

export function RadioGroupCustomLayoutDemo() {
  return (
    <RadioGroup className="w-full" defaultValue="plan-pro">
      <Label className="relative border p-3 rounded-xl bg-card shadow-xs flex items-center gap-3 cursor-pointer has-data-checked:border-primary has-data-checked:ring-1 has-data-checked:ring-primary [transition-property:box-shadow,border-color] duration-200 ease-out">
        <span className="absolute -top-3 -right-2.5 p-0.5 bg-card rounded-full flex items-center justify-center">
          <Radio value="plan-pro" />
        </span>
        <div className="flex flex-col">
          <span className="font-medium">Pro Plan</span>
          <span className="text-muted-foreground text-sm">
            Full access to all features.
          </span>
        </div>
      </Label>
      <Label className="relative border p-3 rounded-xl bg-card shadow-xs flex items-center gap-3 cursor-pointer has-data-checked:border-primary has-data-checked:ring-1 has-data-checked:ring-primary [transition-property:box-shadow,border-color] duration-200 ease-out">
        <span className="absolute -top-3 -right-2.5 p-0.5 bg-card rounded-full flex items-center justify-center">
          <Radio value="plan-free" />
        </span>
        <div className="flex flex-col">
          <span className="font-medium">Free Plan</span>
          <span className="text-muted-foreground text-sm">
            Basic features with limited usage.
          </span>
        </div>
      </Label>
    </RadioGroup>
  );
}
```

### Notes

- The `Radio` component includes its indicator inline. There is no separate `RadioIndicator` export.
- The checked/unchecked indicator uses a CSS pseudo-element animation (scale and opacity transitions).
- Wrap each `Radio` in a `Label` component (from `@/components/ui/label`) to associate it with text and improve accessibility. The `has-data-checked` CSS selector on labels enables styling the parent based on the radio's checked state.
- Base UI's `render` prop is the equivalent of Radix UI's `asChild` for polymorphic rendering.
