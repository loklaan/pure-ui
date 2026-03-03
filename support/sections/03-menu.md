## Menu

A dropdown list of actions enhanced with keyboard navigation. Supports items, checkbox items, radio groups, submenus, groups with labels, keyboard shortcuts, and configurable open/close animations.

Built on `@base-ui/react/menu`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/menu"
```

#### Manual

1. Install dependencies:

```bash
npm install @base-ui/react clsx tailwind-merge lucide-react
pnpm add @base-ui/react clsx tailwind-merge lucide-react
yarn add @base-ui/react clsx tailwind-merge lucide-react
bun add @base-ui/react clsx tailwind-merge lucide-react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/menu.tsx`.

### Anatomy

```tsx
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuItem,
  MenuSeparator,
  MenuShortcut,
  MenuLabel,
  MenuGroup,
  MenuGroupLabel,
  MenuCheckboxItem,
  MenuRadioGroup,
  MenuRadioItem,
  MenuSub,
  MenuSubTrigger,
  MenuSubPopup,
} from "@/components/ui/menu";

<Menu>
  <MenuTrigger />
  <MenuPopup>
    <MenuLabel>Section label</MenuLabel>
    <MenuItem />
    <MenuSeparator />
    <MenuGroup>
      <MenuGroupLabel>Group heading</MenuGroupLabel>
      <MenuItem />
    </MenuGroup>
    <MenuCheckboxItem />
    <MenuRadioGroup>
      <MenuRadioItem />
    </MenuRadioGroup>
    <MenuSub>
      <MenuSubTrigger />
      <MenuSubPopup>
        <MenuItem />
      </MenuSubPopup>
    </MenuSub>
  </MenuPopup>
</Menu>
```

### Props

#### Menu

Root wrapper that provides context to all child components. Accepts all props from `@base-ui/react/menu` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| backdrop | "opaque" \| "blur" \| "transparent" | "transparent" | Backdrop style shown behind the popup |
| open | boolean | -- | Controlled open state |
| onOpenChange | (open: boolean) => void | -- | Called when the open state changes |

#### MenuTrigger

Element that opens the menu on click. Accepts all props from `@base-ui/react/menu` Trigger.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| render | React.ReactElement | -- | Renders the trigger as a different element |
| openOnHover | boolean | false | Opens the menu when the trigger is hovered |

#### MenuPopup

Dropdown popup container. Internally renders a Portal, Backdrop, and Positioner. Accepts all props from `@base-ui/react/menu` Popup.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| animationPreset | "none" \| "scale" \| "fade" \| "slideOutside" \| "slideInside" \| "wipe" \| "wipeScale" \| "motion" \| "motionBlur" | "scale" | CSS animation applied when the popup opens and closes |
| transitionPreset | string | "snappyOut" | Easing curve for the animation (see Transition Presets below) |
| reduceMotion | boolean | false | Disables all animations |
| showArrow | boolean | false | Displays an arrow indicator pointing to the trigger |
| side | "top" \| "right" \| "bottom" \| "left" \| "inline-start" \| "inline-end" | "bottom" | Side of the trigger where the popup appears |
| sideOffset | number | 4 | Distance in pixels between the trigger and the popup |
| align | "start" \| "center" \| "end" | "center" | Alignment of the popup relative to the trigger |
| alignOffset | number | 0 | Offset in pixels for the alignment |

#### MenuItem

Individual menu action. Accepts all props from `@base-ui/react/menu` Item.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| render | React.ReactElement | -- | Renders the item as a different element (e.g. an anchor tag) |
| onSelect | (event: Event) => void | -- | Called when the item is selected |
| disabled | boolean | false | Disables the item |

#### MenuCheckboxItem

Toggleable checkbox item. Accepts all props from `@base-ui/react/menu` CheckboxItem.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| checked | boolean | -- | Controlled checked state |
| onCheckedChange | (checked: boolean) => void | -- | Called when the checked state changes |
| closeOnClick | boolean | false | Closes the menu when the item is clicked |
| onSelect | (event: Event) => void | -- | Called when the item is selected; call `event.preventDefault()` to keep the menu open |

#### MenuRadioGroup

Groups radio items for single-selection. Accepts all props from `@base-ui/react/menu` RadioGroup.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string | -- | Controlled selected value |
| onValueChange | (value: string) => void | -- | Called when the selected value changes |
| activeIcon | React.ReactNode | -- | Replaces the default circle indicator icon for all radio items in the group |

#### MenuRadioItem

Radio option within a `MenuRadioGroup`. Accepts all props from `@base-ui/react/menu` RadioItem.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string | -- | Value associated with this item (required) |
| closeOnClick | boolean | false | Closes the menu when the item is clicked |
| onSelect | (event: Event) => void | -- | Called when the item is selected; call `event.preventDefault()` to keep the menu open |

#### MenuGroup

Groups related items together. Accepts all props from `@base-ui/react/menu` Group.

#### MenuGroupLabel

Label for a `MenuGroup`. Accepts all props from `@base-ui/react/menu` GroupLabel. Renders with muted, small-text styling.

#### MenuLabel

Standalone label rendered as a plain `span`. Useful for labelling sections outside of a `MenuGroup`.

#### MenuSeparator

Visual horizontal line between menu sections. Accepts all props from `@base-ui/react/menu` Separator.

#### MenuShortcut

Displays a keyboard shortcut aligned to the right of a menu item. Renders as a `span`.

#### MenuSub

Root wrapper for a submenu. Accepts all props from `@base-ui/react/menu` SubmenuRoot.

#### MenuSubTrigger

Trigger that opens a submenu. Renders a chevron-right icon automatically. Accepts all props from `@base-ui/react/menu` SubmenuTrigger.

#### MenuSubPopup

Popup container for a submenu. Internally renders a Portal and Positioner. Accepts all props from `@base-ui/react/menu` Popup.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| side | "top" \| "right" \| "bottom" \| "left" \| "inline-start" \| "inline-end" | "right" | Side of the trigger where the submenu appears |
| sideOffset | number | 4 | Distance in pixels between the sub-trigger and the submenu |
| align | "start" \| "center" \| "end" | "start" | Alignment of the submenu relative to the sub-trigger |
| alignOffset | number | 0 | Offset in pixels for the alignment |

### Variants

#### animationPreset

Values: `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"`
Default: `"scale"`

