## Number Field

A numeric input element with increment and decrement buttons. Supports min/max range constraints, custom step values, value formatting, controlled state, and a scrub area for drag-to-change interaction.

Built on `@base-ui/react/number-field`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/number-field"
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

3. Copy the component source into your project at `components/ui/number-field.tsx`.

### Anatomy

```tsx
import {
  NumberField,
  NumberFieldGroup,
  NumberFieldInput,
  NumberFieldDecrement,
  NumberFieldIncrement,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";

<NumberField>
  <NumberFieldScrubArea>
    <Label>Label text</Label>
  </NumberFieldScrubArea>
  <NumberFieldGroup>
    <NumberFieldDecrement />
    <NumberFieldInput />
    <NumberFieldIncrement />
  </NumberFieldGroup>
</NumberField>
```

`NumberFieldScrubArea` is optional. The minimal anatomy is:

```tsx
<NumberField>
  <NumberFieldGroup>
    <NumberFieldDecrement />
    <NumberFieldInput />
    <NumberFieldIncrement />
  </NumberFieldGroup>
</NumberField>
```

### Props

#### NumberField

Root wrapper. Accepts all props from `@base-ui/react/number-field` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| defaultValue | number | -- | Initial value (uncontrolled) |
| value | number \| null | -- | Controlled value |
| onValueChange | (value: number \| null, event?: Event) => void | -- | Called when the value changes |
| min | number | -- | Minimum allowed value |
| max | number | -- | Maximum allowed value |
| step | number | 1 | Increment/decrement step amount |
| format | Intl.NumberFormatOptions | -- | Number formatting options passed to `Intl.NumberFormat` |
| disabled | boolean | false | Disables the entire field |
| allowWheelScrub | boolean | false | Allows mouse wheel to change the value while the input is focused |
| id | string | -- | Associates the input with a label |

#### NumberFieldGroup

Container that wraps the input and increment/decrement buttons. Accepts all props from `@base-ui/react/number-field` Group.

#### NumberFieldInput

Numeric input element. Accepts all props from `@base-ui/react/number-field` Input.

#### NumberFieldDecrement

Decrement button. Renders a minus icon. Accepts all props from `@base-ui/react/number-field` Decrement.

#### NumberFieldIncrement

Increment button. Renders a plus icon. Accepts all props from `@base-ui/react/number-field` Increment.

#### NumberFieldScrubArea

Drag-to-change area. Wrap a label or other content inside it. Dragging horizontally over the scrub area changes the value. Renders a custom bidirectional arrow cursor during drag. Accepts all props from `@base-ui/react/number-field` ScrubArea.

### Usage

#### Basic

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
} from "@/components/ui/number-field";

export function NumberFieldDemo() {
  return (
    <NumberField defaultValue={0}>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

#### With Label and Scrub Area

Wrap a `Label` inside `NumberFieldScrubArea` to enable drag-to-change on the label text. Set `cursor-ew-resize` on the label for a visual affordance.

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";
import { Label } from "@/components/ui/label";

export function NumberFieldWithScrubDemo() {
  return (
    <NumberField defaultValue={0} id="quantity">
      <NumberFieldScrubArea>
        <Label htmlFor="quantity" className="cursor-ew-resize">
          Quantity
        </Label>
      </NumberFieldScrubArea>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

#### Mouse Wheel Scrub

Set `allowWheelScrub` on `NumberField` to let the user change the value with the mouse wheel while the input is focused.

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";
import { Label } from "@/components/ui/label";

export function NumberFieldMouseWheelScrubDemo() {
  return (
    <NumberField defaultValue={0} allowWheelScrub id="marks">
      <NumberFieldScrubArea>
        <Label htmlFor="marks" className="cursor-ew-resize">
          Marks
        </Label>
      </NumberFieldScrubArea>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

#### Controlled

Use `value` and `onValueChange` to control the field state.

```tsx
"use client";

import { useState } from "react";
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";
import { Label } from "@/components/ui/label";

export function NumberFieldControlledDemo() {
  const [value, setValue] = useState(0);

  return (
    <div className="flex flex-col gap-5">
      <NumberField
        value={value}
        onValueChange={(value) => setValue(value ?? 0)}
        id="controlled"
      >
        <NumberFieldScrubArea>
          <Label htmlFor="controlled" className="cursor-ew-resize">
            Controlled
          </Label>
        </NumberFieldScrubArea>
        <NumberFieldGroup>
          <NumberFieldDecrement />
          <NumberFieldInput />
          <NumberFieldIncrement />
        </NumberFieldGroup>
      </NumberField>

      <span className="text-muted-foreground px-1 text-sm">Value: {value}</span>
    </div>
  );
}
```

#### Range

Use `min` and `max` to constrain the allowed value range. The increment and decrement buttons automatically disable at the boundaries.

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";
import { Label } from "@/components/ui/label";

export function NumberFieldRangeDemo() {
  return (
    <NumberField defaultValue={10} min={5} max={25} id="range">
      <NumberFieldScrubArea>
        <Label htmlFor="range" className="cursor-ew-resize">
          Range
        </Label>
      </NumberFieldScrubArea>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

#### Step

Use `step` to set the increment/decrement amount per click or keyboard press.

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";
import { Label } from "@/components/ui/label";

export function NumberFieldStepDemo() {
  return (
    <NumberField defaultValue={0} step={20} id="step-20">
      <NumberFieldScrubArea>
        <Label htmlFor="step-20" className="cursor-ew-resize">
          Step 20
        </Label>
      </NumberFieldScrubArea>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

#### Formatting

Use the `format` prop to apply `Intl.NumberFormat` options such as currency display.

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
  NumberFieldScrubArea,
} from "@/components/ui/number-field";
import { Label } from "@/components/ui/label";

export function NumberFieldFormattingDemo() {
  return (
    <NumberField
      defaultValue={0}
      min={0}
      format={{ currency: "INR", style: "currency" }}
      id="price"
    >
      <NumberFieldScrubArea>
        <Label htmlFor="price" className="cursor-ew-resize">
          Price
        </Label>
      </NumberFieldScrubArea>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

#### Disabled

```tsx
import {
  NumberField,
  NumberFieldDecrement,
  NumberFieldGroup,
  NumberFieldIncrement,
  NumberFieldInput,
} from "@/components/ui/number-field";

export function NumberFieldDisabledDemo() {
  return (
    <NumberField defaultValue={0} disabled>
      <NumberFieldGroup>
        <NumberFieldDecrement />
        <NumberFieldInput />
        <NumberFieldIncrement />
      </NumberFieldGroup>
    </NumberField>
  );
}
```

### Notes

- The sub-components can be reordered within `NumberFieldGroup` to create different layouts (e.g., placing both buttons on one side, stacking buttons vertically). Use `className` overrides on `NumberFieldGroup` and wrapper `div` elements to adjust border radius when rearranging.
- `NumberFieldScrubArea` renders a custom bidirectional arrow cursor icon during drag interaction. Place a `Label` or other clickable content inside it.
- `className` on every sub-component is merged via `cn()`, so Tailwind classes can be appended or overridden.
- The `render` prop from Base UI can be used on sub-components to render as a different element.
