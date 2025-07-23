# Design Tokens

## Typography System

### Font Families
```css
--font-primary: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
--font-monospace: 'SF Mono', Monaco, 'Cascadia Code', 'Roboto Mono', Consolas, monospace;
--font-heading: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
```

### Font Sizes
```css
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */
--text-4xl: 2.25rem;   /* 36px */
```

### Font Weights
```css
--font-light: 300;
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

## Color Palette

### Primary Colors
```css
--serena-blue: #2563eb;         /* Primary brand blue */
--serena-blue-dark: #1d4ed8;    /* Darker variant */
--serena-blue-light: #3b82f6;   /* Lighter variant */
```

### Semantic Colors
```css
--success: #10b981;             /* #10b981 - Success/confirmation */
--warning: #f59e0b;             /* #f59e0b - Warning/caution */
--error: #ef4444;               /* #ef4444 - Error/danger */
--info: #3b82f6;                /* #3b82f6 - Information */
```

### Neutral Colors
```css
--gray-50: #f9fafb;
--gray-100: #f3f4f6;
--gray-200: #e5e7eb;
--gray-300: #d1d5db;
--gray-400: #9ca3af;
--gray-500: #6b7280;
--gray-600: #4b5563;
--gray-700: #374151;
--gray-800: #1f2937;
--gray-900: #111827;
```

### Code Syntax Colors
```css
--syntax-keyword: #7c3aed;      /* Purple for keywords */
--syntax-string: #059669;       /* Green for strings */
--syntax-number: #dc2626;       /* Red for numbers */
--syntax-comment: #6b7280;      /* Gray for comments */
--syntax-function: #2563eb;     /* Blue for functions */
--syntax-variable: #374151;     /* Dark gray for variables */
```

## Visual Effects

### Shadows
```css
--shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
--shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
--shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
--shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
--shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
```

### Border Radius
```css
--radius-sm: 0.125rem;   /* 2px */
--radius: 0.25rem;       /* 4px */
--radius-md: 0.375rem;   /* 6px */
--radius-lg: 0.5rem;     /* 8px */
--radius-xl: 0.75rem;    /* 12px */
--radius-2xl: 1rem;      /* 16px */
--radius-full: 9999px;   /* Full circle */
```

### Transitions
```css
--transition-fast: 150ms ease-in-out;
--transition-normal: 250ms ease-in-out;
--transition-slow: 350ms ease-in-out;
```

## Component Design System

### Dashboard Interface
The web dashboard uses a clean, developer-focused design:

```css
.dashboard {
  background: var(--gray-50);
  font-family: var(--font-primary);
  color: var(--gray-900);
}

.dashboard-header {
  background: white;
  border-bottom: 1px solid var(--gray-200);
  padding: 1rem 2rem;
  box-shadow: var(--shadow-sm);
}

.dashboard-nav {
  background: var(--gray-800);
  color: white;
  width: 250px;
}

.dashboard-content {
  background: white;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow);
  padding: 1.5rem;
}
```

### Code Display
```css
.code-block {
  background: var(--gray-900);
  color: var(--gray-100);
  font-family: var(--font-monospace);
  font-size: var(--text-sm);
  border-radius: var(--radius-md);
  padding: 1rem;
  overflow-x: auto;
}

.code-inline {
  background: var(--gray-100);
  color: var(--gray-800);
  font-family: var(--font-monospace);
  font-size: 0.9em;
  padding: 0.125rem 0.25rem;
  border-radius: var(--radius-sm);
}
```

### Status Indicators
```css
.status-running {
  color: var(--success);
  background: color-mix(in srgb, var(--success) 10%, transparent);
}

.status-stopped {
  color: var(--error);
  background: color-mix(in srgb, var(--error) 10%, transparent);
}

.status-warning {
  color: var(--warning);
  background: color-mix(in srgb, var(--warning) 10%, transparent);
}
```

## Logo and Branding

### Serena Logo
- **Primary Logo**: `resources/serena-logo.svg` - Full color version
- **Dark Mode**: `resources/serena-logo-dark-mode.svg` - Light version for dark backgrounds
- **Icon Only**: `resources/serena-icons.cdr` - Icon variants

### Logo Usage Guidelines
- Minimum size: 24px height for icon, 120px width for full logo
- Clear space: Minimum 16px on all sides
- Color variants: Primary blue, white, and monochrome versions
- Background: Works on light backgrounds, use dark variant for dark themes

## Dashboard Visual System

### Layout Grid
```css
.dashboard-grid {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr;
  height: 100vh;
}

.dashboard-sidebar {
  grid-row: 1 / -1;
  background: var(--gray-800);
}

.dashboard-header {
  grid-column: 2;
  background: white;
  border-bottom: 1px solid var(--gray-200);
}

.dashboard-main {
  grid-column: 2;
  padding: 1.5rem;
  overflow-y: auto;
}
```

### Chart Styling
Using Chart.js with custom color scheme:
```javascript
const chartColors = {
  primary: '#2563eb',
  success: '#10b981',
  warning: '#f59e0b',
  error: '#ef4444',
  gray: '#6b7280'
};

const chartOptions = {
  responsive: true,
  plugins: {
    legend: {
      labels: {
        font: {
          family: '-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif'
        }
      }
    }
  }
};
```

## Animation System

### Hover Effects
```css
.interactive-element {
  transition: var(--transition-fast);
}

.interactive-element:hover {
  transform: translateY(-1px);
  box-shadow: var(--shadow-md);
}
```

### Loading States
```css
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

.loading {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.spinner {
  animation: spin 1s linear infinite;
}
```

## Mobile Design Considerations

### Responsive Breakpoints
```css
--mobile: 640px;
--tablet: 768px;
--desktop: 1024px;
--wide: 1280px;
```

### Mobile Dashboard
```css
@media (max-width: 768px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
    grid-template-rows: 60px auto 1fr;
  }
  
  .dashboard-sidebar {
    grid-row: 2;
    grid-column: 1;
    height: auto;
  }
  
  .dashboard-main {
    grid-row: 3;
    grid-column: 1;
  }
}
```

## Accessibility Guidelines

### Color Contrast
- Text on backgrounds: Minimum 4.5:1 contrast ratio
- Interactive elements: Minimum 3:1 contrast ratio
- Focus indicators: High contrast borders with 2px minimum width

### Focus Management
```css
.focusable:focus {
  outline: 2px solid var(--serena-blue);
  outline-offset: 2px;
}

.focus-visible:focus-visible {
  outline: 2px solid var(--serena-blue);
  outline-offset: 2px;
}
```

### Screen Reader Support
- Semantic HTML structure
- ARIA labels for complex interactions
- Alt text for all images and icons
- Descriptive link text

### Keyboard Navigation
- Tab order follows visual flow
- All interactive elements keyboard accessible
- Escape key closes modals/dropdowns
- Arrow keys for navigation where appropriate

## Keywords <!-- #keywords -->
design system, color palette, typography, visual effects, component design, branding, logo usage, dashboard design, responsive design, accessibility, mobile design, animation, hover effects