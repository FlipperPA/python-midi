# python-midi

This package is a Python 3 only rewrite of [Mark C. Wirt's](https://github.com/MarkCWirt) excellent MIDIUtil.

## Introduction

MIDIUtil is a pure Python library that allows one to write multi-track
Musical Instrument Digital Interface (MIDI) files from within Python
programs (both format 1 and format 2 files are now supported).
It is object-oriented and allows one to create and write these
files with a minimum of fuss.

MIDIUtil isn't a full implementation of the MIDI specification. The actual
specification is a large, sprawling document which has organically grown
over the course of decades. I have selectively implemented some of the
more useful and common aspects of the specification. The choices have
been somewhat idiosyncratic; I largely implemented what I needed. When
I decided that it could be of use to other people I fleshed it out a bit,
but there are still things missing. Regardless, the code is fairly easy to
understand and well structured. Additions can be made to the library by
anyone with a good working knowledge of the MIDI file format and a good,
working knowledge of Python. Documentation for extending the library
is provided.

## Installation

Eventually, you'll be able to install this from PyPI with something like `pip install midi`. But for now, do a `git clone https://github.com/FlipperPA/python-midi.git`, and `pip install python-midi`.

## Quick Start

In this example we'll create a one track MIDI File, assign a tempo to the track, and write a C-Major scale. Then we write it to disk.

```python
from midi import MIDIFile

degrees = [60, 62, 64, 65, 67, 69, 71, 72]  # MIDI note number
track = 0
channel = 0
time = 0  # In beats
duration = 1  # In beats
tempo = 60  # In BPM
volume = 100  # 0-127, as per the MIDI standard

midi_file = MIDIFile(1)  # One track
midi_file.add_tempo(track, time, tempo)

for i, pitch in enumerate(degrees):
    midi_file.add_note(track, channel, pitch, time + i, duration, volume)

with open("major-scale.mid", "wb") as output_file:
    midi_file.write_file(output_file)
```

There are several additional event types that can be added and there are
various options available for creating the MIDIFile object, but the above
is sufficient to begin using the library and creating note sequences.

The above code is found in machine-readable form in the examples directory.
A detailed class reference and documentation describing how to extend
the library is provided in the documentation directory.

Have fun!

## Contributors

* Timothy Allen: author of Python 3 re-write.
* Mark C. Wirt: the original author of the excellent MIDIUtil package.

Feedback, bug fixes, and suggestions:

* Bram de Jong
* Mike Reeves-McMillan
* Egg Syntax
* Nils Gey
* Francis G.
* cclauss (Code formating cleanup and PEP-8 stuff, which I'm not good at following).
* Philippe-Adrien Nousse (Adphi) for the pitch bend implementation.
* meteorsw (https://github.com/meteorsw) for major restructuring and clean-up
  of code.
