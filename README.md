# DVDV-audio

**Using DVD-Video discs for audio playback**

DVDV-audio is a collection of tools for creating audio-oriented DVD-Video discs that can be played on standard DVD players.

The goal is to combine uncompressed digital audio, album and track navigation, and an optional on-screen music player interface using features already available in the DVD-Video specification.

Unlike DVD-Audio, this approach does not require a DVD-Audio-compatible player.

## Concept

A DVD-Video disc normally contains video and audio streams. DVDV-audio takes a different approach:

- **Audio:** Uncompressed stereo LPCM audio, typically 48 kHz / 16-bit.
- **Video:** A static black MPEG-2 video background, encoded at a very low bitrate.
- **Subpictures:** Optional graphical overlays displaying track information and playback progress.
- **Navigation:** DVD titles, chapters and menus provide album selection, track skipping and continuous playback.

The result behaves much like a conventional music player, while remaining compatible with ordinary DVD-Video playback equipment.

### Display modes

The on-screen information is implemented using DVD subpicture streams rather than being embedded in the video.

With subtitles enabled, the player can display information such as:

- Artist, album and track titles
- Track numbers and durations
- Album and track progress indicators

With subtitles disabled, the video remains completely black, allowing music playback without a distracting display.

No changes to the audio or video streams are required when switching between these modes.

## How it works

The disc creation process consists of two main stages.

### 1. Preparing

The source material is prepared for DVD authoring.

The current workflow uses WAV audio files and CUE sheets to describe albums and their track boundaries.

Depending on the source material, preparation may include:

- Audio format conversion and resampling
- Editing or trimming source recordings
- Extracting track and album metadata
- Calculating chapter positions and durations

The objective is to produce consistent audio and metadata for the authoring stage.

### 2. Authoring

The prepared material is converted into a DVD-Video structure.

The process includes:

1. Converting the audio into DVD-compatible LPCM format.
2. Generating a low-bitrate black MPEG-2 video stream.
3. Rendering track information and progress indicators as DVD subpictures.
4. Multiplexing audio, video and subpictures into DVD-compatible VOB files.
5. Creating DVD titles, chapters and navigation menus.
6. Assembling the final `VIDEO_TS` directory for playback or disc burning.

The implementation uses Python scripts together with established tools such as FFmpeg, `mplex` and `dvdauthor`.

## Compatibility

The project aims to produce standard DVD-Video discs that work on conventional standalone DVD players as well as software players.

The current prototype has been tested on multiple standalone players and PC-based playback software.

One important compatibility consideration is the relationship between video resolution and subpicture rendering. Although reduced-resolution MPEG-2 video can save disc space, some software players do not correctly scale full-resolution subpicture overlays.

For this reason, the current implementation uses a 704×576 anamorphic 16:9 black video background for PAL DVD-Video output.

## Current status

**Experimental prototype — functional, but not yet reorganized for public use.**

The current implementation has successfully produced:

- Single-concert DVD-Video titles with LPCM audio and graphical track information.
- Multi-concert DVD-Video discs with navigation menus.
- Chapter-based track selection.
- Continuous playback across multiple concert titles.

A four-concert DVD-5 compilation with more than five hours of music has been successfully tested on a standalone DVD player, including continuous playback and automatic return to the main menu.

The original scripts will be preserved as a historical prototype before the codebase is reorganized into a more maintainable toolkit.

## Planned development

Future work may include:

- A cleaner separation between preparation and authoring tools.
- Shared Python modules and consistent command-line interfaces.
- Improved configuration and error handling.
- Automated validation of generated streams and DVD structures.
- Multiple selectable subpicture layouts.
- Optional elapsed-time and remaining-time displays.
- Improved documentation and reproducible examples.

## License

This project is released under the MIT License. See [LICENSE](LICENSE) for details.
