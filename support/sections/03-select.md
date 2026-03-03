## Select

A dropdown component for choosing a predefined value from a list of options. Supports single and multiple selection, grouped items, object values, custom value formatting, animation presets, and arrow indicators.

Built on `@base-ui/react/select`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/select"
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

3. Add fade-in keyframes to your styles:

```css
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(6px);
    filter: blur(6px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

.fadeIn {
  animation: fadeIn 0.2s ease-out;
}
```

4. Copy the component source into your project at `components/ui/select.tsx`.

### Anatomy

```tsx
import {
  Select,
  SelectTrigger,
  SelectValue,
  SelectIcon,
  SelectPopup,
  SelectList,
  SelectItem,
  SelectItemText,
  SelectItemIndicator,
} from "@/components/ui/select";

<Select>
  <SelectTrigger>
    <SelectValue />
    <SelectIcon />
  </SelectTrigger>
  <SelectPopup>
    <SelectList>
      <SelectItem>
        <SelectItemText />
        <SelectItemIndicator />
      </SelectItem>
    </SelectList>
  </SelectPopup>
</Select>
```

For grouped items, wrap items in `SelectGroup` with a `SelectGroupLabel`:

```tsx
import {
  SelectGroup,
  SelectGroupLabel,
  SelectSeparator,
} from "@/components/ui/select";

<SelectList>
  <SelectGroup>
    <SelectGroupLabel>Group title</SelectGroupLabel>
    <SelectItem value="a">
      <SelectItemText>Option A</SelectItemText>
    </SelectItem>
  </SelectGroup>
  <SelectSeparator />
  <SelectGroup>
    <SelectGroupLabel>Another group</SelectGroupLabel>
    <SelectItem value="b">
      <SelectItemText>Option B</SelectItemText>
    </SelectItem>
  </SelectGroup>
</SelectList>
```

### Props

#### Select

Root wrapper that provides context and manages selection state. Accepts all props from `@base-ui/react/select` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| items | array \| record | -- | Item definitions for value-to-label mapping; enables formatted display in SelectValue |
| value | string \| number \| object \| array | -- | Controlled selected value |
| defaultValue | string \| number \| object \| array | -- | Initial selected value (uncontrolled) |
| onValueChange | (value, event) => void | -- | Called when the selected value changes |
| multiple | boolean | false | Enables multiple selection mode |
| itemToStringValue | (item: unknown) => string | -- | Converts object values to string identifiers |
| backdrop | "opaque" \| "blur" \| "transparent" | "transparent" | Backdrop style behind the popup when open |

#### SelectTrigger

Button that opens and closes the dropdown. Accepts all props from `@base-ui/react/select` Trigger.

#### SelectValue

Displays the selected value text or a placeholder when nothing is selected. Uses a `render` prop internally to support placeholder display and value formatting.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| placeholder | string | "Select..." | Text shown when no value is selected |
| children | (value) => ReactNode | -- | Render function for custom value display |

#### SelectIcon

Container for the dropdown indicator icon. Accepts all props from `@base-ui/react/select` Icon. Pass an icon component as children.

#### SelectPopup

Popup container that renders the dropdown list. Includes the positioner, portal, backdrop, and scroll arrows. Accepts all props from `@base-ui/react/select` Popup plus positioning and animation props.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| animationPreset | "none" \| "scale" \| "fade" \| "slideOutside" \| "slideInside" \| "wipe" \| "wipeScale" \| "motion" \| "motionBlur" | "scale" | CSS animation applied when the popup opens and closes |
| transitionPreset | string | "outQuint" | Easing curve for the popup animation (see Transition Presets below) |
| reduceMotion | boolean | false | Disables all animations |
| showArrow | boolean | false | Shows an arrow pointing from the popup toward the trigger |
| side | "top" \| "bottom" \| "left" \| "right" \| "inline-start" \| "inline-end" | "bottom" | Preferred side for popup placement |
| sideOffset | number | 4 | Distance in pixels between the trigger and the popup |
| align | "start" \| "center" \| "end" | "center" | Alignment of the popup relative to the trigger |
| alignOffset | number | 0 | Offset in pixels along the alignment axis |
| alignItemWithTrigger | boolean | false | Aligns the selected item text with the trigger value text, overlapping the trigger |

