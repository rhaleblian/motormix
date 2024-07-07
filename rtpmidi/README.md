The strategy here is to use an SBC to transmit CMM MIDI output over the network for other devices to receive and use.

@rhaleblian uses a Pi 4 running RaspiOS and a MIDI 5-pin-to-USB converter between the CMM and the Pi.  Converters are for sale on eBay and Amazon.

Install an rtpMIDI daemon on the Pi.
https://github.com/davidmoreno/rtpmidid .

The converter/CMM will appear as an ALSA device.  Get its device ID.

    ray@zaphod:~ $ aconnect -l
    client 0: 'System' [type=kernel]
        0 'Timer           '
        1 'Announce        '
    client 14: 'Midi Through' [type=kernel]
        0 'Midi Through Port-0'
    client 28: 'CH345' [type=kernel,card=3]
        0 'CH345 MIDI 1    '
    client 128: 'rtpmidid' [type=user,pid=4689]
        0 'Network Export  '
        1 'diamond         '
        7 'carbon          '
    
Connect it to the rtpMIDI session:

    ray@zaphod:~ $ aconnect 28:0 128:0

yielding

    ray@zaphod:~ $ aconnect -l
    client 0: 'System' [type=kernel]
        0 'Timer           '
        1 'Announce        '
    client 14: 'Midi Through' [type=kernel]
        0 'Midi Through Port-0'
    client 28: 'CH345' [type=kernel,card=3]
        0 'CH345 MIDI 1    '
            Connecting To: 128:0
    client 128: 'rtpmidid' [type=user,pid=4689]
        0 'Network Export  '
            Connected From: 28:0
        1 'diamond         '
        7 'carbon          '

Set up a receiver using *Audio MIDI Setup* on macOS, or by installing rtpMIDI on Windows
https://www.tobias-erichsen.de/software/rtpmidi.html

If on Windows, strong recommendation to install Bonjour for Windows.  iTunes contains it.  Session dicovery never worked right for @rhaleblian until he did this.

In the Network MIDI dialog, connect to the participant in the Directory matching the Pi side (here, `CH345-CH345 MIDI 1`).

Use a MIDI event viewer like MidiView to watch traffic on the local session when you move faders.
