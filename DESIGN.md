# Liquid Glass Design System

## 1. Visual Theme & Atmosphere

The Liquid Glass design system embodies atmospheric depth paired with tactile responsiveness. The aesthetic prioritizes spatial awareness by allowing underlying content to subtly bleed through structural components, creating a continuous environment. The system exudes premium quality through dynamic WebGL/SVG light refraction, heavy backdrop blurs, and sharp specular edge reflections—simulating physical panels of thick, polished glass. Every interface element reacts to proximity and interaction, offering elastic feedback that makes the digital material feel tangible and organic.

**Key Characteristics**
- Heavy reliance on translucency, backdrop blur, and chromatic aberration
- Dynamic, physics-based elastic scaling on hover and active states
- Specular edge highlights simulating refracted light
- Adaptive shadow intensity based on background luminance
- High-contrast typography supported by sharp text shadows
- Highly rounded geometries (pill shapes to large radii)

## 2. Color Palette & Roles

### Base Surfaces
- **Glass Background Light:** `color-mix(in srgb, #ffffff 15%, transparent)` — Base translucent fill for elements in dark environments.
- **Glass Background Dark:** `color-mix(in srgb, #000000 30%, transparent)` — Base translucent fill for elements in light environments or for high contrast.
- **Glass Interactive:** `color-mix(in srgb, #ffffff 25%, transparent)` — Elevated fill for hovered or focused interactive elements.
- **Glass Pressed:** `color-mix(in srgb, #ffffff 10%, transparent)` — Recessed fill for active (clicked) states.

### Refraction & Edges
- **Highlight Bright:** `rgba(255, 255, 255, 0.6)` — For top-left specular edge reflections.
- **Highlight Dim:** `rgba(255, 255, 255, 0.2)` — For bottom-right rim continuity.
- **Inner Rim Light:** `rgba(255, 255, 255, 0.4)` — Sharp inner shadow to simulate thickness.
- **Inner Rim Dark:** `rgba(0, 0, 0, 0.2)` — Dark mode inner rim for contrast.

### Typography & Content
- **Text Dominant:** `#FFFFFF` — Primary text color in dark/vibrant environments.
- **Text Inverse:** `#171717` — Text used strictly within `.glass--light` contexts over light backgrounds.
- **Placeholder:** `rgba(255, 255, 255, 0.6)` — Soft, readable hints inside inputs.

## 3. Typography Rules

### Font Family
**Primary:** Geist Sans, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif
**Monospace:** Geist Mono, ui-monospace, Menlo, Monaco, "Cascadia Mono", monospace

### Hierarchy

| Role | Font | Size | Weight | Line Height | Shadow | Notes |
|------|------|------|--------|-------------|--------|-------|
| Display Title | Geist Sans | 40px | 700 | 44px | Strong | Hero metrics or giant floating typography |
| Heading Primary | Geist Sans | 24px | 600 | 28px | Medium | Card headlines (e.g. User Info, Settings) |
| Heading Secondary| Geist Sans | 20px | 500 | 24px | Medium | Secondary panel headings |
| Body Default | Geist Sans | 16px | 400 | 24px | Medium | Standard body content within glass sheets |
| Body Compact | Geist Sans | 14px | 400 | 20px | Subtle | Meta details (e.g. Email, Location) |
| Small Label | Geist Sans | 12px | 600 | 16px | Subtle | Categorical pill labels |

*Note: All text resting on a standard `.glass` element MUST utilize a text-shadow (e.g., `0px 2px 12px rgba(0, 0, 0, 0.4)`) to maintain legibility when drifting over bright, unpredictable background imagery.*

## 4. Component Stylings

### Glass Button (`.glass-button`)
- **Background:** `color-mix(in srgb, #ffffff 15%, transparent)`
- **Padding:** `12px 24px`
- **Border Radius:** `9999px` (Pill)
- **Text:** 16px, weight 500, `#FFFFFF`
- **Blur:** `backdrop-filter: blur(20px) saturate(140%)`
- **Shadow:** Outer `0 12px 40px rgba(0, 0, 0, 0.25)`, Inner `inset 0 1px 1px rgba(255,255,255,0.4)`
- **Hover State:** Background intensity 25%, Scale `1.02`
- **Active State:** Scale `0.96`, Physical recess

### Glass Card (`.glass-card` / `.glass-panel`)
- **Background:** `color-mix(in srgb, #ffffff 15%, transparent)`
- **Padding:** `24px` (Card), `32px` (Panel)
- **Border Radius:** `32px`
- **Shadow (Over Dark):** `0 12px 40px rgba(0, 0, 0, 0.25)`
- **Shadow (Over Light):** `0 16px 70px rgba(0, 0, 0, 0.75)`
- **Highlight Edge:** Applied via SVG displacement filter or CSS `::before` pseudo element.

### Glass Input (`.glass-input`)
- **Background:** `color-mix(in srgb, #ffffff 10%, transparent)`
- **Padding:** `12px 16px`
- **Border Radius:** `16px`
- **Text:** 16px, weight 400, `#FFFFFF`
- **Focus State:** Scale `1.01`, Outline `2px solid rgba(255, 255, 255, 0.3)`

