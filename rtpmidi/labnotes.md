## Is the Mackie HUI protocol being used?

there is a "fader release" message

    b0 0f 0z

where z is the zone as per HUI.
this is also the "fader touched" message, however.

mapping faders to Live requires tossing these messages since
they will mask the true controller identity.  use MidiPipe to 
toss CC#15 events and have live take input from MidiPipe.
