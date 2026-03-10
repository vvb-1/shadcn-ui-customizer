# CLAUDE.md - shadcn/ui Customizer

## Project Overview

The **shadcn/ui Customizer** is an open-source extension of [shadcn/ui](https://github.com/shadcn-ui/ui) that provides a comprehensive theme customization interface. This tool allows developers to visually customize shadcn/ui themes by adjusting CSS variables in real-time, with live preview capabilities across multiple components and blocks.

The project serves as both a theme customization tool and a component gallery, demonstrating how shadcn/ui components work with custom color schemes and design tokens.

## Tech Stack

### Core Framework
- **Next.js 14** - React framework with App Router
- **React 18** - UI library  
- **TypeScript** - Type safety and developer experience
- **Tailwind CSS** - Utility-first CSS framework

### UI & Component Libraries
- **shadcn/ui** - UI component library built on Radix UI
- **Radix UI** - Low-level UI primitives (30+ components)
- **Lucide React** - Icon library

### State Management & Logic
- **Jotai** - Atomic state management for theme configuration
- **React Hook Form** - Form state management
- **Zod** - Schema validation

### Development & Styling
- **Tailwind CSS Animate** - CSS animations
- **Class Variance Authority (CVA)** - Component variant management
- **clsx/tailwind-merge** - Conditional CSS classes
- **PostCSS** - CSS processing

### Utility Libraries
- **React Color** - Color picker components
- **ColorJoe** - Advanced color manipulation
- **Next Themes** - Dark/light mode support
- **Framer Motion** - Animations and transitions
- **Lodash** (debounce, template) - Utility functions

### Code Generation & Syntax
- **Shiki** - Syntax highlighting
- **TS-Morph** - TypeScript AST manipulation

### Deployment & Analytics
- **Vercel** (Analytics, KV) - Hosting and analytics
- **Resend** - Email service
- **Upstash** - Rate limiting

## Project Structure

```
src/
├── __registry__/         # Component registry (default & new-york styles)
│   ├── default/
│   └── new-york/
├── app/                  # Next.js App Router pages
│   ├── (app)/           # App group routes
│   │   ├── api/         # API routes (subscribe/unsubscribe)
│   │   └── blocks/      # Blocks gallery page
│   ├── (blocks)/        # Block preview routes
│   │   └── blocks/[style]/[name]/
│   ├── globals.css      # Global styles
│   ├── layout.tsx       # Root layout
│   ├── page.tsx         # Homepage
│   └── header.tsx       # Header component
├── components/          # React components
│   ├── customizer/      # Theme customization components
│   ├── ui/             # shadcn/ui components
│   └── ...             # Other components
├── hooks/              # Custom React hooks
│   ├── use-config.ts   # Theme configuration hook
│   ├── use-debounce.ts # Debouncing utility
│   └── ...
├── lib/                # Utility libraries
│   ├── themes/         # Theme definitions
│   ├── utils.ts        # General utilities
│   └── ...
├── registry/           # Component & block registry
│   ├── default/        # Default style components
│   └── new-york/       # New York style components
├── styles/             # Additional styles
└── types/              # TypeScript type definitions
```

## Commands

```bash
# Development
npm run dev          # Start development server on port 3003
bun dev             # Alternative with Bun

# Build & Deploy
npm run build       # Build for production
npm run start       # Start production server
npm run lint        # Run ESLint

# Package Management
npm install         # Install dependencies
bun install         # Alternative with Bun
```

## Architecture

### Theme System
The customizer uses a sophisticated theme system based on CSS custom properties (variables):

1. **Theme Configuration**: Stored in Jotai atoms with localStorage persistence
2. **CSS Variables**: HSL color values for 20+ design tokens
3. **Live Updates**: Real-time theme application via React state
4. **Export System**: Generate CSS code for custom themes

### Key Design Tokens
- Background & Foreground colors
- Card & Popover styling
- Primary, Secondary, Muted, Accent colors
- Destructive action colors
- Border, Input, Ring focus colors
- Border radius values

### Component Architecture
- **ThemeWrapper**: Applies custom CSS variables to component trees
- **Color Picker Sections**: Interactive color selection with HSL conversion
- **Preview Components**: Live demonstration of themed components
- **Block Gallery**: Showcase of complete UI patterns

### State Management
```typescript
// Theme configuration atom
const configAtom = atomWithStorage<Config>("config", {
  style: "default",
  theme: "zinc", 
  cssVars: { light: {...}, dark: {...} }
});
```

### Color System
- **Input**: Hex color values from color pickers
- **Processing**: Converted to HSL for CSS custom properties
- **Application**: Dynamic CSS variable injection
- **Export**: CSS code generation for theme implementation

## Code Conventions

### Component Structure
- **Client Components**: Use `"use client"` directive for interactive components
- **Server Components**: Default for static content and layouts
- **Props**: TypeScript interfaces with clear naming
- **Styling**: Tailwind classes with conditional logic via `clsx`

### File Organization
- **Page Routes**: Follow Next.js App Router conventions
- **Components**: Organized by feature (customizer, ui, blocks)
- **Utilities**: Separated into lib/ directory
- **Types**: Centralized in types/ directory

### State Patterns
- **Global State**: Jotai atoms for theme configuration
- **Local State**: React hooks for component-specific state  
- **Persistence**: localStorage integration via Jotai utils
- **Performance**: Debounced updates for color changes

### Styling Approach
- **Design System**: shadcn/ui component library
- **Customization**: CSS custom properties for theming
- **Responsive**: Mobile-first Tailwind breakpoints
- **Dark Mode**: Next-themes with system preference detection

## Key Files

### Core Application
- `src/app/page.tsx` - Homepage with theme showcase
- `src/app/layout.tsx` - Root layout with providers
- `src/components/theme-wrapper.tsx` - Theme application component

### Customization Engine
- `src/hooks/use-config.ts` - Theme configuration state management
- `src/components/customizer/color-picker-section.tsx` - Interactive color customization
- `src/components/customizer/color.utils.ts` - Color conversion utilities

### Theme System
- `src/registry/themes.ts` - Pre-built theme definitions
- `src/lib/themes/` - Theme processing utilities
- `src/app/globals.css` - Global CSS variables and base styles

### Component Registry
- `src/registry/default/` - Default style components and examples
- `src/__registry__/` - Component registration system
- `src/components/ui/` - shadcn/ui component implementations

### Configuration
- `package.json` - Dependencies and scripts
- `tailwind.config.js` - Tailwind configuration with custom CSS variables
- `components.json` - shadcn/ui CLI configuration
- `next.config.js` - Next.js configuration

## Development Notes

### Theme Customization Workflow
1. Select base theme (zinc, slate, stone, etc.)
2. Adjust individual color variables via color pickers
3. Preview changes across component gallery
4. Copy generated CSS for implementation

### Component Development
- All components follow shadcn/ui patterns
- Variants managed with Class Variance Authority
- Accessibility features built-in via Radix UI
- Mobile-responsive by default

### Performance Considerations
- Color changes are debounced (300ms) to prevent excessive updates
- Theme state persisted to localStorage
- Component registry supports lazy loading
- Optimized for Vercel deployment

This customizer serves as both a practical tool for theme development and a comprehensive showcase of shadcn/ui's capabilities with custom design systems.