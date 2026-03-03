## Sheet

A slide-out panel that extends the Dialog component to display supplementary content from the edge of the screen. Use it for forms, detail views, or navigation that should overlay the main content without fully replacing it.

Built on `@base-ui/react/dialog`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/sheet"
```

#### Manual

1. Install dependencies:

```bash
npm install @base-ui/react clsx tailwind-merge tailwind-variants
pnpm add @base-ui/react clsx tailwind-merge tailwind-variants
yarn add @base-ui/react clsx tailwind-merge tailwind-variants
bun add @base-ui/react clsx tailwind-merge tailwind-variants
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/sheet.tsx`.

### Anatomy

```tsx
import {
  Sheet,
  SheetTrigger,
  SheetPopup,
  SheetHeader,
  SheetTitle,
  SheetDescription,
  SheetFooter,
  SheetClose,
} from "@/components/ui/sheet";

<Sheet>
  <SheetTrigger>Open</SheetTrigger>
  <SheetPopup>
    <SheetHeader>
      <SheetTitle>Title</SheetTitle>
      <SheetDescription>Description text</SheetDescription>
    </SheetHeader>
    {/* content */}
    <SheetFooter>
      <SheetClose>Close</SheetClose>
    </SheetFooter>
  </SheetPopup>
</Sheet>
```

### Props

#### Sheet

Root wrapper that manages open/close state. Accepts all props from `@base-ui/react/dialog` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| open | boolean | -- | Controlled open state |
| onOpenChange | (open: boolean) => void | -- | Called when the open state changes |

#### SheetTrigger

Element that opens the sheet when clicked. Accepts all props from `@base-ui/react/dialog` Trigger.

#### SheetClose

Element that closes the sheet when clicked. Accepts all props from `@base-ui/react/dialog` Close.

#### SheetPopup

The sheet panel itself. Renders inside a portal with a backdrop overlay. Includes a built-in close button by default. Accepts all props from `@base-ui/react/dialog` Popup.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| side | "right" \| "left" \| "top" \| "bottom" | "right" | Edge of the screen the sheet slides in from |
| variant | "full" \| "rounded" | "full" | Visual style of the sheet panel |
| showCloseButton | boolean | true | Shows or hides the built-in close button |
| reduceMotion | boolean | false | Disables slide and fade transitions |

#### SheetHeader

Plain `div` for the top section of the sheet. Accepts standard `div` props.

#### SheetFooter

Plain `div` pinned to the bottom of the sheet via `mt-auto`. Accepts standard `div` props.

#### SheetTitle

Title element inside the sheet. Accepts all props from `@base-ui/react/dialog` Title.

#### SheetDescription

Description text inside the sheet. Accepts all props from `@base-ui/react/dialog` Description.

### Variants

#### side

Values: `"right"` | `"left"` | `"top"` | `"bottom"`
Default: `"right"`

Controls which edge of the viewport the sheet slides in from. Left and right sheets have a max width of `sm:max-w-sm` and take 75% of the viewport width by default. Top and bottom sheets expand to the full width of the viewport.

```tsx
<SheetPopup side="left">
  ...
</SheetPopup>
```

```tsx
<SheetPopup side="bottom">
  ...
</SheetPopup>
```

#### variant

Values: `"full"` | `"rounded"`
Default: `"full"`

The `"full"` variant stretches the sheet flush to the screen edge. The `"rounded"` variant adds padding around the sheet and applies rounded corners with a border.

```tsx
<SheetPopup variant="rounded">
  ...
</SheetPopup>
```

### Usage

#### Basic

```tsx
import {
  Sheet,
  SheetPopup,
  SheetHeader,
  SheetTitle,
  SheetDescription,
  SheetTrigger,
} from "@/components/ui/sheet";
import { Button } from "@/components/ui/button";

export function SheetBasicExample() {
  return (
    <Sheet>
      <SheetTrigger render={<Button variant="outline" />}>
        Open Sheet
      </SheetTrigger>
      <SheetPopup>
        <SheetHeader>
          <SheetTitle>Sheet Title</SheetTitle>
          <SheetDescription>
            This action cannot be undone. This will permanently delete your
            account and remove your data from our servers.
          </SheetDescription>
        </SheetHeader>
      </SheetPopup>
    </Sheet>
  );
}
```

#### Side

Pass `side` to `SheetPopup` to change the edge the sheet slides in from.

```tsx
import {
  Sheet,
  SheetClose,
  SheetPopup,
  SheetDescription,
  SheetFooter,
  SheetHeader,
  SheetTitle,
  SheetTrigger,
} from "@/components/ui/sheet";
import { Button } from "@/components/ui/button";
import { Label } from "@/components/ui/label";
import { Input } from "@/components/ui/input";

