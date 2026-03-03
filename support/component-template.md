# Component Documentation Template

This template defines the structure for a single component section in
`llms.txt`. Replace all `{{PLACEHOLDER}}` values with real content.
Follow `support/writing-guide.md` for tone, formatting, and constraints.

Each component section lives in its own file at
`support/sections/03-{{component-slug}}.md` (e.g. `03-button.md`).

---

## How to Use This Template

1. Read the component source at
   `src/registry/pure-ui/ui/{{component-slug}}/index.tsx`.
2. Read the component's entry in `registry.json` for dependencies and
   description.
3. Read the example demos at
   `src/registry/pure-ui/examples/{{component-slug}}/`.
4. Read the existing MDX docs at
   `src/content/docs/components/{{component-slug}}.mdx` for usage
   patterns and API notes worth carrying over.
5. Fill in each section below, removing any sections marked
   **(if applicable)** when they do not apply to the component.
6. Run the consistency checklist at the bottom before submitting.

---

## Template

Everything below the horizontal rule is the actual template to copy. The
file must start directly with the `##` heading (no front matter).

---

## {{ComponentName}}

{{One to two sentences describing what the component does and when to use
it. Pull from the `description` field in `registry.json` and expand if
needed. Do not use marketing language.}}

Built on `@base-ui/react/{{base-ui-primitive}}`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/{{component-slug}}"
```

#### Manual

1. Install dependencies:

```bash
npm install {{space-separated-deps}}
pnpm add {{space-separated-deps}}
yarn add {{space-separated-deps}}
bun add {{space-separated-deps}}
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at
   `components/ui/{{component-slug}}.tsx`.

### Anatomy

Show all imports the user needs, followed by a minimal JSX tree that
demonstrates how the sub-components compose together. Use
`@/components/ui/...` import paths.

```tsx
import {
  {{ComponentName}},
  {{SubComponentA}},
  {{SubComponentB}},
} from "@/components/ui/{{component-slug}}";

<{{ComponentName}}>
  <{{SubComponentA}}>
    <{{SubComponentB}} />
  </{{SubComponentA}}>
</{{ComponentName}}>
```

For single-part components (e.g. Button, Input), the anatomy is just:

```tsx
import { {{ComponentName}} } from "@/components/ui/{{component-slug}}";

<{{ComponentName}}>{{default children if any}}</{{ComponentName}}>
```

### Props

List props for each exported component that has configurable props.
Use a separate `####` heading per sub-component when there are multiple.

#### {{ComponentName}}

Accepts all props from `@base-ui/react/{{base-ui-primitive}}`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| {{propName}} | {{TypeScript type}} | {{default or --}} | {{One sentence}} |

**(Repeat the `####` + table pattern for each sub-component that has
its own props.)**

### Variants **(if applicable)**

When the component uses `tailwind-variants` or has an explicit variant
system, list every variant key with its values and defaults. Show a
short code example for each non-default variant.

#### {{variantKey}}

Values: `"{{value1}}"` | `"{{value2}}"` | `"{{value3}}"`
Default: `"{{defaultValue}}"`

```tsx
<{{ComponentName}} {{variantKey}}="{{non-default-value}}">
  {{children}}
</{{ComponentName}}>
```

### Usage

Provide at least one basic example. Add more `####` sub-sections for
major features: controlled state, sizes, disabled state, composition
with other components, rendering as another element, etc.

#### Basic

```tsx
import { {{ComponentName}} } from "@/components/ui/{{component-slug}}";

export function {{ComponentName}}Example() {
  return (
    <{{ComponentName}}>
      {{minimal example content}}
    </{{ComponentName}}>
  );
}
```

#### {{Feature Name}} **(repeat as needed)**

{{One to two sentences explaining when or why to use this feature.}}

```tsx
{{complete, runnable example}}
```

### Notes **(if applicable)**

Use this section for:

- Accessibility considerations specific to the component.
- Migration notes from Radix UI / shadcn (e.g. `render` prop replaces
  `asChild`).
- Caveats or gotchas (e.g. `focusableWhenDisabled` behaviour).
- Required context providers or wrapper components.

Keep each note to one or two sentences. Use a bullet list.

---

## Consistency Checklist

Before submitting the completed section, verify:

- [ ] No HTML tags anywhere in the content
- [ ] No MDX component syntax (`<ComponentShowcase>`, `<Tabs>`, etc.)
- [ ] No front matter block
- [ ] No image or link references
- [ ] Heading levels start at `##` for the component name, `###` for
      subsections, `####` for sub-subsections
- [ ] All code blocks have a language tag (`tsx`, `ts`, `bash`, `css`)
- [ ] Import paths use `@/components/ui/...` not registry paths
- [ ] At least one complete, runnable usage example is present
- [ ] Prop table exists for every component with configurable props
- [ ] Installation includes the shadcn CLI command
- [ ] Variant values and defaults match the source code exactly
- [ ] Description does not use marketing language
- [ ] No emoji anywhere in the file
