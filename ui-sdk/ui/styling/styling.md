# Styling Guide

## Prerequisites

### 1. Tailwind CSS Installation

First, ensure you have Tailwind CSS installed in your project:

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### 2. Tailwind Configuration

Add the Alquimia UI path to your `tailwind.config.js`:

```javascript
const baseConfig = require("@alquimia-ai/ui/tailwind.config")

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
    ...baseConfig.content,
  ],
  theme: {
    extend: {
      // Your custom theme extensions
    },
  },
  plugins: [
    require("tailwindcss-animate"),
    // Your other plugins
  ],
}
```
### 3. Global Stylesheet

Create or update your global stylesheet to import Tailwind's base styles:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Styling Components

### 1. Using className Prop

All Alquimia UI components accept a `className` prop for custom styling:

```tsx
<Button className="my-custom-class">
  Click me
</Button>
```

### 2. Direct Component Targeting

All components can be targeted using the `alq--` prefix convention. Here's a list of available selectors:

```css
/* Assistant Components */
.alq--assistant-button-send
.alq--drawer-assistant-header
.alq--card-container
.alq--callout-box
.alq--callout-box
.alq--callout-date
.alq--callout-actions
.alq--callout-clicked-action
.alq--messages-window

/* Basic Elements */
.alq--avatar
.alq--badge
.alq--button
.alq--callout-box
.alq--card
.alq--checkbox
.alq--dialog
.alq--drawer
.alq--input
.alq--label
.alq--radio
.alq--select
.alq--slider
.alq--switch
.alq--tabs
.alq--textarea
.alq--toast
.alq--toggle
.alq--typography
```

Example usage in your CSS:

```css
.alq--badge {
  /* Custom styles for all badges */
  border-width: 2px;
}

.alq--assistant-button-send {
  /* Custom styles for assistant send button */
  background-color: #0066cc;
}
```

### 3. Component Variants

Many components come with built-in variants that can be combined with custom classes:

```tsx
<Badge 
  variant="secondary" 
  className="my-custom-badge"
>
  Label
</Badge>
```