#### SelectList

Scrollable container for the list of options. Accepts all props from `@base-ui/react/select` List.

#### SelectItem

Individual option within the list. Accepts all props from `@base-ui/react/select` Item.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string \| number \| object | -- | The value associated with this item |

#### SelectItemText

Text label for an option. Accepts all props from `@base-ui/react/select` ItemText.

#### SelectItemIndicator

Visual indicator for the selected item (typically a checkmark icon). Accepts all props from `@base-ui/react/select` ItemIndicator. Pass an icon component as children.

#### SelectGroup

Groups related options together. Accepts all props from `@base-ui/react/select` Group.

#### SelectGroupLabel

Label for a group of options. Accepts all props from `@base-ui/react/select` GroupLabel.

#### SelectSeparator

Visual divider between groups or items. Accepts all props from `@base-ui/react/select` Separator.

#### SelectScrollUpArrow

Scroll indicator shown at the top of the list when there are items above the visible area. Rendered automatically inside `SelectPopup`.

#### SelectScrollDownArrow

Scroll indicator shown at the bottom of the list when there are items below the visible area. Rendered automatically inside `SelectPopup`.

### Variants

#### animationPreset

Values: `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"`
Default: `"scale"`

Controls the CSS animation applied when the popup opens and closes. Side-aware presets (`slideOutside`, `slideInside`, `wipe`, `wipeScale`, `motion`, `motionBlur`) adapt their direction based on the `side` prop.

```tsx
<SelectPopup animationPreset="wipe" side="bottom">
  <SelectList>...</SelectList>
</SelectPopup>
```

```tsx
<SelectPopup animationPreset="motion" side="right">
  <SelectList>...</SelectList>
</SelectPopup>
```

#### transitionPreset

24 named easing curves that control the timing of the popup animation. Set on `SelectPopup`.

Default: `"outQuint"`

Available values: `"inExpo"`, `"outExpo"`, `"inOutExpo"`, `"anticipate"`, `"quickOut"`, `"overshootOut"`, `"swiftOut"`, `"snappyOut"`, `"in"`, `"out"`, `"inOut"`, `"outIn"`, `"inQuad"`, `"outQuad"`, `"inOutQuad"`, `"inCubic"`, `"outCubic"`, `"inOutCubic"`, `"inQuart"`, `"outQuart"`, `"inOutQuart"`, `"inQuint"`, `"outQuint"`, `"inOutQuint"`, `"inCirc"`, `"outCirc"`, `"inOutCirc"`, `"inOutBase"`

```tsx
<SelectPopup transitionPreset="outCubic">
  <SelectList>...</SelectList>
</SelectPopup>
```

#### backdrop

Values: `"opaque"` | `"blur"` | `"transparent"`
Default: `"transparent"`

Set on the `Select` root to control the backdrop behind the popup.

```tsx
<Select backdrop="blur">
  ...
</Select>
```

### Usage

#### Basic

```tsx
import { CheckIcon, ChevronsUpDownIcon } from "lucide-react";
import {
  Select,
  SelectTrigger,
  SelectValue,
  SelectIcon,
  SelectPopup,
  SelectList,
  SelectItem,
  SelectItemText,
  SelectItemIndicator,
} from "@/components/ui/select";

const languages = [
  { label: "JavaScript", value: "javascript" },
  { label: "TypeScript", value: "typescript" },
  { label: "Python", value: "python" },
  { label: "Java", value: "java" },
  { label: "Rust", value: "rust" },
];

export function SelectBasic() {
  return (
    <Select items={languages}>
      <SelectTrigger>
        <SelectValue />
        <SelectIcon>
          <ChevronsUpDownIcon className="size-3.5" />
        </SelectIcon>
      </SelectTrigger>
      <SelectPopup>
        <SelectList>
          {languages.map(({ label, value }) => (
            <SelectItem key={value} value={value}>
              <SelectItemText>{label}</SelectItemText>
              <SelectItemIndicator>
                <CheckIcon className="size-3" />
              </SelectItemIndicator>
            </SelectItem>
          ))}
        </SelectList>
      </SelectPopup>
    </Select>
  );
}
```

#### Placeholder