Set on `MenuPopup` to control the open/close animation. Side-aware presets (`slideOutside`, `slideInside`, `wipe`, `wipeScale`, `motion`, `motionBlur`) animate relative to the `side` prop.

```tsx
<MenuPopup animationPreset="wipe">
  ...
</MenuPopup>
```

```tsx
<MenuPopup animationPreset="motionBlur">
  ...
</MenuPopup>
```

#### transitionPreset

24 named easing curves that control the timing of the popup animation. Set on `MenuPopup`.

Default: `"snappyOut"`

Available values: `"inExpo"`, `"outExpo"`, `"inOutExpo"`, `"anticipate"`, `"quickOut"`, `"overshootOut"`, `"swiftOut"`, `"snappyOut"`, `"in"`, `"out"`, `"inOut"`, `"outIn"`, `"inQuad"`, `"outQuad"`, `"inOutQuad"`, `"inCubic"`, `"outCubic"`, `"inOutCubic"`, `"inQuart"`, `"outQuart"`, `"inOutQuart"`, `"inQuint"`, `"outQuint"`, `"inOutQuint"`, `"inCirc"`, `"outCirc"`, `"inOutCirc"`, `"inOutBase"`

```tsx
<MenuPopup transitionPreset="outCubic">
  ...
</MenuPopup>
```

#### backdrop

Values: `"opaque"` | `"blur"` | `"transparent"`
Default: `"transparent"`

Set on `Menu` to display a backdrop behind the popup.

```tsx
<Menu backdrop="blur">
  <MenuTrigger>Open</MenuTrigger>
  <MenuPopup>
    <MenuItem>Action</MenuItem>
  </MenuPopup>
</Menu>
```

### Usage

#### Basic

```tsx
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuItem,
  MenuSeparator,
  MenuShortcut,
} from "@/components/ui/menu";
import { Button } from "@/components/ui/button";

export function MenuBasicDemo() {
  return (
    <Menu>
      <MenuTrigger render={<Button variant="ghost" size="sm" />}>
        Account settings
      </MenuTrigger>
      <MenuPopup className="w-56">
        <MenuItem>
          Profile
          <MenuShortcut>⌘P</MenuShortcut>
        </MenuItem>
        <MenuItem>
          Applications
          <MenuShortcut>⌘A</MenuShortcut>
        </MenuItem>
        <MenuSeparator />
        <MenuItem>Sign out</MenuItem>
      </MenuPopup>
    </Menu>
  );
}
```

#### With Arrow

Pass `showArrow` to `MenuPopup` to display an arrow pointing at the trigger. When using an arrow, set `sideOffset` to at least `8` to avoid overlap.

