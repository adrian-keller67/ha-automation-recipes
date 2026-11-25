# Home Assistant Automation Recipes — 50 YAML automations & 2 blueprints

Companion repository for the book *Home Assistant Automation Recipes* (EN) / *Home Assistant Praxis-Automationen* (DE) by Adrian Keller.
Every recipe is free to use here. The book explains the *why* behind each pattern, edge cases and testing.

**Target:** Home Assistant 2026.11 · modern `triggers` / `conditions` / `actions` syntax · all configs load without errors on Home Assistant Core 2026.11.3

> Not affiliated with the Open Home Foundation, Nabu Casa or the Home Assistant project. "Home Assistant" is used nominatively. No Home Assistant logo is used.

## Quick start (5 minutes)

1. Create the helpers from [`helpers/book_helpers.yaml`](helpers/book_helpers.yaml) (or via Settings → Devices & services → Helpers). `presence_helpers.yaml` is a smaller subset: use one of the two, not both.
2. Open any file in [`automations/`](automations/), copy it, replace the placeholder entities (`person.alex`, `light.living_room`, ...).
3. Paste into Settings → Automations → ⋮ → *Edit in YAML*, save, then check the trace once.
4. Blueprints: copy to `config/blueprints/automation/adrian_keller/` and create the automation from the UI.

## Recipe index

