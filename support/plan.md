# Pure UI — llms.txt Generation Plan

## Goal

Generate a comprehensive `llms.txt` file for the Pure UI component library
(a Shadcn registry). The file serves as machine-readable documentation for
LLMs, covering general setup, theming, and every UI component with
installation, anatomy, and usage examples.

## Output Structure

The final `llms.txt` lives at `public/llms.txt`. It is assembled from
section files written to `support/sections/`:

```
support/sections/
  00-introduction.md        # Library overview, philosophy, tech stack
  01-installation.md        # Framework-specific setup guides
  02-theming.md             # CSS variables, color system, dark mode
  03-accordion.md           # Component docs (alphabetical)
  03-avatar.md
  03-badge.md
  ...                       # One file per component, all prefixed 03-
  03-tooltip.md
```

The `03-` prefix for all components ensures they sort together. The
assembly step concatenates them in order.

---

## References

These files inform the work but subagents should read them directly:

| Reference | Path |
|-----------|------|
| Registry manifest | `registry.json` |
| Component sources | `src/registry/pure-ui/ui/{component}/index.tsx` |
| Example demos | `src/registry/pure-ui/examples/{component}/*.tsx` |
| Existing MDX docs | `src/content/docs/components/{component}.mdx` |
| Installation guides | `src/content/docs/installation/*.mdx` |
| Theming docs | `src/content/docs/theming.mdx` |
| Get started | `src/content/docs/get-started.mdx` |
| CSS variables | `src/content/docs/installation/nextjs.mdx` (lines 39-169) |
| Style guide | `support/writing-guide.md` |
| Component template | `support/component-template.md` |
| Utility lib | `src/registry/pure-ui/lib/classes.ts` |

---

## Milestones

### Milestone 1 — Documentation Guidelines (sequential)

Establish the writing standards before any content is written.

- [x] **1.1** Create `support/writing-guide.md` — documentation style guide
  covering tone, formatting rules, code block conventions, what to include
  vs omit, and how to handle llms.txt-specific concerns (no HTML, no MDX
  components, plain markdown only, optimised for LLM consumption).
  Read a few existing MDX docs and component sources first to understand
  the voice and patterns.

- [x] **1.2** Create `support/component-template.md` — a reusable template
  for documenting a single component. Must include sections for:
  description, installation (CLI + manual), dependencies, anatomy (imports
  and JSX structure), props/API, usage examples (basic + variations), and
  notes. Reference the writing guide.

### Milestone 2 — Component Inventory (sequential)

Build a reference catalogue so doc writers know what to cover.

- [x] **2.1** Create `support/component-inventory.md` — read every component
  source file (`src/registry/pure-ui/ui/*/index.tsx`) and catalogue:
  - Component name and description (from `registry.json`)
  - All exported sub-components (e.g. `Accordion`, `AccordionItem`, etc.)
  - All exported types, variants, and utility functions
  - Dependencies and registry dependencies
  - List of available example demos (filenames from `examples/` dir)
  - Any special patterns (animation presets, context providers, etc.)

### Milestone 3 — Foundation Sections (parallelisable)

Write the non-component sections of llms.txt. These three tasks are
independent and may run in parallel.

- [x] **3.1** Write `support/sections/00-introduction.md`
  Read: `src/content/docs/index.mdx`, `src/content/docs/get-started.mdx`,
  `registry.json`, `package.json`.
  Cover: what Pure UI is, its philosophy, tech stack (Base UI, Tailwind
  CSS v4, Motion, tailwind-variants), the shadcn registry model, the `cn()`
  utility, and how components are composed.

- [x] **3.2** Write `support/sections/01-installation.md`
  Read: `src/content/docs/installation/*.mdx`,
  `src/content/docs/get-started.mdx`.
  Cover: prerequisites (Tailwind CSS v4, React 19), framework-specific
  setup (Next.js, Vite, React Router, TanStack Start, TanStack Router,
  Manual), shadcn CLI init, adding components via CLI, the `cn()` utility
  setup, and the tw-animate-css dependency. Include the full CSS variables
  block from the Next.js guide.

- [x] **3.3** Write `support/sections/02-theming.md`
  Read: `src/content/docs/theming.mdx`,
  `src/content/docs/installation/nextjs.mdx` (CSS vars section),
  `src/styles/globals.css` if accessible.
  Cover: CSS variable system, OKLch color space, light/dark mode, the
  `@theme inline` directive, semantic color naming (background vs
  foreground), radius system, all variable names and their purposes,
  how to customise colors.

### Milestone 4 — Component Docs Batch A (parallelisable)

Simple components with few or no sub-parts. All tasks in this milestone
may run in parallel.

- [x] **4.1** Write `support/sections/03-badge.md` for **Badge**
- [x] **4.2** Write `support/sections/03-button.md` for **Button**
- [x] **4.3** Write `support/sections/03-card.md` for **Card**
- [x] **4.4** Write `support/sections/03-checkbox.md` for **Checkbox**
- [x] **4.5** Write `support/sections/03-input.md` for **Input**
- [x] **4.6** Write `support/sections/03-kbd.md` for **Kbd**
- [x] **4.7** Write `support/sections/03-label.md` for **Label**
- [x] **4.8** Write `support/sections/03-separator.md` for **Separator**
- [x] **4.9** Write `support/sections/03-spinner.md` for **Spinner**
- [x] **4.10** Write `support/sections/03-switch.md` for **Switch**
- [x] **4.11** Write `support/sections/03-textarea.md` for **Textarea**

