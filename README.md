# P-6 Sample Banks

A browser tool for the Roland AIRA Compact **P-6** sampler's sample banks, so you don't need Roland's P-6 SampleTool. Load sounds onto its 48 pads (8 banks × 6), shape them, set the P-6's own pad settings, and save kits that go straight onto the P-6.

Live at **https://aaronvandorn.github.io/P-6/**. Nothing is uploaded; everything happens in your browser.

## What it does

- **Banks and pads:** banks A–H, six pads each, with a waveform, length and memory bar on every pad. Drag one pad onto another to swap them. Keys **1–6** play the pads of the current bank; the space bar plays the selected pad.
- **Open anything:** a kit `.zip` saved here, a folder or zip copied from the P-6 drive (such as `EXPORT`), Roland's factory sample download, or plain audio (WAV, MP3, OGG, FLAC, M4A). P-6 files land on their own pads with their settings; other sounds fill empty pads. Drop on a pad to put a sound there.
- **Import check:** after every import a dialog lists each pad that got a sound, whether it came with its P-6 settings, what it replaced, anything skipped, and anything too long. Click a row to hear it, then **Keep**, or **Undo import** to put every pad back as it was.
- **Edit (baked into the file):** trim with handles, trim silence, fades with linear, exponential or S-curves, gain, normalize, reverse, and **seamless loop** (crossfades the end into the start and turns on Loop on the P-6).
- **Tone (baked in):** varispeed pitch, low cut, low shelf, a parametric mid, high shelf, high cut, drive (warm, clip or fold) and compression.
- **Format:** the P-6's rates (44.1, 22.05, 14.7, 11.025 kHz), mono or stereo, 16/12/10/8-bit resolution with optional dither. **Fit to the P-6** picks the best rate that fits. Apply one pad's format to the whole bank or kit.
- **P-6 settings:** pitch, fine tune, level, pan, loop, gate, reverse, lo-fi, filter cutoff and resonance, delay and reverb sends, chop, and the P-6's start, end and loop points (drag them on the lower waveform). Every one of the 62 values is editable under *All 62 settings*. The preview follows pitch, level, pan, start/end, loop and reverse.
- **Memory:** each pad shows how much of a pad it uses; banks show their fill; too-long pads are flagged.
- **Save kit:** one `.zip` with the P-6 files, your original sounds and every setting (`kit.json`), so you can open it later and keep editing without losing quality. **Device zip** has only the P-6 files.
- **Write to P-6** (Chrome or Edge on a computer): writes straight to the P-6 drive.
- The current kit is kept in your browser between visits.

## Getting sounds onto the P-6

1. Connect the P-6 by USB, hold **[SAMPLING]** and switch it on. It shows up as a drive called **P-6**.
2. Either use **Write to P-6…**, or copy from a Device zip:
   - **One bank:** copy the `PAD_1` … `PAD_6` folders from inside a `BANK_x` folder into `IMPORT`. This is how Roland's manual loads samples.
   - **Several banks:** copy `BANK_A` … `BANK_D` into `IMPORT` (Roland's factory-restore method), then repeat for `BANK_E` … `BANK_H`.
3. Eject the drive, then press **[KYBD]** on the P-6. Wait for **donE**.

## Getting sounds off the P-6

Export one bank at a time: with USB connected, hold that bank's button (**[A/E]** to **[D/H]**) and switch on; add **[SAMPLING]** for banks E–H. Wait about a minute, then copy the `EXPORT` folder and open it here with **Open folder…**. Save pad edits on the P-6 first (**[SHIFT] + [TIE] (WRITE)**, then **PAd** or **Pd.AL**), or the export won't include them.

## From the rest of the set

- **Record from an app:** grab the last bars (or record the next bars) from Logic Rhythm, Melody Machine, Choir and the other apps open in this browser, cut on their bar lines, onto the selected pad. (Shared JAM-CLIPS block.)
- **Take a tape:** pull a tape's loop from Tape Loop Deck onto the selected pad. (Shared DECK-LINK block, as a taker.)
- **Kits:** any app that sends kits with the shared KIT-LINK block can send to `p6`; you choose the bank and pad they start on.
- **Session export:** the shared Export bar saves what you've played on the pads as WAV and MIDI.
- **MIDI in:** notes play the selected pad at their pitch (C4 plays it as set).

`jam-clips.js`, `kit-link.js` and `deck-link.js` are the source copies of the shared blocks embedded in `index.html`.

## The P-6's files

Worked out from real exports on firmware 1.02, and checked by re-saving them here byte for byte.

- Each pad is `PAD_n/P6_<bank>-<n>.WAV` plus `P6_<bank>-<n>.PRM`.
- The WAV is 16-bit PCM, mono or stereo, followed by a Roland `PAD ` chunk (88 bytes): `"Roland  P-6     "` and the same settings as the PRM, packed as bytes (start, size and loop size as 32-bit, the stretch speed as 16-bit, the rest as single bytes, tunings signed).
- The PRM is plain text: one `KEY<tab>= value` line per setting, 62 lines, LF line ends.
- `START_POS`, `SIZE` and `LOOP_SIZE` count samples into the file. Trimming on the P-6 never cuts the audio. The P-6 can save an end past the end of the file, and a loop size longer than the size; both are kept as they are.
- A pad holds up to 262,144 samples in mono, 131,072 in stereo.

### Still to confirm on the device

- Which bank a set of `PAD_1`–`PAD_6` folders imports into, and whether `BANK_x` folders hold `PAD_n` folders, as written here.
- Whether the P-6 keeps files at lower sample rates or converts them to 44.1 kHz on import.
- `PHRASE` is 0–5 on bank A. Here it's written as the pad's number across the whole kit (0–47); a bank B export will show whether that's right.