| File | Recipe | What it does |
|---|---|---|
| [`r01_welcome_home_lights.yaml`](automations/r01_welcome_home_lights.yaml) | R01 Welcome home lights | When a person arrives home after sunset, turn on living room lights. Skip if guest mode is on. |
| [`r02_everything_off_when_leaving.yaml`](automations/r02_everything_off_when_leaving.yaml) | R02 Everything off when leaving | When zone.home drops to 0 people, turn off lights and selected switches. Respects guest mode. |
| [`r03_guest_mode_pause_note.yaml`](automations/r03_guest_mode_pause_note.yaml) | R03 Guest mode enabled notice | Confirms guest mode is on so presence automations stay paused. |
| [`r04_late_arrival_dimmed.yaml`](automations/r04_late_arrival_dimmed.yaml) | R04 Late arrival dimmed | Soft hallway + living room lights if someone arrives between 22:00 and 06:00. |
| [`r05_arrival_notification.yaml`](automations/r05_arrival_notification.yaml) | R05 Arrival notification | Persistent notification when a person arrives. Replace with notify.mobile_app_... for phone push (mobile_app i |
| [`r06_away_after_quiet.yaml`](automations/r06_away_after_quiet.yaml) | R06 Away after quiet period | When everyone is away, wait 20 minutes. If still empty and hallway motion is off, turn on input_boolean.house_ |
| [`r06b_clear_house_away_on_arrival.yaml`](automations/r06b_clear_house_away_on_arrival.yaml) | R06b Clear house away on arrival | Turns off input_boolean.house_away when any tracked person returns home. |
| [`r07_motion_illuminance.yaml`](automations/r07_motion_illuminance.yaml) | R07 Motion light only if dark | Turn on light on motion when illuminance is below threshold. |
| [`r08_lights_off_after_quiet.yaml`](automations/r08_lights_off_after_quiet.yaml) | R08 Lights off after quiet | Turn hallway light off after no motion for 5 minutes while light is on. |
| [`r09_sunset_living_room.yaml`](automations/r09_sunset_living_room.yaml) | R09 Sunset living room | Turn living room lights on 20 minutes before sunset if someone is home. |
| [`r10_night_hallway_glow.yaml`](automations/r10_night_hallway_glow.yaml) | R10 Night hallway glow | Low brightness hallway light on motion between 23:00 and 06:00. |
| [`r11_movie_mode.yaml`](automations/r11_movie_mode.yaml) | R11 Movie mode | When movie mode helper turns on, dim main lights and enable bias light. |
| [`r11b_movie_mode_off.yaml`](automations/r11b_movie_mode_off.yaml) | R11b Movie mode off restore | Restore living room lighting when movie mode turns off. |
| [`r12_all_lights_except.yaml`](automations/r12_all_lights_except.yaml) | R12 Ground floor lights except kitchen | Turn on ground-floor lights excluding kitchen area (Home Assistant 2026.11 exclude). |
| [`r13_morning_ramp.yaml`](automations/r13_morning_ramp.yaml) | R13 Weekday morning light ramp | On weekdays at 06:30, gently turn on bedroom light if someone is home. |
| [`r14_sync_two_lights.yaml`](automations/r14_sync_two_lights.yaml) | R14 Sync two lights | Mirror living room light on/off and brightness to a secondary lamp. |
| [`r15_heat_away_home.yaml`](automations/r15_heat_away_home.yaml) | R15 Heat away and home presets | Set climate to eco when house empty; comfort when someone arrives. |
| [`r16_window_open_pause_heat.yaml`](automations/r16_window_open_pause_heat.yaml) | R16 Window open pause heat | When a window opens, set climate off; restore when closed. |
| [`r17_weekday_climate_schedule.yaml`](automations/r17_weekday_climate_schedule.yaml) | R17 Weekday climate schedule | Comfort temperature weekday mornings and evenings. |
| [`r18_summer_vent_hint.yaml`](automations/r18_summer_vent_hint.yaml) | R18 Summer vent hint | Notify when indoor is warmer than outdoor in the evening. |
| [`r19_frost_protection_alert.yaml`](automations/r19_frost_protection_alert.yaml) | R19 Frost protection alert | Alert when a temperature sensor drops below frost threshold. |
| [`r20_heat_boost_30min.yaml`](automations/r20_heat_boost_30min.yaml) | R20 Heat boost 30 minutes | Temporary temperature boost when helper turns on, then restore. |
| [`r21_dishwasher_on_surplus.yaml`](automations/r21_dishwasher_on_surplus.yaml) | R21 Dishwasher on solar surplus | Start dishwasher when export power stays high; safety-first example. |
| [`r22_high_usage_warning.yaml`](automations/r22_high_usage_warning.yaml) | R22 High power usage warning | Notify if whole-home power stays above threshold. |
| [`r23_cheap_tariff_hint.yaml`](automations/r23_cheap_tariff_hint.yaml) | R23 Cheap tariff hint | Notify when electricity price sensor drops below a threshold. |
| [`r24_standby_killer.yaml`](automations/r24_standby_killer.yaml) | R24 Standby killer at night | Turn off entertainment switch late at night if TV is off. |
| [`r25_ev_charge_with_sun.yaml`](automations/r25_ev_charge_with_sun.yaml) | R25 EV charge only with surplus | Enable charger switch when export high; disable when export low. |
| [`r26_daily_energy_digest.yaml`](automations/r26_daily_energy_digest.yaml) | R26 Daily energy digest | Morning notification with yesterday-style energy reading from a sensor. |
| [`r27_door_open_at_night.yaml`](automations/r27_door_open_at_night.yaml) | R27 Door open at night | Alert if front door stays open during night hours. |
| [`r28_alert_when_away.yaml`](automations/r28_alert_when_away.yaml) | R28 Alert when away | Notify if a door or window opens while the house is empty. |
| [`r29_doorbell_snapshot.yaml`](automations/r29_doorbell_snapshot.yaml) | R29 Doorbell snapshot | Take a camera snapshot and notify when doorbell rings. |
| [`r30_quiet_hours_gate.yaml`](automations/r30_quiet_hours_gate.yaml) | R30 Quiet hours — critical path example | Example wrapper: only create a non-critical notice outside quiet hours. Pair critical alerts (smoke) with sepa |
| [`r31_smoke_escalation.yaml`](automations/r31_smoke_escalation.yaml) | R31 Smoke escalation | On smoke detected: notify and turn on lights for exit path. |
| [`r32_auto_lock_door.yaml`](automations/r32_auto_lock_door.yaml) | R32 Auto-lock door when away | Lock front door a few minutes after it closes while house is empty. |
| [`r33_tv_off_amp_off.yaml`](automations/r33_tv_off_amp_off.yaml) | R33 TV off turns amp off | When TV goes off, wait briefly then power down amplifier switch. |
| [`r34_good_night_script_runner.yaml`](automations/r34_good_night_script_runner.yaml) | R34 Good night from helper | When good-night helper turns on, run the good-night script and clear helper. |
| [`r35_assist_light_sentence.yaml`](automations/r35_assist_light_sentence.yaml) | R35 Assist sentence toggle living room | Custom conversation sentence toggles living room light. |
| [`r36_tablet_night_mode.yaml`](automations/r36_tablet_night_mode.yaml) | R36 Tablet night mode | Dim wall-tablet backlight lamp at night; brighter in the morning. |
| [`r37_device_unavailable_alert.yaml`](automations/r37_device_unavailable_alert.yaml) | R37 Device unavailable alert | Notify when a critical entity stays unavailable. |
| [`r38_zigbee_stick_health.yaml`](automations/r38_zigbee_stick_health.yaml) | R38 Zigbee coordinator check | Periodic check that Zigbee coordinator entity is not unavailable. |
| [`r39_automation_fail_notify.yaml`](automations/r39_automation_fail_notify.yaml) | R39 Watchdog stale sensor | Practical reliability pattern: if a temperature sensor does not change for hours, notify. Complements traces;  |
| [`r40_anti_flapping_lights.yaml`](automations/r40_anti_flapping_lights.yaml) | R40 Anti-flapping motion light | Motion light with restart mode and minimum on-time to reduce flapping. |
| [`r41_esp_temp_alert.yaml`](automations/r41_esp_temp_alert.yaml) | R41 ESPHome temperature alert | Alert on ESPHome-exported temperature sensor crossing threshold. |
| [`r42_esp_button_scene.yaml`](automations/r42_esp_button_scene.yaml) | R42 ESPHome button scene | ESPHome binary button press activates evening lights. |
| [`r43_esp_leak_shutoff.yaml`](automations/r43_esp_leak_shutoff.yaml) | R43 ESPHome leak shutoff | On leak sensor, close valve switch and notify. |
| [`r44_esp_status_led_sync.yaml`](automations/r44_esp_status_led_sync.yaml) | R44 ESPHome status LED sync | Mirror house_away helper to an ESPHome LED light. |
| [`r45_backup_reminder.yaml`](automations/r45_backup_reminder.yaml) | R45 Weekly backup reminder | Remind to download a Home Assistant backup every Sunday morning. |
| [`r46_battery_report.yaml`](automations/r46_battery_report.yaml) | R46 Low battery report | Daily template list of battery sensors below 30%. |
| [`r47_update_available.yaml`](automations/r47_update_available.yaml) | R47 Update available | Notify when a Home Assistant Core update entity turns on. |
| [`r48_maintenance_window_notify.yaml`](automations/r48_maintenance_window_notify.yaml) | R48 Maintenance window notify | At 04:00, if an update is pending, notify — does NOT auto-restart. Restart remains a manual decision after bac |
| [`r49_trace_hygiene_reminder.yaml`](automations/r49_trace_hygiene_reminder.yaml) | R49 Monthly trace hygiene reminder | Monthly reminder to review automation traces and stored_traces settings. |
| [`r50_monthly_inventory.yaml`](automations/r50_monthly_inventory.yaml) | R50 Monthly automation inventory | First-Sunday reminder to review the automations list and disable unused ones. |

## Blueprints

- [`late_arrival_dimmed`](blueprints/automation/late_arrival_dimmed.yaml): dimmed welcome light for late arrivals
- [`motion_illuminance_light`](blueprints/automation/motion_illuminance_light.yaml): motion light that respects ambient brightness

## Safety

Energy, heating and water recipes are patterns, not certified safety systems. Manufacturer limits, electrical codes and common sense win. R48 only notifies, it never restarts Core.

## Bonus recipes (not in the book)

- [`extra_low_battery_digest.yaml`](automations/extra_low_battery_digest.yaml): one daily digest of all battery sensors below a threshold, found via `device_class` instead of entity names
- [`extra_mass_unavailable_watchdog.yaml`](automations/extra_mass_unavailable_watchdog.yaml): one alert when many entities become unavailable at once (dead Zigbee stick, MQTT broker, router)

## How this repo was made and what was tested (transparency)

The recipes were written with AI assistance. What was checked, on Home Assistant Core **2026.11.3**:

- All automations, the `good_night` script and both blueprints (instantiated with sample entities) load in a test instance without errors, and `check_config` passes.
- The two bonus recipes were also **run** with test entities (the battery digest lists exactly the sensors below the threshold and stays silent otherwise; the watchdog stays silent below the threshold and fires above it).
- The recipes R01–R50 use placeholder entity names and were **not** run against real devices. Entity names and device capabilities differ in every home, so test each recipe on your instance and look at its trace before you rely on it.

Found a problem? Please [open an issue](../../issues).

## Get the book / Zum Buch

The repository is the free part. The book adds explanations, troubleshooting and the reasoning behind each recipe.

- **English:** [Paperback](https://www.amazon.com/dp/B0HSLDFP3C) · [Kindle](https://www.amazon.com/dp/B0HR8QM6RQ) · [PDF + EPUB + all YAML (Payhip)](https://payhip.com/b/63gt9)
- **Deutsch:** [Taschenbuch](https://www.amazon.de/dp/B0HSLJMJHJ) · [Kindle](https://www.amazon.de/dp/B0HR8V5T57) · [PDF + EPUB + alle YAML-Dateien (Payhip)](https://payhip.com/b/9j6sp)

## Contributing

Issues and pull requests with better entity patterns, additional recipes or translations are welcome.

## License

MIT, see [LICENSE](LICENSE). It covers the YAML files in this repository; the book text is not part of the license.
