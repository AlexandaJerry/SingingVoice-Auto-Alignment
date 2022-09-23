# Split audio according to information in srt-file.

To be able to train the speech-recognition engine <a href='https://github.com/mozilla/DeepSpeech'> DeepSpeech</a>, audio-files should not be longer than 10s.
Therefore, this repo offers the possibility to easily split audio files based on the subtitle-info in srt-files and prepare corresponding transcript files.


**Table of Contents**

- [Split audio according to information in srt-file.](#split-audio-according-to-information-in-srt-file)
  - [Prerequisites](#prerequisites)
  - [Walk-through](#walk-through)
    - [Example Files](#example-files)
    - [Modules](#modules)
  - [About this project:](#about-this-project)


## Prerequisites

* [Python 3.6](https://www.python.org/)
* [librosa](https://librosa.github.io/librosa/)
* [SoundFile](https://pypi.org/project/SoundFile/)
* [pydub](https://pypi.org/project/pydub/)
* [moviepy](https://zulko.github.io/moviepy/)


## Walk-through

<b>This section will explain what the modules and script do in order to provide a deeper understanding of the individual steps and facilitate modification</b>

<b>First:</b> Create a folder called "srt_files" where you store your srt_files and a folder "audio" where you store your audio-files (wmv or mp4).

### Example Files

<p> Check the folder Example Files to see how the information is extracted from an srt-file to a csv-file.</p>

### Modules
<p><b>- change_encoding: </b>The encoding of srt-files is changed from utf-8 to utf-8-sig.</p>
<p><b>- convert_srt_to_csv: </b>Start time, end-time and subtitle are extracted from the srt-files and stored in a csv. In preparation for audio-splitting, a column id is generated from the filename with the addition of a unique number.</p>
<p><b>- pre_process_audio: </b>Audio is processed to meet DeepSpeechs requirements of sample-rate 16kHz and bit-rate 16. I revised this part to 44.1KHz to meet the sampling rate of original songs.</p>
<p><b>- split_files: </b>The audio files are splitted according to the start- and end-times in the csv files. The splitted audio-files are named after the id given in the transcripts.</p>
<p><b>- create_DS_csv: </b>This module creates a csv with filepaths and filesizes of all processed audio files. </p>
<p><b>- merge_csv: </b>Merge_csv joins all seperate csv-files.</p>
<p><b>- merge_transcripts_and_wav_files: </b>This module matches the transcripts to the available audio files.</p>
<p><b>- clean_unwanted_characters: </b>Unwanted characters are removed. After cleaning the transcripts, the text is extracted and saved in a txt file which can be used for training the language model.</p>

<br>
<p><b>Estimation on execution time: </b>full processing with all above modules took 1h 11m for an audio-dataset of 12GB.</p>

## About this project:

<p>This importer was created as part of the Master Thesis "Automatic Speech Recognition for Swiss German using Deep Neural Networks" for the degree Master of Business Innovation at the University of St. Gallen by Tobias Rordorf. In case of questions please feel free to contact me through <a href='https://www.linkedin.com/in/tobiasrordorf/'>LinkedIn</a>.

Revised by Alexanda Jerry to make it suitable for auto-alignment of Mandarin Songs. The output of split wav files and transciptions would be sent to MFA forced alignment.