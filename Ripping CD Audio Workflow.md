---
title: My Ripping CD Audio Workflow
permalink: index.html
---

Ripping CD Audio Workflow
=========================

My humble *"bit perfect"* ripping setup & configuration.

Table of content
================

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=4 orderedList=true} -->
<!-- code_chunk_output -->

1. [Intro](#intro)
2. [Tools & Settings](#tools--settings)
    1. [Exact Audio Copy (EAC)](#exact-audio-copy-eac)
        1. [Settings](#settings)
            1. [EAC Options](#eac-options)
            2. [Drive Options](#drive-options)
            3. [Compression Options](#compression-options)
            4. [Metadata Options](#metadata-options)
        2. [Rip process](#rip-process)
    2. [CUETools](#cuetools)
        1. [Settings](#settings-1)
        2. [Verifying Process](#verifying-process)
    3. [MusicBrainz Picard](#musicbrainz-picard)
        1. [Setup & requirements](#setup--requirements)
        2. [Tag & Move to library Process](#tag--move-to-library-process)
3. [Convert to M4A/AAC for mobile usage](#convert-to-m4aaac-for-mobile-usage)
    1. [fre:ac](#freac)
        1. [fre:ac Settings](#freac-settings)
            1. [Encoders](#encoders)
            2. [Output files](#output-files)
            3. [Verification](#verification)
            4. [Metadata -> Album Art](#metadata---album-art)
    2. [MP3Tag](#mp3tag)
        1. [Add an action to adjust cover size](#add-an-action-to-adjust-cover-size)
        2. [Process](#process)
    3. [fatsort](#fatsort)
4. [Wine](#wine)
5. [Sources](#sources)

<!-- /code_chunk_output -->

# Intro

While using exclusively Linux I wanted to keep logs from EAC Rips so I included a basic script to create the Wine prefix I use at the end of this guide.

Global process:
- EAC rip securely CD Audio
- CUETools verify the generated FLAC files (even if it has been done with EAC, double check doesn't hurt)
- MusicBrainz Picard tags and moves audio files to master library

For usage on various devices that does not support FLAC, I convert the desired albums to M4A/AAC:
- Select a bunch of albums from my library and convert them with fre:ac which also adds the cover to every converted files
- Use Mp3Tag to resize covers (better player compat and saves some space)


# Tools & Settings

## Exact Audio Copy (EAC)

### Settings

Avoid to run the wizard and just follow any well documented various "perfect-bit" recommendations (check [Sources](#sources)).

Here are my settings:

#### EAC Options

![alt text](images/image-14.png)

![alt text](images/image-15.png)

![alt text](images/image-16.png)

![alt text](images/image-17.png)

![alt text](images/image-18.png)

![alt text](images/image-19.png)

![alt text](images/image-20.png)

![alt text](images/image-21.png)

![alt text](images/image-22.png)

![alt text](images/image-23.png)

#### Drive Options

![alt text](images/image-24.png)

![alt text](images/image-25.png)

![alt text](images/image-26.png)

**Offsets should be automatically setup during the AccuRip test.**

![alt text](images/image-27.png)

#### Compression Options

![alt text](images/image-28.png)

Additional command-line options:
`-8 -V -T "ARTIST=%artist%" -T "TITLE=%title%" -T "ALBUM=%albumtitle%" -T "DATE=%year%" -T "TRACKNUMBER=%tracknr%" -T "GENRE=%genre%" -T "PERFORMER=%albuminterpret%" -T "COMPOSER=%composer%" %haslyrics%"tag-from-file=LYRICS="%lyricsfile%"%haslyrics% -T "ALBUMARTIST=%albumartist%" -T "DISCNUMBER=%cdnumber%" -T "TOTALDISCS=%totalcds%" -T "TOTALTRACKS=%numtracks%" -T "COMMENT=%comment%" %source% -o %dest%`

![alt text](images/image-29.png)

![alt text](images/image-30.png)

![alt text](images/image-31.png)

#### Metadata Options

Configure to fit your needs as you wish.

### Rip process

- detect gaps

![alt text](images/image-32.png)

- create CUE file

![alt text](images/image-33.png)

- test & compress

![alt text](images/image-34.png)

> Note:
> If you don't want to read logs, you can upload them here [Cambia](https://logs.musichoarders.xyz/) to get a visual summary of your RIPs.

## CUETools

### Settings

- write all accurip tags to files
- Verify AccuRip (write ac tags and log file)

![alt text](images/image-13.png)

### Verifying Process

- Select `Verify` and `only if rip log present`.
- Open the directory containing the `.cue` file and `.flac`, select the `.cue` file
- Click `Go`

![alt text](images/image-35.png)

## MusicBrainz Picard

### Setup & requirements

First, install the file naming script:
- Download the script [Salty's MusicBrainz Picard Naming Script](https://musichoarders.xyz/assets/doc/salty-picard-naming-script.txt)
- Install the script in MusicBrainz Picard

![alt text](images/image-3.png)

Open options (Menu: Options -> Options...)

1) General
  - Login your MusicBrainz account
2) Covert Art

![alt text](images/image.png)

4) Covert Art Archive
Select the images you want to download for each release. I choose all.

![alt text](images/image-1.png)

5) File Naming
- `Destination directory`: choose your output directory
- Select the file naming script previously installed

![alt text](images/image-4.png)

6) Fingerprinting

![alt text](images/image-2.png)

7) Plugins
- AccousticBrainz

![alt text](images/image-5.png)

- Last.fm

![alt text](images/image-6.png)

- ReplayGain v2.0
Install ReplayGain binaries from here https://github.com/complexlogic/rsgain

![alt text](images/image-7.png)

### Tag & Move to library Process

- Add files
- Cluster

![alt text](images/image-9.png)

- Right click the cluster (album) choose `PLugins -> Calculate Cluster ReplayGain as Album...`

![alt text](images/image-8.png)

- Match release
  - Ideally use
![alt text](images/image-10.png)
  - Alternatively use `Lookup` or `Scan`
![alt text](images/image-11.png)

- Update tags manually if needed
- Save files
![alt text](images/image-12.png)

# Convert to M4A/AAC for mobile usage

## fre:ac

### fre:ac Settings

#### Encoders

![alt text](images/image-40.png)

##### FDK-AAC Encoder Settings

- use 192Kbps per channel (total>320Kbps but should work on every players)
- maximum low pass filter (20KHz)

![alt text](images/image-41.png)

#### Output files

![alt text](images/image-42.png)

Filename pattern, one of:
- `<albumartist> - <album>/<disc>-<track> - <artist> - <title>`
- `<albumartist>/<album>/<disc>-<track> - <title>`

#### Verification

![alt text](images/image-43.png)

Disable all verification, we are doing loosy encoding so nevermind.

#### Metadata -> Album Art

![alt text](images/image-44.png)

Make sure to check `Restrict file names` and enter `front` as name so only the first cover file matching `front.png` or `front.jpg` will be embedded in the encoded file.

If you enter a file pattern with jokers (like `front*`) fre:ac will embed ALL files matching the pattern, this is useless and will make the encoded files pretty heavy.

Also set `File size limit` to `unlimited`.

## MP3Tag

### Add an action to adjust cover size

Follow these steps:

![alt text](images/image-51.png)

![alt text](images/image-50.png)

![alt text](images/image-52.png)

![alt text](images/image-53.png)

![alt text](images/image-54.png)

![alt text](images/image-55.png)

Select Jpeg format and 300x300 pixels size for maximum compatibility.

And now you have to confirm everything by clicking `OK`

### Process

- Add directories where are your M4A/MP4/MP3 files (usualy output directory of `fre:ac`)
- Select all files
- Right click the selection and apply the `Adjust Cover` action
![alt text](images/image-56.png)

## fatsort

Some player are really dumb and either sort tracks based on title tag or even weirder some sort tracks based on file creation time. For the last I use `fatsort`.

Insert the USB drive, make sure the USB partition is not mounted and run:
`fatsort /dev/sda1`

# Wine

Script to automate wine prefix creation compatible with EAC & CUETools.

```shell
eac_install=$HOME/Downloads/eac-1.8.exe
export WINEPREFIX=$HOME/wineprefixes/eac64
export WINEARCH=win64
mkdir -p "$WINEPREFIX"
# Set up the prefix if missing.
if [ ! -d "${WINEPREFIX}/.wine" ]; then
  echo "Setting up a prefix for EAC/CUETools. Stand by!"
  WINEDLLOVERRIDES="mscoree=" wine wineboot
  winetricks -q dotnet20 dotnet40 dotnet48 vcrun2008 vcrun2022
fi
wine $eac_install
cd $WINEPREFIX/drive_c/Program\ Files\ \(x86\)/Exact\ Audio\ Copy/ && regsvr32 sql*
```

# Sources

- [Exact Audio Copy](https://www.exactaudiocopy.de/en/)
- [EAC Setup & Config](https://web.archive.org/web/2/https://flemmingss.com/perfect-cd-ripping-to-flac-with-exact-audio-copy/)
- [Guides from HydrogenAudio](https://wiki.hydrogenaudio.org/index.php?title=Category:Guides)
- [Music Hoarders](https://musichoarders.xyz/)
- [Cambia Logs Analyzer](https://logs.musichoarders.xyz/)

