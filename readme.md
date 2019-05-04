# yt_clipper

## Browser Support

- Works best on Chrome. Better Firefox support is a work in progress.
- Not tested on browsers other than Chrome or Firefox.

## Hotkeys

### Marker Hotkeys

**alt+shift+A(changed in v0.0.66):** toggle hotkeys on/off.

**A:** Add marker at current time (start = green, end = yellow, selected = white glow).

**Z:** Undo last marker (disabled if a marker pair is currently selected).

**shift+mouseover:** View marker pair info and edit a pair's crop or speed (output webm fps is **multiplied** by the speed factor).

<img src="https://i.imgur.com/AYJYeTf.png">

- While a pair is selected use **shift+Q/shift+A** to move the start/end marker to current time.
  - Adjust marker position more precisely using the '<' and '>' keys to view YouTube videos frame by frame.
- While a pair is selected use **shift+Z** to delete the pair.

**W:**

<img src="https://i.imgur.com/FEhjqkj.png">

1. Change default new marker speed or crop (output webm fps is **multiplied** by the speed factor).
2. Specify crop resolution (automatically scales any existing crops on change). This resolution must match the downloaded videos resolution, by default the maximum available.
   - Note that you can mark up the video at any quality/resolution and simply change the intended download resolution before saving the clipper script.
3. Specify any concatenated (merged) webms you want to make from the clipped webms. The format is similar to that for print ranges: comma separated marker pair numbers or ranges (eg '1-3,5,7'). Use semicolons to separate merged webms (eg '1-3,5,7;4-6,9' will create two merged webms)
4. Specify title prefix that will be prefixed to output script and webms.

**shift+E/D:** Update all markers to default new marker speed(**E**)/crop(**D**).

**X:** When marker or defaults editor is open, begin drawing crop. **Shift+click** in the video to set the top left crop boundary and then **shift+click** again to set the bottom right. Any other click action (eg ctrl+click) will stop drawing.

**shift+X(v0.0.57+):** Like **X**, begin drawing a crop but set only the left and right boundaries on **shift+click**. Vertically fills the crop, that is, it sets the top to 0 and the bottom to the video height.

### Video Playback Hotkeys

**shift+G:** Toggle auto video playback speed adjustment based on markers. When outside of a marker pair the playback speed is set back to 1 (and cannot be changed without toggling off auto speed adjustment).

**alt+G(v0.0.60+):** Toggle auto looping of currently selected marker pair.

**Q:** Decrease video playback speed by 0.25. If the speed falls below 0 it will cycle back to 1.

### Save and Upload Hotkeys

**S:** Save generated python clipper script (save it beside input webm).

**shift+S:** Copy generated python clipper script to clipboard (useful if saving breaks).

**alt+S or ctrl+alt+S:** Save markers info to a file (.json). Use ctrl+alt+s on `Firefox` to avoid interfering with built in shortcuts.

**G:** Toggle markers .json file upload for reloading markers (must be from the same video). Click `Choose File`, pick your markers .json file, then click `Load`.

<img src="https://i.imgur.com/19rao2O.png">

**alt+C(changed in v0.0.66):** Upload anonymously to gfycat (only supports slowdown through the gfycat url).

**alt+shift+S:** Save yt_clipper authorization server script (run it with python ./yt_clipper_auth.py, close it with ctrl+C). Does not work on `Firefox` yet.

**alt+shift+C(changed in v0.0.66):** Open gfycat browser authentication and upload under account (auth server must be running).

## Values

Crop is given as x:y:w:h where x:y is the distance left:top from the top left corner and w:h defines the width:height of the output video. Each value is a positive integer in pixels. w and h can also be iw and ih respectively for the input width and input height.

## Useful YouTube Controls

1. Use [space_bar] or K to pause/play the video.
2. Use '<' and '>' to view a video frame by frame.

## Tips

### User Script Tips

1. If you're new to userscripts checkout <https://openuserjs.org/about/Userscript-Beginners-HOWTO> for instructions.
2. Checkout the companion script for copying gfy links from the gfycat upload results page as markdown at <https://openuserjs.org/scripts/elwm/gfy2md>.
3. The script can be slow to load sometimes, so wait a bit before adding markers.
4. Refresh the page if the script doesn't load and to clear markers when switching videos in the same window.
5. Videos can be marked up and the markers json or clipper script can be saved before higher quality levels are available, but the final generated webm quality depends on the quality formats available.

### Clipper Script Tips

1. The clipper script skips regenerating any existing webms. This makes it easy to delete webms you want regenerated and by rerunning the script.

### Quality and CRF Tips

Articles on crf and vp9 encoding:

