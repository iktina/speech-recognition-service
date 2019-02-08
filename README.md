# Automatic Speech Recognition


## Welcome

The service receives an audio file and uses it as an input for a pre-trained model.

## What’s the point?

The service performs speech recognition using machine learning techniques.
The service receives the audio file in binary format and outputs the text string resulting from audio recognition. 

##  Model details:

The service receives an English-speech WAV audio file and uses it as an input to the advanced Wave2Letter + model, based on a deep convolutional neural network trained in half-precision using a mixture of natural and synthetic data, and outputs the result of the speech sample recognition in form of a text sequence. The model runs on a V100 GPU equipped with tensor cores to provide greater service bandwidth. The scaling factor is 3-4x Services per 1xV100 GPU. The input audio file size is limited to 4Mb, in practice the optimal duration of the processed audio track should be no more than 90 seconds for 320 kbps audio.

## How does it work?

The user must provide the following inputs in order to start the service and get a response:

Inputs:

 -   `endpoint`: asr.naint.tech.
 -   `method`: s2t.
 -   `input_path`: Path to '\*.txt' file containing JSON representation of input argument 'file@data' and its value - path to '\*.wav' input audio file.

Example of input file content:

```
{"file@data": "samples/sample.wav"}
```

You can call the service from SingularityNET CLI (`snet`).

Assuming that you have an open channel (`id: 0`) to this service:

```
$ snet client call 0 0.1 asr.naint.tech:81 s2t samples/sample.txt

Read call params from the file: samples/sample.txt

text: "after a time she heard a little pattering of feet in the distance and she hastily dried her eyes to see what was coming"
```

## What to expect from this service?

Input audio:
samples/sample.wav

Response:
`text: "after a time she heard a little pattering of feet in the distance and she hastily dried her eyes to see what was coming"`
