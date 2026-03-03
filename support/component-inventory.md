# Component Inventory

Reference catalogue of all 30 Pure UI components. Each entry lists the
registry metadata, exported symbols, dependencies, example demos, and
any special patterns found in the source.

All source paths are relative to `src/registry/pure-ui/`.

---

## Accordion

**Description:** A customizable accordion component

**Source:** `ui/accordion/index.tsx`

**Base UI primitive:** `@base-ui/react/accordion`

**Dependencies:** clsx, tailwind-merge, @base-ui/react, motion

**Registry dependencies:** classes

**Exported components:**
- `Accordion` -- root wrapper; manages value state and provides context
- `AccordionItem` -- individual collapsible section
- `AccordionHeader` -- header wrapper (wraps Base UI Accordion.Header)
- `AccordionTrigger` -- clickable trigger; accepts `icon` render prop
- `AccordionPanel` -- collapsible content panel

**Exported types (internal, not exported):**
- `AccordionProps` (extends AccordionPrimitive.Root.Props)
- `AccordionItemProps`
- `AccordionHeaderProps`
- `AccordionTriggerProps` (adds `icon` prop)
- `AccordionPanelProps`
- `CSSAnimationPreset` (type alias)
- `CSSTransitionPreset` (type alias)
- `AccordionVariant` -- `"default" | "card" | "swiss"`

**Variants:**
- `variant`: `"default"` | `"card"` | `"swiss"` (default: `"default"`)
- `animationPreset`: `"none"` | `"fade"` | `"scale"` | `"slide"` | `"perspective"` | `"perspectiveBlur"` (default: `"fade"`)
- `transitionPreset`: 24 easing presets (default: `"outQuad"`)

**Special patterns:**
- CSS animation presets (`cssAnimationPresets` object) with Tailwind class strings for each animation type
- CSS transition presets (`cssTransitionPresets` object) with 24 named easing curves
- `AccordionContext` -- React context provider for animation/variant state
- `AccordionItemContext` -- React context for per-item open state
- `reduceMotion` prop disables all animations

**Example demos:**
- accordion-demo.tsx
- accordion-default-variant-demo.tsx
- accordion-swiss-variant-demo.tsx
- accordion-card-variant-demo.tsx
- accordion-multiple-expanded-demo.tsx
- accordion-custom-indicator-demo.tsx
- accordion-disabled-state-demo.tsx
- accordion-reduce-motion-demo.tsx
- accordion-fade-demo.tsx
- accordion-perspective-demo.tsx
- accordion-perspective-blur-demo.tsx
- accordion-scale-demo.tsx
- accordion-slide-demo.tsx

---

## Avatar

**Description:** An easily stylable avatar component.

**Source:** `ui/avatar/index.tsx`

**Base UI primitive:** `@base-ui/react/avatar`

**Dependencies:** clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Avatar` -- root container (renders AvatarPrimitive.Root)
- `AvatarImage` -- image element (renders AvatarPrimitive.Image)
- `AvatarFallback` -- fallback content when image fails to load

**Exported types (public):**
- `AvatarProps` (extends AvatarPrimitive.Root.Props)
- `AvatarImageProps` (extends AvatarPrimitive.Image.Props)
- `AvatarFallbackProps` (extends AvatarPrimitive.Fallback.Props)

**Variants:** None (styled via className)

**Special patterns:** None

**Example demos:**
- avatar-demo.tsx
- avatar-size-demo.tsx
- avatar-radius-demo.tsx
- avatar-grouping-demo.tsx

---

## Badge

**Description:** An easily stylable badge component.

**Source:** `ui/badge/index.tsx`

**Base UI primitive:** Uses `@base-ui/react/merge-props` and `@base-ui/react/use-render`

**Dependencies:** tailwind-variants, clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Badge` -- inline badge element (default tag: `span`; supports `render` prop)

**Exported utilities:**
- `badgeVariants` -- tailwind-variants config object

**Variants (via tailwind-variants):**
- `shape`: `"simple"` | `"bar"` | `"dot"` (default: `"simple"`)
- `variant`: `"default"` | `"destructive"` | `"secondary"` | `"outline"` (default: `"default"`)
- Compound variants combine shape + variant for specific styling

**Special patterns:**
- Uses Base UI `useRender` for polymorphic rendering via `render` prop

**Example demos:**
- badge-demo.tsx
- badge-simple-shape-demo.tsx
- badge-bar-shape-demo.tsx
- badge-dot-shape-demo.tsx
- badge-default-variant-demo.tsx
- badge-destructive-variant-demo.tsx
- badge-secondary-variant-demo.tsx
- badge-outline-variant-demo.tsx
- badge-custom-demo.tsx

---

## Button

**Description:** A customizable button component

**Source:** `ui/button/index.tsx`

**Base UI primitive:** `@base-ui/react/button`

