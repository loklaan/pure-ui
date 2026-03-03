## Input OTP

Accessible one-time password input with copy-paste support. Renders a row of individual digit slots with animated transitions between values and an animated active-slot indicator.

Built on the `input-otp` library and `motion/react` for animations.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/input-otp"
```

#### Manual

1. Install dependencies:

```bash
npm install tailwind-variants clsx tailwind-merge input-otp motion
pnpm add tailwind-variants clsx tailwind-merge input-otp motion
yarn add tailwind-variants clsx tailwind-merge input-otp motion
bun add tailwind-variants clsx tailwind-merge input-otp motion
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/input-otp.tsx`.

### Anatomy

```tsx
import {
  InputOTP,
  InputOTPGroup,
  InputOTPSlot,
  InputOTPSeparator,
} from "@/components/ui/input-otp";

<InputOTP maxLength={6}>
  <InputOTPGroup>
    <InputOTPSlot index={0} />
    <InputOTPSlot index={1} />
    <InputOTPSlot index={2} />
  </InputOTPGroup>
  <InputOTPSeparator />
  <InputOTPGroup>
    <InputOTPSlot index={3} />
    <InputOTPSlot index={4} />
    <InputOTPSlot index={5} />
  </InputOTPGroup>
</InputOTP>
```

### Props

#### InputOTP

Accepts all props from the `OTPInput` component in the `input-otp` library, plus the following:

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| maxLength | number | -- | Total number of OTP digits (required) |
| variant | "bordered" \| "underlined" | "bordered" | Visual style of the slots |
| slotSize | "sm" \| "md" \| "lg" | "md" | Size of each digit slot |
| pattern | string | -- | Regular expression string restricting allowed input characters |
| value | string | -- | Controlled OTP value |
| onChange | (value: string) => void | -- | Callback fired when the value changes |
| disabled | boolean | false | Disables all slots |
| containerClassName | string | -- | Class name applied to the outer container div |

#### InputOTPSlot

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| index | number | -- | Zero-based position of this slot in the OTP sequence (required) |

#### InputOTPGroup

Renders a `div` wrapper. Accepts standard `div` props.

#### InputOTPSeparator

Renders a visual dash between groups. Accepts standard `div` props. Includes `aria-hidden` by default.

### Variants

#### variant

Values: `"bordered"` | `"underlined"`
Default: `"bordered"`

The `bordered` variant renders each slot with a rounded border on all sides. The `underlined` variant renders only a bottom border.

```tsx
<InputOTP maxLength={6} variant="underlined">
  <InputOTPGroup>
    <InputOTPSlot index={0} />
    <InputOTPSlot index={1} />
    <InputOTPSlot index={2} />
    <InputOTPSlot index={3} />
    <InputOTPSlot index={4} />
    <InputOTPSlot index={5} />
  </InputOTPGroup>
</InputOTP>
```

#### slotSize

Values: `"sm"` | `"md"` | `"lg"`
Default: `"md"`

```tsx
<InputOTP maxLength={6} slotSize="lg">
  <InputOTPGroup>
    <InputOTPSlot index={0} />
    <InputOTPSlot index={1} />
    <InputOTPSlot index={2} />
    <InputOTPSlot index={3} />
    <InputOTPSlot index={4} />
    <InputOTPSlot index={5} />
  </InputOTPGroup>
</InputOTP>
```

### Usage

#### Basic

```tsx
import {
  InputOTP,
  InputOTPGroup,
  InputOTPSlot,
} from "@/components/ui/input-otp";

export function InputOTPBasic() {
  return (
    <InputOTP maxLength={6}>
      <InputOTPGroup>
        <InputOTPSlot index={0} />
        <InputOTPSlot index={1} />
        <InputOTPSlot index={2} />
        <InputOTPSlot index={3} />
        <InputOTPSlot index={4} />
        <InputOTPSlot index={5} />
      </InputOTPGroup>
    </InputOTP>
  );
}
```

#### With Separator

Use `InputOTPSeparator` between groups to add a visual dash.

```tsx
import {
  InputOTP,
  InputOTPGroup,
  InputOTPSlot,
  InputOTPSeparator,
} from "@/components/ui/input-otp";

