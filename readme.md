# yt_clipper

## Notices

- If the mainline (non-beta) release is out of date and has old dependencies (when using the clipper installation), you can check for a newer beta release. Since clipper script `v3.6.1`, releases can be tracked here: <https://github.com/exwm/yt_clipper/releases>. Older releases can be found here: <https://mega.nz/#F!4HYDAKDS!NqS5Nk9heN7QBxvQapudeg>.
  - When using a beta release use the shortcuts reference table in the markup script and the `yt_clipper_options` helper script or `-h` help flag for a review of any usage changes.

- This readme is synchronized only with the mainline release and does not talk about any beta or alpha releases.

- Windows users on `v3.6.0` or higher of the `clipper script` installation getting ffmpeg crashes may want to try the following:
  - Update visual c++ redistributables:
    - For 64-bit Windows: <https://aka.ms/vs/16/release/vc_redist.x64.exe>
    - For other Windows versions and older redistributables check this page: <https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads>.
  - Switch to static ffmpeg build: <https://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-4.2.3-win64-static.zip>
    - Replace contents of `yt_clipper_win_3.x.x/bin` with the contents of the `bin` folder in the ffmpeg zip.

## Quick Start

Visit [this quickstart guide](https://github.com/exwm/yt_clipper/blob/master/quickstart.md) to get up and running with `yt_clipper`.

The contents of the quickstart guide are included here for convenience:

1) First install a user script extension (preferably Tampermonkey) for your browser (preferably chrome).
   - See [this article](https://openuserjs.org/about/Userscript-Beginners-HOWTO) for more information.
2) Next install the `markup script` component of `yt_clipper` by clicking [here](https://openuserjs.org/install/elwm/yt_clipper.user.js).
3) Install the standalone `clipper script` component of `yt_clipper` by visiting [this section](https://openuserjs.org/scripts/elwm/yt_clipper#clipper-script-installation).
   - Alternatively download the python source [here](https://github.com/exwm/yt_clipper/blob/master/src/clipper/yt_clipper.py) and see [this section](https://openuserjs.org/scripts/elwm/yt_clipper#clipper-script-usage) for usage instructions.
4) Visit a YouTube video page. Check that the `markup script` is [active on the page](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_active_on_page.png). Refresh the page if it is not active.
5) Press **Alt+Shift+A** to activate the `markup script` and its hotkeys. You should see a [flash message](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_hotkeys_activated.png) below the video.
   - Use the various hotkeys to add marker pairs and edit settings to specify how to clip the video.
     - **A** to add markers, **Z** to undo markers, **Shift+Mouseover** a yellow end marker to open [its settings editor](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_marker_pair_editor.png).
     - **W** to open global settings editor, **Shift+W** to toggle additional settings.
   - Click the [shortcuts reference toggle](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_shortcuts_table.png) in the video player bar for an overview of all shortcuts.
   - Hover over an option in a settings editor to see a [tooltip](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_tooltip.png) describing the option.
