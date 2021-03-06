# Infinity ErgoDox layout and Kiibohd kll compiler

Based entirely off of fredZen's compilation mechanism, with my own KLL files.

The pictured keyboard layout is the spec I am trying to achieve; I can't do
it all through the Infinity Ergodox
[online keyboard configurator](https://input.club/configurator-ergodox/)
(though I did use that to generate a rough draft of the KLL files), so instead
I use an
[online keyboard layout editor](http://www.keyboard-layout-editor.com/) to
draft the spec.

The actual app-launcher mechanism is through BetterTouchTool.

The "tap" functionality for Esc and Control/Shift is implemented through
[Karabiner-Elements](https://github.com/tekezo/Karabiner-Elements).

My layout for the
[Infinity ErgoDox](http://input.club/devices/infinity-ergodox) keyboard.

![Keyboard layout](layout.png)

The default layout, for reference regarding the KLL mappings:

![Default keyboard layout](ergodox-default-layout.png)
## Editing

The layout files are in kiibohd/\*.kll.

- ergodox-0.kll is the main layer
- ergodox-1.kll is the layer with arrows, function keys and braces
- ergodox-2.kll is the layer with the keypad

## Workflow

My workflow uses the
[docker version](https://hub.docker.com/r/fmerizen/ergodox-infinity-layout/)
of the KLL compiler. First make sure that you have a working docker
installation.

1. Edit ergodox-\*.kll to my liking.
2. If I added or removed a layer, I need to change the value of PartialMaps in
   kiibohd/ergodox.bash accordingly
3. Run `./compile.sh ergodox.bash` from a docker aware bash. For me that will
   just be git-bash. And yes, that's correct, there is no directory before
   ergodox.bash
   although ergodox.bash is in the kiibohd subdirectory.
4. The compiled firmware is now available as kiibohd/\*.dfu.bin.
5. Flash each side of the keyboard with
   [dfu-util](https://github.com/kiibohd/controller/wiki/Loading-DFU-Firmware).
   More specifically, run:

    ```bash
    dfu-util -D <firmware>
    ```

   where `<firmware>` is the firmware file created by docker and stored in the
   `kiibohd` directory.