export function InputOTPWithSeparator() {
  return (
    <InputOTP maxLength={6}>
      <InputOTPGroup>
        <InputOTPSlot index={0} />
        <InputOTPSlot index={1} />
        <InputOTPSlot index={2} />
      </InputOTPGroup>
      <InputOTPSeparator />
      <InputOTPGroup>
        <InputOTPSlot index={3} />
        <InputOTPSlot index={4} />
        <InputOTPSlot index={5} />
      </InputOTPGroup>
    </InputOTP>
  );
}
```

#### Pattern Restriction

Use the `pattern` prop to restrict input to characters matching a regular expression.

```tsx
import {
  InputOTP,
  InputOTPGroup,
  InputOTPSlot,
} from "@/components/ui/input-otp";

export function InputOTPNumericOnly() {
  return (
    <InputOTP maxLength={6} pattern="^[0-9]*$">
      <InputOTPGroup>
        <InputOTPSlot index={0} />
        <InputOTPSlot index={1} />
        <InputOTPSlot index={2} />
        <InputOTPSlot index={3} />
        <InputOTPSlot index={4} />
        <InputOTPSlot index={5} />
      </InputOTPGroup>
    </InputOTP>
  );
}
```

#### Controlled

Use `value` and `onChange` to control the OTP state.

```tsx
"use client";

import { useState } from "react";
import {
  InputOTP,
  InputOTPGroup,
  InputOTPSlot,
} from "@/components/ui/input-otp";

export function InputOTPControlled() {
  const [value, setValue] = useState("");

  return (
    <div className="flex flex-col gap-3">
      <InputOTP maxLength={6} value={value} onChange={setValue}>
        <InputOTPGroup>
          <InputOTPSlot index={0} />
          <InputOTPSlot index={1} />
          <InputOTPSlot index={2} />
          <InputOTPSlot index={3} />
          <InputOTPSlot index={4} />
          <InputOTPSlot index={5} />
        </InputOTPGroup>
      </InputOTP>

      <p className="text-sm text-muted-foreground">
        Value: <span className="font-semibold">{value}</span>
      </p>
    </div>
  );
}
```

#### Disabled

Pass `disabled` to prevent interaction with all slots.

```tsx
import {
  InputOTP,
  InputOTPGroup,
  InputOTPSlot,
  InputOTPSeparator,
} from "@/components/ui/input-otp";

export function InputOTPDisabled() {
  return (
    <InputOTP maxLength={6} disabled>
      <InputOTPGroup>
        <InputOTPSlot index={0} />
        <InputOTPSlot index={1} />
        <InputOTPSlot index={2} />
      </InputOTPGroup>
      <InputOTPSeparator />
      <InputOTPGroup>
        <InputOTPSlot index={3} />
        <InputOTPSlot index={4} />
        <InputOTPSlot index={5} />
      </InputOTPGroup>
    </InputOTP>
  );
}
```

### Notes

- The component exports a `useInputOTPContext` hook that provides access to the current `variant` and `slotSize` values from the nearest `InputOTP` parent.
- Digit entry is animated using `motion/react`. The `MotionConfig` wrapper on each slot sets `reducedMotion="user"`, so animations are automatically disabled when the user has enabled reduced motion in their OS settings.
- The active slot indicator uses `layoutId` from `motion/react` to animate smoothly between slots as the user types.
- Copy-paste of full OTP codes is supported by the underlying `input-otp` library.
- Each `InputOTPSlot` must receive an `index` prop matching its zero-based position across all groups. For a 6-digit OTP split into two groups of three, the first group uses indices 0-2 and the second uses 3-5.
