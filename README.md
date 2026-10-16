<h1 align="center">OpenFadeR-Map</h1>

<p align="center">
  <a href="LICENSE"><img alt="License: AGPL-3.0" src="https://img.shields.io/github/license/OpenRsG/OpenFadeR-Map"></a>
</p>

MIDI controller mappings for [OpenFadeR](https://github.com/OpenRsG/OpenFadeR), the open-source DJ app: one `<controller>.xml` per controller, more than 170 of them. A mapping is picked when a connected MIDI input port's name contains the file's `<port>` (the longest match wins).

## Install in one click

In the app: PREFERENCES > CONTROLLER > GET MAPPINGS lists every mapping of this repository (it is there by default; search by controller name) and installs one in one click. Plug in a controller that has no mapping yet and the app offers the matching file from this repository: press INSTALL and the controller works.

## Other ways

The app looks for mapping files in each folder of `$OPENFADER_MAPPINGS` (`:`-separated), then in
`~/.config/openfader/mappings/`, then in a `mappings/` folder next to the executable. Either copy the files you need there or
point the app at this checkout:

```sh
OPENFADER_MAPPINGS=/path/to/OpenFadeR-Map openfader
```

The core's `start.sh` clones this repository as `mappings/` in the core checkout, where the app finds it next to its binary.

`audio-cards.json` lists sound-card name fragments whose headphone output is on channels 3/4.

## Format

```xml
<OpenFadeRMapping schemaVersion="1">
  <info>
    <name>Example Controller</name>
    <port>Example</port>             <!-- picked when an input port name contains it -->
    <outInterval>2</outInterval>     <!-- ms between two messages to the controller (optional) -->
    <ringInterval>12</ringInterval>  <!-- jog ring refresh in ms (optional) -->
  </info>
  <controls>
    <control status="0x90" midino="0x0B" action="play" deck="0"/>
    <control status="0xB4" midino="0x02" action="fx-level-1" deck="0" hires="true"/> <!-- 14-bit: LSB on midino + 0x20 -->
    <control status="0x97" midino="0x00" action="hw-pad" deck="0" arg="0"/>
  </controls>
  <outputs>
    <output status="0x90" midino="0x58" light="Sync" deck="0" blink="600"/>
  </outputs>
</OpenFadeRMapping>
```

`deck` is 0..3 (deck A..D), `arg` the action's constant. The action and light names are listed in the core repository
(`src/app/midi/actions/`, `src/app/midi/mod.rs` `Led`). Only the default layer of a controller is mapped; a controller's
own SHIFT that sends different MIDI messages works, software shift layers do not.

## Contributing and license

Mapping files for new controllers are welcome. For anything more than a small fix, open an issue first. [CONTRIBUTING.md](CONTRIBUTING.md) shows how to try a mapping with `OPENFADER_MIDI_LOG=1` and the test every file must pass. The [code of conduct](CODE_OF_CONDUCT.md) applies. Related repositories: [OpenFadeR](https://github.com/OpenRsG/OpenFadeR), [OpenFadeR-Plugins](https://github.com/OpenRsG/OpenFadeR-Plugins) and [OpenFadeR-Themes](https://github.com/OpenRsG/OpenFadeR-Themes).

AGPL-3.0, see [LICENSE](LICENSE).
