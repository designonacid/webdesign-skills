---
name: webdesign
description: Apply Marco's code-first Astro, Tailwind, HTML and JavaScript webdesign workflow with GitHub and bidirectional Figma MCP translation, brand colors, semantic tokens and Tailwind-based sizing names. Use when creating or reviewing web designs, Figma variables, typography, spacing, corner radii, atomic or combined components, responsive section components, Auto Layout, brand palettes or design-to-code tokens.
---

# Webdesign

## Brand variables and color naming

Apply these defaults unless the project already has an established convention or the user requests another approach. Treat them as preferred conventions, not a universal industry standard.

Separate raw palette values from brand and UI roles:

| Layer | Example | Store |
| --- | --- | --- |
| Palette primitives | color/yellow/500, color/purple/500, color/neutral/100 | Actual color values |
| Brand roles | color/brand/primary, color/brand/secondary, color/brand/accent | Aliases to palette primitives |
| Semantic UI roles | color/background/default, color/text/primary, color/border/default, color/action/primary | Aliases expressing intended use |

Use a mapping such as:
color/action/primary → color/brand/primary → color/yellow/500

- Prefer primary, secondary and accent for a simple brand hierarchy.
- Avoid opaque names such as brand1 and brand2.
- For equally important brand colors, use descriptive names such as brand/yellow and brand/purple rather than forcing a hierarchy.
- For a simple identity palette, keep the system small; do not require all three layers.
- For websites and product systems, use semantic UI aliases so themes and brand changes can change values without renaming usage roles.
- Keep brand hierarchy distinct from text hierarchy: text/primary means primary text, not necessarily the primary brand color.
- Add state suffixes where needed, such as color/action/primary/hover; add component-specific tokens only when reusable roles do not suffice.
- Use consistent lowercase slash-separated names in Figma. Translate consistently for code, for example color/action/primary to --color-action-primary.
- Define shade scales only when needed and document their direction consistently.
- When implementing light/dark themes, vary semantic mappings by mode and verify foreground/background contrast for the actual pairings.

Before proposing names, inspect existing variables. Preserve coherent brand color conventions; apply the Tailwind naming requirement below to sizing and related tokens. Present a compact table of names, values or aliases, and intended uses.

## Tailwind naming conventions

Always use Tailwind naming conventions for font sizes, spacing, corner radii and comparable design tokens, in both design specifications and implementation. Apply this requirement even when Tailwind itself is not used. Do not substitute a bespoke naming scale unless the user explicitly instructs otherwise.

- Font sizes: use Tailwind names such as text-xs, text-sm, text-base, text-lg, text-xl and text-2xl.
- Spacing: use Tailwind numeric scale keys, such as 0, 0.5, 1, 2, 4, 6 and 8; use appropriate utility prefixes in code, such as p-4, gap-6 and mt-8.
- Corner radii: use rounded-none, rounded-sm, rounded-md, rounded-lg, rounded-xl and rounded-full, as supported by the project's Tailwind version.
- Apply the same principle to related scales, including line height, letter spacing, font weight and shadows; use supported names such as leading-tight, tracking-wide, font-semibold and shadow-lg.
- In Figma, use slash groups while preserving Tailwind scale keys, for example font-size/base, font-size/2xl, spacing/4 and radius/lg. Document the matching utility, such as text-base, p-4 or rounded-lg.
- Resolve actual values from the project's Tailwind version and theme configuration. For new projects, verify current official Tailwind documentation before choosing values. Do not assume utility names imply identical values across versions or custom themes.
- Use the standard scales by default. If custom values are required, keep Tailwind-compatible theme naming and document the extension rather than inventing an unrelated scale.
- Keep semantic brand color aliases from the preceding section; this sizing convention does not replace their purpose-based names.

## Default Figma artboards

- Use a desktop frame width of 1440 px by default. Let page height follow content; do not impose a fixed desktop height.
- Use a portrait mobile frame of 393 × 852 logical design pixels by default, a common iPhone 15/15 Pro/16 size. Treat this as the chosen reusable baseline, not a verified claim of highest device market share.
- Design at logical viewport dimensions, not physical Retina resolution. Let full-page mobile frame height grow with content; use 852 px as the initial viewport height.
- Keep layouts responsive between these baselines; do not treat artboard widths as fixed implementation widths.
- Override these defaults only when the user or an explicit project requirement specifies another target.

## Component architecture and Auto Layout

Build reusable components at every composition level:

- Atomic components: make individual UI parts such as buttons, input fields, labels, checkboxes, icons and badges into components.
- Combined components: compose atoms into reusable groups such as a labelled input with help/error text, search bars, cards and button groups. Use nested component instances rather than detached copies.
- Section components: make complete page sections into reusable components, such as headers, heroes, feature sections, forms and footers. Define both desktop and mobile layouts for each section, using responsive variants where appropriate.
- In code, map section components to semantic HTML section elements where appropriate; use header, nav, main or footer for their respective landmarks.
- Compose page frames from section instances. Keep shared atomic and combined components consistent across desktop and mobile variants.
- Use Figma Auto Layout wherever possible, including atoms, combined components, sections and page stacks. Set padding, gaps, alignment, wrapping, and Hug contents / Fill container deliberately.
- Reserve absolute positioning for intentional overlays or decorative elements that need it. Avoid manual positioning for ordinary layout.
- Apply the Tailwind token naming and default desktop/mobile frame dimensions defined above.
- Verify that layouts handle content changes, longer labels and both target widths without clipping or unintended overflow.

