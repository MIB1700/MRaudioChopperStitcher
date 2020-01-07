# MRaudioChopperStitcher

This repository holds the scripts used to create the piece I. Catalogue: Start, II. Catalogue: Endings, III. Catalogue: Sliding, which can be found here:

https://youtu.be/jSdTxsaH4fw

https://youtu.be/pJbKEQ3r4BA

https://youtu.be/k-lPCxh8vSQ


## Scripts:
There are 4 seperate scripts that need to be run from the terminal:

1. MRaudioChopper
2. MRaudioChopperSliding
3. MRaudioStitcher
4. MRaudioStitcherSliding

You need to have **ffmpeg** (https://ffmpeg.org) installed for the scripts to work. 
The scripts are pretty basic and dumb. No serious error checking or input checking is done, therefor the following rules should be observed:

- The folder in which the script is run must only contain audio files
- Create 3 subfolders called:
  * shortStart
  * shortEnd
  * shortSliding

### MRaudioChopper

`cd folder/with/sound/files/` to the folder containing the sound files...

Run `MRaudioChopper arg` where arg is an integer value that is the amount in seconds the audio file
is chopped to.
A *positive* value trims the file from the beginning and expects a folder named */shortStart*
in the `pwd`.

A *negative* value trims it from the end and expects a folder named /shortEnd in the `pwd`.

**The resulting file is transcoded to a .aiff at 44.1kHz**

**no checks** are made if the files in the directory are actually soundfiles...
**no checks** are made if */shortStart* exist


### MRaudioChopperSliding

`cd folder/with/sound/files/` to the folder containing the sound files

Run `MRaudioChopperSliding` (no arguments)


The script takes into account the number of files in the directory to decide on the starting
point of the trim -> each file will start a bit further into the file therefore sliding through
all files by the end. This means that for the first couple of files mostly the beginning of the files will be heard
and towards the last files only the ending of the files.

The duration of the files is `30sec + 1%` of the total length of the current file.

The trimmed version is saved to */shortSliding*

**The resulting file is transcoded to a .aiff at 44.1kHz**

**no checks** are made if the files in the directory are actually soundfiles...
**no checks** are made if */shortSliding* exist


### MRaudioStitcher

`cd` to either */short[Start/End]*

Run `MRaudioStitcher` (no arguments)

Decides on a random **cross-fade** based on the length of the current file.

Final file is named **output.aiff** and should be moved and renamed before running this script again or it will be overwritten!!

### MRaudioStitcherSliding

`cd` to */shortSliding*

Run `MRaudioStitcherSliding arg` where arg is a positive integer value that is subtracted from the total length of the file, in seconds, and used as the **cross-fade** time

Final file is named **output.aiff** and should be moved and renamed before running this script again or it will be overwritten!!

## Typical usage:

    cd /folder/with/audio
    MRaudioChopper 20
    cd /folder/with/audio/shortStart
    MRaudioStitcher

or

    cd /folder/with/audio
    MRaudioChopper -20 
    cd /folder/with/audio/shortEnd
    MRaudioStitcher

or 
  
    cd /folder/with/audio
    MRaudioChopperSliding 
    cd /folder/with/audio/shortSliding
    MRaudioStitcherSliding 4
    
It is of course also possible to run `MRaudioStitcherSliding` on */short[Start/End]*:

    cd /folder/with/audio
    MRaudioChopper -20 
    cd /folder/with/audio/shortEnd
    MRaudioStitcherSliding 2
    
    
## If you use or alter the code, please share your results with me!