**Dependencies:** tailwind-variants, clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Button` -- button element (wraps Base UI Button)

**Exported utilities:**
- `buttonVariants` -- tailwind-variants config object

**Variants (via tailwind-variants):**
- `variant`: `"default"` | `"secondary"` | `"outline"` | `"ghost"` | `"link"` | `"destructive"` (default: `"default"`)
- `size`: `"default"` | `"xs"` | `"sm"` | `"lg"` | `"xl"` | `"icon-sm"` | `"icon"` | `"icon-lg"` | `"icon-xl"` (default: `"default"`)
- `radius`: `"none"` | `"sm"` | `"default"` | `"lg"` | `"xl"` | `"full"` (default: `"default"`)

**Special patterns:** None

**Example demos:**
- button-demo.tsx
- button-default-variant-demo.tsx
- button-secondary-variant-demo.tsx
- button-outline-variant-demo.tsx
- button-ghost-variant-demo.tsx
- button-link-variant-demo.tsx
- button-destructive-variant-demo.tsx
- button-size-demo.tsx
- button-icon-demo.tsx
- button-icon-size-demo.tsx
- button-radius-demo.tsx
- button-with-icons-demo.tsx
- button-disabled-demo.tsx
- button-loading-demo.tsx
- button-reduce-motion-demo.tsx

---

## Button Group

**Description:** A customizable button group component

**Source:** `ui/button-group/index.tsx`

**Base UI primitive:** Uses `@base-ui/react/merge-props` and `@base-ui/react/use-render`

**Dependencies:** tailwind-variants, clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** separator, classes

**Exported components:**
- `ButtonGroup` -- wrapper div with `role="group"`
- `ButtonGroupText` -- text segment within the group (supports `render` prop)
- `ButtonGroupSeparator` -- visual separator between group items (wraps Separator)

**Exported utilities:**
- `buttonGroupVariants` -- tailwind-variants config object

**Variants (via tailwind-variants):**
- `orientation`: `"horizontal"` | `"vertical"` (default: `"horizontal"`)

**Special patterns:**
- Imports `Separator` from the separator registry component
- Uses `useRender` for `ButtonGroupText` polymorphic rendering

**Example demos:**
- button-group-demo.tsx
- button-group-basic-demo.tsx
- button-group-separator-demo.tsx
- button-group-orientation-demo.tsx
- button-group-size-demo.tsx
- button-group-input-demo.tsx
- button-group-input-group-demo.tsx
- button-group-menu-demo.tsx
- button-group-nested-demo.tsx
- button-group-popover-demo.tsx
- button-group-select-demo.tsx
- button-group-split-demo.tsx

---

## Calendar

**Description:** A customizable calendar component

**Source:** `ui/calendar/index.tsx`

**Base UI primitive:** None (uses `react-day-picker`)

**Dependencies:** clsx, tailwind-merge, react-day-picker, lucide-react

**Registry dependencies:** classes, button

**Exported components:**
- `Calendar` -- date picker component (wraps react-day-picker DayPicker)

**Variants:** None (uses `classNames` prop pass-through from react-day-picker)

**Special patterns:**
- Uses the `Button` component internally for day buttons (`CalendarDayButton`)
- Uses `buttonVariants` for navigation button styling
- Registers custom CSS keyframe animations for slide transitions (defined in `registry.json` `css` field)
- Supports `captionLayout`, `showOutsideDays`, `showWeekNumber` from react-day-picker
- Range selection support via react-day-picker data attributes

**Example demos:**
- calendar-demo.tsx
- calendar-simple-demo.tsx
- calendar-animate-demo.tsx
- calendar-multiple-selection-demo.tsx
- calendar-range-selection-demo.tsx
- calendar-multiple-months-demo.tsx
- calendar-multi-months-range-selection-demo.tsx

---

## Card

**Description:** A customizable card component

**Source:** `ui/card/index.tsx`

**Base UI primitive:** None (plain HTML elements)

**Dependencies:** clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Card` -- root container div
- `CardHeader` -- header section
- `CardTitle` -- h3 title element
- `CardDescription` -- paragraph description
- `CardContent` -- main content area
- `CardFooter` -- footer section

**Variants:** None

**Special patterns:** None -- pure HTML composition with no Base UI primitives

**Example demos:**
- card-demo.tsx
- card-horizontal-layout.tsx
- card-with-image-demo.tsx
- card-with-background-images-demo.tsx

---

## Checkbox

**Description:** A customizable checkbox component

**Source:** `ui/checkbox/index.tsx`

**Base UI primitive:** `@base-ui/react` (Checkbox)

**Dependencies:** tailwind-variants, clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Checkbox` -- convenience wrapper combining CheckboxRoot + CheckboxIndicator
- `CheckboxRoot` -- root checkbox element with context provider
- `CheckboxIndicator` -- visual indicator (checkmark/indeterminate icon)

**Exported types (internal, not exported):**
- `CheckboxRootProps`
- `CheckboxIndicatorProps` (accepts custom `icon` render prop)
- `CheckboxProps`

**Variants (via tailwind-variants on `checkboxRootStyles`):**
- `size`: `"sm"` | `"default"` | `"lg"` (default: `"default"`)
- `radius`: `"none"` | `"sm"` | `"default"` | `"lg"` | `"full"` (default: `"default"`)
- `reduceMotion`: `true` | `false` (default: `false`)

**Special patterns:**
- `CheckboxContext` -- React context for checked state, indeterminate state, size, and reduceMotion
- `CheckboxIcon` -- internal SVG component with animated stroke-dashoffset for check animation
- Supports `indeterminate` state
- `CheckboxIndicator` accepts custom `icon` as ReactNode or render function

**Example demos:**
- checkbox-demo.tsx
- checkbox-sizes-demo.tsx
- checkbox-radius-demo.tsx
- checkbox-icons-demo.tsx
- checkbox-disabled-demo.tsx

---

## Collapsible

**Description:** A customizable collapsible component

**Source:** `ui/collapsible/index.tsx`

**Base UI primitive:** `@base-ui/react/collapsible`

**Dependencies:** clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Collapsible` -- root wrapper (wraps CollapsiblePrimitive.Root)
- `CollapsibleTrigger` -- clickable trigger
- `CollapsiblePanel` -- collapsible content panel