## Figma component organization

Use Figma's “Wrap in section” to organize all components into their own clearly named categories on the component page. Group related main components and component sets together, for example Buttons, Inputs, Navigation, Cards and Page sections. Keep each category in its own Figma Section and extend categories as needed.

Distinguish organizational Figma Sections from reusable page-section components: use Sections to organize the canvas; use component frames and variants for reusable UI and desktop/mobile layouts. Keep Auto Layout on the component frames inside these organizational Sections.

## Code-first foundation and bidirectional workflow

Build a reusable base that supports both code-to-Figma and Figma-to-code work, starting with code.

1. Set up a lightweight local Astro project with Tailwind CSS, semantic HTML and JavaScript. Prefer Astro components and minimal client-side JavaScript; add a framework only when a concrete interaction requires it.
2. Define the complete design foundation in code: palette, brand and semantic colors, typography, spacing, radii and other relevant tokens. Apply the Tailwind naming rules above. Keep canonical token definitions centralized and reusable rather than duplicating values across components.
3. Implement atomic components, combined components and complete responsive section components. Include a local reference/showcase page exposing tokens, component variants and states, and desktop/mobile section layouts for review and Figma translation.
4. Validate the local build and responsive layouts. Push the foundation to the project's GitHub repository as part of an authorized setup; reuse an existing project/repository when supplied. Keep repository-backed code in that repository rather than making a separate Library copy.
5. Use the available Figma MCP workflow to translate the code foundation onto the Figma canvas as editable native design elements, including variables, components, variants, Auto Layout, category Sections and desktop/mobile section layouts. Load the applicable Figma skills before tool calls. Use token bindings and reusable instances; verify the translated result rather than treating screenshots as a synchronized design system.
6. Continue working in both directions. For each change, identify the changed tokens/components/sections, propagate them to the counterpart, validate both representations, and save the code changes to GitHub within the user's authorized scope.

Treat the code and its token definitions as the initial canonical baseline. Allow deliberate design changes in Figma, then translate them back into code and reconcile the resulting shared definitions before further propagation. Preserve stable token names and component mappings, recording Figma file/node links alongside code component identifiers where useful.

Do not silently overwrite conflicting edits. Inspect both sides and reconcile intent; ask only when the intended result cannot be determined. Keep responsive behavior and semantic code structure while matching design intent.

Treat ongoing synchronization as an explicit, repeatable workflow during active work. Do not claim automatic, continuous background or lossless bidirectional synchronization unless an actual integration has been implemented and verified. Inspect current MCP capabilities and report any unsupported conversion or synchronization step accurately.

## Portable tokens and Astro scope

Keep the design foundation portable across tools and frameworks.

- Store canonical token definitions in centralized, version-controlled, DTCG-compatible token files, independent of Astro, Tailwind and Figma. Use the stable specification supported by the selected tooling; verify current official documentation before implementation.
- Preserve the Tailwind naming conventions required above for font sizes, spacing, radii and related scales. Separate these names and their underlying values from framework configuration.
- Generate the Tailwind theme and relevant CSS variables from the canonical token files. Map the same definitions into Figma variables. Do not maintain divergent hand-edited copies of the same values.
- Resolve aliases and validate generated outputs. Keep semantic roles distinct from primitives and document any transformation required by the target tool.
- Treat the portable tokens as the canonical foundation within the code-first workflow, rather than treating Astro or Tailwind configuration as the only source of token truth.

Use Astro as the default website implementation and reference/showcase layer for lightweight brand websites, retaining semantic HTML, Tailwind and minimal JavaScript.

- Do not couple the entire reusable design system to Astro unnecessarily.
- For complex applications, shared interactive components or multiple consuming frameworks, assess the component implementation independently of the Astro showcase. Choose a suitable component framework or framework-neutral approach based on actual consumers and interaction requirements.
- Keep tokens, component contracts and documentation reusable across consumers. Add client-side islands only where interactivity requires them; do not add a framework solely for hypothetical future needs.

## Reference foundations

Use these for background, and verify current documentation if asked about current industry practice:
- Adobe Spectrum token tiers and aliases: https://spectrum.adobe.com/foundations/design-data/design-tokens
- Material color roles: https://m3.material.io/styles/color/the-color-system
- Tailwind CSS documentation: https://tailwindcss.com/docs/theme
- iPhone logical frame dimensions: https://trimmarks.com/screen-sizes
- Stable Design Tokens reports: https://www.designtokens.org/tr/2025.10/
- Astro islands architecture: https://docs.astro.build/en/concepts/islands/
