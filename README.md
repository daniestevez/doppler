# doppler
GNUradio Doppler correction flowgraphs

These flowgraphs require the OOT module https://github.com/wnagele/gr-gpredict-doppler

* gr-doppler.grc *

Used to correct for Doppler before an SDR receiver software such as linrad or any other
that supports input from an ALSA device. This flowgraph simply takes IQ data from ALSA,
computes the Doppler shift from GPredict's radio control frequency and a frequency set
on the flowgraph, corrects for Doppler shift in a phase continuous manner by mixing with
a cosine signal source and then outputs the IQ to another ALSA device.

You have to load the module 'snd-aloop' on Linux and take note of the device number it gets
('cat /proc/asound/cards'). This is used to connect the audio output of gr-doppler to your
SDR software. For instance, if the loop device is number 1, then gr-doppler should output 
to hw:0,0,0 and the SDR software should input from hw:0,1. You must set the correct device
in the flowgraph and in your SDR software.

The flowgraph comes ready to get input on the ALSA device hw:2,0 at 192kHz. This can be used
for the FUNCube Dongle Pro+ (check your device on '/proc/asound/cards' and adjust accordingly).
Other SDR devices supported by GNURadio can be used by modifying the flowgraph.

The centre frequency must also be set in the variable 'freq' in the flowgraph. You have to set
GPredict to the same centre frequency. If using the FUNCube Dongle Pro+, you must also use QTHid
to set the centre frequency in the dongle, because the flowgraph doesn't interface with the dongle's
frequency selection.

Also, adjust the GPredict port on the flowgraph. Port 4534 comes by default.