**Exported types (internal, not exported):**
- `CollapsiblePanelProps` (extends CollapsiblePrimitive.Panel.Props; adds animationPreset, transitionPreset, reduceMotion)
- `CSSAnimationPresets` (type alias)
- `CSSTransitionPresets` (type alias)

**Variants:**
- `animationPreset` (on CollapsiblePanel): `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"motion"` | `"motionBlur"` | `"perspective"` | `"perspectiveBlur"` (default: `"fade"`)
- `transitionPreset` (on CollapsiblePanel): 24 easing presets (default: `"outQuint"`)

**Special patterns:**
- CSS animation presets (`cssAnimationPresets` object) -- more presets than Accordion (adds `slideOutside`, `slideInside`, `motion`, `motionBlur`)
- CSS transition presets (`cssTransitionPresets` object) -- same 24 named easing curves
- `reduceMotion` prop disables all animations

**Example demos:**
- collapsible-demo.tsx
- collapsible-fade-demo.tsx
- collapsible-scale-demo.tsx
- collapsible-slide-outside-demo.tsx
- collapsible-slide-inside-demo.tsx
- collapsible-motion-demo.tsx
- collapsible-motion-blur-demo.tsx
- collapsible-perspective-demo.tsx
- collapsible-perspective-blur-demo.tsx

---

## Combobox

**Description:** A customizable combobox component

**Source:** `ui/combobox/index.tsx`

**Base UI primitive:** `@base-ui/react/combobox`

**Dependencies:** clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** input, classes, label, scroll-area

**Exported components:**
- `Combobox` -- root wrapper (generic: `Combobox<Value, Multiple>`)
- `ComboboxValue` -- displays selected value
- `ComboboxInput` -- input field (single mode uses Input component; multi mode uses plain input)
- `ComboboxClear` -- clear button
- `ComboboxTrigger` -- dropdown trigger button
- `ComboboxChips` -- chip container for multi-select
- `ComboboxChip` -- individual chip with remove button
- `ComboboxList` -- scrollable option list (wraps ScrollArea)
- `ComboboxPopup` -- dropdown popup (includes Portal and Positioner)
- `ComboboxEmpty` -- empty state content
- `ComboboxCollection` -- collection wrapper
- `ComboboxRow` -- row wrapper
- `ComboboxItem` -- individual option item (includes ItemIndicator)
- `ComboboxGroup` -- option group
- `ComboboxGroupLabel` -- group label
- `ComboboxSeparator` -- visual separator between groups
- `ComboboxLabel` -- label (wraps Label component)

**Exported utilities (also exported):**
- `ChevronsUpDownIcon` -- SVG icon component
- `CloseIcon` -- SVG icon component
- `CheckIcon` -- SVG icon component

**Special patterns:**
- `ComboboxContext` -- React context for `chipsRef` and `multiple` flag
- Anchors popup to `chipsRef` in multi-select mode
- Uses `Input` component from registry for single-select input rendering via `render` prop
- Uses `ScrollArea` component from registry for scrollable list
- Uses `Label` component from registry
- `isClearable` prop on ComboboxInput shows a clear button
- `showTrigger` prop on ComboboxInput controls trigger visibility

**Example demos:**
- combobox-demo.tsx
- combobox-basic-demo.tsx
- combobox-with-label-demo.tsx
- combobox-clearable-demo.tsx
- combobox-controlled-demo.tsx
- combobox-grouping-items-demo.tsx
- combobox-input-inside-popup-demo.tsx
- combobox-item-to-string-label-demo.tsx
- combobox-multiple-selection-demo.tsx
- combobox-objects-without-label-demo.tsx
- combobox-with-auto-highlighting-demo.tsx
- combobox-with-objects-items-demo.tsx

---

## Dialog

**Description:** A customizable dialog component

**Source:** `ui/dialog/index.tsx`

**Base UI primitive:** `@base-ui/react/dialog`

**Dependencies:** clsx, tailwind-merge, @base-ui/react, lucide-react

**Registry dependencies:** classes

**Exported components:**
- `Dialog` -- root wrapper with context provider
- `DialogClose` -- close button primitive
- `DialogPopup` -- dialog content panel (includes Portal, Backdrop, and close button)
- `DialogDescription` -- description text
- `DialogFooter` -- footer section (plain div)
- `DialogHeader` -- header section (plain div)
- `DialogBackdrop` -- overlay backdrop
- `DialogViewport` -- viewport container
- `DialogPortal` -- portal wrapper
- `DialogTitle` -- title element
- `DialogTrigger` -- trigger element

