## Dialog

A popup that opens on top of the entire page. Use it for confirmations, forms, or focused tasks that require user attention before returning to the main content.

Built on `@base-ui/react/dialog`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/dialog"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge @base-ui/react lucide-react
pnpm add clsx tailwind-merge @base-ui/react lucide-react
yarn add clsx tailwind-merge @base-ui/react lucide-react
bun add clsx tailwind-merge @base-ui/react lucide-react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/dialog.tsx`.

### Anatomy

```tsx
import {
  Dialog,
  DialogTrigger,
  DialogPopup,
  DialogHeader,
  DialogTitle,
  DialogDescription,
  DialogFooter,
  DialogClose,
} from "@/components/ui/dialog";

<Dialog>
  <DialogTrigger>Open</DialogTrigger>
  <DialogPopup>
    <DialogHeader>
      <DialogTitle>Title</DialogTitle>
      <DialogDescription>Description</DialogDescription>
    </DialogHeader>
    <DialogFooter>
      <DialogClose>Close</DialogClose>
    </DialogFooter>
  </DialogPopup>
</Dialog>
```

`DialogBackdrop`, `DialogPortal`, and `DialogViewport` are also exported but are rendered automatically by `DialogPopup`. Use them directly only when building a custom dialog layout.

### Props

#### Dialog

Root wrapper that provides context and manages open/close state. Accepts all props from `@base-ui/react/dialog` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| open | boolean | -- | Controlled open state |
| onOpenChange | (open: boolean) => void | -- | Called when the open state changes |
| modal | boolean \| "trap-focus" | true | Controls focus trapping, scroll locking, and outside interaction |
| disablePointerDismissal | boolean | false | Prevents closing the dialog by clicking outside |

#### DialogTrigger

Element that opens the dialog. Accepts all props from `@base-ui/react/dialog` Trigger. Use the `render` prop to render as a different element.

#### DialogPopup

Dialog content panel. Automatically renders a `DialogPortal`, `DialogBackdrop` (when modal), and a close button.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| animationPreset | "none" \| "scale" \| "fade" \| "topFlip" \| "bottomFlip" \| "rightFlip" \| "leftFlip" \| "topSlide" \| "bottomSlide" \| "leftSlide" \| "rightSlide" \| "wipe" | "scale" | CSS animation applied when the dialog opens and closes |
| transitionPreset | string | "outCubic" | Easing curve for the animation (see Transition Presets below) |
| reduceMotion | boolean | false | Disables all animations |
| showCloseButton | boolean | true | Shows an X button in the top-right corner |

#### DialogHeader

Plain `div` for grouping the title and description at the top of the dialog. Accepts standard `div` props.

#### DialogFooter

Plain `div` for action buttons at the bottom of the dialog. Accepts standard `div` props.

#### DialogTitle

Title element for the dialog. Accepts all props from `@base-ui/react/dialog` Title.

#### DialogDescription

Description element for the dialog. Accepts all props from `@base-ui/react/dialog` Description.

#### DialogClose

Close button primitive. Accepts all props from `@base-ui/react/dialog` Close. Use the `render` prop to render as a different element.

#### DialogBackdrop

Overlay backdrop behind the dialog. Accepts all props from `@base-ui/react/dialog` Backdrop. Rendered automatically by `DialogPopup` when `modal` is `true`.

#### DialogPortal

Portal wrapper. Accepts all props from `@base-ui/react/dialog` Portal. Rendered automatically by `DialogPopup`.

#### DialogViewport

Viewport container. Accepts all props from `@base-ui/react/dialog` Viewport.

### Variants

#### animationPreset

Values: `"none"` | `"scale"` | `"fade"` | `"topFlip"` | `"bottomFlip"` | `"rightFlip"` | `"leftFlip"` | `"topSlide"` | `"bottomSlide"` | `"leftSlide"` | `"rightSlide"` | `"wipe"`
Default: `"scale"`

Controls the CSS animation applied when the dialog opens and closes.

- `"none"` -- no animation
- `"scale"` -- scales up from 98% while fading in
- `"fade"` -- opacity transition
- `"topFlip"` -- 3D rotation from the top with blur
- `"bottomFlip"` -- 3D rotation from the bottom with blur
- `"rightFlip"` -- 3D rotation from the right with blur
- `"leftFlip"` -- 3D rotation from the left with blur
- `"topSlide"` -- slides in from above
- `"bottomSlide"` -- slides in from below
- `"leftSlide"` -- slides in from the left
- `"rightSlide"` -- slides in from the right
- `"wipe"` -- clip-path wipe reveal from top to bottom

```tsx
<DialogPopup animationPreset="fade">
  ...