Pass a `placeholder` prop to `SelectValue` to display custom text when no value is selected.

```tsx
<SelectTrigger>
  <SelectValue placeholder="Select a food" />
  <SelectIcon>
    <ChevronDownIcon className="size-4" />
  </SelectIcon>
</SelectTrigger>
```

#### Formatting the Displayed Value

By default, `SelectValue` renders the raw value of the selected item. Pass the `items` prop to `Select` so it can look up and display the matching label instead.

```tsx
const items = [
  { value: "system", label: "System default" },
  { value: "light", label: "Light" },
  { value: "dark", label: "Dark" },
];

<Select items={items}>
  <SelectTrigger>
    <SelectValue />
    <SelectIcon>
      <PlusIcon className="size-4" />
    </SelectIcon>
  </SelectTrigger>
  <SelectPopup>
    <SelectList>
      {items.map(({ label, value }) => (
        <SelectItem key={value} value={value}>
          <SelectItemText>{label}</SelectItemText>
          <SelectItemIndicator>
            <CheckIcon className="size-3" />
          </SelectItemIndicator>
        </SelectItem>
      ))}
    </SelectList>
  </SelectPopup>
</Select>
```

Pass a render function as `children` of `SelectValue` for full control over the displayed value.

```tsx
import { CheckIcon, PlusIcon } from "lucide-react";
import {
  Select,
  SelectTrigger,
  SelectValue,
  SelectIcon,
  SelectPopup,
  SelectList,
  SelectItem,
  SelectItemText,
  SelectItemIndicator,
} from "@/components/ui/select";

const countries = [
  { label: "Argentina", value: "argentina", flag: "https://flagcdn.com/ar.svg" },
  { label: "Brazil", value: "brazil", flag: "https://flagcdn.com/br.svg" },
  { label: "Germany", value: "germany", flag: "https://flagcdn.com/de.svg" },
];

export function SelectFormattedCountry() {
  return (
    <Select items={countries}>
      <SelectTrigger>
        <SelectValue placeholder="Select a country">
          {(value: string) => {
            const country = countries.find((c) => c.value === value);
            if (!country) return null;
            return (
              <span className="flex items-center gap-2">
                <img
                  src={country.flag}
                  alt={country.label}
                  className="size-5.5 rounded-full object-cover"
                />
                {country.label}
              </span>
            );
          }}
        </SelectValue>
        <SelectIcon>
          <PlusIcon className="size-4" />
        </SelectIcon>
      </SelectTrigger>
      <SelectPopup>
        <SelectList>
          {countries.map(({ label, value, flag }) => (
            <SelectItem key={value} value={value}>
              <img
                src={flag}
                alt={label}
                className="size-5.5 rounded-full object-cover"
              />
              <SelectItemText>{label}</SelectItemText>
              <SelectItemIndicator>
                <CheckIcon className="size-3" />
              </SelectItemIndicator>
            </SelectItem>
          ))}
        </SelectList>
      </SelectPopup>
    </Select>
  );
}
```

#### Object Values

Select items can use objects as values instead of primitives. Use `itemToStringValue` on `Select` to provide a string identifier, and pass a render function to `SelectValue` to format the display.

```tsx
import {
  Select,
  SelectTrigger,
  SelectValue,
  SelectIcon,
  SelectPopup,
  SelectList,
  SelectItem,
  SelectItemText,
  SelectItemIndicator,
} from "@/components/ui/select";

interface ShippingMethod {
  id: string;
  name: string;
  duration: string;
  price: string;
}

const shippingMethods: ShippingMethod[] = [
  { id: "standard", name: "Standard", duration: "4-6 business days", price: "$4.99" },
  { id: "express", name: "Express", duration: "2-3 business days", price: "$9.99" },
  { id: "overnight", name: "Overnight", duration: "Next business day", price: "$19.99" },
];

export function SelectObjectValues() {
  return (
    <Select
      defaultValue={shippingMethods[0]}
      itemToStringValue={(item: unknown) => (item as ShippingMethod).id}
    >
      <SelectTrigger>
        <SelectValue placeholder="Select shipping">
          {(method: ShippingMethod) => (
            <span className="flex flex-col items-start gap-0.5">
              <span className="text-sm leading-6">{method.name}</span>
              <span className="text-xs leading-4 text-muted-foreground">
                {method.duration} ({method.price})
              </span>
            </span>
          )}
        </SelectValue>
        <SelectIcon />
      </SelectTrigger>
      <SelectPopup alignItemWithTrigger>
        <SelectList>
          {shippingMethods.map((method) => (
            <SelectItem key={method.id} value={method}>
              <SelectItemText className="flex flex-col items-start gap-0.5">
                <span className="text-sm leading-6">{method.name}</span>
                <span className="text-xs leading-4 text-muted-foreground">
                  {method.duration} ({method.price})
                </span>
              </SelectItemText>
              <SelectItemIndicator />
            </SelectItem>
          ))}
        </SelectList>
      </SelectPopup>
    </Select>
  );
}
```