**Variants:**
- `animationPreset` (on DialogPopup): `"none"` | `"scale"` | `"fade"` | `"topFlip"` | `"bottomFlip"` | `"rightFlip"` | `"leftFlip"` | `"topSlide"` | `"bottomSlide"` | `"leftSlide"` | `"rightSlide"` | `"wipe"` (default: `"scale"`)
- `transitionPreset` (on DialogPopup): 24 easing presets (default: `"outCubic"`)

**Special patterns:**
- CSS animation presets specific to dialog (includes flip and wipe variants)
- `DialogContext` -- React context for `modal` state
- Supports nested dialogs via `--nested-dialogs` CSS variable
- `showCloseButton` prop on DialogPopup (default: true)
- `modal` prop on Dialog (default: true); non-modal hides backdrop
- Uses `lucide-react` XIcon for close button

**Example demos:**
- dialog-demo.tsx
- dialog-scale-demo.tsx
- dialog-fade-demo.tsx
- dialog-top-flip-demo.tsx
- dialog-bottom-flip-demo.tsx
- dialog-right-flip-demo.tsx
- dialog-left-flip-demo.tsx
- dialog-top-slide-demo.tsx
- dialog-bottom-slide-demo.tsx
- dialog-left-slide-demo.tsx
- dialog-right-slide-demo.tsx
- dialog-wipe-demo.tsx
- dialog-controlled-demo.tsx
- dialog-nested-demo.tsx
- dialog-nested-direction-aware-demo.tsx
- dialog-non-dismissible-demo.tsx
- dialog-non-modal-demo.tsx
- dialog-open-from-menu-demo.tsx
- dialog-outside-scroll-demo.tsx
- dialog-reduce-motion-demo.tsx

---

## Input

**Description:** A customizable input component

**Source:** `ui/input/index.tsx`

**Base UI primitive:** `@base-ui/react/input`

**Dependencies:** clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Input` -- text input element (wraps InputPrimitive)

**Exported types (public):**
- `InputProps` (extends InputPrimitive.Props; overrides `size`)

**Variants:**
- `size`: `"sm"` | `"default"` | `"lg"` | `number` (default: `"default"`)

**Special patterns:**
- Handles `type="search"` and `type="file"` with specific styling
- Passes numeric `size` to the underlying HTML input attribute

**Example demos:**
- input-demo.tsx
- input-controlled-demo.tsx
- input-disabled-demo.tsx
- input-file-type-demo.tsx
- input-small-demo.tsx
- input-large-demo.tsx
- input-types-demo.tsx

---

## Input Group

**Description:** A customizable input group component

**Source:** `ui/input-group/index.tsx`

**Base UI primitive:** None directly (composes Input, Textarea, Button)

**Dependencies:** clsx, tailwind-merge, tailwind-variants, @base-ui/react

**Registry dependencies:** input, textarea, button, classes

**Exported components:**
- `InputGroup` -- root container div with `role="group"`
- `InputGroupAddon` -- addon wrapper for icons, buttons, or text (supports `align` prop)
- `InputGroupButton` -- button within the group (wraps Button)
- `InputGroupText` -- text content within the group
- `InputGroupInput` -- styled input for use inside the group (wraps Input)
- `InputGroupTextarea` -- styled textarea for use inside the group (wraps Textarea)

**Exported utilities (internal, not exported):**
- `inputGroupAddonVariants` -- tailwind-variants for addon alignment
- `inputGroupButtonVariants` -- tailwind-variants for button sizes

**Variants:**
- `InputGroupAddon.align`: `"inline-start"` | `"inline-end"` | `"block-start"` | `"block-end"` (default: `"inline-start"`)
- `InputGroupButton.size`: `"xs"` | `"sm"` | `"icon-xs"` | `"icon-sm"` (default: `"xs"`)

**Special patterns:**
- Composes Input, Textarea, and Button from other registry components
- Uses CSS `has-[]` selectors for focus and error state propagation from child inputs

**Example demos:**
- input-group-demo.tsx
- input-group-icon-demo.tsx
- input-group-text-demo.tsx
- input-group-button-demo.tsx
- input-group-label-demo.tsx
- input-group-spinner-demo.tsx
- input-group-textarea-demo.tsx
- input-group-menu-demo.tsx
- input-group-tooltip-demo.tsx

---

## Input OTP

**Description:** A customizable input OTP component

**Source:** `ui/input-otp/index.tsx`

**Base UI primitive:** None (uses `input-otp` library and `motion/react`)

**Dependencies:** tailwind-variants, clsx, tailwind-merge, input-otp, motion

**Registry dependencies:** classes

**Exported components:**
- `InputOTP` -- root OTP input (wraps `OTPInput` from input-otp)
- `InputOTPGroup` -- visual grouping wrapper
- `InputOTPSlot` -- individual digit slot with animated indicator
- `InputOTPSeparator` -- visual separator between groups

**Exported hooks:**
- `useInputOTPContext` -- hook for accessing OTP context

**Utilities (internal, not exported):**
- `inputOtpSlotVariants` -- tailwind-variants for slot styling
- `inputOtpSlotIndicatorVariants` -- tailwind-variants for active indicator

**Variants:**
- `variant` (on InputOTP): `"bordered"` | `"underlined"` (default: `"bordered"`)
- `slotSize` (on InputOTP): `"sm"` | `"md"` | `"lg"` (default: `"md"`)

**Special patterns:**
- Uses `motion/react` (AnimatePresence, motion, MotionConfig) for slot animations
- `InputOTPContext` -- React context for variant and slot size
- `InputOTPAnimatedNumber` -- animated number display with enter/exit transitions
- `FakeCaret` -- blinking caret indicator
- `MotionConfig` with `reducedMotion="user"` for accessibility
- Animated layout indicator that slides between active slots (`layoutId`)

**Example demos:**
- input-otp-demo.tsx
- input-otp-controlled-demo.tsx
- input-otp-disabled-demo.tsx
- input-otp-patterns-demo.tsx
- input-otp-separator-demo.tsx
- input-otp-sizes-demo.tsx
- input-otp-variants-demo.tsx

---

## Kbd

**Description:** A customizable kbd component

**Source:** `ui/kbd/index.tsx`

**Base UI primitive:** None (plain HTML elements)

**Dependencies:** clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Kbd` -- keyboard shortcut indicator (`<kbd>` element)
- `KbdGroup` -- wrapper for grouping multiple Kbd elements

