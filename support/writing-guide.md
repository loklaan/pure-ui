# Writing Guide for llms.txt

This guide defines the tone, structure, and formatting rules for all
sections of `public/llms.txt`. The file is plain markdown consumed
directly by LLMs -- not rendered in a browser. Every decision here
optimises for machine readability while remaining useful to humans who
open the file.

---

## Audience

The reader is an LLM (or an LLM-assisted developer) that needs to
generate, modify, or explain Pure UI components. Assume the reader:

- Understands React, TypeScript, and Tailwind CSS.
- Has no prior knowledge of Pure UI or Base UI.
- Cannot follow links, view images, or execute interactive demos.

---

## Tone and Voice

- **Direct and declarative.** State what things are and how they work.
  Avoid hedging ("you might want to", "consider using").
- **Second person is fine** ("Use the `variant` prop to change...") but
  keep sentences short.
- **No marketing language.** Do not call the library "powerful",
  "elegant", "beautiful", or similar. Describe capabilities factually.
- **Match the existing docs voice.** The MDX docs use concise
  imperative sentences ("Use `open` and `onOpenChange` props if you
  need to access or control the state"). Mirror that style.

---

## Format Constraints

These rules are non-negotiable. The output is a single `.txt` file
containing plain markdown.

### Allowed

- Markdown headings (`#`, `##`, `###`, `####`)
- Fenced code blocks with language identifiers (` ```tsx `, ` ```bash `,
  ` ```ts `, ` ```css `)
- Inline code (backticks)
- Unordered lists (`-`), ordered lists (`1.`)
- Bold (`**text**`) and italic (`*text*`) for emphasis
- Horizontal rules (`---`) to separate major sections
- Markdown tables (for prop listings)
- Blank lines for readability

### Forbidden

- HTML tags of any kind (`<div>`, `<br>`, `<table>`, etc.)
- MDX components (`<ComponentShowcase>`, `<Tabs>`, `<Steps>`, etc.)
- Image references or links (no `![alt](url)` or `[text](url)`)
- Emoji
- Footnotes
- Front matter (`---` YAML blocks at the top of a section)

---

## Heading Hierarchy

The assembled `llms.txt` uses a strict hierarchy. Section files must
follow these levels:

| Level | Use |
|-------|-----|
| `#`   | Top-level document title (added once by the assembly step) |
| `##`  | Major sections: Introduction, Installation, Theming, and each component name |
| `###` | Subsections within a major section (e.g., Anatomy, Props, Usage) |
| `####`| Sub-subsections (e.g., individual variant names, specific prop groups) |

Component section files start at `##` (the component name). Never use
`#` inside a component section file.

---

## Code Blocks

Code blocks are the most important part of the documentation. LLMs
rely on them to generate correct code.

### Language Tags

Always include a language identifier:

- `tsx` -- React component code (JSX with TypeScript)
- `ts` -- TypeScript without JSX
- `bash` -- Shell commands
- `css` -- CSS / Tailwind directives

### Import Paths

Use the user-facing import paths, not the registry-internal paths:

```tsx
// Correct -- what the user writes
import { Button } from "@/components/ui/button";

// Wrong -- internal registry path
import { Button } from "@/registry/pure-ui/ui/button";
```

### Code Block Content

- Show complete, runnable examples. Do not use `...` or `// rest of
  code` to abbreviate JSX trees unless the omitted part is truly
  irrelevant.
- Omit wrapper `div`s and layout utilities that are not part of the
  component API. Show only what matters.
- Omit file names, highlight annotations, and other MDX-specific code
  fence metadata (no `filename=`, `highlight=`, `noCopy`, `add=`,
  `remove=`). Use plain fences only.
- For installation commands, show all four package managers in a single
  block, one command per line, each on its own line:

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/button"
```

For manual dependency installation, list each package manager:

```bash
npm install @base-ui/react tailwind-variants clsx tailwind-merge
pnpm add @base-ui/react tailwind-variants clsx tailwind-merge
yarn add @base-ui/react tailwind-variants clsx tailwind-merge
bun add @base-ui/react tailwind-variants clsx tailwind-merge
```

---

## Component Section Structure

Every component section must include these subsections in order.
See `support/component-template.md` for the full template.

1. **Heading and description** (`## Component Name` followed by a
   one-to-two sentence description)
