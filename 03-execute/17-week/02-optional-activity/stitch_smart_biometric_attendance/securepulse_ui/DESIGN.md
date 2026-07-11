---
name: SecurePulse UI
colors:
  surface: '#faf8ff'
  surface-dim: '#d9d9e5'
  surface-bright: '#faf8ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f3f3fe'
  surface-container: '#ededf9'
  surface-container-high: '#e7e7f3'
  surface-container-highest: '#e1e2ed'
  on-surface: '#191b23'
  on-surface-variant: '#434655'
  inverse-surface: '#2e3039'
  inverse-on-surface: '#f0f0fb'
  outline: '#737686'
  outline-variant: '#c3c6d7'
  surface-tint: '#0053db'
  primary: '#004ac6'
  on-primary: '#ffffff'
  primary-container: '#2563eb'
  on-primary-container: '#eeefff'
  inverse-primary: '#b4c5ff'
  secondary: '#5c5f60'
  on-secondary: '#ffffff'
  secondary-container: '#dee0e2'
  on-secondary-container: '#606365'
  tertiary: '#006229'
  on-tertiary: '#ffffff'
  tertiary-container: '#007e37'
  on-tertiary-container: '#c1ffc5'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#dbe1ff'
  primary-fixed-dim: '#b4c5ff'
  on-primary-fixed: '#00174b'
  on-primary-fixed-variant: '#003ea8'
  secondary-fixed: '#e1e2e4'
  secondary-fixed-dim: '#c5c6c8'
  on-secondary-fixed: '#191c1e'
  on-secondary-fixed-variant: '#444749'
  tertiary-fixed: '#6bff8f'
  tertiary-fixed-dim: '#4ae176'
  on-tertiary-fixed: '#002109'
  on-tertiary-fixed-variant: '#005321'
  background: '#faf8ff'
  on-background: '#191b23'
  surface-variant: '#e1e2ed'
typography:
  display-lg:
    fontFamily: Inter
    fontSize: 48px
    fontWeight: '700'
    lineHeight: 56px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.01em
  headline-lg-mobile:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  title-md:
    fontFamily: Inter
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
  label-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
    letterSpacing: 0.01em
  label-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '600'
    lineHeight: 16px
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  base: 4px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  xxl: 48px
  gutter: 20px
  margin-mobile: 16px
  margin-desktop: 40px
---

## Brand & Style

This design system is built for a biometric attendance environment where speed, security, and institutional trust are paramount. The aesthetic follows a **Modern Professional Minimalism** approach, stripping away unnecessary decorative elements to focus on the biometric verification flow. 

The target audience includes students, instructors, and administrative staff. The UI must evoke a sense of high-tech reliability and "frictionless security"—the feeling that the system is sophisticated yet effortless to use. By utilizing generous whitespace and a "Mobile-First for Physical Terminals" philosophy, the design ensures that interaction points are obvious and accessible, even in high-traffic entryways.

## Colors

The color palette is rooted in a high-trust "SENA Blue" (#2563EB) used for primary actions and brand identity. 

- **Primary Blue:** Used for the main "Scan" buttons, active states, and focus indicators.
- **Surface & Background:** A pure white surface sits atop a light gray background (#F3F4F6) to create subtle depth without relying on heavy borders.
- **Semantic Feedback:** Success Green is reserved for confirmed identifications, while Alert Red is used exclusively for failed scans or unauthorized access attempts.
- **Neutrals:** Dark grays are used for text hierarchy to maintain high legibility under various lighting conditions common in physical building lobbies.

## Typography

The design system utilizes **Inter** for its exceptional legibility and neutral, systematic tone. 

- **Hierarchy:** High-contrast sizing distinguishes between the status of the system (e.g., "Ready to Scan") and secondary information (e.g., User ID or Timestamp).
- **Readability:** For attendance terminals, body text is kept at a minimum of 16px to ensure accessibility from a standing distance.
- **Tracking:** Headings use slight negative letter-spacing for a tighter, more modern look, while labels use increased tracking for clarity at small sizes.

## Layout & Spacing

The layout utilizes a **Fluid Grid** system with a focus on central vertical alignment for terminal screens. 

- **Grid:** A 12-column grid is used for desktop administrative dashboards, while a 4-column grid is used for mobile/tablet scanning interfaces.
- **Rhythm:** An 8pt spatial system governs all padding and margins to ensure a consistent visual cadence.
- **Negative Space:** This design system mandates "Generous Whitespace." Elements should never feel crowded; the "Scan Area" must occupy at least 40% of the viewport on terminal screens to guide the user's eye toward the biometric sensor.

## Elevation & Depth

To maintain a minimalist but tactile feel, the design system uses **Ambient Shadows** to define the z-axis.

- **Level 0 (Background):** Flat #F3F4F6.
- **Level 1 (Cards/Surface):** White background with a very soft, diffused shadow: `0px 4px 20px rgba(0, 0, 0, 0.05)`.
- **Level 2 (Active/Modals):** A more pronounced shadow to indicate focus or floating elements: `0px 10px 30px rgba(0, 0, 0, 0.08)`.
- **Interaction:** Buttons do not use heavy shadows; they use a subtle depth increase on hover and a "pressed" state that removes the shadow to simulate physical contact.

## Shapes

The shape language is defined by **Large Radius Geometry**.

- **Standard Elements:** Buttons and input fields use a 0.5rem (8px) radius.
- **Containers:** Primary cards and scanning modules use `rounded-xl` (1.5rem/24px) to create a friendly, modern silhouette.
- **Biometric Indicators:** The scanning frame and user avatars should always be perfectly circular (full rounded) to contrast against the structured rectangular grid of the rest of the UI.

## Components

- **Buttons:** Use high-saturation Primary Blue for "Action" buttons. Ensure a minimum touch target of 48px. Labels are centered and semi-bold.
- **Scanning Frame:** A specialized component with a pulsating "Success Green" or "Primary Blue" border to guide biometric placement. 
- **Cards:** Use for user profiles and history logs. Cards should have no borders, relying entirely on Level 1 shadows for definition.
- **Input Fields:** Soft gray backgrounds (#F9FAFB) with a 1px border that turns Primary Blue on focus. Labels sit clearly above the input.
- **Status Chips:** Small, pill-shaped indicators for "Present," "Late," or "Absent." Use low-opacity fills of the semantic colors with high-opacity text (e.g., Light Green fill with Dark Green text).
- **Material Icons:** Use "Rounded" or "Outline" variations of Material Design icons. Maintain a consistent 24px bounding box.