**Variants:** None

**Special patterns:** None

**Example demos:**
- kbd-demo.tsx
- kbd-group-demo.tsx
- kbd-button-demo.tsx
- kbd-input-group-demo.tsx
- kbd-tooltip-demo.tsx

---

## Label

**Description:** A customizable label component

**Source:** `ui/label/index.tsx`

**Base UI primitive:** None (plain HTML `<label>` element)

**Dependencies:** clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Label` -- label element

**Variants:** None

**Special patterns:** None

**Example demos:**
- label-demo.tsx
- label-with-checkbox.tsx

---

## Menu

**Description:** A customizable menu component

**Source:** `ui/menu/index.tsx`

**Base UI primitive:** `@base-ui/react/menu`

**Dependencies:** @base-ui/react, clsx, tailwind-merge, lucide-react

**Registry dependencies:** classes

**Exported components:**
- `Menu` -- root wrapper with context provider
- `MenuTrigger` -- trigger element
- `MenuPopup` -- dropdown popup (includes Positioner, Portal, and Backdrop)
- `MenuGroup` -- item group
- `MenuGroupLabel` -- group label
- `MenuItem` -- menu item
- `MenuSeparator` -- visual separator
- `MenuCheckboxItem` -- checkbox menu item (includes CheckboxItemIndicator)
- `MenuRadioGroup` -- radio group wrapper with context for custom icon
- `MenuRadioItem` -- radio menu item (includes RadioItemIndicator)
- `MenuSub` -- submenu root
- `MenuSubTrigger` -- submenu trigger (includes chevron icon)
- `MenuSubPopup` -- submenu popup (includes sub-positioner and sub-portal)
- `MenuShortcut` -- keyboard shortcut display
- `MenuLabel` -- standalone label (plain span)

**Variants:**
- `animationPreset` (on MenuPopup): `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"` (default: `"scale"`)
- `transitionPreset` (on MenuPopup): 24 easing presets (default: `"snappyOut"`)
- `backdrop` (on Menu): `"opaque"` | `"blur"` | `"transparent"` (default: `"transparent"`)

**Special patterns:**
- CSS animation/transition presets with side-aware animations
- `MenuContext` -- React context for backdrop setting
- `MenuRadioGroupContext` -- React context for custom `activeIcon`
- `showArrow` prop on MenuPopup for arrow indicator (includes custom ArrowSvg)
- Uses `lucide-react` for CheckIcon, ChevronRightIcon, CircleIcon

**Example demos:**
- menu-demo.tsx
- menu-basic-demo.tsx
- menu-scale-demo.tsx
- menu-slide-outside-demo.tsx
- menu-slide-inside-demo.tsx
- menu-wipe-demo.tsx
- menu-wipe-scale-demo.tsx
- menu-motion-demo.tsx
- menu-motion-blur-demo.tsx
- menu-checkboxes-demo.tsx
- menu-radio-group-demo.tsx
- menu-radiogroup-with-custom-icon-demo.tsx
- menu-nested-demo.tsx
- menu-sides-demo.tsx
- menu-with-arrow-demo.tsx
- menu-with-groups-demo.tsx
- menu-with-hover-demo.tsx

---

## Number Field

**Description:** A customizable number field component

**Source:** `ui/number-field/index.tsx`

**Base UI primitive:** `@base-ui/react/number-field`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `NumberField` -- root wrapper
- `NumberFieldGroup` -- input group container
- `NumberFieldInput` -- numeric input
- `NumberFieldDecrement` -- decrement button (includes MinusIcon)
- `NumberFieldIncrement` -- increment button (includes PlusIcon)
- `NumberFieldScrubArea` -- scrub area for drag-to-change (includes ScrubAreaCursor)

**Variants:** None

**Special patterns:**
- Internal SVG icon components: `PlusIcon`, `MinusIcon`, `CursorGrowIcon`
- Scrub area with custom cursor icon for drag-to-change interaction

**Example demos:**
- number-field-demo.tsx
- number-field-default-demo.tsx
- number-field-controlled-demo.tsx
- number-field-disabled-demo.tsx
- number-field-formatting-demo.tsx
- number-field-range-demo.tsx
- number-field-step-demo.tsx
- number-field-up-down-demo.tsx
- number-field-with-scrub-demo.tsx
- number-field-mouse-wheel-scrub-demo.tsx
- number-field-together-demo.tsx

