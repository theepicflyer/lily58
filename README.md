# lily58

Keyboard-side ZMK firmware for the SplitKB Aurora Lily58. This repo covers
**both** of my Lily58s — one standalone, one driven by a
[MacroKnob dongle](https://github.com/theepicflyer/macroknob-shield/tree/splitkb_aurora_lily58) —
and supports either half acting as the central.

## Flash a matched pair

The two halves must agree on who is central. Pick a row and flash both:

| Setup | Left half | Right half |
|---|---|---|
| **Standalone, left central** (ZMK default) | `splitkb_aurora_lily58_left_central` | `splitkb_aurora_lily58_right_peripheral` |
| **Standalone, right central** | `splitkb_aurora_lily58_left_peripheral` | `splitkb_aurora_lily58_right_central` |
| **Dongled** (MacroKnob is central) | `splitkb_aurora_lily58_left_dongled` | `splitkb_aurora_lily58_right_peripheral` |

`settings_reset` is universal — flash it to any half to clear stored settings
and Bluetooth pairings.

Note the right half is identical for the two left-central setups: it is a
peripheral in both, so one artifact serves both keyboards.

### Switching which side is central

Old pairings survive a reflash and will fight the new role assignment. Do this:

1. Flash `settings_reset` to **both** halves.
2. Flash the new matched pair.
3. Re-pair with the host.

## Where the keymap actually lives

- **Standalone keyboard** → `config/splitkb_aurora_lily58.keymap`, in this repo.
- **Dongled keyboard** → the *dongle's* keymap, in
  [macroknob-shield@splitkb_aurora_lily58](https://github.com/theepicflyer/macroknob-shield/tree/splitkb_aurora_lily58).

The central owns the keymap. Editing this repo's keymap will not change what the
dongled keyboard types.

ZMK Studio is enabled on whichever half is central, so you can also edit the
live keymap over USB without rebuilding.

## Releases

Pushing a `v*` tag builds and publishes a Release with every `.uf2` attached:

```bash
git tag v1.0.0 && git push origin v1.0.0
```

Prefer Releases over Actions artifacts for anything you might need later —
artifacts are deleted after 90 days.

## Editing the keymap

<https://nickcoutsos.github.io/keymap-editor/>