1. [Basic crf guide](https://slhck.info/video/2017/02/24/crf-guide.html)
2. [ffmpeg vp9 encoding guide](https://trac.ffmpeg.org/wiki/Encode/VP9)
3. [Google vp9 basic encoding](https://developers.google.com/media/vp9/the-basics/)
4. [More vp9 encoding](https://developers.google.com/media/vp9/live-encoding/)
5. [vp9 encoding tests](https://github.com/deterenkelt/Nadeshiko/wiki/Tests.-VP9:-encoding-to-size,-part%C2%A01)

Tips:

1. The script is set to use the vp9 encoder by default (this is the encoding used for webm videos on YouTube).
2. The vp9 encoder is set up to flexibly assign bitrate, providing more for high complexity scenes and less for simple scenes. The script is set to use a min value for the quantizer of 0 and a max of 60 (qmin=0, qmax=60).
3. The default crf is 30 and provides a good balance of size and quality for most YouTube video reencodes. This can be adjusted with the --crf flag in the script. There is unlikely to be any quality benefit to crf values below 22.
4. A crf of about 35 is more appropriate for 4k 60fps videos.

## Output Script Usage

```sh
python ./clip.py -h # Prints help. Details all options and arguments.

python ./clip.py ./filename.webm

python ./clip.py ./filename.webm --overlay ./overlay.png --gfycat

python ./clip.py ./filename.webm --format bestvideo+bestaudio # this is the default format

python ./clip.py --url https://www.youtube.com/watch?v=0vrdgDdPApQ --audio

python ./clip.py --json markers.json # automatically generate webms using markers json
```

## Windows Installation

For windows there is an experimental installation that does not require the dependencies below.

1. Download this [zip file (v1.2.0)](https://mega.nz/#!4exyXA7a!hzsQrpYOx4UTbDMWkmzVWHawo-9ADatgbZpEGqBQczA) and extract it anywhere.
2. Use the user script on YouTube as usual, but use **alt+S** to save the markers json in the extracted yt_clipper folder.
3. Lastly, just drag and drop the markers json file onto the `yt_clipper.bat` file.
4. All generated clips will be placed in `./webms/<markers-json-filename>`.
5. Install [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) if necessary.

A couple of alternative bat files provide more options and all work by dropping the markers json onto them:

- Use `yt_clipper_clock.bat` and `yt_clipper_counterclock.bat` to also rotate the generated webms by 90 degrees clockwise or counter clockwise respectively.
- Use `yt_clipper_audio.bat` to include audio in the generated webms.
- Use `yt_clipper_opts.bat` to print all the available options and to be prompted for a string with additional options before running the script. This allows you to combine options (eg include audio and rotate and denoise).

## Dependencies

These dependencies are not required by the windows installation above.

- ffmpeg must be in your path for the python script (<https://www.ffmpeg.org>).
- passing --url to the python script requires youtube-dl be in your path
  - `pip install youtube-dl`
- passing --gfycat requires the urllib3 python package.
  - `pip install urllib3`

## Changelog

- v0.0.70: Fix speed multipliers (slowdowns) being saved as string values instead of numbers in Firefox. Add visual clarity to default settings editor and marker pair settings editor. Add more flash messages, primarily for toggleable features.
- v0.0.69: Add preview of first click (top left dimension) of crop. Make crop preview more visible in bright videos. Add message flash on hotkeys enable and disable.
- v0.0.68: Add visual clarity to crop preview rectangle and selected marker pairs. Reword some aspects of UI (Download Res -> Crop Resolution, Short Title -> Title Prefix, Concats -> Merge List)
- v0.0.67: Add borders and padding around input controls.
- v0.0.66:
  - Improve Firefox support:
    - Change interfering hotkey **ctrl+shift+A**, which is used to open the Firefox extension manager: Toggle hotkeys binding moved from **ctrl+shift+A** to **alt+shift+A**.
    - Fix marker positioning in YouTube video.
  - Avoid interfering with YouTube closed caption toggle hotkey: Change upload to gfycat binding from **C** to **alt+C** and open gfycat auth page binding from **shift+C** to **alt+shift+C**.
- v0.0.65: Skip generating existing webm clips before executing ffmpeg for faster script reruns.
- v0.0.64: Add denoise, deinterlace and crf options in clipper script.
- v0.0.63: Add creating webms using markers json in python clipper script. Add concatenating (merging) clips.
- v0.0.62: Make short title input in defaults editor wider and improve YouTube video fps detection.
- v0.0.61: Fix cropping when not in theater mode on YouTube.
- v0.0.60: Add **alt+G** for auto looping currently selected marker pair.
- v0.0.59: **Q** key now decreases playback speed by 0.25, cycling back to 1 if speed becomes 0 or less.
- v0.0.58: Slowdown is now a speed multiplier rather than divider.
- v0.0.57: Add **shift+X** for cropping with top and bottom automatically set to 0 and video height respectively.