### Milestone 5 — Component Docs Batch B (parallelisable)

Moderate complexity components. All tasks in this milestone may run in
parallel.

- [x] **5.1** Write `support/sections/03-accordion.md` for **Accordion**
- [x] **5.2** Write `support/sections/03-avatar.md` for **Avatar**
- [x] **5.3** Write `support/sections/03-button-group.md` for **Button Group**
- [x] **5.4** Write `support/sections/03-calendar.md` for **Calendar**
- [x] **5.5** Write `support/sections/03-collapsible.md` for **Collapsible**
- [x] **5.6** Write `support/sections/03-input-group.md` for **Input Group**
- [x] **5.7** Write `support/sections/03-input-otp.md` for **Input OTP**
- [x] **5.8** Write `support/sections/03-number-field.md` for **Number Field**
- [x] **5.9** Write `support/sections/03-radio-group.md` for **Radio Group**
- [x] **5.10** Write `support/sections/03-scroll-area.md` for **Scroll Area**

### Milestone 6 — Component Docs Batch C (parallelisable)

Complex components with many sub-parts. All tasks in this milestone may
run in parallel.

- [x] **6.1** Write `support/sections/03-combobox.md` for **Combobox**
- [x] **6.2** Write `support/sections/03-dialog.md` for **Dialog**
- [x] **6.3** Write `support/sections/03-menu.md` for **Menu**
- [x] **6.4** Write `support/sections/03-popover.md` for **Popover**
- [x] **6.5** Write `support/sections/03-select.md` for **Select**
- [x] **6.6** Write `support/sections/03-sheet.md` for **Sheet**
- [x] **6.7** Write `support/sections/03-tabs.md` for **Tabs**
- [x] **6.8** Write `support/sections/03-toast.md` for **Toast**
- [x] **6.9** Write `support/sections/03-tooltip.md` for **Tooltip**

### Milestone 7 — Assembly & Validation (sequential)

- [x] **7.1** Assemble `public/llms.txt` — concatenate all section files
  from `support/sections/` in sort order (00, 01, 02, then 03-* alpha).
  Add a header line: `# Pure UI — Component Library Documentation`.
  Ensure no MDX/HTML artifacts leaked through. Ensure consistent heading
  levels (# for top sections, ## for component names, ### for subsections).

- [x] **7.2** Validate the assembled file:
  - Every component from `registry.json` (type `registry:ui`) has a section
  - Each component section has: description, installation, anatomy, and
    at least one usage example
  - No broken markdown, no HTML tags, no MDX components
  - Heading hierarchy is consistent throughout
  - File is valid UTF-8 plain text

- [x] **7.3** Commit the final `public/llms.txt` and all `support/` files.

---

## Component Reference (30 UI components)

For quick lookup during task assignment:

| Component | Source | Examples Dir |
|-----------|--------|-------------|
| accordion | `ui/accordion/index.tsx` | `examples/accordion/` |
| avatar | `ui/avatar/index.tsx` | `examples/avatar/` |
| badge | `ui/badge/index.tsx` | `examples/badge/` |
| button | `ui/button/index.tsx` | `examples/button/` |
| button-group | `ui/button-group/index.tsx` | `examples/button-group/` |
| calendar | `ui/calendar/index.tsx` | `examples/calendar/` |
| card | `ui/card/index.tsx` | `examples/card/` |
| checkbox | `ui/checkbox/index.tsx` | `examples/checkbox/` |
| collapsible | `ui/collapsible/index.tsx` | `examples/collapsible/` |
| combobox | `ui/combobox/index.tsx` | `examples/combobox/` |
| dialog | `ui/dialog/index.tsx` | `examples/dialog/` |
| input | `ui/input/index.tsx` | `examples/input/` |
| input-group | `ui/input-group/index.tsx` | `examples/input-group/` |
| input-otp | `ui/input-otp/index.tsx` | `examples/input-otp/` |
| kbd | `ui/kbd/index.tsx` | `examples/kbd/` |
| label | `ui/label/index.tsx` | `examples/label/` |
| menu | `ui/menu/index.tsx` | `examples/menu/` |
| number-field | `ui/number-field/index.tsx` | `examples/number-field/` |
| popover | `ui/popover/index.tsx` | `examples/popover/` |
| radio-group | `ui/radio-group/index.tsx` | `examples/radio-group/` |
| scroll-area | `ui/scroll-area/index.tsx` | `examples/scroll-area/` |
| select | `ui/select/index.tsx` | `examples/select/` |
| separator | `ui/separator/index.tsx` | `examples/separator/` |
| sheet | `ui/sheet/index.tsx` | `examples/sheet/` |
| spinner | `ui/spinner/index.tsx` | `examples/spinner/` |
| switch | `ui/switch/index.tsx` | `examples/switch/` |
| tabs | `ui/tabs/index.tsx` | `examples/tabs/` |
| textarea | `ui/textarea/index.tsx` | `examples/textarea/` |
| toast | `ui/toast/index.tsx` | `examples/toast/` |
| tooltip | `ui/tooltip/index.tsx` | `examples/tooltip/` |

All source paths are relative to `src/registry/pure-ui/`.