#### Align Item With Trigger

Set `alignItemWithTrigger` on `SelectPopup` to overlay the popup so the selected item text aligns with the trigger value text. When enabled, animation presets are not applied and scroll arrows appear at the top and bottom of the list.

```tsx
<SelectPopup alignItemWithTrigger>
  <SelectList>
    ...
  </SelectList>
</SelectPopup>
```

#### Multiple Selection

Set `multiple` on the `Select` root to allow selecting more than one value. Pass a render function to `SelectValue` to format the multi-value display.

```tsx
import {
  Select,
  SelectTrigger,
  SelectValue,
  SelectIcon,
  SelectPopup,
  SelectList,
  SelectItem,
  SelectItemText,
  SelectItemIndicator,
} from "@/components/ui/select";

const languages = {
  javascript: "JavaScript",
  typescript: "TypeScript",
  python: "Python",
  rust: "Rust",
  go: "Go",
};

type Language = keyof typeof languages;
const values = Object.keys(languages) as Language[];

function renderValue(value: Language[]) {
  if (value.length === 0) return "Select languages...";
  const first = languages[value[0]];
  const rest = value.length > 1 ? ` (+${value.length - 1} more)` : "";
  return first + rest;
}

export function SelectMultiple() {
  return (
    <Select multiple defaultValue={["javascript", "typescript"]}>
      <SelectTrigger>
        <SelectValue>{renderValue}</SelectValue>
        <SelectIcon />
      </SelectTrigger>
      <SelectPopup>
        <SelectList>
          {values.map((value) => (
            <SelectItem key={value} value={value}>
              <SelectItemText>{languages[value]}</SelectItemText>
              <SelectItemIndicator />
            </SelectItem>
          ))}
        </SelectList>
      </SelectPopup>
    </Select>
  );
}
```

#### Animation Presets

Set `animationPreset` on `SelectPopup` to change the open/close animation. Combine with `side` and `align` to control placement.

```tsx
<SelectPopup animationPreset="scale">
  <SelectList>...</SelectList>
</SelectPopup>
```

```tsx
<SelectPopup animationPreset="wipe" side="bottom" align="start">
  <SelectList>...</SelectList>
</SelectPopup>
```

```tsx
<SelectPopup animationPreset="wipeScale" side="top">
  <SelectList>...</SelectList>
</SelectPopup>
```

```tsx
<SelectPopup animationPreset="motion" side="right">
  <SelectList>...</SelectList>
</SelectPopup>
```

```tsx
<SelectPopup animationPreset="motionBlur" side="left">
  <SelectList>...</SelectList>
</SelectPopup>
```

### Notes

- Pass the `items` prop (an array of `{ label, value }` objects or a record) to `Select` so that `SelectValue` can display the correct label for the selected value. Without `items`, the raw value string is displayed.
- The `render` prop is Base UI's replacement for Radix UI's `asChild`. Use it on any sub-component to render as another element.
- `alignItemWithTrigger` on `SelectPopup` changes the popup rendering path: scroll arrows are shown inline, and CSS animation presets are not applied.
- The `SelectValue` component includes a built-in fade-in animation (via a CSS `fadeIn` keyframe class) when the displayed value changes. The keyframe CSS must be added to your stylesheet during manual installation.
- `className` on all sub-components is merged via `cn()`, so Tailwind classes can be appended or overridden.
- The popup renders in a portal by default, ensuring it is not clipped by overflow containers.
