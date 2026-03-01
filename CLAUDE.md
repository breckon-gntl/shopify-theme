# CLAUDE.md

## Project: Shopify Theme

## Rules
- Never push to production directly. Always push to staging first.
- Make all changes on a feature branch, never directly on main.
- Commit after each logical change with a clear message.
- Do not modify shopify.theme.toml.

## Push commands
Staging: shopify theme push --environment staging
Production (only after my approval): shopify theme push --environment production

## File structure
- templates/ — page and product layout templates
- sections/ — reusable content sections
- snippets/ — small reusable Liquid snippets
- assets/ — CSS, JS, image files
- config/ — theme settings (settings_schema.json, settings_data.json)