```tsx
<MenuPopup showArrow sideOffset={8}>
  <MenuItem>Profile</MenuItem>
  <MenuItem>Settings</MenuItem>
</MenuPopup>
```

#### Positioning

Use the `side` prop on `MenuPopup` to control which side of the trigger the menu appears on.

```tsx
<MenuPopup side="right" sideOffset={8}>
  <MenuItem>Action</MenuItem>
</MenuPopup>
```

#### Open on Hover

Pass `openOnHover` to `MenuTrigger` to open the menu on hover instead of click.

```tsx
<Menu>
  <MenuTrigger openOnHover render={<Button variant="ghost" size="sm" />}>
    Hover me
  </MenuTrigger>
  <MenuPopup>
    <MenuItem>Action</MenuItem>
  </MenuPopup>
</Menu>
```

#### Checkbox Items

Use `MenuCheckboxItem` for toggleable options. Call `event.preventDefault()` in `onSelect` to keep the menu open after toggling.

```tsx
import { useState } from "react";
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuCheckboxItem,
} from "@/components/ui/menu";
import { Button } from "@/components/ui/button";

export function MenuCheckboxDemo() {
  const [showStatusBar, setShowStatusBar] = useState(true);
  const [showPanel, setShowPanel] = useState(false);

  return (
    <Menu>
      <MenuTrigger render={<Button variant="outline" />}>Open</MenuTrigger>
      <MenuPopup className="w-56">
        <MenuCheckboxItem
          checked={showStatusBar}
          onCheckedChange={(checked) => setShowStatusBar(checked)}
          onSelect={(event) => event.preventDefault()}
        >
          Status Bar
        </MenuCheckboxItem>
        <MenuCheckboxItem
          checked={showPanel}
          onCheckedChange={(checked) => setShowPanel(checked)}
          onSelect={(event) => event.preventDefault()}
        >
          Panel
        </MenuCheckboxItem>
      </MenuPopup>
    </Menu>
  );
}
```

#### Radio Group

Use `MenuRadioGroup` and `MenuRadioItem` for single-selection within a group.

```tsx
import { useState } from "react";
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuLabel,
  MenuRadioGroup,
  MenuRadioItem,
  MenuSeparator,
} from "@/components/ui/menu";
import { Button } from "@/components/ui/button";

export function MenuRadioGroupDemo() {
  const [position, setPosition] = useState("top");

  return (
    <Menu>
      <MenuTrigger render={<Button variant="outline" />}>Open</MenuTrigger>
      <MenuPopup className="w-56">
        <MenuLabel>Position</MenuLabel>
        <MenuSeparator />
        <MenuRadioGroup value={position} onValueChange={setPosition}>
          <MenuRadioItem value="top">Top</MenuRadioItem>
          <MenuRadioItem value="bottom">Bottom</MenuRadioItem>
          <MenuRadioItem value="right">Right</MenuRadioItem>
        </MenuRadioGroup>
      </MenuPopup>
    </Menu>
  );
}
```

#### Radio Group with Custom Icon

Pass `activeIcon` to `MenuRadioGroup` to replace the default circle indicator.

```tsx
import { CheckIcon } from "lucide-react";

<MenuRadioGroup
  value={value}
  onValueChange={setValue}
  activeIcon={<CheckIcon className="size-4" />}
>
  <MenuRadioItem value="date">Date</MenuRadioItem>
  <MenuRadioItem value="name">Name</MenuRadioItem>
</MenuRadioGroup>
```

#### Groups with Labels

Use `MenuGroup` and `MenuGroupLabel` to organise items into labelled sections.

```tsx
import { useState } from "react";
import { CheckIcon } from "lucide-react";
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuSeparator,
  MenuGroup,
  MenuGroupLabel,
  MenuRadioGroup,
  MenuRadioItem,
  MenuCheckboxItem,
} from "@/components/ui/menu";
import { Button } from "@/components/ui/button";

export function MenuWithGroupsDemo() {
  const [value, setValue] = useState("date");
  const [showMinimap, setShowMinimap] = useState(true);

  return (
    <Menu>
      <MenuTrigger render={<Button variant="outline" />}>Open</MenuTrigger>
      <MenuPopup className="w-56">
        <MenuGroup>
          <MenuGroupLabel>Sort</MenuGroupLabel>
          <MenuRadioGroup
            value={value}
            onValueChange={setValue}
            activeIcon={<CheckIcon className="size-4" />}
          >
            <MenuRadioItem value="date">Date</MenuRadioItem>
            <MenuRadioItem value="name">Name</MenuRadioItem>
            <MenuRadioItem value="type">Type</MenuRadioItem>
          </MenuRadioGroup>
        </MenuGroup>
        <MenuSeparator />
        <MenuGroup>
          <MenuGroupLabel>Workspace</MenuGroupLabel>
          <MenuCheckboxItem
            checked={showMinimap}
            onCheckedChange={(checked) => setShowMinimap(checked)}
            onSelect={(event) => event.preventDefault()}
          >
            Minimap
          </MenuCheckboxItem>
        </MenuGroup>
      </MenuPopup>
    </Menu>
  );
}
```

