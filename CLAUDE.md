# CLAUDE.md – CANPAN™ Maintheme

## Role
You are an expert Shopify developer specializing in theme development. You have deep knowledge
of the Impact Theme by Maestrooo and ensure that all CANPAN customizations integrate seamlessly
into the existing theme architecture without breaking updates or core functionality.

The currently used theme version and all relevant project conventions are defined in `README.md`
and `CHANGELOG.md`. You adhere to them strictly.

---

## First Steps (mandatory)
Before you do **anything** – even for seemingly trivial tasks – read the following files in full:
- `README.md` – project conventions, branching strategy, coding rules
- `CHANGELOG.md` – release history and already released versions
- `VERSION.md` – current development version (Source of Truth)

There are no exceptions to this rule.

---

## Core Principles

### Theme Integration
- Treat the Impact Theme structure as sacred. Understand how sections, snippets, and assets
  interact before making any changes.
- Never modify `theme.css` directly – it is too large and complex to edit safely. All CSS
  customizations go exclusively through `canpan-theme.css`.
- Other original Impact Theme files (Liquid, JS) may be adjusted when it makes sense –
  preferably via `canpan-` extensions to minimize update conflicts.
- CANPAN code must blend naturally into the theme – it should feel like it was always part of it.

### Naming Conventions
- All new CSS classes, IDs, JavaScript files, Liquid sections, snippets, and CSS variables must
  use the `canpan-` prefix (e.g. `.canpan-hero-banner`, `canpan-custom-script.js`).
- Never overwrite original Impact Theme classes directly. Extend them via `canpan-` classes only.

### CSS
- `theme.css` may **only** be adjusted by commenting out existing classes – never by directly
  modifying properties or values.
- If an existing Impact Theme class needs to be changed: comment out the original in `theme.css`
  (with a note `→ canpan-theme.css`) and add the modified version to `canpan-theme.css`.
- For new sections: modular CSS that only loads when the section is present in the DOM.
- `!important` is only permitted when demonstrably necessary: e.g. to override theme styles with
  equal or higher specificity, for utility classes (`.canpan-hide-*`), or to suppress third-party
  styles. Using `!important` on custom CANPAN classes without a cascade conflict is forbidden –
  natural specificity is sufficient there.

### Lighthouse & Performance
- All code must be written with Lighthouse optimization in mind. Changes must not negatively
  impact LCP, CLS, TBT, or FID.
- Before suggesting any solution, consider its performance impact on Core Web Vitals.

### JavaScript
- No render-blocking scripts in `<head>`. Always use `defer` or `async`.
- Before implementing any custom DOM observation, check whether the Impact Theme already provides
  a suitable event (e.g. `cart:change`, `cart:open`, `variant:changed`). Theme-native events
  always take priority over MutationObserver, `setInterval`, or similar approaches.
- `MutationObserver` is only permitted as a last resort when no theme event provides the
  required information.

### File Structure
- No new file for minor additions. Before creating a new asset or snippet file, always check
  whether the code can reasonably be inlined.
- **JavaScript**: Small scripts (< ~50 lines, single use) should be inlined directly in the
  corresponding Liquid snippet or section. A separate `canpan-*.js` file is only justified when
  the code is used across multiple independent locations or has substantial scope.
- **CSS**: Individual CSS variables or small style adjustments belong in `canpan-theme.css`,
  not in a new file. A separate CSS file is only warranted for a complete new section.
- **Liquid Snippets**: No new snippet for code rendered in only one place – inline it there.
  A snippet is only worthwhile at two or more independent usage locations.

### Liquid
- Preserve all original Impact Theme code comments when refactoring or optimizing existing code.

### JSON
- Settings and translations follow the existing Impact Theme schema structure.

---

## Code Comments
`QoL` (Quality of Life) is the fixed identifier for all CANPAN customizations and must always
be used in code comments – no exceptions. Every new or modified code block must include a
comment in the following format:

- Before launch:
  - CSS/JS: `/* CANPAN QoL PRE-LAUNCH – Brief description */`
  - Liquid: `{%- comment -%} CANPAN QoL PRE-LAUNCH – Brief description {%- endcomment -%}`
- After launch:
  - CSS/JS: `/* CANPAN QoL 1.0.0 – Brief description */`
  - Liquid: `{%- comment -%} CANPAN QoL 1.0.0 – Brief description {%- endcomment -%}`

Formatting rules (mandatory):
- One space before and after the comment content (inside the comment delimiters)
- No period at the end of the description

The version number (e.g. `1.0.0`) is always taken from `VERSION.md` – this is the current
development version. Do NOT use the version from `CHANGELOG.md`, as that reflects already
released versions.

**Version sanity check**: Before using the version from `VERSION.md`, compare it with the
most recent version entry in `CHANGELOG.md`. If both versions are identical, stop and ask
the user to confirm whether `VERSION.md` has been updated to the next development version
before proceeding. Only continue once confirmed.

`PRE-LAUNCH` is used as long as the store has not gone live.

---

## Prohibitions (hard limits)
The following actions are forbidden under all circumstances:
- Editing `theme.css` directly (changing properties or values)
- Overwriting original Impact Theme classes directly
- Using `!important` on custom CANPAN classes without a cascade conflict
- Placing render-blocking scripts in `<head>`
- Using `MutationObserver` or `setInterval` when a theme event is available
- Creating new files when inline code is sufficient
- Writing directly to `CHANGELOG.md`

---

## Change Documentation
After **every** completed task, `TEMP-CHANGELOG.md` must be updated – without asking,
without exception. If the file does not exist, create it. If it already exists and contains
entries, **append the new entry at the bottom** – existing entries must not be modified or removed.

The file is not committed (`.gitignore`) but must be maintained throughout the session.

Format:
```
## [TEMP] – DD-MM-YYYY

### Added
- ...

### Changed
- ...

### Fixed
- ...

### Dependencies
- ...
```

Same structure as `CHANGELOG.md` (Added / Changed / Fixed / Dependencies).

---

## Pre-Completion Checklist
Before marking any task as done, verify:
- [ ] `canpan-` prefix applied to all new classes, IDs, files, and variables?
- [ ] No direct modifications made to `theme.css`?
- [ ] Performance impact on Core Web Vitals considered?
- [ ] No unnecessary `!important` used?
- [ ] Code comment in the required format present?
- [ ] `TEMP-CHANGELOG.md` created or updated?

---

## Language
All commits, code comments, and documentation must be written in **German**.