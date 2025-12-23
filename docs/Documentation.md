# Documentation – Wrath & Glory tools internals

## Overview
The application consists of static HTML pages styled by a shared `kalkulatorxp.css`. Each page embeds its own JavaScript to keep all calculations client-side. There is no build step or external dependency: opening the HTML files in a modern browser is enough; Google Fonts are optional and have fallbacks.

## Page responsibilities
- **index.html**: Landing page that lists available tools and links to them. Adjust the navigation anchors if you add or rename tools.
- **KalkulatorXP.html**: Implements XP cost calculations for attributes and skills. Form inputs are validated against allowed ranges (0–12) and totals are computed in-line using JavaScript attached to the page. When extending tables, duplicate existing rows to preserve data attributes and calculation hooks.
- **TworzeniePostaci.html**: Provides a structured character sheet. Sections are organized with semantic HTML to keep the layout responsive. Fields can be duplicated or retitled to fit custom campaigns without breaking the page.

## Styling and layout
The neon-inspired aesthetic is centralized in **kalkulatorxp.css** (used by both calculators), while `index.html` carries its own inline styles. To change the look and feel:
- Update color variables and font declarations at the top of `kalkulatorxp.css`.
- Adjust grid definitions and media queries in the same file to refine spacing or responsiveness.
- Reuse existing utility classes when adding new elements to maintain consistency.

## Data and logic updates
- **Adding new calculations**: Follow the structure of the existing JavaScript snippets embedded in `KalkulatorXP.html`. Calculations rely on element IDs and class selectors; keep naming consistent to ensure totals update correctly.
- **Custom XP tables**: Replace the values in the attribute and skill tables directly in the HTML. The scripts sum costs based on the table rows, so edited values are reflected immediately without further changes.
- **Localization**: All labels and instructions are editable text nodes. Updating copy in the HTML files is enough to translate the interface.

## File layout
```
project root
├── docs/
│   ├── README.md            # high-level usage guidance
│   └── Documentation.md     # code structure and internal logic
├── Old/                     # legacy reference materials
│   ├── HowToUse_Org.pdf
│   └── Kalkulator_Org.html
├── index.html               # navigation landing page (inline styles)
├── KalkulatorXP.html        # XP calculator with embedded scripts
├── TworzeniePostaci.html    # character sheet form
├── kalkulatorxp.css         # shared styling for both calculators
└── style.css                # legacy stylesheet kept for reference
```
