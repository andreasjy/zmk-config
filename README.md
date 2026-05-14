# Corne ZMK Config

Personal ZMK configuration for the Corne (crkbd) split keyboard.

## Layout overview

- **Base**: QWERTY with home row mods (middle row)
- **5 layers**: default, symbol, numbers, nav, adjust
- **Estonian Ü**: top-right key sends `[`, which produces `Ü` when OS layout is Estonian

## Layers

### Default

- **Left column** (top→bottom): Copy/Paste mod-tap (tap=Ctrl+C, hold=Ctrl+V) · Esc · Tab
- **Right column**: `[` (Ü in Estonian) · `'` · Backspace
- **Home row mods**: GASC/CSAG (Gui/Alt/Shift/Ctrl mirrored)
- **Left thumbs**: GUI · `LT(NUM) tap=Enter` · `LT(SYM) tap=Backspace`
- **Right thumbs**: `LT(SYM) tap=Space` · `MO(NAV)` · Alt

### Symbol (held via either thumb's outer key)

```
` @ # $ ~       ^ { } _ +
! _ < > %       & ( ) - =
_ _ \ | _       _ [ ] * _
```

### Numbers (held via left center thumb)

PgUp/PgDn on D/F (top-row navigation while held), numpad-style on right hand:

```
_ _ _ _ _       _ 7 8 9 _
_ _ _ Pu Pd     _ 4 5 6 _
_ _ _ _ _       _ 1 2 3 _
                0
```

### Navigation (held via right center thumb)

Vim-ish arrows on ESDF, Home on W, End on R:

```
_ _ Home _ End _    _ _ _ _ _
_ _ ←  ↓  ↑  →     _ _ _ _ _
```

### Adjust (combo: hold both NUM and NAV thumb keys)

Bluetooth profiles, output toggle, F7-F12, media keys, `->` and `=>` macros, reset/bootloader.

## Combos (base layer only)

- `A + S` → Esc
- `S + D` → Tab
- `E + R` → `(`
- `U + I` → `)`

## Home row mod tuning

Conservative settings to reduce misfires:
- `tapping-term-ms = 280`
- `quick-tap-ms = 175` (fast typing disables hold)
- `require-prior-idle-ms = 150` (needs brief pause before holding)
- `hold-trigger-on-release` with opposite-hand-only positions

If you still get accidental mods, bump `tapping-term-ms` to 300. If mods feel slow, drop to 250.

## Estonian Ü note

The top-right key sends `LBKT` (`[`). On an Estonian OS layout, that physical position maps to `Ü`. If you sometimes use a US layout and want a literal `Ü` regardless of OS settings, replace `&kp LBKT` with a Unicode macro instead — let me know.

## Building

Push to GitHub and the included Actions workflow builds firmware automatically.
Download the artifact zip, then flash:

1. Double-tap reset on the nice!nano to enter bootloader mode (it mounts as a USB drive)
2. Drag `corne_left.uf2` onto it
3. Repeat for the right half with `corne_right.uf2`

## Customizing

- `config/corne.keymap` — keys, layers, combos, macros
- `config/corne.conf` — board features (sleep, BT power, display)
- Use the [ZMK keymap editor](https://nickcoutsos.github.io/keymap-editor/) for a GUI

## Quick reference: thumb access

```
              left thumbs              right thumbs
position:    outer  center  inner    inner   center  outer
binding:     GUI    NUM/Ent SYM/Bsp  SYM/Spc NAV     Alt
hold action: -      Numbers Symbol   Symbol  Nav     -
combo:                      [hold both center thumbs → Adjust]
```