6) Use the **S** key to save markers data in `.json` format.
7) Generate webms using the saved markers data and the `clipper script`.
   - **Windows:** Drag and drop the saved markers data onto the `yt_clipper_auto.bat`.
   - **Mac:** Launch the `yt_clipper_auto.sh` program, drag and drop the saved markers data onto the terminal, and hit **Enter**.
   - Find generated webms in `yt_clipper/webms/title-suffix` folder where `title-suffix` is the file name stem of the markers data file.
   - See [this section](https://openuserjs.org/scripts/elwm/yt_clipper#additional-helper-scripts) for details on the other helper scripts available.
8) See the [full instructions](https://openuserjs.org/scripts/elwm/yt_clipper) for more detail and advanced usage as well as changelogs.
9) Check the [changelogs](https://openuserjs.org/scripts/elwm/yt_clipper#markup-script-changelog) for updates as there is not yet an automated mechanism.
10) Join the [`yt_clipper` discord server](https://discord.gg/5RVGNCU) if you want further help or want to contribute.

## Browser Support

- Works best on Chrome with the Tampermonkey extension and YouTube video in theater mode.
- You may need to refresh the video page and ensure this user script is active.
- FireFox, Opera, and most Chromium-based browsers not fully tested, but reportedly work as intended.
  - FireFox audio slowdown stutters and in mainline FireFox has a min speed of 0.5.
- Other browsers may or may not work as intended.

## Related Scripts

- Check out the companion script with tools for making some tasks on `gfycat.com` easier (e.g., quickly tagging multiple gfys, copying gfy links in various formats) at <https://openuserjs.org/scripts/elwm/gfy-tools>.

## Table of Contents

- [yt_clipper](#yt_clipper)
  - [Notices](#notices)
  - [Quick Start](#quick-start)
  - [Browser Support](#browser-support)
  - [Related Scripts](#related-scripts)
  - [Table of Contents](#table-of-contents)
  - [Terminology and Installation](#terminology-and-installation)
  - [Markup Script Shortcuts](#markup-script-shortcuts)
    - [Marker Shortcuts](#marker-shortcuts)
    - [Cropping Shortcuts](#cropping-shortcuts)
    - [Video Playback and Preview Shortcuts](#video-playback-and-preview-shortcuts)
    - [Time-Variable Speed Chart Shortcuts](#time-variable-speed-chart-shortcuts)
    - [Frame Capturing Shortcuts](#frame-capturing-shortcuts)
    - [Save and Upload Shortcuts](#save-and-upload-shortcuts)
  - [Useful YouTube Controls](#useful-youtube-controls)
  - [Tips](#tips)
    - [User Script Tips](#user-script-tips)
    - [Clipper Script Tips](#clipper-script-tips)
  - [Encoding Settings Guide](#encoding-settings-guide)
    - [Articles on CRF and vp9 Encoding](#articles-on-crf-and-vp9-encoding)
    - [Tips and Settings](#tips-and-settings)
      - [Markup Script](#markup-script)
      - [Clipper Script](#clipper-script)
    - [Gamma Correction](#gamma-correction)
  - [Clipper Script Source](#clipper-script-source)
  - [Clipper Script Usage](#clipper-script-usage)
  - [Clipper Script Preview Shortcuts](#clipper-script-preview-shortcuts)
  - [Clipper Script Installation](#clipper-script-installation)
    - [Additional Helper Scripts](#additional-helper-scripts)
      - [Windows Merge Helper Bat Script](#windows-merge-helper-bat-script)
  - [All Releases](#all-releases)
  - [Clipper Script Dependencies](#clipper-script-dependencies)
  - [Changelog](#changelog)

## Terminology and Installation

- `Markup script` refers to this user script and is used to mark up YouTube videos before creating webm clips.
  - It requires a user script extension such as _Tampermonkey_ which you can install from your browser's add-ons store.
  - See <https://openuserjs.org/about/Userscript-Beginners-HOWTO> for more information on user scripts.
- `Clipper script` refers to the python script or installation that consumes marker data in `json` format to generate webm clips.
  - See [Clipper Script Usage](#clipper-script-usage) for usage instructions.
  - See [Clipper Script Installation](#clipper-script-installation) for installation instructions.

## Markup Script Shortcuts

First ensure the script is active on the page by checking your user script extension.

- ![yt_clipper_active_on_page](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_active_on_page.png)

**Alt+Shift+A:** Toggle hotkeys on/off. A green message will flash below the video indicating hotkeys are enabled.

A shortcuts reference can be toggled by clicking the scissor icon in the video controls bar.

- ![yt_clipper_shortcuts_table](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_shortcuts_table.png)

### Marker Shortcuts

**A:** Add marker at current time (start = green, end = yellow, selected = black center). Multiple marker pairs can be added simultaneously.

**Z:** Undo last marker.

**Shift+Z:** Redo last undone marker.

**Ctrl+Shift+Alt+Z:** Delete currently selected marker pair. Does nothing if no pair selected.

**Shift+Mouseover:** Toggle marker pair editor. Must be done over an end marker (yellow). Selected marker pairs have a black center.
  ![yt_clipper_marker_pair_editor](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_marker_pair_editor.png)

- Modified marker pair settings are accented orange while settings redundant with a global setting are accented red.
- Reorder marker pairs using the input box in the title of the marker pair settings panel.
- Edit pair crop or speed multiplier.
- Edit `Title Prefix` that will be prepended to the `Title Suffix` and used in the webm name for the marker pair.

**Ctrl+Up**: Select/deselect the most recently selected marker pair or else the first available pair.

**Ctrl+Down**: Toggle auto-hiding of unselected marker pairs.

**Adjusting marker position:**

- While a pair is selected use **Shift+Q/Shift+A** to move the start/end marker to current time.
  - Adjust marker position more precisely by first using the **<** and **>** keys to seek videos frame by frame.
  - Use **Alt+Shift+Mousewheel** and scroll up/down to move marker one frame forward/backward.
    - When performed on the left half of the window moves the start marker and on the right half the end marker.
  - Use **Alt+Z/Alt+Shift+Z** to undo/redo marker moves.
    - Move history is kept separately for each marker pair.

- Jumping to and selecting marker pairs without the mouse
  - **Ctrl+Left/Right:** Jumps to the nearest previous/next marker.
  - **Alt+Left/Right:** Select the next/previous marker pair relative to the currently or previously selected pair.
  - **Ctrl+Alt+Left/Right:** Select the next/previous marker pair _and jump to its start marker_.

**W:** Global settings editor:
  ![yt_clipper_globals_editor](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_globals_editor.png)

1. Modified global settings are accented red.
2. Change default new marker speed or crop.
   - Any new markers added will use these defaults, but this will not update existing markers.
   - To update existing markers to the default new marker speed/crop use **Alt+Shift+Q/Alt+Shift+X**.
3. Specify crop resolution (automatically scales any existing crops on change).
   - This resolution must match the downloaded video's resolution.
   - By default the max available video resolution is downloaded by the `clipper script` and the crop resolution auto-scaled if a mismatch is detected.
4. Specify any webms you want to merge from the clipped webms.
   - Very fast as it does not require re-encoding webms.
   - The format is similar to that for printer page ranges:
     - Each merge is a comma separated list of marker pair numbers or ranges (e.g., '1-3,5,9' = '1,2,3,5,9').
     - Multiple merges are separated with semicolons (e.g., '1-3,5,9;4-6,8' will create two merged webms).
5. Specify `Title Suffix` appended to each marker pair `Title Prefix` to produce its `Full Title`.
   - By default the `Title Suffix` is the YouTube video ID in square brackets (e.g., \[Bey4XXJAqS8\]).
   - The `Title Suffix` is used for the name of the folder containing all generated webms.

**Shift+W:** Open additional settings when the global settings editor or a marker pair editor is open.

- Settings left blank with a placeholder of `Auto` will be automatically calculated based on the input video bitrate and other video properties. This is the recommended default.
- Marker pair settings are overrides that if set will override the global value for that marker pair only.
- Marker pair settings set to `Inherit` will get their value from the global settings.
- Global settings set to `Inherit` will get their value from the command line options or the `yt_clipper_options` `.bat/.app` prompt.
- See [Encoding Settings Guide](#encoding-settings-guide) for more information and tips about the possible settings.
- Marker Pair Overrides:
  - ![yt_clipper_marker_pair_editor_overrides](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_marker_pair_editor_overrides.png)
- Global Encode Settings:
  - ![yt_clipper_globals_editor_additional_settings](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_globals_editor_additional_settings.png)

**Alt+Shift+Q/alt+Shift+X:** Update all existing markers to default new marker speed (**Q**) or crop (**X**).

- Set the default new marker speed or crop using **W**.

### Cropping Shortcuts

**X:** When marker or defaults editor is open, begin drawing crop. 

- **Click+Drag** on the video to set draw a rectangular crop.

- While drawing crop, pressing **X** again will cancel drawing.

- Crop is given as `x-offset:y-offset:width:height`. Each value is a positive integer in pixels. `Width` and `height` can also be `iw` and `ih` respectively for input width and input height.

**Shift+X:** Like **X**, begin drawing a crop but set only the left and right boundaries.

- Vertically fills the crop, that is, it sets the top to 0 and the bottom to the video height.

**Ctrl+X:** Cycle crop dim opacity by +0.25.

**Mouse-Based crop Adjustment:**

- **Ctrl+Hover:** Indicate potential drag action when hovering over crop.
- **Ctrl+Click+Drag:** Drag and move crop or resize crop in the indicated directions.
  - Can release **Ctrl** after dragging begins. Dragging ends when mouse is released.
- **Ctrl+Alt+Drag:** Approximately aspect-ratio-locked mouse resizing of crop.

  ![yt_clipper_crop_preview.png](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_crop_preview.png)

**Arrow Key Crop Adjustment**:

- When a crop input box has focus:
  - **UpArrow/DownArrow:** Increment/decrement the value indicated by the current cursor position by `10`.
- When a crop input box does not have focus:
  - **Alt+X:** Toggle crop adjustment with arrow keys.
  - **UpArrow/DownArrow:** Increment/decrement the `y offset` by `10`.
  - **LeftArrow/RightArrow:** Increment/decrement the `x offset` by `10`.
  - **Ctrl** modifier key changes target from `y offset` to `height` or from `x offset` to `width`.
- The **Alt** and **Shift** modifier keys alter the increment/decrement amount.
  - **Alt** sets the amount to `1`, **Shift** to `50`, **Alt+Shift** to `100`.
- The resulting crop values are clamped to valid values.

### Video Playback and Preview Shortcuts

**Shift+Mouse-Wheel:** Scroll the mouse wheel up/down over the video to skip forward/backward one frame per tick.

**C:** Toggle auto video playback speed adjustment based on markers. When outside of a marker pair the playback speed is set back to 1 (and cannot be changed without toggling off auto speed adjustment).

**Shift+C:** Toggle auto looping of currently selected marker pair.

**Alt+C:** Toggle auto previewing gamma correction setting when between a marker pair.

**Alt+Shift+C:** Toggle fade loop previewing.

- Note that fade duration defaults to 0.5 and is clamped to a minimum of 0.1 seconds and a maximum of 40% of the output clip duration.

**Ctrl+Alt+Shift+C:** Toggle all previews.

- If any preview feature is disabled, turns it on. If all preview features are enabled, disables all of them.

**R/Alt+R:** Toggle between a 90 degree clockwise/counter-clockwise rotation and no rotation.

- Works only when in fullscreen mode or theater mode.
- **Note that this does not yet work with drawing and previewing crops and should be disabled when doing so.**
- **This feature is only for watching or previewing the video, and does not affect webm output.**

**Shift+R:** Toggle big video previews on video progress bar hover.

**Q:** Decrease video playback speed by 0.25. If the speed falls to or below 0 it will cycle back to 1.

### Time-Variable Speed Chart Shortcuts

![yt_clipper_speed_chart](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_speed_chart.jpg)

**D:** Toggle time-variable speed chart.

**Right-Click:** Seek to time on bottom time-axis when clicking anywhere in chart area.

**Alt+Right-Click/Ctrl+Alt+Right-Click:** Set speed chart looping start/end marker.

**Shift+D:** Toggle speed chart looping (note speed chart looping only works when speed previewing is on with **C**).

**Alt+D:** Reset speed chart looping markers.

**Click+Drag:** Drag a speed point to move it or drag chart area to pan when zoomed in.

**Shift+Click:** Add a speed point.

**Alt+Shift+Click:** Delete a speed point.

**Ctrl+mouse-wheel:** Zoom in and out of speed chart. **Ctrl+Click:** Reset zoom.

**Notes:**

- Points are auto-sorted based on their time value on adding or removing points or on drag-end when moving points.
- ouTube playback speed can only be set to a multiple of `0.05` and greater than or equal to `0.25`.
- Audio is not compatible with time-variable speed.

### Frame Capturing Shortcuts

**E:** Capture frame at current time of video at currently selected video quality/resolution.

- Frame must be buffered and loaded.
- Opens a pop-up window where captured frames are saved.
  - **Download** and **Delete** buttons are provided above each captured frame.
  - You may need to allow pop-ups from `https://www.youtube.com` in your browser settings.

  ![yt_clipper_frame_capturer](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_frame_capturer.png)

**Alt+E** Trigger zipping of all captured frames for download.

### Save and Upload Shortcuts

**S:** Save markers info to a `.json` file.

- Can be dropped onto the installation's `yt_clipper_auto.bat` or `.bat` files to generate webms.
- Can be passed to the `clipper script` using `--json`.

**Alt+S:** Copy markers `json` data to clipboard. Useful if saving breaks.

**G:** Toggle markers `json` file upload for reloading markers (must be from the same video).

- Click `Choose File`, pick your markers `json` file, then click `Load`.
  - ![yt_clipper_load_markers](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_load_markers.png)

**Alt+V:** Upload anonymously to gfycat.

- The quality is not generally good.
- Most encoding settings are not used, including speed adjustments.

**Alt+Shift+V(Disabled):** Open gfycat browser authentication and upload under account (auth server must be running).

- Same caveats as **Alt+V** for anonymous uploading.

## Useful YouTube Controls

1. Use **[space_bar]** or **K** to pause/play the video.
2. Use **<** and **>** to view a video frame by frame.

## Tips

### User Script Tips

1. If you're new to userscripts check out <https://openuserjs.org/about/Userscript-Beginners-HOWTO> for instructions.
2. Check out the companion script for copying gfy links from gfycat as reddit markdown at <https://openuserjs.org/scripts/elwm/gfy2md>.
3. Refresh the page if the script doesn't load and to clear markers when switching videos in the same window.
4. Videos can be marked up and the markers json or clipper script can be saved before higher quality levels are available, but the final generated webm quality depends on the quality formats available.

### Clipper Script Tips

1. The `clipper script` skips regenerating any existing webms.
   - This makes it easy to delete webms you want regenerated and by rerunning the script.
   - Use this to work incrementally, saving markers data, starting a batch encode, continuing to mark up, overwriting the markers data, and then rerunning the encoding.

## Encoding Settings Guide

### Articles on CRF and vp9 Encoding

1. [Basic crf guide](https://slhck.info/video/2017/02/24/crf-guide.html)
2. [ffmpeg vp9 encoding guide](https://trac.ffmpeg.org/wiki/Encode/VP9)
3. [Google vp9 basic encoding](https://developers.google.com/media/vp9/the-basics/)
4. [vp9 encoding tests](https://github.com/deterenkelt/Nadeshiko/wiki/Tests.-VP9:-encoding-to-size,-part%C2%A01)

### Tips and Settings

#### Markup Script

1. Move between input fields with **Tab**.
2. Non-text input fields can be set using the **Up/Down** arrow keys or the **Mousewheel**.
3. Override the default encoding settings using the **Shift+W** additional settings editors.
4. Hover over settings in the `markup script` to view tooltips describing each setting.
  ![yt_clipper_tooltip](https://raw.githubusercontent.com/exwm/yt_clipper/master/assets/image/yt_clipper_tooltip.png)

#### Clipper Script

1. The `clipper script` is set to use the vp9 encoder by default (encoding used for webm videos on YouTube).
2. Use `--help`, `-h`, or the `yt_clipper_options` helper script for additional options that can be enabled on the command line.
3. Encoding settings will be automatically selected unless overriden based on the detected bitrate of the input video.

### Gamma Correction

- Play around with the `gamma` setting to bring back shadow or highlight detail.
- Use **Alt+C** to preview `gamma values` with the `markup script`.
- A value of 1 does nothing. Use a value between 0 and 1 to bring back shadow detail and a value greater than 1 to bring back highlight detail.
- Refer to this [gamma correction guide](https://www.cambridgeincolour.com/tutorials/gamma-correction.htm) for more details.

## Clipper Script Source

- You can find the clipper script python source file here: <https://github.com/exwm/yt_clipper/blob/master/src/clipper/yt_clipper.py>

## Clipper Script Usage

```sh
python ./yt_clipper.py -h # Prints help. Details all options and arguments.

python ./yt_clipper.py --markers-json markers.json # automatically generate webms using markers json

python ./yt_clipper.py --input-video ./clip.webm --markers-json markers.json # provide a local input video

python ./yt_clipper.py -j markers.json --preview  # preview marker pairs using ffplay

python ./yt_clipper.py -j markers.json --format bestvideo[width<=1080] # specify download format used by youtube-dl
```

## Clipper Script Preview Shortcuts

See <https://ffmpeg.org/ffplay.html#While-playing>.

## Clipper Script Installation

There is an installation that does not require the dependencies below.

1. Extract the appropriate zip file anywhere:
   - On _Windows_ download this [zip file (win_v3.6.5)](https://github.com/exwm/yt_clipper/releases/download/msv0.0.89%2Bcsv3.6.5/yt_clipper_win_3.6.5.zip)
   - On _Mac_ download this [zip file (mac_v3.6.5)](https://github.com/exwm/yt_clipper/releases/download/msv0.0.89%2Bcsv3.6.5/yt_clipper_mac_3.6.5.zip)
   - The latest install (`v3.6.5`) is only compatible with `v0.0.75` or higher of the `markup script`
2. Simply drag and drop the markers .json file onto the `yt_clipper_auto.bat` file on Windows or at the terminal prompt after executing `yt_clipper_auto` on Mac.
3. Use `Ctrl+C` if you need to cancel the process.
4. All generated webm clips will be placed in `./webms/<markers-json-filename>`.
5. Windows users may require [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555).

### Additional Helper Scripts

There are some alternative helper scripts for more options:

- Use `yt_clipper_options` to print all the available options and to be prompted for a string with additional options before running the script. This allows you to combine options (e.g., include audio and rotate and denoise).
  - The other helper scripts provide preconfigured subsets of these options.
- Use `yt_clipper_preview` to locally preview markers `json` data with `ffplay`.
  - _Cannot preview audio, video stabilization, or expanded color range._
- Use `yt_clipper_auto_download` to download video before processing markers.
- Use `yt_clipper_auto_input_video` to specify both markers `json` data and an input video for processing.
  - On Windows simply drag and drop both the `json` and the input video onto `yt_clipper_auto_input_video`.
  - On Mac, `yt_clipper_auto_input_video` will prompt for the `json` then the input video.
- Use `yt_clipper_auto_interpolate` to apply motion interpolation to output video targeting 60 fps.

The helper scripts have a simple format. Copy and edit `yt_clipper_auto` in a text editor to create custom automated versions.

- On Windows:

  ```bat
  @echo off
  chcp 65001
  cd /D "%~dp0"

  FOR %%A IN (%*) DO (
    REM add options after %%A of the next line as shown
    .\yt_clipper.exe --markers-json %%A --denoise --audio --rotate clock
  )

  pause
  ```

- On Mac

  ```bash
  #!/bin/bash
  cd "$(dirname "$0")"

  read -p "First enter the paths of 1 or more markers json data files (you may be able to drag and drop files at the prompt): " JSONPROMPT

  IFS=$'\n' JSONS=( $(xargs -n1 <<< "$JSONPROMPT") )

  for JSON in "${JSONS[@]}"
  do
    if [ -f "$JSON" ]; then
      # add options after $JSON of the next line as shown
      ./yt_clipper --markers-json "$JSON" --denoise --audio --rotate clock
    else
      echo "$JSON does not exist"
    fi
  done
  ```

#### Windows Merge Helper Bat Script

The `yt_clipper_merge.bat` can be used to merge any webm files in any order:

- Rename the webm files so they sort in ascending lexicographic order.
- Select/highlight all webms to be merged in your file explorer and drag and drop them onto the `bat`.
- The output file will be `-merged` appended to the first input file.
- Check the `merge.txt` file to confirm the correct videos were merged in the correct order.

## All Releases

Since clipper script `v3.6.1`, releases can be tracked here: <https://github.com/exwm/yt_clipper/releases>. Older releases can be found here: <https://mega.nz/#F!4HYDAKDS!NqS5Nk9heN7QBxvQapudeg>.

## Clipper Script Dependencies

These dependencies must be manually installed when not using the clipper script installation:

- ffmpeg must be in your path for the python script (<https://www.ffmpeg.org>).
- `--markers-json`/`-j` require youtube-dl as a python package
  - `pip install youtube-dl`
- `--gfycat` requires urllib3
  - `pip install urllib3`

## Changelog

For a complete changelog, including beta and alpha releases,
see <https://github.com/exwm/yt_clipper/blob/develop/changelog.md>.
