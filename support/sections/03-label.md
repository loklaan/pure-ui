## Label

Renders an accessible `<label>` element associated with form controls. Use it to provide visible labels for inputs, checkboxes, and other interactive elements.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/label"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge
pnpm add clsx tailwind-merge
yarn add clsx tailwind-merge
bun add clsx tailwind-merge
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/label.tsx`.

### Anatomy

```tsx
import { Label } from "@/components/ui/label";

<Label htmlFor="field-id">Field name</Label>
```

### Props

#### Label

Accepts all props from the standard HTML `<label>` element (`React.ComponentProps<"label">`).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| htmlFor | string | -- | The `id` of the form element this label is associated with |
| className | string | -- | Additional CSS classes, merged via `cn()` |

The component renders with `data-slot="label"` for styling hooks.

### Usage

#### Basic

```tsx
import { Label } from "@/components/ui/label";
import { Input } from "@/components/ui/input";

export function LabelDemo() {
  return (
    <div className="flex flex-col items-start gap-2">
      <Label htmlFor="email">Email</Label>
      <Input
        id="email"
        type="email"
        placeholder="you@example.com"
        aria-label="Email"
      />
    </div>
  );
}
```

#### With Checkbox

Wrap a checkbox and its text inside Label to create an inline clickable label. Clicking anywhere on the label toggles the checkbox.

```tsx
import { Checkbox } from "@/components/ui/checkbox";
import { Label } from "@/components/ui/label";

export function LabelWithCheckbox() {
  return (
    <Label>
      <Checkbox />
      Accept terms and conditions
    </Label>
  );
}
```

### Notes

- Label renders as an inline flex container (`inline-flex items-center gap-2`), so wrapping an inline control and text inside it produces a horizontally aligned pair.
- Associate a Label with a separate control using the `htmlFor` prop matching the control's `id`. Alternatively, wrap the control inside the Label element for implicit association.
