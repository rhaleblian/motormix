# RX

## faders

    z b0 0z vv

where *z* is the 0-based zone for 1-8 and *vv* is the fader
value 0-127.  all faders emit

    b0 0f 0z

on touch and release.

## buttons
all buttons only emit

    z b0 0f 0z

on touch and release.

button zones:

    10  0 1 2 3 4 5 6 7  11
    8                     9

## "user is touching" (UIT) sensor

there is a general "control was touched/released" message

    b0 0f 0z

mapping faders to Live requires tossing these messages since
as the last message they will mask the true controller identity.  use MidiPipe to 
toss CC#15 events and have live take input from MidiPipe.


# TX

finding the polling message is essential since buttons do not send state, only a touch or release message for that zone.  there would need to be a TX message that gets the button on/off for a zone.

the UIT message might be used by the CM driver
to disable automation.


# Is the Mackie HUI protocol being used?

difference: no "fader touched" vs "fader released" message.
