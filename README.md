# bformdec2

## Compile

Linux:

g++ -O2 -shared -o /usr/lib64/csound/plugins64/bformdec2.so -fPIC bformdec2.cpp -I /usr/local/include/csound/

OSX:

g++ -O2 -dynamiclib -o /Library/Frameworks/CsoundLib64.framework/Versions/6.0/Resources/Opcodes64/bformdec2.dylib bformdec2.cpp -DUSE_DOUBLE -I/Library/Frameworks/CsoundLib64.framework/Headers


## Sintax and usage

aout[] bformdec2 isetup, abform[], [idecoder, idistance, ifreq, imix]

### Initialization

Note that as bformdec1 horizontal angles are measured anticlockwise in this description.

isetup –- loudspeaker setup. There are five supported setups:

1. Stereo - L(90), R(-90); this is an M+S style stereo decode.
2.	Quad - FL(45), BL(135), BR(-135), FR(-45). This is a first-order `in-phase' decode.
3.	5.0 - L(30),R(-30),C(0),BL(110),BR(-110). Note that many people do not actually use the angles above for their speaker arrays and a good decode for DVD etc can be achieved using the Quad configuration to feed L, R, BL and BR (leaving C silent).
4.	Octagon - FFL(22.5),FLL(67.5),BLL(112.5),BBL(157.5),BBR(-157.5),BRR(-112.5),FRR(-67.5),FFR(-22.5). This is a first-, second- or third-order `in-phase' decode, depending on the number of input channels.
5.	Cube - FLD(45,-35.26),FLU(45,35.26),BLD(135,-35.26),BLU(135,35.26),BRD(-135,-35.26),BRU(-135,35.26),FRD(-45,-35.26),FRU(-45,35.26). This is a first-order `in-phase' decode.

idecoder -- select the type of decoder

0. Mix decoder (velocity and energy decoders using dual-band splitting).
1. Velocity decoder.
2. Energy decoder.

idistance -- select the distance (meters) to the loudspeaker (radius if regular configuration)
By default, the distance is set to 1 meter.

ifreq - frequency cut (Hz) of the band splitting filter (only importante if idecoder=0)
By default the frequency is set to 400 Hz.

imix - type of mix of the velocity and energy decoders' outputs
0. Energy
1. RMS
2. Amplitude

### Performance
abform[] -- input signal array in the B format.
aout[] -– loudspeaker specific output signals.

### Example
See test/test_binaural.csd