## 5. Layout Principles & Spacing

### Spacing System (Base 8)
- `8px` — Inner gaps (icons next to text)
- `12px` — Vertical padding for interactive targets
- `16px` — Standard horizontal padding for inputs
- `24px` — Card internal padding; horizontal padding for buttons
- `32px` — Large panel internal padding
- `40px` — Modal internal padding

### Border Radius Scale
- `8px` — Interior list items
- `16px` — Inputs, toolbars, and nested containers
- `32px` — Primary floating surfaces (Cards, Modals, Panels)
- `9999px` — Buttons, Badges, Navbars

## 6. Depth & Elevation

| Level | Blur Intensity | Shadow | Use |
|-------|----------------|--------|-----|
| Subtle | `blur(8px) saturate(110%)` | `0 4px 16px rgba(0,0,0,0.1)` | Toolbars, Nested inner cards |
| Base | `blur(20px) saturate(140%)` | `0 12px 40px rgba(0,0,0,0.25)`| Standard buttons, default cards |
| Strong| `blur(40px) saturate(140%)` | `0 16px 70px rgba(0,0,0,0.75)`| Hero modals, floating headers, high-contrast areas |

## 7. Responsive Behavior & Interaction

### Breakpoints
| Breakpoint | Width | Liquid Glass Adjustments |
|------------|-------|--------------------------|
| Mobile | < 768px | Reduce base blur to `12px`. Disable SVG WebGL displacement for battery performance. Convert `32px` paddings to `24px`. |
| Tablet | 768–1024px| Retain base blurs. Fallback to CSS-only hover states if hardware acceleration stutters. |
| Desktop | > 1024px | Full capability: SVG Light refraction, elastic mouse tracking, directional distortion. |

### Motion & Physics
- **Elastic Attraction:** The structural boundary of the glass should stretch directionally (via JS calculation) based on mouse proximity. 
- **Transition Default:** Use `cubic-bezier(0.4, 0, 0.2, 1)` for color/shadow fades.
- **Transition Elastic:** Use `cubic-bezier(0.34, 1.56, 0.64, 1)` for scale and positional translations.

## 8. Liquid Glass Implementation Guide

### CSS Reflection Execution (Without JS)
For a pure CSS fallback that beautifully fakes the edge-refraction:
```css
.glass::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px; /* Emulates edge thickness */
  background: linear-gradient(135deg, rgba(255,255,255,0.6) 0%, rgba(255,255,255,0) 40%, rgba(255,255,255,0.2) 100%);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  pointer-events: none;
}
```

### Full Displacement Engine (With React)
For true chromatic aberration, wrap content in a container driving an SVG `<feDisplacementMap>` mapped to cursor events, generating a visual warp offset. *(Refer to `LiquidGlass` component inside `src/index.tsx` for matrix values).*

## 9. Do's and Don'ts

### Do
- **Do** wrap readable text in a text-shadow when laying over highly transparent glass.
- **Do** fallback gracefully to CSS backdrop-blur if SVG `<feFilter>` performance drops.
- **Do** utilize `radius: 9999px` exclusively for terminal interactive nodes (Buttons, badges).
- **Do** increase box-shadow intensity/opacity dramatically when the glass object hovers over bright background areas to avoid getting "washed out".

### Don't
- **Don't** stack multiple heavily blurred `<feDisplacementMap>` components together—limit it to isolated, floating UI chunks.
- **Don't** use opaque background colors. If transparency is lost, the entire physical illusion breaks.
- **Don't** disable focus outlines (`outline: 2px solid`) purely for aesthetics. Keep keyboard navigation sharply visible.

---

## 10. Agent Prompt Guide & Iteration Guide

When tasked with generating, fixing, or modifying UI within this project, adhere strictly to these rules:

1. **Always use Backdrop Blur:** Transparent backgrounds MUST be paired with `backdrop-filter: blur(...)`. Transparency without blur is prohibited.
2. **Gradient Border over Solid:** Never apply a solid `1px solid rgba(...)` border. Always use the `::before` pseudo-element gradient mask technique (detailed in Section 8) to simulate light hitting the top-left edge of the glass.
3. **Pill vs Panel:** Buttons, Toolbars, and Navbars must always be pill-shaped (`9999px`). Panels, Cards, and Inputs must use standard radii (`16px`, `32px`).
4. **Text Legibility over Bleed:** If requested to make text cleaner on glass, immediately add `text-shadow: 0px 2px 12px rgba(0, 0, 0, 0.4)` instead of removing the glass transparency.
5. **No Flat Shadows:** Shadows must be deeply diffused (`0 12px 40px`). Never use tight, flat drops (`0 2px 4px`).
6. **Inner Shadows create Mass:** Combine a heavy outer drop shadow with a sharp whitish inner shadow (`inset 0 1px 1px rgba(255,255,255,0.4)`) to simulate physical glass thickness.
7. **Scale over Color for Press:** Active/Pressed states should scale the element down (`transform: scale(0.96)`) elastically rather than significantly darkening the background color. 
8. **Semantic Tokens:** Whenever generating CSS/Tailwind, use structural custom properties like `var(--glass-bg-light)` where possible to ensure global synchronicity.