---

## Popover

**Description:** A customizable popover component

**Source:** `ui/popover/index.tsx`

**Base UI primitive:** `@base-ui/react/popover`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Popover` -- root wrapper with context provider
- `PopoverTrigger` -- trigger element
- `PopoverPopup` -- popup content (includes Positioner, Portal, Backdrop)
- `PopoverViewport` -- viewport wrapper
- `PopoverTitle` -- title element
- `PopoverDescription` -- description element

**Variants:**
- `animationPreset` (on PopoverPopup): `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"` (default: `"scale"`)
- `transitionPreset` (on PopoverPopup): 24 easing presets (default: `"snappyOut"`)
- `backdrop` (on Popover): `"opaque"` | `"blur"` | `"transparent"` (default: `"transparent"`)

**Special patterns:**
- CSS animation/transition presets with side-aware animations
- `PopoverContext` -- React context for backdrop setting
- `showArrow` prop on PopoverPopup for arrow indicator (includes custom ArrowSvg)
- Side/align/offset positioning props forwarded to Positioner

**Example demos:**
- popover-demo.tsx
- popover-controlled-demo.tsx
- popover-custom-trigger-demo.tsx
- popover-sides-demo.tsx
- popover-offset-demo.tsx
- popover-backdrop-demo.tsx
- popover-modality-demo.tsx
- popover-with-arrow-demo.tsx
- popover-with-form-demo.tsx
- popover-with-hover-demo.tsx

---

## Radio Group

**Description:** A customizable radio group component

**Source:** `ui/radio-group/index.tsx`

**Base UI primitive:** `@base-ui/react/radio`, `@base-ui/react/radio-group`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `RadioGroup` -- group container (wraps RadioGroupPrimitive)
- `Radio` -- individual radio button (wraps RadioPrimitive.Root; includes RadioPrimitive.Indicator)

**Variants:**
- `orientation` (on RadioGroup): `"horizontal"` | `"vertical"` (default: `"vertical"`)

**Special patterns:**
- Radio includes its own Indicator inline (not a separate export)
- CSS pseudo-element animation for checked/unchecked state

**Example demos:**
- radio-group-demo.tsx
- radio-group-basic-demo.tsx
- radio-group-controlled-demo.tsx
- radio-group-orientation-demo.tsx
- radio-group-disabled-demo.tsx
- radio-group-with-description-demo.tsx
- radio-group-custom-layout-demo.tsx

---

## Scroll Area

**Description:** A customizable scroll area component

**Source:** `ui/scroll-area/index.tsx`

**Base UI primitive:** `@base-ui/react/scroll-area`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `ScrollArea` -- root scroll container (wraps Viewport, Scrollbar, Corner)
- `ScrollAreaContent` -- content wrapper (wraps ScrollAreaPrimitive.Content)
- `ScrollBar` -- scrollbar element (wraps ScrollAreaPrimitive.Scrollbar + Thumb)

**Variants:**
- `orientation` (on ScrollArea): `"horizontal"` | `"vertical"` | `"both"` (default: `"vertical"`)
- `scrollShadow` (on ScrollArea): `"vertical"` | `"horizontal"` | `"both"` | `"none"` (default: `"none"`)

**Special patterns:**
- Scroll shadow effect using CSS gradient pseudo-elements (`::before`, `::after`)
- Shadow visibility driven by `--scroll-area-overflow-*` CSS variables from Base UI
- Auto-hides scrollbar with opacity transitions

**Example demos:**
- scroll-area-demo.tsx
- scroll-area-horizontal-demo.tsx
- scroll-area-both-scroll-demo.tsx
- scroll-area-vertical-shadow-demo.tsx
- scroll-area-horizontal-shadow-demo.tsx
- scroll-area-both-shadow-demo.tsx

---

## Select

**Description:** A customizable select component

**Source:** `ui/select/index.tsx`

**Base UI primitive:** `@base-ui/react/select`

**Dependencies:** @base-ui/react, clsx, tailwind-merge, lucide-react

**Registry dependencies:** classes

**Exported components:**
- `Select` -- root wrapper with context provider
- `SelectTrigger` -- trigger button
- `SelectValue` -- displays selected value (with placeholder support)
- `SelectIcon` -- dropdown icon
- `SelectPopup` -- popup content (includes Positioner, Portal, Backdrop, ScrollUpArrow, ScrollDownArrow)
- `SelectList` -- scrollable list of options
- `SelectItem` -- individual option
- `SelectItemText` -- option text
- `SelectItemIndicator` -- selection indicator
- `SelectGroup` -- option group
- `SelectGroupLabel` -- group label
- `SelectScrollUpArrow` -- scroll up indicator
- `SelectScrollDownArrow` -- scroll down indicator
- `SelectSeparator` -- visual separator

**Variants:**
- `animationPreset` (on SelectPopup): `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"` (default: `"scale"`)
- `transitionPreset` (on SelectPopup): 24 easing presets (default: `"outQuint"`)
- `backdrop` (on Select): `"opaque"` | `"blur"` | `"transparent"` (default: `"transparent"`)

