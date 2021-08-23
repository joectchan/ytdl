![linters](https://github.com/nth10sd/ytdl/workflows/linters/badge.svg)

# ytdl

Download [Termux](https://f-droid.org/en/packages/com.termux/) from F-Droid. Note that a rooted device is **not** necessary.


Optionally, download [Termux:API](https://f-droid.org/packages/com.termux.api/) to provide `termux-media-player`, and other command you may want to use. Or download play-audio [link](https://github.com/termux/play-audio)
    

**\[Important\]** Give Termux permissions to access storage, if access has not been previously granted:

`termux-setup-storage`

Run the script:

`curl -L --proto '=https' --tlsv1.2 -sSf https://git.io/JEqID | bash -s -- REPLACEME`

`REPLACEME` must be changed to the name of another forked repo which is also under my github. (`REPLACEME` is not `ytdl` for certain. Please search.)

More optional steps:
Base on [this](https://www.reddit.com/r/termux/comments/gwfs6t/how_to_listen_to_music_with_playaudio/)
`pip install cplay-ng` to install `cplay-ng` which is a text-base ui to select files. It tries to use `mpv` player by default. We need to override this. I override it by editing the script file directly.

The reddit post mentioned `/data/data/com.termux/files/usr/lib/python3.8/site-packages/cplay/cplay.py`. Change python3.8 with the actual python version. Use `nano` to edit that file. Search for the phrase `mpv` using ctrl-w. That should bring you to [here](https://github.com/xi/cplay-ng/blob/0247517cee4842b97b997170951ce92344731315/cplay.py#L169)

This is a python list showing the command line to invoke `mpv`. You can comment out this list and insert your own python list to invoke `play-audio` or `termux-media-player`. For examle, I replace
```
            [
                'mpv',
                '--audio-display=no',
                '--start=%i' % self.position,
                '--volume=100',
                '--replaygain=track',
                self.path,
            ],
```
with
```
['play-audio', self.path],
```
for `play-audio`. Make sure indentation matches the surrounding code. (Python!)
