heuristic-autoload
==================

*heuristic-autoload* uses a simple heuristic based on similarities in the file name to automatically populate the playlist with files related to the currently playing file.


Installation
------------

Download `scripts/heuristic-autoload.lua`, and place it in your `~~scripts` folder (eg. `%AppData%\mpv\scripts` on Windows).


Options
-------

To configure *heuristic-autoload*, download `script-opts/heuristic_autoload.conf` and place it in your `~~script-opts` folder (eg. `%AppData%\mpv\script-opts` on Windows).

Available configuration options:

 - `disabled`: disable the plugin
 - `video`: enable/disable for video files
 - `audio`: enable/disable for audio files
 - `same_type`: only add files with the same media type (audio/video) as the current file to the playlist
 - `pattern_ignore`: comma-separated list of [lua patterns](https://www.lua.org/manual/5.5/manual.html#6.5.1) to ignore for prefix comparison
 - `prefix_min_length`: minimum length for the common prefix


Additionally, the following *mpv* options are respected:

- `video-exts`: file extensions designating video files
- `audio-exts`: file extensions designating audio files


How it works
------------

*heuristic-autoload* will scan the directory of the initially played media file for eligible files (see options `video`,`audio` and `same_type`),
removing patterns according to `pattern_ignore` from the file names of the current file and all eligible files for further comparison.

Afterwards, it will look for common prefixes (ie. same text at the beginning of the filename) between the current file and all other files.
The longest prefix found has any trailing digits removed, and is then used to filter the list of eligible files.

The remaining files will then be sorted (case-insensitive) and added to the playlist at the corresponding positions relative to the current file.


Non-Features
------------

 - Search subdirectories. Only the directory of the currently playing file is searched, subdirectories are ignored.
 - Search for more files after initial playlist creation. Modifying an existing playlist could interfere with playlist creation/modification done by the user.
 - Support images. There are better programs out there for image viewing.

