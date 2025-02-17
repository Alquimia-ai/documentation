# Using Custom Themes with Tailwind CSS

Alquimia UI provides custom stylesheets that allow users to easily apply different themes to their assistant. These stylesheets are designed to be used alongside Tailwind CSS and should be imported into your global CSS file.

## Base styles

The base styles are provided in the `base.css` file. This file contains the foundational styling for the assistant, ensuring proper layout and basic styles.

## How to Use Custom Themes

To integrate a theme, import the corresponding CSS file in your global CSS file before the Tailwind directives:

```css
@import "@alquimia-ai/ui/styles/themes/base-nordic.css";

@tailwind base;
@tailwind components;
@tailwind utilities;

body {
  color: var(--foreground);
  background: var(--background);
  font-family: Arial, Helvetica, sans-serif;
}

html, body {
  height: 100%;
  margin: 0;
  padding: 0;
}
```

## Available Themes

### Base Theme
`base.css` provides the foundational styling for the assistant, ensuring proper layout and basic styles.

### Color Themes
On top of the base styling, the following themes provide predefined color schemes:

- **`base-primary.css`** – A general-purpose primary theme.
- **`base-nordic.css`** – A cool-toned, nordic-inspired color palette.
- **`base-alquimia.css`** – A theme aligned with Alquimia AI’s brand identity.

## Switching Themes

To switch themes, simply update the `@import` statement in your global CSS file to reference a different theme file. For example:

```css
@import "@alquimia-ai/ui/styles/themes/base-alquimia.css";
```

This system allows for easy customization and seamless integration of different styles without modifying component-level code.

## Summary
- **Base styles** are provided in `base.css`.
- **Color themes** (`base-primary.css`, `base-nordic.css`, `base-alquimia.css`) offer different visual styles.
- **Themes should be imported in the global CSS file** before Tailwind directives.
- **Switching themes** is as simple as changing the `@import` reference.

By leveraging these predefined styles, you can effortlessly adapt the assistant's look to match your application's aesthetic.

