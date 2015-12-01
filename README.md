# dl-tools

Small scripts to download videos and subtitles.

## Usage

### Download videos from put.io

``` sh
$ putio-videos | dl | dl-watch
```

* `putio-videos` will list any videos that are in [put.io](https://put.io) but
  not in your local filesystem.
* `dl` will fire up [axel](http://axel.alioth.debian.org) to download these
  files.
* `dl-watch` is an optional OS X only script that will show a Notification
  Center notification when a file finishes downloading.

### Find and download subtitles

``` sh
$ sub-less | sub-search | sub-dl
```

* `sub-less` will list any local video files that don't have a matching subtitle
  file (i.e. a file with the same name as the video but an `.srt` extension).
* `sub-search` will search OpenSubtitles for subtitles to any videos passed to
  it. If you want to specify a different language for the subtitles, pass it in
  the command line with the `--lang` argument. For example, for Spanish:

  ``` sh
  $ sub-less | sub-search --lang spa | sub-dl
  ```

  The language can be either a single or a comma separated list of [ISO 639-2][]
  codes. If a list is passed, the first match in _any_ of the given languages
  will be selected.
* `sub-dl` will download the subtitles and place them next to the video file
  with the same name (but the `.srt` extension).

[ISO 639-2]: https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes

### Sort videos into subdirectories

```
$ vid-sort ~/Downloads ~/Media
```

This will create a directory structure in `$2` (`~/Media` in the example) with
all the video / subtitle files found in `$1` (`~/Downloads` in the example).

For example, if you downloaded The Matrix, The Usual Suspects, and Fargo S02E06
along with its respective subtitles, and then run this script, you'll get
something like this:

```
~/Media
|_ Movies
|  |_ The Matrix
|  |  |_ The.Matrix.1999.1080p.BrRip.x264.YIFY.mp4
|  |  |_ The.Matrix.1999.1080p.BrRip.x264.YIFY.srt
|  |_ The Usual Suspects
|     |_ The.Usual.Suspects.1995.m720p.mkv
|     |_ The.Usual.Suspects.1995.m720p.srt
|_ Series
   |_ Fargo
      |_ Season 2
         |_ fargo.s02e06.720p.hdtv.x264.fleet[rartv].mkv
         |_ fargo.s02e06.720p.hdtv.x264.fleet[rartv].srt
```

I then just rsync this directory into my NAS and add update my
[Kodi](http://kodi.tv) library.

## Install

Just clone somewhere and add the `bin` directory to your `PATH`. You'll need the
following for running some of the scripts:

* `jq`
* `axel`
* A recent-ish version of ruby (2.0 or newer).

The scripts use the GNU version of some tools, so it might not work with the BSD
version of them.

## License

The code is released under the MIT license. See the attached
[LICENSE](./LICENSE) for details.

And just to be clear, I'm not responsible for what you do with this. If you use
these tools for illegal stuff, that's on you, not me.