2. **Installation** -- CLI command and manual dependency list
3. **Anatomy** -- imports and minimal JSX tree showing how parts
   compose together
4. **Props / API** -- table or list of props with types and defaults
5. **Usage examples** -- at least a basic example; include variant and
   feature examples as appropriate
6. **Notes** (optional) -- migration tips, caveats, accessibility
   notes

---

## Props / API Tables

Use markdown tables. Keep columns to: Name, Type, Default, and
Description.

```
| Prop | Type | Default | Description |
|------|------|---------|-------------|
| variant | "default" \| "outline" \| "ghost" | "default" | Visual style of the button |
| size | "default" \| "sm" \| "lg" \| "icon" | "default" | Size preset |
| disabled | boolean | false | Disables the button |
```

Rules for prop tables:

- Use TypeScript union syntax for enumerated values.
- Use `--` or omit the cell when there is no default.
- Keep descriptions to one sentence.
- List only the component's own props. Do not re-document standard HTML
  or React props (className, children, style, ref, etc.) unless the
  component handles them in a non-standard way.
- If a component extends a Base UI primitive, note that it accepts all
  props from the primitive (e.g., "Accepts all props from
  `@base-ui/react/button`").

---

## Describing Variants and Presets

When a component uses `tailwind-variants` (tv) or has an explicit
variant system:

- List every variant key and its possible values.
- Show the default value.
- Provide a short code example for non-default variants.

```tsx
<Button variant="outline">Outline</Button>
```

Do not describe what the variant looks like visually (colours, shadows,
gradients). Describe what it is intended for or when to use it.

---

## What to Include

- Every exported component and sub-component.
- Every exported type, variant config, or utility.
- Installation instructions (both CLI and manual).
- Complete anatomy showing how sub-components compose.
- Props that users set directly.
- One basic usage example as a minimum.
- Additional examples for each major feature: variants, sizes,
  controlled state, disabled state, composition with other components.
- Migration notes from Radix UI / shadcn where the API differs (e.g.,
  `render` prop vs `asChild`).

## What to Omit

- Visual descriptions ("the button has a blue gradient background").
- Interactive demos or references to them.
- Tailwind class strings from the implementation. Users do not set
  these directly; they use props.
- Internal implementation details (context providers, animation
  preset objects, CSS transition configs) unless they are part of
  the public API.
- Links to external documentation. The reader cannot follow them.
- Version history or changelogs.

---

## Referring to Base UI

Pure UI is built on Base UI (`@base-ui/react`), not Radix UI. When
discussing primitives:

- Use "Base UI" not "Radix".
- When a component wraps a Base UI primitive, state which one (e.g.,
  "Built on `@base-ui/react/accordion`").
- Note the `render` prop as Base UI's equivalent of Radix's `asChild`.

---

## The `cn()` Utility

The `cn()` function combines `clsx` and `tailwind-merge`. It appears
in every component. Mention it once in the Installation / Introduction
section and do not re-explain it per component. In component sections,
just note that `className` is merged via `cn()` if relevant.

---

## Consistency Checklist

Before finalising any section, verify:

- [ ] No HTML tags anywhere in the content
- [ ] No MDX component syntax
- [ ] No front matter block
- [ ] No image or link references
- [ ] Heading levels follow the hierarchy (component files start at `##`)
- [ ] All code blocks have a language tag
- [ ] Import paths use `@/components/ui/...` not registry paths
- [ ] At least one complete usage example is present
- [ ] Prop table exists for components with configurable props
- [ ] Installation includes the shadcn CLI command
