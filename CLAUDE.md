# CLAUDE.md

## Project
Shopify theme for **GNTL** — a men's skincare brand (gntl-body.myshopify.com).
Three core products: `skin-wash`, `skin-emulsion`, `2-step-ritual`.

## Git
- User: BreckonJAnthony <breckonlewis@outlook.com>
- Main branch: `main`
- Always commit after each logical change with a clear message.
- Do not commit directly to main for risky changes — use a feature branch.

## Shopify environments (shopify.theme.toml)
| Environment | Theme ID | Use |
|---|---|---|
| staging | 154097025182 | All dev work goes here first |
| production | 153871253662 | Only push after explicit user approval |

## Push commands
```
shopify theme push --environment staging     # always use this
shopify theme push --environment production  # only with user approval
```
**Never push to production without explicit user sign-off.**
Do not modify `shopify.theme.toml`.

## File structure
- `templates/` — page and product layout templates (JSON)
- `sections/` — reusable content sections (Liquid + schema)
- `snippets/` — small reusable Liquid snippets
- `assets/` — CSS, JS, image files
- `config/` — `settings_schema.json`, `settings_data.json`

## Key custom files (what we've built)
| File | Purpose |
|---|---|
| `snippets/product-hero-copy.liquid` | CRO hero block: title, review summary, subheading, benefit bullets — rendered on skin-wash, skin-emulsion, 2-step-ritual PDPs |
| `snippets/product-subscription.liquid` | Custom subscription UI (currently **disabled** — see below) |
| `sections/sticky-atc.liquid` | Sticky Add-to-Cart bar that slides up after user scrolls past the buy box |
| `snippets/cart-shipping-message.liquid` | Free-shipping progress bar in cart drawer |

## Subscription setup — IMPORTANT
- **Recharge** is the subscription app. The Recharge global app embed in `config/settings_data.json` is **enabled** (`"disabled": false`) and provides the subscription widget on PDPs.
- The theme's own subscription block (`type: "subscription"`) is **disabled** (`"disabled": true`) in both `templates/product.skin-wash.json` and `templates/product.skin-emulsion.json`. Do not re-enable it — it creates a duplicate selector alongside the Recharge widget.
- Recharge brand colors configured in `settings_data.json`: `color_brand: #1b3731`, `contrast_color: #fff6e4`.

## Brand colours
| Token | Hex |
|---|---|
| Primary green | `#1b3731` |
| Cream / off-white | `#fff6e4` |
| Body background | `#f5f3ee` |
| Body text | `#000000` |

## Sticky ATC — selling_plan sync
`sections/sticky-atc.liquid` has a hidden `<input name="selling_plan">` and JS that syncs the selected Recharge plan from the main product form. The sync listens for `change` events on `[name="selling_plan"]` and `[name="selling-plan-group"]`. If Recharge's widget uses different selectors, this sync may need updating.

## Rules
- Never push to production directly. Staging first, always.
- Do not modify `shopify.theme.toml`.
- Do not re-enable the theme's native subscription block — rely on Recharge.
- Commit granularly with descriptive messages.
- Before touching any file, read it first.
