---
name: Vistoria Certa System
colors:
  surface: '#f8f9ff'
  surface-dim: '#cbdbf5'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e5eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d3e4fe'
  on-surface: '#0b1c30'
  on-surface-variant: '#434653'
  inverse-surface: '#213145'
  inverse-on-surface: '#eaf1ff'
  outline: '#737685'
  outline-variant: '#c3c6d6'
  surface-tint: '#2156ca'
  primary: '#00328a'
  on-primary: '#ffffff'
  primary-container: '#0047bb'
  on-primary-container: '#afc1ff'
  inverse-primary: '#b3c5ff'
  secondary: '#575f6b'
  on-secondary: '#ffffff'
  secondary-container: '#dbe3f1'
  on-secondary-container: '#5d6571'
  tertiary: '#243961'
  on-tertiary: '#ffffff'
  tertiary-container: '#3b5079'
  on-tertiary-container: '#aec3f3'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#dbe1ff'
  primary-fixed-dim: '#b3c5ff'
  on-primary-fixed: '#00174a'
  on-primary-fixed-variant: '#003ea6'
  secondary-fixed: '#dbe3f1'
  secondary-fixed-dim: '#bfc7d4'
  on-secondary-fixed: '#141c26'
  on-secondary-fixed-variant: '#3f4752'
  tertiary-fixed: '#d8e2ff'
  tertiary-fixed-dim: '#b2c6f7'
  on-tertiary-fixed: '#001a41'
  on-tertiary-fixed-variant: '#32466f'
  background: '#f8f9ff'
  on-background: '#0b1c30'
  surface-variant: '#d3e4fe'
typography:
  display-lg:
    fontFamily: Hanken Grotesk
    fontSize: 48px
    fontWeight: '700'
    lineHeight: 56px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Hanken Grotesk
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.01em
  headline-md:
    fontFamily: Hanken Grotesk
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-sm:
    fontFamily: Hanken Grotesk
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
  body-lg:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '400'
    lineHeight: 28px
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  label-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '600'
    lineHeight: 16px
    letterSpacing: 0.05em
  headline-lg-mobile:
    fontFamily: Hanken Grotesk
    fontSize: 28px
    fontWeight: '600'
    lineHeight: 36px
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  base: 4px
  xs: 8px
  sm: 16px
  md: 24px
  lg: 40px
  xl: 64px
  gutter: 24px
  margin-mobile: 16px
  margin-desktop: 32px
---

## Brand & Style

This design system is engineered for a professional real estate inspection SaaS, prioritizing trust, precision, and operational efficiency. The brand personality is authoritative yet modern, evoking the feeling of a high-end architectural firm combined with the utility of a logistics platform.

The visual style is **Corporate Modern with a Glassmorphic edge**. It utilizes a "Clean-Room" aesthetic: expansive white space, a structured grid, and technical precision. We introduce premium depth through subtle frosted-glass overlays and translucent layers, ensuring the dashboard feels airy despite the density of data required for property inspections. Linear icons and a restricted color palette maintain a high-signal, low-noise environment.

## Colors

The palette is anchored by "Professional Blue," a high-contrast, deep sapphire that represents stability and legal certainty. 

- **Primary (#0047BB):** Used for primary actions, branding, and active states. 
- **Secondary (#E8F0FE):** A soft, "Ice Blue" used for background washes, light glassmorphism tinting, and subtle highlights.
- **Tertiary (#001A41):** An ultra-dark navy for high-level navigation and primary text, providing a premium anchor to the lighter UI elements.
- **Surface Foundations:** We use a pure white (#FFFFFF) for base surfaces and a very light grey (#F8FAFC) for sectional backgrounds to create clear visual separation without heavy borders.

## Typography

The typography strategy balances character and utility. **Hanken Grotesk** is used for headlines to provide a sharp, contemporary, and premium feel. Its geometric nature aligns with architectural themes. 

**Inter** is utilized for all functional UI elements, body text, and data inputs. It is chosen for its exceptional legibility in data-heavy environments, such as inspection checklists and property reports. We utilize a strict vertical rhythm, ensuring that line heights are always multiples of 4px to maintain an organized, operational layout.

## Layout & Spacing

The design system employs a **12-column fluid grid** for desktop dashboards, transitioning to a **single-column fluid layout** for mobile inspection tools. 

- **Desktop:** Side navigation is fixed at 280px. The content area uses a fluid grid with 24px gutters.
- **Tablet:** Navigation collapses into an icon bar (80px) to maximize the workspace for photo galleries and checklists.
- **Mobile:** All margins shrink to 16px. Touch targets are prioritized, with full-width buttons and expanded list items.

A strict 8px-based spacing scale is used for all internal component margins to ensure an "organized and operational" feel. White space is used generously around property details to prevent cognitive overload.

## Elevation & Depth

Hierarchy is established through **Tonal Layers** and **Subtle Glassmorphism**. We avoid heavy drop shadows in favor of ambient depth:

1.  **Level 0 (Background):** Soft grey (#F8FAFC) or subtle linear gradients.
2.  **Level 1 (Cards):** Pure white with a very fine 1px border (#E2E8F0) and no shadow.
3.  **Level 2 (Active/Floating):** Subtle glassmorphism (Background blur: 12px, Opacity: 80% white) with an ultra-soft ambient shadow (0px 4px 20px rgba(0, 71, 187, 0.05)).
4.  **Level 3 (Modals):** Stronger glassmorphism with a tinted primary-blue border (10% opacity) to focus user attention on critical inspection tasks.

This approach ensures the interface feels high-tech and "premium" without sacrificing the speed and clarity required for professional use.

## Shapes

We use **Level 2 (Rounded)** settings to soften the industrial nature of real estate inspections. 

- Standard components (buttons, inputs) use **0.5rem (8px)** corner radii. 
- Content containers and cards use **1rem (16px)** to create a friendly, modern containerized look. 
- Elements like status badges or "Add" buttons may utilize pill-shapes to distinguish them from data entry fields.

This soft-corner approach makes the software feel more approachable and less like a legacy government database.

## Components

### Buttons
Primary buttons use the Brand Blue with white text. Secondary buttons use the Ice Blue background with Brand Blue text. All buttons have a subtle 1px inner highlight on the top edge to give a slight tactile feel without being skeuomorphic.

### Inputs & Forms
Form fields are minimal: a 1px border that turns Primary Blue on focus. Labels are in `label-md` (uppercase) to provide clear visual anchors. Multi-line text areas for inspection notes should auto-expand to accommodate long descriptions.

### Cards & Property Tiles
Cards use the Level 1 elevation style. In the property list, cards feature a high-aspect-ratio image on the left and organized metadata on the right. Status indicators (e.g., "Pending," "Completed") use highly desaturated background tints with high-contrast text.

### Inspection Checklists
A custom component featuring a linear icon for the item type (e.g., plumbing, electrical), a toggle for "Pass/Fail," and a quick-action button for "Add Photo."

### Glassmorphic Overlays
Used for mobile navigation bars and top headers in the dashboard to maintain a sense of context and depth as the user scrolls through long inspection reports.
