# RubberDub
Audio track importing and synchronizing tool
Written from scratch using **QtCreator** and the **Qt 6.8.2 open-source library**.
According to Qt licensing terms this program is released under **GNU Lesser General Public License (LGPL) version 3 or later**. Please refer to https://doc.qt.io/qt-6/licensing.html Qt source code can be obtained at https://download.qt.io/archive/qt/6.8/
**Required: FFmpeg installed & inside execution path**
FFmpeg and FFprobe are used via CLI command line interface as backend for multiplexing, audio extraction, recoding etc. and are not parts of this program. Please install FFmpeg 4.4.2 or later following the instructions which can be found at https://www.ffmpeg.org and visit https://www.ffmpeg.org/legal.html for legal considerations.
Any appimage / deb_package / win_package is for evaluation only – it is planned to go open source.
Evaluation package might has been compiled and packed using linuxdeployqt and/or cqtdeployer and/or windeployqt. 

# ! DISCLAIMER !
**If you do not agree with the terms of use or if you don’t understand them you are not allowed to use this program!
This Program is supplied “AS IS” – you are using it on your own risk!
By downloading, compiling, installing and/or using this program you accept that no warranty of any kind can be given. Neither functionality nor data integrity can be guaranteed.
The author cannot guarantee that this program is free of viruses, trojans, spyware or any other harmful software.
The author cannot held responsible for malfunctions, data loss of any kind, corruptionof any other software installed or stored on your system, permanent hardware damage or profit loss.
Only the user is responsible to obey all applicable laws e.g. copyrights etc.**

# SHORT DESCRIPTION
RubberDub should be useful for transplanting and synchronizing audio tracks from low quality sources into high quality movies.
Thatfore it provides a video and an audio waveform preview of both movies.
The main concept is to set syncpoints linking the import audio track to the reference.
The import audio track is converted to 16bit stereo. When linking has finished the import track will be “rubberbanded” between the given syncpoints. Default method is spline resampling. Linear resampling, inserting silence or copying parts of the reference track is also provided.
If only one syncpoint is given, the “import” audio track will be multiplexed “as is” applying the necessary delay.
Work flow is intended to be straightforward and intuitive.
 
## The "Project" tab 
**Create a new project: -> New**
Select HQ-video source containing a - well synchronized - reference audio track
Select AV-file containing the desired audio track
Save the project file. The given “project” name also applies to the resulting “./project.mkv” and the directory containing temporary files “./project_RD”.
 
## The "Muxer" tab 
**Inside "RefSource" and "RubSource"**
Enable/disable audio/subtitle tracks which are to be kept by doubleclicking column "Copy"
If multiple audio tracks are available, select syncronizer sources by doubleclicking column "Sync". These tracks will appear in waveform previews.
Add missing language codes by doubleclicking & editing column "Language."
### "Add Subtitles"
Optionally add text subtitles in .srt .vtt .ass format.
Add missing language codes by doubleclicking & editing column "Language."
Rearrange channel layout by dragging "Description" fields: "video", "audio", then "subs" sequence is recommended
"Ctrl-S" will save your project file.
### Synchronizing subtitles (.srt only, .vtt converts to .srt)
Open the editor by doubleclicking "Modify" - "internal" text subtitles will be demuxed & converted to .srt (needed for syncing).
If umlauts greek etc. appear as strange characters try selecting a different text codec and "Reload external".
Hearing impaired & format tags might be stripped here.
For synchronizing "Load reference" (internal subs have to be demuxed first - see above)
Select corresponding text lines in both subs & "Add link". Hint: doubleclicking a text line helps finding corresponding text line in other subs.
"Synchronize" adjusts all linked text lines & rubberbands (interpolates timing of) all lines between
Additionally "Stretch" & "Shift" by milliseconds is provided.
"Save Modified" or "Ok" will save & close
Info: modified file will be saved as .mod.srt. The original will stay untouched.
 
## The “Syncer” tab
The audio tracks which had been selected inside the "Muxer" are extracted and converted to 16bit stereo. The waveform viewers have a resolution of 10ms per pixel. A 25fps has a frame time of 40ms. Higher precision is not required for the synchronization process.
Clicking inside the waveform viewer will set a sync cursor: from the clicked point the waveform is searched horizontally to the right for the first exceeding amplitude. If there is no such peak, or clicking inside the highlighted area, the cursor is set at the clicked point. Hint: is is wise to set cursors to noises - not to speech.
If both cursors are visible, the time difference "Diff:" is shown. Clicking "SetSync" centers both waveviews and creates an entry into the synclist. Clicking a synclist entry will position both movies to this point.
The "-Strategy-" dropdown list specifies the behavior from the highlighted syncpoint up to the next one. Default is "spline resampling".
Doubleclicking a synclist entry will delete this syncpoint.
The "Video Framerate"/"Largest Block"/"Keep 1/1" dropdown list selects the behavior beyond the first & the last syncpoint - factor is shown as "Stretch Pre&Post". Don't forget to select it.
"Ctrl-S" will save your project file including the synclist.
 
Switch back to the "Muxer" tab & click "Run Muxer"

# Donations welcome via PayPal
marsoupilamis@yahoo.gr

# Current restrictions
Imported audio tracks will be converted to stereo 16bit integer for processing and recoded to ac3
Text subtitles will be converted to .srt for editing if possible – same for time stretching if content of the “rubber” file.

# History & changelog
1.0 1st release / Dec.2025
