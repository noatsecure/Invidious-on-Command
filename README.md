# Invidious on Command
This Python script allows you to browse Invidious, a front-end to YouTube, as well as select and play videos with mpv. It was written in Python 3 and requires no external Python dependencies outside of the standard library. The media player [mpv](https://mpv.io) should also be installed, along with either [youtube-dl](https://youtube-dl.org), or its fork, [yt-dlp](https://github.com/yt-dlp/yt-dlp).

## Commands
There are a number of built-in commands, which are entered into the script the same way search queries are. An exhaustive list of commands and their constraints are shown below:

| Command | Description | Availability |
|---------|:-----------:|--------------|
| `uu`  | Show the usage information | Everywhere except selection mode            |
| `rr`  | Reload the page            | Only when search results/channels are shown |
| `qq`  | Quit                       | Everywhere                                  |
| `.`   | Enter selection mode       | Only when search results/channels are shown |
| `,`   | Exit selection mode        | Only while in selection mode                |
| `]`   | Next page                  | Only when search results/channels are shown |
| `[`   | Previous page              | Only when search results/channels are shown |

## Searching
To browse videos, type your search query into the script to search Invidous. This process involves connecting the Invidious API in order to select an instance and obtain the results. Videos are streamed through their Invidious URL, just as they would normally play in the browser. However, YouTube playlists are streamed through YouTube since Invidious does not support this feature.

## Selecting
Enter selection mode by entering `.`, the period character and exit selection mode by entering the `,` or comma character. In selection mode, you input the index of the video(s) you wish to play. For example:

```Select video index (press ',' to exit): 1```

The above example will play the video with index 1 from the results for the search query `test`. Note that videos are played in the background, so after a selection is made you can select another video or search again.

### Multiple Videos at Once
Additionally, you can load multiple videos at once by separating each video index with a comma:

```Select video index (press ',' to exit): 1, 3, 19, 2```

This will load the videos with the specified indexes all at once. Note that the first video will play while the rest are loaded as paused using mpv's '--pause' flag.

### Creating a Playlist
You can create your own playlists with the displayed results using the following syntax:

```Select video index (press ',' to exit): 1 < 3 < 19 < 2```

This will create a file "/tmp/playlist.txt" and will play the videos in the order they were entered. The above example will play video 1, 3, 19, and 2 in that order. After the playlist has completed, or if you exit, the "/tmp/playlist.txt" file is deleted. Note that while the playlist is running the script will not allow any input.

### Channels
YouTube channels are shown in the results and can be selected in the same manner as a video index. Upon selecting a channel, another set of results will be shown from the channel's page, allowing you to select any of the videos shown.

## Pages
This script allows you to browse multiple pages of results. Enter the `]` or right bracket character to move forward one page, or enter the `[` (left bracket character) to move back to the previous page.

## Reload
Sometimes you will search and there will be no results. In this instance you can enter the `rr` string to reload the results. Note that this script will only show what your particular Invidious shows, so any issues will need to be fixed on the instance's end.
