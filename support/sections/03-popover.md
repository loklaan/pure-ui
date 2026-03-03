## Popover

An accessible popup anchored to a trigger element. Use it to display supplementary content, forms, or interactive controls without navigating away from the current page.

Built on `@base-ui/react/popover`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/popover"
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

3. Copy the component source into your project at `components/ui/popover.tsx`.

### Anatomy

```tsx
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
  PopoverViewport,
  PopoverTitle,
  PopoverDescription,
} from "@/components/ui/popover";

<Popover>
  <PopoverTrigger>Open</PopoverTrigger>
  <PopoverPopup>
    <PopoverTitle>Title</PopoverTitle>
    <PopoverDescription>Description text</PopoverDescription>
  </PopoverPopup>
</Popover>
```

`PopoverViewport` is also exported for use when you need to wrap the popup content in a scrollable viewport.

### Props

#### Popover

Root wrapper that provides context to all child components. Accepts all props from `@base-ui/react/popover` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| open | boolean | -- | Controlled open state |
| onOpenChange | (open: boolean) => void | -- | Called when the open state changes |
| modal | boolean \| "trap-focus" | true | Controls focus trapping, scroll locking, and outside interaction |
| backdrop | "opaque" \| "blur" \| "transparent" | "transparent" | Backdrop style shown behind the popover |

#### PopoverTrigger

