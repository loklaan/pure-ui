## Calendar

A date picker component that allows users to select dates. Calendar supports single date selection, multiple date selection, and date range selection across one or multiple months.

Calendar does not use a Base UI primitive. It wraps `react-day-picker` (`DayPicker`) and uses the Pure UI `Button` component for day buttons and navigation styling.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/calendar"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge react-day-picker lucide-react
pnpm add clsx tailwind-merge react-day-picker lucide-react
yarn add clsx tailwind-merge react-day-picker lucide-react
bun add clsx tailwind-merge react-day-picker lucide-react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/calendar.tsx`.

4. Add the Button component (registry dependency). Calendar uses the `Button` and `buttonVariants` exports internally.

5. Add calendar keyframes to your global CSS. These are required for the `animate` prop to work:

```css
@keyframes rdp-slide_in_left {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(0); }
}

@keyframes rdp-slide_in_right {
  0% { transform: translateX(100%); }
  100% { transform: translateX(0); }
}

@keyframes rdp-slide_out_left {
  0% { transform: translateX(0); }
  100% { transform: translateX(-100%); }
}

@keyframes rdp-slide_out_right {
  0% { transform: translateX(0); }
  100% { transform: translateX(100%); }
}

@keyframes rdp-fade_in {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes rdp-fade_out {
  from { opacity: 1; }
  to { opacity: 0; }
}

.rdp-weeks_before_enter {
  animation: rdp-slide_in_left var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-weeks_before_exit {
  animation: rdp-slide_out_left var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-weeks_after_enter {
  animation: rdp-slide_in_right var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-weeks_after_exit {
  animation: rdp-slide_out_right var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-caption_after_enter {
  animation: rdp-fade_in var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-caption_after_exit {
  animation: rdp-fade_out var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-caption_before_enter {
  animation: rdp-fade_in var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

.rdp-caption_before_exit {
  animation: rdp-fade_out var(--rdp-animation_duration, 0.3s)
    var(--rdp-animation_timing, cubic-bezier(0.4, 0, 0.2, 1)) forwards;
}

@media (prefers-reduced-motion: reduce) {
  .rdp-weeks_before_enter,
  .rdp-weeks_before_exit,
  .rdp-weeks_after_enter,
  .rdp-weeks_after_exit,
  .rdp-caption_after_enter,
  .rdp-caption_after_exit,
  .rdp-caption_before_enter,
  .rdp-caption_before_exit {
    animation: none;
  }
}
```

When installing via CLI, the keyframes are added automatically.

### Anatomy

```tsx
import { Calendar } from "@/components/ui/calendar";

<Calendar mode="single" />
```

Calendar is a single exported component. All sub-parts (navigation buttons, day buttons, week numbers) are composed internally.

### Props

#### Calendar

Accepts all props from `react-day-picker` `DayPicker`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| mode | "single" \| "multiple" \| "range" | -- | Selection mode |
| selected | Date \| Date[] \| DateRange \| undefined | -- | Currently selected date(s) |
| onSelect | function | -- | Callback when selection changes |
| showOutsideDays | boolean | true | Show days from adjacent months |
| captionLayout | "label" \| "dropdown" \| "dropdown-months" \| "dropdown-years" | "label" | Layout of the month/year caption |
| numberOfMonths | number | 1 | Number of months to display |
| animate | boolean | -- | Enable slide and fade animations when navigating months |
| defaultMonth | Date | -- | Initial month to display |
| classNames | object | -- | Override internal class names for each calendar part |
| components | object | -- | Override internal sub-components |
| formatters | object | -- | Override date formatting functions |
| disabled | Matcher \| Matcher[] | -- | Dates to disable |
| required | boolean | -- | Require at least one date to be selected |
| max | number | -- | Maximum number of selectable dates (multiple mode) |
| showWeekNumber | boolean | -- | Show week numbers column |

### Usage

#### Basic

```tsx
import { Calendar } from "@/components/ui/calendar";

export function CalendarBasicExample() {
  return <Calendar mode="single" />;
}
```

#### Controlled Single Selection

Use `selected` and `onSelect` to control the selected date.

```tsx
"use client";

import { useState } from "react";
import { Calendar } from "@/components/ui/calendar";

export function CalendarControlledExample() {
  const [date, setDate] = useState<Date | undefined>(new Date());

  return (
    <Calendar
      animate
      mode="single"
      defaultMonth={date}
      selected={date}
      onSelect={setDate}
    />
  );
}
```

#### Animated Navigation

Pass the `animate` prop to enable slide transitions when navigating between months.

```tsx
import { Calendar } from "@/components/ui/calendar";

export function CalendarAnimateExample() {
  return <Calendar animate mode="single" />;
}
```

#### Multiple Date Selection

Set `mode="multiple"` to allow selecting more than one date. Use `max` to limit the number of selectable dates.

```tsx
"use client";

import { useState } from "react";
import { Calendar } from "@/components/ui/calendar";

export function CalendarMultipleSelectionExample() {
  const [dates, setDates] = useState<Date[]>([
    new Date(2025, 5, 12),
    new Date(2025, 6, 24),
  ]);

  return (
    <Calendar
      animate
      mode="multiple"
      numberOfMonths={2}
      defaultMonth={dates[0]}
      required
      selected={dates}
      onSelect={setDates}
      max={5}
    />
  );
}
```

#### Range Selection

Set `mode="range"` to select a date range. The selected value uses the `DateRange` type from `react-day-picker`.

```tsx
"use client";

import { useState } from "react";
import { type DateRange } from "react-day-picker";
import { Calendar } from "@/components/ui/calendar";

export function CalendarRangeSelectionExample() {
  const [dateRange, setDateRange] = useState<DateRange | undefined>({
    from: new Date(2025, 5, 9),
    to: new Date(2025, 5, 26),
  });

  return (
    <Calendar
      animate
      mode="range"
      defaultMonth={dateRange?.from}
      selected={dateRange}
      onSelect={setDateRange}
    />
  );
}
```

#### Multiple Months

Use `numberOfMonths` to display more than one month side by side.

```tsx
"use client";

import { useState } from "react";
import { Calendar } from "@/components/ui/calendar";

export function CalendarMultipleMonthsExample() {
  const [date, setDate] = useState<Date | undefined>(new Date(2025, 5, 12));

  return (
    <Calendar
      animate
      mode="single"
      defaultMonth={date}
      numberOfMonths={2}
      selected={date}
      onSelect={setDate}
    />
  );
}
```

#### Multiple Months with Range Selection

Combine `numberOfMonths` and `mode="range"` to select a range spanning multiple months.

```tsx
"use client";

import { useState } from "react";
import { type DateRange } from "react-day-picker";
import { Calendar } from "@/components/ui/calendar";

export function CalendarMultiMonthsRangeExample() {
  const [dateRange, setDateRange] = useState<DateRange | undefined>({
    from: new Date(2025, 5, 12),
    to: new Date(2025, 6, 15),
  });

  return (
    <Calendar
      animate
      mode="range"
      defaultMonth={dateRange?.from}
      selected={dateRange}
      onSelect={setDateRange}
      numberOfMonths={2}
    />
  );
}
```

### Notes

- Calendar requires the `"use client"` directive when using controlled state (`selected`/`onSelect`).
- The `animate` prop enables slide-in/slide-out transitions for month navigation. These rely on CSS keyframes that must be present in your global styles. The CLI installation adds them automatically; manual installation requires copying the keyframes from the installation section above.
- Animations respect `prefers-reduced-motion: reduce` and are disabled automatically when the user has this preference set.
- The `classNames` prop accepts an object keyed by react-day-picker class name slots. Use it to override styling of individual calendar parts (nav, day, weekday, etc.).
- The `components` prop allows replacing internal sub-components (Root, Chevron, DayButton, WeekNumber). Calendar provides styled defaults for each.
- Calendar uses the `Button` component internally for day cells. The day buttons render with `variant="ghost"` and `size="icon-sm"`.
- The `captionLayout` prop controls whether the month/year caption is a static label (`"label"`) or a dropdown (`"dropdown"`). When set to `"dropdown"`, the month dropdown formats months using short names (e.g. "Jan", "Feb").
- RTL direction is supported. Animation directions reverse automatically when the root element has `dir="rtl"`.