</DialogPopup>
```

```tsx
<DialogPopup animationPreset="topFlip">
  ...
</DialogPopup>
```

```tsx
<DialogPopup animationPreset="wipe">
  ...
</DialogPopup>
```

#### transitionPreset

24 named easing curves that control the timing of the dialog animation. Set on `DialogPopup`.

Default: `"outCubic"`

Available values: `"inExpo"`, `"outExpo"`, `"inOutExpo"`, `"anticipate"`, `"quickOut"`, `"overshootOut"`, `"swiftOut"`, `"snappyOut"`, `"in"`, `"out"`, `"inOut"`, `"outIn"`, `"inQuad"`, `"outQuad"`, `"inOutQuad"`, `"inCubic"`, `"outCubic"`, `"inOutCubic"`, `"inQuart"`, `"outQuart"`, `"inOutQuart"`, `"inQuint"`, `"outQuint"`, `"inOutQuint"`, `"inCirc"`, `"outCirc"`, `"inOutCirc"`, `"inOutBase"`

```tsx
<DialogPopup transitionPreset="snappyOut">
  ...
</DialogPopup>
```

### Usage

#### Basic

```tsx
import {
  Dialog,
  DialogPopup,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
  DialogClose,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

export function DialogDemo() {
  return (
    <Dialog>
      <DialogTrigger render={<Button variant="outline" />}>
        Edit profile
      </DialogTrigger>
      <DialogPopup className="sm:max-w-sm">
        <DialogHeader>
          <DialogTitle>Edit profile</DialogTitle>
          <DialogDescription>
            Make changes to your profile here. Click save when you're done.
          </DialogDescription>
        </DialogHeader>
        <div className="flex flex-col gap-4">
          <div>
            <Label>Name</Label>
            <Input type="text" defaultValue="Krishna" />
          </div>
          <div>
            <Label>Username</Label>
            <Input type="text" defaultValue="@krishna" />
          </div>
        </div>
        <DialogFooter>
          <DialogClose render={<Button variant="ghost" />}>Cancel</DialogClose>
          <Button type="submit">Save</Button>
        </DialogFooter>
      </DialogPopup>
    </Dialog>
  );
}
```

#### Controlled

Use `open` and `onOpenChange` props to control the dialog state. This is useful for closing the dialog programmatically, such as after a form submission.

```tsx
"use client";

import { useState, useTransition } from "react";
import {
  Dialog,
  DialogPopup,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
  DialogClose,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

export function DialogControlledDemo() {
  const [open, setOpen] = useState(false);
  const [isSubmitting, startSubmitting] = useTransition();

  const handleSubmit = async () => {
    startSubmitting(async () => {
      await submitData();
      setOpen(false);
    });
  };

  return (
    <Dialog open={open} onOpenChange={setOpen}>
      <DialogTrigger render={<Button variant="outline" />}>
        Edit profile
      </DialogTrigger>
      <DialogPopup className="sm:max-w-sm">
        <form
          onSubmit={(e) => {
            e.preventDefault();
            handleSubmit();
          }}
        >
          <DialogHeader>
            <DialogTitle>Edit profile</DialogTitle>
            <DialogDescription>
              Make changes to your profile here. Click save when you're done.
            </DialogDescription>
          </DialogHeader>
          <div className="flex flex-col gap-4">
            <div>
              <Label>Name</Label>
              <Input type="text" defaultValue="Krishna" />
            </div>
            <div>
              <Label>Username</Label>
              <Input type="text" defaultValue="@krishna" />
            </div>
          </div>
          <DialogFooter>
            <DialogClose render={<Button variant="ghost" />}>
              Cancel
            </DialogClose>
            <Button type="submit" disabled={isSubmitting}>
              Save
            </Button>
          </DialogFooter>
        </form>
      </DialogPopup>
    </Dialog>
  );
}
```

#### Non-Dismissible

Set `disablePointerDismissal` on the `Dialog` root to prevent closing the dialog by clicking outside.

```tsx
import {
  Dialog,
  DialogPopup,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";

export function DialogNonDismissibleDemo() {
  return (
    <Dialog disablePointerDismissal={true}>
      <DialogTrigger render={<Button />}>Open</DialogTrigger>
      <DialogPopup>
        <DialogHeader>
          <DialogTitle>Terms of Service</DialogTitle>
          <DialogDescription>
            Please read the following terms of service carefully.
          </DialogDescription>
        </DialogHeader>
        <DialogFooter>
          <Button variant="outline">Decline</Button>
          <Button type="submit">Accept</Button>
        </DialogFooter>
      </DialogPopup>
    </Dialog>
  );
}
```

#### Non-Modal

The `modal` prop controls how users interact with the page while the dialog is open.

- `modal={true}` (default) -- focus is trapped, scrolling is locked, and outside interactions are disabled.
- `modal={false}` -- users can interact with both the dialog and the rest of the page freely. The backdrop is hidden.
- `modal="trap-focus"` -- focus is trapped for keyboard navigation, but scrolling and outside pointer interactions remain enabled.

```tsx
import {
  Dialog,
  DialogPopup,
  DialogHeader,
  DialogTitle,
  DialogDescription,
  DialogTrigger,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";

export function DialogNonModalDemo() {
  return (
    <Dialog modal={false}>
      <DialogTrigger render={<Button />}>Open</DialogTrigger>
      <DialogPopup>
        <DialogHeader>
          <DialogTitle>Non-modal dialog</DialogTitle>
          <DialogDescription>
            You can still interact with the page behind this dialog.
          </DialogDescription>
        </DialogHeader>
      </DialogPopup>
    </Dialog>
  );
}
```

#### Nested Dialogs

Nest `Dialog` components inside each other. The parent dialog scales down and shifts when a child dialog opens. Use `showCloseButton={false}` on nested popups to keep the close button only on the innermost dialog.

```tsx
import {
  Dialog,
  DialogPopup,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
  DialogClose,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

export function DialogNestedDemo() {
  return (
    <Dialog>
      <DialogTrigger render={<Button />}>View details</DialogTrigger>
      <DialogPopup showCloseButton={false}>
        <DialogHeader>
          <DialogTitle>Manage team member</DialogTitle>
          <DialogDescription>
            View and manage a user in your team.
          </DialogDescription>
        </DialogHeader>
        <DialogFooter>
          <Dialog>
            <DialogTrigger render={<Button variant="outline" />}>
              Edit details
            </DialogTrigger>
            <DialogPopup showCloseButton={false}>
              <DialogHeader>
                <DialogTitle>Edit details</DialogTitle>
                <DialogDescription>
                  Make changes to the member's information.
                </DialogDescription>
              </DialogHeader>
              <div className="flex flex-col gap-4">
                <div className="flex flex-col gap-1">
                  <Label htmlFor="input-name">Name</Label>
                  <Input id="input-name" placeholder="Krishna" type="text" />
                </div>
                <div className="flex flex-col gap-1">
                  <Label htmlFor="input-email">Email</Label>
                  <Input
                    id="input-email"
                    placeholder="krishna@example.com"
                    type="text"
                  />
                </div>
              </div>
              <DialogFooter>
                <DialogClose render={<Button variant="ghost" />}>
                  Cancel
                </DialogClose>
                <Button type="submit">Save changes</Button>
              </DialogFooter>
            </DialogPopup>
          </Dialog>
        </DialogFooter>
      </DialogPopup>
    </Dialog>
  );
}
```

#### Open from a Menu

Use controlled state to open a dialog from a menu item. Place the `Dialog` outside the `Menu` tree and control it with `open` and `onOpenChange`.

```tsx
"use client";

import { useState } from "react";
import { Button } from "@/components/ui/button";
import {
  Dialog,
  DialogClose,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogPopup,
  DialogTitle,
} from "@/components/ui/dialog";
import {
  Menu,
  MenuItem,
  MenuPopup,
  MenuTrigger,
} from "@/components/ui/menu";

export function DialogOpenFromMenuDemo() {
  const [dialogOpen, setDialogOpen] = useState(false);

  return (
    <>
      <Menu>
        <MenuTrigger render={<Button variant="outline" />}>
          Open menu
        </MenuTrigger>
        <MenuPopup align="start">
          <MenuItem onClick={() => setDialogOpen(true)}>Open dialog</MenuItem>
        </MenuPopup>
      </Menu>
      <Dialog onOpenChange={setDialogOpen} open={dialogOpen}>
        <DialogPopup>
          <DialogHeader>
            <DialogTitle>Settings</DialogTitle>
            <DialogDescription>Change your preferences</DialogDescription>
          </DialogHeader>
          <DialogFooter>
            <DialogClose render={<Button variant="ghost" />}>Close</DialogClose>
          </DialogFooter>
        </DialogPopup>
      </Dialog>
    </>
  );
}
```

#### Reduce Motion

Set `reduceMotion` on `DialogPopup` to disable all open/close animations.

```tsx
import {
  Dialog,
  DialogPopup,
  DialogHeader,
  DialogTitle,
  DialogDescription,
  DialogTrigger,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";

export function DialogReduceMotionDemo() {
  return (
    <Dialog>
      <DialogTrigger render={<Button />}>Open</DialogTrigger>
      <DialogPopup reduceMotion>
        <DialogHeader>
          <DialogTitle>Terms of Service</DialogTitle>
          <DialogDescription>
            Please read the following terms of service carefully.
          </DialogDescription>
        </DialogHeader>
      </DialogPopup>
    </Dialog>
  );
}
```

#### Animation Presets

Set `animationPreset` on `DialogPopup` to change the open/close animation style.

```tsx
<DialogPopup animationPreset="scale">
  ...
</DialogPopup>
```

```tsx
<DialogPopup animationPreset="fade">
  ...
</DialogPopup>
```

```tsx
<DialogPopup animationPreset="topFlip">
  ...
</DialogPopup>
```

```tsx
<DialogPopup animationPreset="bottomSlide">
  ...
</DialogPopup>
```

```tsx
<DialogPopup animationPreset="wipe">
  ...
</DialogPopup>
```

### Notes

- When `modal` is `true` (the default), focus is trapped inside the dialog, page scrolling is locked, and an overlay backdrop is rendered.
- When `modal` is `false`, the backdrop is hidden and users can interact with the rest of the page.
- Nested dialogs are supported. The parent dialog automatically scales down and shifts to indicate stacking. The flip and slide animation presets are direction-aware when nested.
- `DialogPopup` internally renders a `DialogPortal` and `DialogBackdrop`. You do not need to add these manually.
- Use the `render` prop on `DialogTrigger` and `DialogClose` to render them as a different element (e.g., `render={<Button variant="outline" />}`). This is Base UI's equivalent of Radix UI's `asChild`.
- `showCloseButton` on `DialogPopup` defaults to `true`. Set it to `false` to hide the built-in X close button.
