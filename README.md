# Companion — Home Assistant Praxis-Automationen / Automation Recipes

**Repository:** https://github.com/adrian-keller67/ha-automation-recipes


**Author pen name:** Adrian Keller  
**Target:** Home Assistant **2026.11**  
**YAML:** modern `triggers` / `conditions` / `actions` (2024.10+); action calls use `action:` (2024.8+)

## Layout

```
companion/
  automations/     # R01–R50 + teaching examples + R11b/R06b helpers
  blueprints/automation/  # late_arrival_dimmed, motion_illuminance_light
  helpers/         # presence + book helpers (input_boolean)
  scripts/         # good_night script for R34
  README.md
```

## Import

1. Create helpers from `helpers/book_helpers.yaml` (UI Helpers also fine).
2. Copy or paste automations; replace placeholder entities (`person.alex`, `light.living_room`, …).
3. Blueprints → `config/blueprints/automation/adrian_keller/` then create from UI.
4. Script `good_night` → include as package or paste under `script:`.
5. Reload automations / scripts (Settings → Tools → YAML).

## Validation

All YAML in this folder is checked with PyYAML and yamllint in the authoring workspace. Still test on your instance — entity names and device capabilities differ.

## Safety

Energy and water recipes are patterns. Manufacturer limits, electrical codes, and common sense win. Do not auto-restart Core without a backup (R48 notifies only).

## Disclaimer

Not affiliated with the Open Home Foundation, Nabu Casa, or the Home Assistant project. “Home Assistant” is used nominatively. Do not use the Home Assistant logo.