**Special patterns:**
- CSS animation/transition presets with side-aware animations
- `SelectContext` -- React context for backdrop setting
- `showArrow` prop on SelectPopup
- `alignItemWithTrigger` prop enables aligned item selection mode (different rendering path)
- Uses `lucide-react` ChevronDownIcon, ChevronUpIcon for scroll arrows
- `SelectValue` uses `render` prop for custom placeholder rendering

**Example demos:**
- select-demo.tsx
- select-basic-demo.tsx
- select-country-demo.tsx
- select-formatting-country-demo.tsx
- select-formatting-value.tsx
- select-object-values-demo.tsx
- select-multiple-selection-demo.tsx
- select-scale-demo.tsx
- select-wipe-demo.tsx
- select-wipe-scale-demo.tsx
- select-motion-demo.tsx
- select-motion-blur-demo.tsx

---

## Separator

**Description:** A customizable separator component

**Source:** `ui/separator/index.tsx`

**Base UI primitive:** `@base-ui/react/separator`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Separator` -- horizontal or vertical separator line

**Variants:**
- `orientation`: `"horizontal"` | `"vertical"` (default: `"horizontal"`)

**Special patterns:** None

**Example demos:**
- separator-demo.tsx

---

## Sheet

**Description:** A customizable sheet component

**Source:** `ui/sheet/index.tsx`

**Base UI primitive:** `@base-ui/react/dialog` (reuses Dialog primitive)

**Dependencies:** @base-ui/react, clsx, tailwind-merge, tailwind-variants

**Registry dependencies:** classes

**Note:** Source also imports `lucide-react` (XIcon) but it is not listed in registry.json dependencies.

**Exported components:**
- `Sheet` -- root wrapper (wraps DialogPrimitive.Root)
- `SheetTrigger` -- trigger element
- `SheetClose` -- close button primitive
- `SheetPopup` -- sheet panel (includes Portal, Backdrop, Viewport, and close button)
- `SheetHeader` -- header section (plain div)
- `SheetFooter` -- footer section (plain div)
- `SheetTitle` -- title element
- `SheetDescription` -- description text

**Exported utilities (internal, not exported):**
- `sheetVariants` -- tailwind-variants with slot variants (`viewport`, `popup`)

**Variants (via tailwind-variants slots):**
- `side`: `"right"` | `"left"` | `"top"` | `"bottom"` (default: `"right"`)
- `variant`: `"full"` | `"rounded"` (default: `"full"`)

**Special patterns:**
- Built on Dialog primitive (not a separate Base UI Sheet primitive)
- Uses `tailwind-variants` slot variants for coordinated viewport + popup styling
- Supports nested sheets via `--nested-dialogs` CSS variable
- `showCloseButton` prop (default: true)
- `reduceMotion` prop disables transitions
- Uses `lucide-react` XIcon for close button

**Example demos:**
- sheet-demo.tsx
- sheet-side-demo.tsx
- sheet-size-demo.tsx
- sheet-variant-demo.tsx
- sheet-nested-demo.tsx
- sheet-reduce-motion-demo.tsx

---

## Spinner

**Description:** A customizable spinner component

**Source:** `ui/spinner/index.tsx`

**Base UI primitive:** None (custom SVG with animateTransform)

**Dependencies:** tailwind-variants, tailwind-merge, @base-ui/react, clsx

**Registry dependencies:** classes

**Exported components:**
- `Spinner` -- loading spinner (wraps internal SpinnerPrimitive SVG)

**Variants (via tailwind-variants):**
- `size`: `"sm"` | `"md"` | `"lg"` | `"xl"` (default: `"md"`)

**Special patterns:**
- Internal `SpinnerPrimitive` SVG with `animateTransform` for rotation
- Auto-sizes when used inside toast content via `in-data-[slot='toast-content']` selector

**Example demos:**
- spinner-demo.tsx
- spinner-sizes-demo.tsx

---

## Switch

**Description:** A customizable switch component

**Source:** `ui/switch/index.tsx`

**Base UI primitive:** `@base-ui/react/switch`

**Dependencies:** clsx, tailwind-merge, @base-ui/react

**Registry dependencies:** classes

**Exported components:**
- `Switch` -- toggle switch (wraps SwitchPrimitive.Root; includes SwitchPrimitive.Thumb inline)

**Variants:**
- `size`: `"sm"` | `"md"` | `"lg"` (default: `"md"`)
- `reduceMotion`: boolean (default: false)
- `isInteractive`: boolean (default: false) -- enables press-to-stretch animation on thumb

**Special patterns:**
- Thumb is rendered inline within Switch (not a separate export)
- `isInteractive` enables a press animation that stretches the thumb width on click

**Example demos:**
- switch-demo.tsx
- switch-controlled-demo.tsx
- switch-disabled-demo.tsx
- switch-sizes-demo.tsx
- switch-interactive-demo.tsx
- switch-reduce-motion-demo.tsx
- switch-with-icons-demo.tsx
- switch-with-label.tsx
- custom-switch-card-style-demo.tsx

---

## Tabs

**Description:** A customizable tabs component

**Source:** `ui/tabs/index.tsx`

**Base UI primitive:** `@base-ui/react/tabs`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Tabs` -- root wrapper with context provider
- `TabsList` -- tab list container (includes animated Indicator)
- `TabsTrigger` -- individual tab button
- `TabsPanelsWrapper` -- animated height container for tab panels (uses ResizeObserver)
- `TabsPanel` -- tab panel content