export function SheetSideExample() {
  return (
    <Sheet>
      <SheetTrigger render={<Button variant="outline" />}>
        Left
      </SheetTrigger>
      <SheetPopup side="left">
        <SheetHeader>
          <SheetTitle>Edit profile</SheetTitle>
          <SheetDescription>
            Make changes to your profile here. Click save when you're done.
          </SheetDescription>
        </SheetHeader>
        <div className="grid gap-6 px-4">
          <div className="grid gap-3">
            <Label htmlFor="name">Name</Label>
            <Input id="name" defaultValue="Pedro Duarte" />
          </div>
          <div className="grid gap-3">
            <Label htmlFor="username">Username</Label>
            <Input id="username" defaultValue="@peduarte" />
          </div>
        </div>
        <SheetFooter>
          <Button type="submit" className="w-full">Save changes</Button>
          <SheetClose render={<Button variant="outline" className="w-full" />}>
            Close
          </SheetClose>
        </SheetFooter>
      </SheetPopup>
    </Sheet>
  );
}
```

#### Custom Size

Override the default width or height using `className` on `SheetPopup`.

```tsx
import {
  Sheet,
  SheetPopup,
  SheetHeader,
  SheetTitle,
  SheetDescription,
  SheetTrigger,
} from "@/components/ui/sheet";
import { Button } from "@/components/ui/button";

export function SheetCustomSizeExample() {
  return (
    <Sheet>
      <SheetTrigger render={<Button variant="outline" />}>
        Wide Sheet
      </SheetTrigger>
      <SheetPopup className="w-[700px] sm:max-w-[1080px]">
        <SheetHeader>
          <SheetTitle>Wide Sheet</SheetTitle>
          <SheetDescription>
            Use className to set a custom width or height.
          </SheetDescription>
        </SheetHeader>
      </SheetPopup>
    </Sheet>
  );
}
```

#### Nested Sheets

Nest a `Sheet` inside another sheet's content to create layered panels. The parent sheet scales down and shifts when a child sheet opens.

```tsx
import {
  Sheet,
  SheetPopup,
  SheetHeader,
  SheetTitle,
  SheetDescription,
  SheetFooter,
  SheetTrigger,
  SheetClose,
} from "@/components/ui/sheet";
import { Button } from "@/components/ui/button";
import { Label } from "@/components/ui/label";
import { Input } from "@/components/ui/input";

export function SheetNestedExample() {
  return (
    <Sheet>
      <SheetTrigger render={<Button variant="outline" />}>
        Open Sheet
      </SheetTrigger>
      <SheetPopup>
        <SheetHeader>
          <SheetTitle>Parent Sheet</SheetTitle>
          <SheetDescription>
            This is the parent sheet. Open a child sheet from here.
          </SheetDescription>
        </SheetHeader>
        <SheetFooter>
          <Sheet>
            <SheetTrigger render={<Button variant="outline" className="w-full" />}>
              Edit Info
            </SheetTrigger>
            <SheetPopup>
              <SheetHeader>
                <SheetTitle>Child Sheet</SheetTitle>
                <SheetDescription>
                  Edit details without losing context from the parent sheet.
                </SheetDescription>
              </SheetHeader>
              <div className="grid gap-6 px-4">
                <div className="grid gap-3">
                  <Label htmlFor="title">Title</Label>
                  <Input id="title" defaultValue="Example" />
                </div>
              </div>
              <SheetFooter>
                <Button type="submit" className="w-full">Save changes</Button>
                <SheetClose render={<Button variant="outline" className="w-full" />}>
                  Close
                </SheetClose>
              </SheetFooter>
            </SheetPopup>
          </Sheet>
        </SheetFooter>
      </SheetPopup>
    </Sheet>
  );
}
```

#### Reduce Motion

Set `reduceMotion` on `SheetPopup` to disable all slide and fade transitions.

```tsx
import {
  Sheet,
  SheetPopup,
  SheetHeader,
  SheetTitle,
  SheetDescription,
  SheetTrigger,
} from "@/components/ui/sheet";
import { Button } from "@/components/ui/button";

export function SheetReduceMotionExample() {
  return (
    <Sheet>
      <SheetTrigger render={<Button variant="outline" />}>
        Open Sheet
      </SheetTrigger>
      <SheetPopup reduceMotion>
        <SheetHeader>
          <SheetTitle>No Transitions</SheetTitle>
          <SheetDescription>
            This sheet opens and closes without animations.
          </SheetDescription>
        </SheetHeader>
      </SheetPopup>
    </Sheet>
  );
}
```

### Notes

- Sheet is built on the Dialog primitive from Base UI, not a separate sheet primitive. It uses the same open/close state management and accessibility features as Dialog.
- The `render` prop on `SheetTrigger` and `SheetClose` is Base UI's equivalent of Radix UI's `asChild` for rendering as a different element.
- Nested sheets use the `--nested-dialogs` CSS variable to coordinate scaling and offset of parent sheets when a child sheet opens.
- Left and right sheets default to `w-3/4` with `sm:max-w-sm`. Override these with `className` on `SheetPopup` for a custom width.
- Top and bottom sheets auto-size to their content height.