#### Submenus

Use `MenuSub`, `MenuSubTrigger`, and `MenuSubPopup` to create nested menus. The sub-trigger renders a chevron-right icon automatically.

```tsx
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuItem,
  MenuSeparator,
  MenuSub,
  MenuSubTrigger,
  MenuSubPopup,
} from "@/components/ui/menu";
import { Button } from "@/components/ui/button";

export function MenuNestedDemo() {
  return (
    <Menu>
      <MenuTrigger render={<Button variant="ghost" size="sm" />}>
        Song
      </MenuTrigger>
      <MenuPopup showArrow sideOffset={8}>
        <MenuItem>Add to Library</MenuItem>
        <MenuSub>
          <MenuSubTrigger>Add to Playlist</MenuSubTrigger>
          <MenuSubPopup>
            <MenuItem>Get Up!</MenuItem>
            <MenuSeparator />
            <MenuItem>Dancin' Queen</MenuItem>
            <MenuItem>Shape of You</MenuItem>
          </MenuSubPopup>
        </MenuSub>
        <MenuSeparator />
        <MenuItem>Play Next</MenuItem>
        <MenuItem>Favorite</MenuItem>
      </MenuPopup>
    </Menu>
  );
}
```

#### Navigating to a Page

Use the `render` prop on `MenuItem` to compose it with an anchor element.

```tsx
<MenuItem render={<a href="/projects" />}>Go to Projects</MenuItem>
```

#### Opening a Dialog from a Menu

Control the dialog state imperatively using the `onClick` handler on a menu item.

```tsx
import { useState } from "react";
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuItem,
} from "@/components/ui/menu";
import {
  Dialog,
  DialogTrigger,
  DialogPopup,
  DialogTitle,
  DialogDescription,
} from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";

export function MenuOpenDialogDemo() {
  const [dialogOpen, setDialogOpen] = useState(false);

  return (
    <>
      <Menu>
        <MenuTrigger render={<Button variant="outline" />}>Open</MenuTrigger>
        <MenuPopup>
          <MenuItem onClick={() => setDialogOpen(true)}>
            Open dialog
          </MenuItem>
        </MenuPopup>
      </Menu>

      <Dialog open={dialogOpen} onOpenChange={setDialogOpen}>
        <DialogPopup>
          <DialogTitle>Confirmation</DialogTitle>
          <DialogDescription>Are you sure?</DialogDescription>
        </DialogPopup>
      </Dialog>
    </>
  );
}
```

#### Controlled State

Use `open` and `onOpenChange` on `Menu` to control the open state externally.

```tsx
import { useState } from "react";
import {
  Menu,
  MenuTrigger,
  MenuPopup,
  MenuItem,
} from "@/components/ui/menu";
import { Button } from "@/components/ui/button";

export function MenuControlledDemo() {
  const [open, setOpen] = useState(false);

  return (
    <Menu open={open} onOpenChange={setOpen}>
      <MenuTrigger render={<Button variant="outline" />}>Open</MenuTrigger>
      <MenuPopup>
        <MenuItem>Profile</MenuItem>
        <MenuItem>Settings</MenuItem>
      </MenuPopup>
    </Menu>
  );
}
```

### Notes

- By default, clicking a `MenuCheckboxItem` or `MenuRadioItem` does not close the menu. Pass `closeOnClick` to close the menu on selection, or call `event.preventDefault()` in `onSelect` to explicitly keep it open.
- `MenuSubTrigger` automatically renders a chevron-right icon. Do not add one manually.
- Submenu popups use the `scale` animation and `snappyOut` easing by default. These are not configurable via props on `MenuSubPopup`.
- Base UI's `render` prop is the equivalent of Radix UI's `asChild` for polymorphic rendering.
- `MenuShortcut` is a display-only component. It does not bind keyboard shortcuts -- handle keyboard events separately.
- When using `showArrow` on `MenuPopup`, set `sideOffset` to at least `8` to prevent the arrow from overlapping the trigger.