Element that opens the popover. Accepts all props from `@base-ui/react/popover` Trigger.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| render | React.ReactElement | -- | Renders the trigger as a different element (Base UI's equivalent of `asChild`) |
| openOnHover | boolean | false | Opens the popover when the trigger is hovered instead of clicked |
| delay | number | 100 | Delay in milliseconds before opening on hover (only used when `openOnHover` is true) |
| closeDelay | number | 0 | Delay in milliseconds before closing after hover ends (only used when `openOnHover` is true) |

#### PopoverPopup

Popup content panel. Wraps the Base UI Popup inside a Positioner and Portal automatically. Accepts all props from `@base-ui/react/popover` Popup plus positioning and animation props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| side | "top" \| "right" \| "bottom" \| "left" \| "inline-start" \| "inline-end" | "bottom" | Side of the trigger where the popup appears |
| sideOffset | number | 4 | Distance in pixels between the popup and the trigger |
| align | "start" \| "center" \| "end" | "center" | Alignment of the popup relative to the trigger |
| alignOffset | number | 0 | Offset in pixels for the alignment |
| animationPreset | "none" \| "scale" \| "fade" \| "slideOutside" \| "slideInside" \| "wipe" \| "wipeScale" \| "motion" \| "motionBlur" | "scale" | CSS animation applied when the popup opens and closes |
| transitionPreset | string | "snappyOut" | Easing curve for the animation (see Transition Presets below) |
| reduceMotion | boolean | false | Disables all animations |
| showArrow | boolean | false | Displays an arrow pointing from the popup to the trigger |

#### PopoverViewport

Scrollable viewport wrapper for popup content. Accepts all props from `@base-ui/react/popover` Viewport.

#### PopoverTitle

Title element rendered inside the popup. Accepts all props from `@base-ui/react/popover` Title.

#### PopoverDescription

Description text rendered inside the popup. Accepts all props from `@base-ui/react/popover` Description.

### Variants

#### animationPreset

Values: `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"`
Default: `"scale"`

Controls the CSS animation applied when the popover opens and closes. The `slideOutside`, `slideInside`, `wipe`, `wipeScale`, `motion`, and `motionBlur` presets are side-aware -- the animation direction adjusts based on the `side` prop.

```tsx
<PopoverPopup animationPreset="fade">
  ...
</PopoverPopup>
```

```tsx
<PopoverPopup animationPreset="slideOutside">
  ...
</PopoverPopup>
```

```tsx
<PopoverPopup animationPreset="motion">
  ...
</PopoverPopup>
```

#### transitionPreset

24 named easing curves that control the timing of the popup animation. Set on `PopoverPopup`.

Default: `"snappyOut"`

Available values: `"inExpo"`, `"outExpo"`, `"inOutExpo"`, `"anticipate"`, `"quickOut"`, `"overshootOut"`, `"swiftOut"`, `"snappyOut"`, `"in"`, `"out"`, `"inOut"`, `"outIn"`, `"inQuad"`, `"outQuad"`, `"inOutQuad"`, `"inCubic"`, `"outCubic"`, `"inOutCubic"`, `"inQuart"`, `"outQuart"`, `"inOutQuart"`, `"inQuint"`, `"outQuint"`, `"inOutQuint"`, `"inCirc"`, `"outCirc"`, `"inOutCirc"`, `"inOutBase"`

```tsx
<PopoverPopup transitionPreset="outCubic">
  ...
</PopoverPopup>
```

#### backdrop

Values: `"opaque"` | `"blur"` | `"transparent"`
Default: `"transparent"`

Set on the `Popover` root to control the backdrop displayed behind the popover when open.

- `"transparent"` -- no visible backdrop
- `"opaque"` -- semi-transparent dark overlay
- `"blur"` -- blurred backdrop

```tsx
<Popover backdrop="blur">
  <PopoverTrigger>Open</PopoverTrigger>
  <PopoverPopup>Content</PopoverPopup>
</Popover>
```

### Usage

#### Basic

```tsx
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
  PopoverTitle,
  PopoverDescription,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export function PopoverDemo() {
  return (
    <Popover>
      <PopoverTrigger render={<Button variant="default" size="sm" />}>
        <span>Open Popover</span>
      </PopoverTrigger>
      <PopoverPopup className="min-w-70">
        <div className="mb-4">
          <PopoverTitle className="text-base">
            Subscribe to our newsletter
          </PopoverTitle>
          <PopoverDescription>
            Get weekly updates, new product announcements, and exclusive offers
            delivered to your inbox.
          </PopoverDescription>
        </div>
        <div className="flex flex-col gap-2">
          <Input placeholder="Enter your email" type="email" />
          <Button className="w-full" variant="default">
            Submit
          </Button>
        </div>
      </PopoverPopup>
    </Popover>
  );
}
```

#### With Arrow

Set `showArrow` on `PopoverPopup` to display an arrow pointing from the popup to the trigger. When using an arrow, set `sideOffset` to at least 8 to prevent the arrow from overlapping the trigger.

```tsx
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
  PopoverTitle,
  PopoverDescription,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";

export function PopoverWithArrowDemo() {
  return (
    <Popover>
      <PopoverTrigger render={<Button variant="outline" size="icon" />}>
        Notifications
      </PopoverTrigger>
      <PopoverPopup showArrow sideOffset={8}>
        <PopoverTitle>Notifications</PopoverTitle>
        <PopoverDescription>
          You are all caught up. Good job!
        </PopoverDescription>
      </PopoverPopup>
    </Popover>
  );
}
```

#### Sides

Set `side` on `PopoverPopup` to control which side of the trigger the popup appears on.

```tsx
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
  PopoverDescription,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";

export function PopoverSidesDemo() {
  return (
    <Popover>
      <PopoverTrigger render={<Button size="sm" />}>
        Open Right
      </PopoverTrigger>
      <PopoverPopup showArrow side="right" sideOffset={8}>
        <PopoverDescription>This popover opens to the right.</PopoverDescription>
      </PopoverPopup>
    </Popover>
  );
}
```

#### Offset

Set `sideOffset` on `PopoverPopup` to control the distance between the popup and the trigger.

```tsx
<PopoverPopup sideOffset={20} side="right">
  ...
</PopoverPopup>
```

#### Open on Hover

Set `openOnHover` on `PopoverTrigger` to open the popover when the trigger is hovered instead of clicked. Use `delay` and `closeDelay` to control hover timing.

```tsx
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
  PopoverDescription,
} from "@/components/ui/popover";

export function PopoverHoverDemo() {
  return (
    <Popover>
      <PopoverTrigger openOnHover>
        Hover me
      </PopoverTrigger>
      <PopoverPopup>
        <PopoverDescription>Opened on hover</PopoverDescription>
      </PopoverPopup>
    </Popover>
  );
}
```

To customise hover timing:

```tsx
<PopoverTrigger openOnHover delay={200} closeDelay={200}>
  Hover me
</PopoverTrigger>
```

#### Controlled

Use `open` and `onOpenChange` props on the `Popover` root to control the popover state externally.

```tsx
"use client";

import { useState } from "react";
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export function PopoverControlledDemo() {
  const [open, setOpen] = useState(false);

  return (
    <Popover open={open} onOpenChange={setOpen}>
      <PopoverTrigger render={<Button size="sm" />}>
        <span>Open Popover</span>
      </PopoverTrigger>
      <PopoverPopup>
        <div className="flex flex-col gap-2">
          <Input placeholder="Your Email" />
          <Button
            className="w-full"
            size="sm"
            onClick={() => setOpen(false)}
          >
            Submit
          </Button>
        </div>
      </PopoverPopup>
    </Popover>
  );
}
```

#### Modality

The `modal` prop on `Popover` controls how users interact with the page when the popover is open.

- `modal={true}` (default) -- focus is trapped, scrolling is locked, and outside interactions are disabled.
- `modal={false}` -- users can interact with both the popover and the rest of the page freely.
- `modal="trap-focus"` -- focus is trapped for keyboard navigation, but scrolling and outside pointer interactions remain enabled.

```tsx
<Popover modal={false}>
  <PopoverTrigger>Open</PopoverTrigger>
  <PopoverPopup>Non-modal content</PopoverPopup>
</Popover>
```

```tsx
<Popover modal="trap-focus">
  <PopoverTrigger>Open</PopoverTrigger>
  <PopoverPopup>Focus-trapped content</PopoverPopup>
</Popover>
```

#### Backdrop

Set `backdrop` on the `Popover` root to display a backdrop behind the popover.

```tsx
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";

export function PopoverBackdropDemo() {
  return (
    <Popover backdrop="blur">
      <PopoverTrigger render={<Button size="sm" variant="outline" />}>
        Open with Blur
      </PopoverTrigger>
      <PopoverPopup showArrow sideOffset={8}>
        Content behind a blurred backdrop.
      </PopoverPopup>
    </Popover>
  );
}
```

#### With Form

Combine controlled state with form elements inside the popover to close it programmatically after submission.

```tsx
"use client";

import { useState, useTransition } from "react";
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export function PopoverWithFormDemo() {
  const [open, setOpen] = useState(false);
  const [isSubmitting, startSubmitting] = useTransition();

  const handleSubmit = () => {
    startSubmitting(async () => {
      await new Promise((resolve) => setTimeout(resolve, 2000));
      setOpen(false);
    });
  };

  return (
    <Popover open={open} onOpenChange={setOpen}>
      <PopoverTrigger render={<Button size="sm" variant="outline" />}>
        <span>Customize</span>
      </PopoverTrigger>
      <PopoverPopup>
        <div className="flex flex-col gap-2">
          <Input defaultValue="100%" size="sm" />
          <Input defaultValue="300px" size="sm" />
          <Button
            className="w-full"
            size="sm"
            onClick={handleSubmit}
            disabled={isSubmitting}
          >
            Submit
          </Button>
        </div>
      </PopoverPopup>
    </Popover>
  );
}
```

#### Custom Trigger

Use the `render` prop on `PopoverTrigger` to render the trigger as any element. This example combines `render` with `openOnHover` to show a user profile card on hover.

```tsx
"use client";

import { useState } from "react";
import {
  Popover,
  PopoverTrigger,
  PopoverPopup,
} from "@/components/ui/popover";
import { Button } from "@/components/ui/button";
import {
  Card,
  CardContent,
  CardFooter,
  CardHeader,
} from "@/components/ui/card";

export function PopoverCustomTriggerDemo() {
  const [isFollowing, setIsFollowing] = useState(false);

  return (
    <Popover>
      <PopoverTrigger
        openOnHover
        render={<button className="flex items-center gap-2 cursor-pointer" />}
      >
        <img
          src="https://example.com/avatar.jpg"
          alt="Avatar"
          className="size-8 rounded-full"
        />
        <div className="flex flex-col items-start">
          <span className="text-sm font-medium">User Name</span>
          <span className="text-xs text-foreground/70">Description</span>
        </div>
      </PopoverTrigger>
      <PopoverPopup>
        <Card className="min-w-[260px] border-none p-1 shadow-none!">
          <CardHeader className="justify-between flex flex-row">
            <div className="flex gap-3">
              <img
                className="size-8 rounded-full"
                src="https://example.com/avatar.jpg"
              />
              <div className="flex flex-col items-start justify-center">
                <h4 className="text-sm font-semibold leading-none">User Name</h4>
                <h5 className="text-xs tracking-tight text-foreground/70">@username</h5>
              </div>
            </div>
            <Button
              size="sm"
              radius="full"
              variant={isFollowing ? "outline" : "default"}
              onClick={() => setIsFollowing(!isFollowing)}
            >
              {isFollowing ? "Unfollow" : "Follow"}
            </Button>
          </CardHeader>
          <CardContent className="py-0">
            <p className="text-xs text-foreground/70">User bio text here.</p>
          </CardContent>
          <CardFooter className="gap-3">
            <div className="flex gap-1">
              <p className="font-semibold text-sm">570</p>
              <p className="text-foreground/70 text-sm">Following</p>
            </div>
            <div className="flex gap-1">
              <p className="font-semibold text-sm">210K</p>
              <p className="text-foreground/70 text-sm">Followers</p>
            </div>
          </CardFooter>
        </Card>
      </PopoverPopup>
    </Popover>
  );
}
```

### Notes

- The `render` prop on `PopoverTrigger` is Base UI's equivalent of Radix UI's `asChild` for polymorphic rendering.
- When `showArrow` is true, set `sideOffset` to at least 8 to prevent the arrow from overlapping the trigger.
- The arrow is hidden automatically when `side` is set to `"inline-start"` or `"inline-end"`.
- The `delay` and `closeDelay` props on `PopoverTrigger` only take effect when `openOnHover` is true.
- The default popup width is `w-72` (18rem). Override it by passing a `className` with a width utility to `PopoverPopup`.
