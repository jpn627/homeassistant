# Home Assistant Blueprints

A collection of [Home Assistant](https://www.home-assistant.io/) automation
blueprints for Inovelli switches, Lutron Pico remotes, and a Nest doorbell →
WiiM/soundbar chime.

## Contents

- [Inovelli White Fan Switch — Tap Sequences with LED Colors](#inovelli-white-fan-switch--tap-sequences-with-led-colors)
- [Lutron Pico Remote → Fan & Light Controller](#lutron-pico-remote--fan--light-controller)
- [Nest Doorbell Chime on WiiM Speakers](#nest-doorbell-chime-on-wiim-speakers)

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

## Nest Doorbell Chime on WiiM Speakers

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjpn627%2Fhomeassistant%2Fblob%2Fmain%2Fnest-doorbell-wiim-chime.yaml)

**File:** [`nest-doorbell-wiim-chime.yaml`](./nest-doorbell-wiim-chime.yaml)

Play a chime through one or more WiiM (or any announce-capable) media players
when a Nest doorbell is pressed. Built around the `media_player` **announce**
feature so the chime ducks/overlays current audio, with extra handling for
TV / physical-input setups.

**Features**

- Chime via `announce: true` (ducks and auto-resumes on WiiM native sources)
- **Chime sound** picker, optional **chime volume** (restored afterward)
- **Time-of-day chime**: a different sound and/or volume during an evening
  window (overnight-aware)
- **Quiet Hours** to silence the chime entirely during set times
- **Cooldown** to ignore repeated presses
- **Restore source after chime** — switches the speaker back to its prior input
  (HDMI / optical / line-in), so live TV audio returns
- **Pause a TV / streamer** during the chime (e.g. a Google TV Streamer via the
  Android TV Remote integration), with optional resume (default: stay paused)
- **Waits for the chime to actually finish** (state-watched, with a fallback)
  before restoring input / resuming

**Setup notes**

- Put a chime file (e.g. `doorbell.mp3`) in `/media` or `/config/www`, then
  pick it as the Chime Sound.
- To pause content on an external HDMI device, target the **streamer that's
  actually playing** (e.g. the Google TV Streamer) — pausing the TV itself
  won't pause external HDMI playback.

**Caveats (WiiM firmware, not the blueprint)**

- Auto-resume does **not** work for Spotify Connect / AirPlay / Bluetooth
  sources — the chime interrupts and can't resume those.
- With `announce`, the device may apply its own volume handling, so the chime
  volume control is most predictable on the TV / physical-input path.

---

## Credits

- Inovelli blueprint forked from
  [jay-kub/inovelli-matter-switch-tap-sequences](https://github.com/jay-kub/inovelli-matter-switch-tap-sequences).
