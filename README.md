# Audio to MIDI Converter – Atari 8-bit Edition

A browser-based audio and MIDI conversion tool designed to create MIDI files for the **Atari 8-bit MIDI-PLAY 1.3 player**.

Convert MP3 and WAV audio into simplified MIDI arrangements, import existing MIDI files, normalize them for Atari playback, and export MIDI files or Atari ATR disk images.

## Features

- 🎵 **Audio to MIDI:** Convert MP3 and WAV files into MIDI arrangements.
- 🎹 **MIDI Import:** Load existing Standard MIDI files (`.mid`, `.midi`).
- 🕹️ **Atari Compatibility:** Normalize MIDI files to a restricted format intended for MIDI-PLAY 1.3.
- ▶️ **Audio Preview:** Test generated arrangements directly in your browser.
- ⏱️ **Timeline Navigation:** Scrub through the arrangement.
- 🎚️ **Conversion Controls:** Adjust sensitivity, duration, note grid, and number of voices.
- 💾 **MIDI Export:** Download converted arrangements as Standard MIDI files.
- 💿 **ATR Export:** Generate Atari 8-bit disk images containing the converted MIDI.

## MIDI Output Specifications

The converter uses a deliberately restricted MIDI structure to improve compatibility with Atari 8-bit playback software.

| Parameter | Specification |
|---|---|
| MIDI Format | Standard MIDI Format 0 |
| Tracks | 1 |
| Resolution | 384 PPQ |
| Tempo | 120 BPM |
| Time Signature | 4/4 |
| Voices | 1 or 2 |
| Voice 1 | Piano (Program 0) |
| Voice 2 | Steel Guitar (Program 25) |
| Note Range | MIDI pitches 50–86 |
| Velocity | 21–127 |

Imported MIDI files are not simply copied. Their note data is normalized to the converter's output restrictions.

## Atari MIDI Compatibility

Vintage Atari MIDI software can be considerably more restrictive than modern MIDI applications.

To address these limitations, imported MIDI files are processed before export:

- Convert timing to 384 PPQ and 120 BPM.
- Restrict pitches to the supported range of 50–86.
- Limit the arrangement to one or two voices.
- Quantize notes to the selected grid.
- Apply controlled note durations.
- Rebuild the MIDI as a single-track Format 0 file.
- Insert timing filler events to split excessively long gaps between MIDI events.

### Timing Filler Events

Some MIDI files contain long periods without note events. These gaps may cause compatibility problems with MIDI-PLAY 1.3.

The converter addresses this by inserting harmless note-off events to divide long delays into smaller intervals.

The current maximum event gap is set to **1,155 ticks**, based on comparison with a MIDI file successfully played by MIDI-PLAY 1.3.

This is an experimentally determined compatibility measure, not a formally documented limit of the Atari software.

## Conversion Settings

### Length

Adjust the output duration from 25% to 400% of the original duration.

### When Length Changes

- **Stretch:** Adjusts the timing to fit the selected duration.
- **Loop / Trim:** Repeats or truncates the arrangement to fit the selected duration.

### Sensitivity

Controls how easily audio frequency peaks are detected during MP3 and WAV conversion.

### Note Grid

Controls the timing resolution of generated notes.

| Grid | Resolution |
|---|---:|
| 16th Notes | 96 ticks |
| 8th Notes | 192 ticks |
| Quarter Notes | 384 ticks |

### Voices

Choose between:

- **1 Voice:** Piano.
- **2 Voices:** Piano and Steel Guitar.

## ATR Disk Image Export

The application can generate Atari 8-bit ATR disk images containing the converted MIDI arrangement.

The disk image uses a DOS II+ boot disk structure and includes:

- `MIDIPL13.COM`
- `AUTORUN.SYS`
- `NAME.MID` – The converted song.

This provides a convenient way to transfer converted music into an Atari 8-bit environment.

## How to Use

1. Open the HTML application in a modern desktop browser.
2. Load an MP3, WAV, or MIDI file using the file picker or drag-and-drop area.
3. Adjust the conversion settings.
4. Click **Test** to preview the arrangement.
5. Use the timeline slider to navigate through the music.
6. Select **Download .mid** to export a MIDI file.
7. Select **Download .atr** to generate an Atari disk image.

## Technical Implementation

The application is built as a standalone HTML document containing its own:

- HTML interface
- CSS styling
- JavaScript conversion engine
- Audio decoding and frequency analysis
- MIDI parsing and generation
- ATR disk image generation

Audio analysis uses browser audio capabilities, including FFT-based frequency analysis.

MIDI files are parsed and reconstructed directly in JavaScript without requiring an external conversion service.

The application runs locally in the browser and does not require a server-side backend.

## Project Goal

The purpose of this project is to bridge modern audio and MIDI formats with the limitations of vintage Atari 8-bit MIDI playback software.

Rather than attempting to preserve every detail of a complex musical arrangement, the converter prioritizes:

- Predictable MIDI structure
- Limited polyphony
- Restricted pitch range
- Controlled note timing
- Atari-oriented compatibility

**Modern audio in, Atari 8-bit MIDI out.**

## Compatibility

- Modern desktop browsers
- MP3 and WAV audio files
- Standard MIDI Format 0 and Format 1 input
- Atari 8-bit MIDI-PLAY 1.3-oriented MIDI output
- Atari ATR disk image export