**Variants:**
- `variant` (on Tabs): `"segmented"` | `"underline"` | `"card"` (default: `"segmented"`)

**Special patterns:**
- `TabsContext` -- React context for variant
- Animated tab indicator using Base UI `Tabs.Indicator` with CSS transitions
- `TabsPanelsWrapper` uses ResizeObserver to animate panel height changes
- Supports horizontal and vertical orientations via Base UI `orientation` prop

**Example demos:**
- tabs-demo.tsx
- tabs-segmented-demo.tsx
- tabs-underline-demo.tsx
- tabs-card-demo.tsx
- tabs-horizontal-orientation-demo.tsx
- tabs-vertical-orientation-demo.tsx
- tabs-panel-demo.tsx
- tabs-auto-height-demo.tsx

---

## Textarea

**Description:** A customizable textarea component

**Source:** `ui/textarea/index.tsx`

**Base UI primitive:** `@base-ui/react/field` (uses Field.Control with render prop)

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Textarea` -- textarea element (renders via Field.Control render prop)

**Exported types (public):**
- `TextareaProps` (extends React.ComponentProps<"textarea">; adds `size`)

**Variants:**
- `size`: `"sm"` | `"default"` | `"lg"` | `number` (default: `"default"`)

**Special patterns:**
- Uses `field-sizing-content` CSS for auto-sizing
- Wraps in `FieldPrimitive.Control` with `render` prop for Base UI field integration
- Uses `mergeProps` from Base UI for prop merging

**Example demos:**
- textarea-demo.tsx
- textarea-controlled-demo.tsx
- textarea-disabled-demo.tsx
- textarea-small-size-demo.tsx
- textarea-large-size-demo.tsx

---

## Toast

**Description:** A customizable toast component

**Source:** `ui/toast/index.tsx`

**Base UI primitive:** `@base-ui/react/toast`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** button, spinner, classes

**Exported components:**
- `ToastProvider` -- toast provider and viewport (wraps Toast.Provider; renders ToastList)

**Exported utilities:**
- `toast` -- toast manager instance (created via `Toast.createToastManager()`)

**Exported types:**
- `ToastPosition` -- `"top-left"` | `"top-center"` | `"top-right"` | `"bottom-left"` | `"bottom-center"` | `"bottom-right"`

**Variants:**
- `position` (on ToastProvider): 6 position values (default: `"bottom-right"`)
- `radius` (on toast data): `"none"` | `"sm"` | `"md"` | `"lg"` | `"full"` (default: `"md"`)

**Special patterns:**
- Uses `Toast.createToastManager()` to create a singleton manager exported as `toast`
- Renders all toast types (loading, success, error, info, warning) with type-specific icons
- Internal icon components: `WarningIcon`, `SuccessIcon`, `DangerIcon`, `InfoIcon`
- Uses `buttonVariants` from Button for action button styling
- Uses `Spinner` from Spinner for loading state
- Complex stacking/animation system using CSS custom properties (`--toast-index`, `--toast-scale`, etc.)
- Swipe-to-dismiss with direction-aware animations
- Expandable toast stack on hover

**Example demos:**
- toast-demo.tsx
- toast-action-demo.tsx
- toast-loading-demo.tsx
- toast-positions-demo.tsx
- toast-promise-demo.tsx
- toast-radius-demo.tsx
- toast-with-status-demo.tsx

---

## Tooltip

**Description:** A customizable tooltip component

**Source:** `ui/tooltip/index.tsx`

**Base UI primitive:** `@base-ui/react/tooltip`

**Dependencies:** @base-ui/react, clsx, tailwind-merge

**Registry dependencies:** classes

**Exported components:**
- `Tooltip` -- root wrapper
- `TooltipTrigger` -- trigger element
- `TooltipPopup` -- popup content (includes Positioner and Portal)
- `TooltipProvider` -- provider for shared tooltip delay settings

**Variants:**
- `animationPreset` (on TooltipPopup): `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"` (default: `"scale"`)
- `transitionPreset` (on TooltipPopup): 24 easing presets plus `"none"` (default: `"outQuint"`)

**Special patterns:**
- CSS animation/transition presets with side-aware animations
- `showArrow` prop on TooltipPopup -- uses CSS pseudo-element for arrow (not a separate component)
- `delay` prop on TooltipProvider (default: 300ms)
- `data-instant` attribute disables duration for instant tooltips

**Example demos:**
- tooltip-demo.tsx
- tooltip-scale-demo.tsx
- tooltip-fade-demo.tsx
- tooltip-slide-outside-demo.tsx
- tooltip-slide-inside-demo.tsx
- tooltip-wipe-demo.tsx
- tooltip-wipe-scale-demo.tsx
- tooltip-motion-demo.tsx
- tooltip-motion-blur-demo.tsx
- tooltip-sides-demo.tsx
- tooltip-offset-demo.tsx
- tooltip-delay-demo.tsx
- tooltip-controlled-demo.tsx
- tooltip-with-arrow-demo.tsx
- tooltip-custom-content.tsx
