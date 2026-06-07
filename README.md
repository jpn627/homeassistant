# Home Assistant Blueprints

A collection of [Home Assistant](https://www.home-assistant.io/) automation
blueprints for Inovelli switches, Lutron Pico remotes, and a Leviton Matter
scene controller.

## Contents

- [Inovelli White Fan Switch — Tap Sequences with LED Colors](#inovelli-white-fan-switch--tap-sequences-with-led-colors)
- [Lutron Pico Remote → Fan & Light Controller](#lutron-pico-remote--fan--light-controller)
- [Leviton Scene Controller — Toggle Light Groups (Matter)](#leviton-scene-controller--toggle-light-groups-matter)

## How to import a blueprint

Click an **Import Blueprint** button below and confirm in your Home Assistant
instance, then create an automation from it (**Settings → Automations & Scenes →
Blueprints**).

Prefer to do it manually? **Settings → Automations & Scenes → Blueprints →
Import Blueprint**, and paste the blueprint's GitHub URL.

---

## Inovelli White Fan Switch — Tap Sequences with LED Colors

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjpn627%2Fhomeassistant%2Fblob%2Fmain%2Finovelli-white-fan-switch-colors.yaml)

**File:** [`inovelli-white-fan-switch-colors.yaml`](./inovelli-white-fan-switch-colors.yaml)

Run actions from an Inovelli **White Series Fan Switch** (and Fan/Light Canopy
Module) and set the LED bar color for each action. A fork of
[jay-kub's Inovelli Matter Switch Tap Sequences](https://github.com/jay-kub/inovelli-matter-switch-tap-sequences),
with per-action LED color control added on top.

**Features**

- Up / Down / Config button actions for 1–5 taps, plus **Held** and **Released**
- Optional **LED bar color per action** (13 official White Series colors), each
  defaulting to *No Change* so the bar is only touched where you assign a color
- **Fan Speed → LED Color**: the bar continuously reflects the bound fan's
  speed, as a deepening cool-blue ramp (Off = White, Low = Aqua, Med = Cyan,
  High = Blue) — all configurable
- **Light binding** (brightness sync, reverse sync, minimum brightness)
- **Fan binding** to the Config button (Held = Off, 1× = Low, 2× = Med, 3× = High)

**Supported models:** VTM35-SN (White Fan Switch), VTM36 (White Fan/Light
Canopy Module); VTM30-SN / VTM31-SN also work for the button + LED features.

---

## Lutron Pico Remote → Fan & Light Controller

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjpn627%2Fhomeassistant%2Fblob%2Fmain%2Fpico-remote-fan-controller.yaml)

**File:** [`pico-remote-fan-controller.yaml`](./pico-remote-fan-controller.yaml)

Control a fan and its light with a 5-button Lutron Caséta Pico remote.

**Features**

- **On** restores the fan's last speed; **Off** turns it off
- **Center** toggles the fan light
- **Raise / Lower** step the fan speed (queued so rapid presses aren't dropped)
- Optional **`input_number` helper** for true last-speed restore across off/on
  cycles, with a configurable fallback speed

**Setup note:** for the best "restore last speed," create a **Number** helper
(**Settings → Devices & Services → Helpers**, min 0 / max 100) and select it as
the *Last Speed Helper*. Without it, the automation falls back to the fan's
current speed, then the default speed.

---

## Leviton Scene Controller — Toggle Light Groups (Matter)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjpn627%2Fhomeassistant%2Fblob%2Fmain%2Fleviton-scene-controller-light-groups.yaml)

**File:** [`leviton-scene-controller-light-groups.yaml`](./leviton-scene-controller-light-groups.yaml)

Control two groups of lights with a Leviton Matter scene controller (e.g.
D2SCS): one button toggles a **bulbs** group, one toggles a **fixtures** group,
and one turns **everything off**. Built for an all-Matter setup (Leviton
controller + Govee lights) so Home Assistant drives the lights locally — low
latency, with every light in a group commanded in a single call.

**Features**

- Three button → action mappings (toggle bulbs, toggle fixtures, all off)
- **Smart group toggle**: if any light in a group is on, the whole group turns
  off; if all are off, it turns on (keeps the group in sync)
- Triggers on the buttons' Matter `event` entities (the reliable path, since
  Matter device-triggers aren't consistently exposed)
- Configurable **press event type** (default `initial_press`) for controllers
  that report a different value

**Setup notes**

- The D2SCS exposes its **top three buttons** as event entities (the bottom
  button is line power and can't be used).
- If a press does nothing, open **Developer Tools → States**, press the button,
  read the entity's `event_type`, and set the Options field to match (commonly
  `initial_press`, `short_release`, or `multi_press_1`).

---

## Credits

- Inovelli blueprint forked from
  [jay-kub/inovelli-matter-switch-tap-sequences](https://github.com/jay-kub/inovelli-matter-switch-tap-sequences).
