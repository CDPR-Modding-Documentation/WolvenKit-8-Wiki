---
description: Extracting and playing from archives
---

# Video and audio files (CLI)

## Archives

Required files are contained within these archives

* audio\_1\_general.archive
* audio\_2\_soundbanks.archive
* basegame\_5\_video.archive
* lang\_en\_voice.archive

## Video files

Using [the tool](https://github.com/WolvenKit/WolvenKit-nightly-releases/releases/latest), decompress **basegame\_5\_video.archive** located at: `<gamedir>\Cyberpunk 2077\archive\pc\content`.

```
WolvenKit.Cli.exe unbundle -p "<gamedir>\Cyberpunk 2077\archive\pc\content\<nameofarchive>" -o "<outputfolder>"
```

Once extracted, they can be viewed via [RADTools](http://www.radgametools.com/bnkdown.htm) as Bink Videos and converted to other formats.

## Audio files

[ww2ogg](https://github.com/hcs64/ww2ogg) can be used to convert decompressed archive audio to .ogg through command line, as well as [Revorb](https://cloudflare-ipfs.com/ipfs/QmVgjfU7qgPEtANatrfh7VQJby9t1ojrTbN7X8Ei4djF4e/revorb.exe) (both of these tools have Linux versions that can be found [here](https://www.nexusmods.com/witcher3/mods/6265)) to get smaller and cleaner files that can be played via other media players such as VLC. [ffmpeg](https://ffmpeg.org/download.html) can be used for more convenient playback.

To execute conversion:\
`.\ww2ogg.exe "<!AudioFilePath!>.wem" --pcb packed_codebooks_aoTuV_603.bin`\
_**The argument --pcb is important so as not to return gibberish audio files.**_

It is also recommended to turn down the volume upon playback.

Playback through ffmpeg:\
`ffplay.exe <!AudioFilePath!>.ogg`\
\
[Foobar2000](http://www.foobar2000.org) can also be used along with its [vgmstream](https://www.foobar2000.org/components/view/foo\_input\_vgmstream) plugin.
