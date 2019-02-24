# FakeCyton #

The `fake_cyton.py` script creates a "virtual" serial device that 
streams data in the format of a Cyton board. Useful for testing software 
when you don't have a real board.

Samples are loaded from `sample-cyton.csv`. These samples are looped to
provide an endless stream.

## Start ##

Run `fake_cyton.py` to create the serial device. Note the serial port, 
printed immediately after starting. This is the address of your 
imaginary Cyton board:

```sh
~:$ python fake_cyton.py
Connect @ /dev/ttys006
```

## Use with OpenBCI Python ##

To use the fake device with OpenBCI Python's `user.py` script, specify 
the device's port as `--port`:

```
~:$ python user.py --port /dev/ttys006 --add print
------------user.py-------------
Board type: OpenBCI Cyton (v3 API)
Port:  /dev/ttys006
...
```

Once connected, run the `user.py` script's `/start` command to tell the 
fake device to start generating samples:

```
--> /start
---------------------------------
ID: 0.000000
25307.33797637677, 35450.96194159531, -187500.02235174447, -187500.02235174447, -187500.02235174447, -187500.02235174447, -187500.02235174447, -187500.02235174447
0.008, -0.006, 1.01
---------------------------------
...
```

When you're done, use the `/stop` or `/exit` commands to tell the fake
device to stop generating samples:

```
--> /stop
Stopping streaming...
Wait for buffer to flush...
```

## Todo ##

- [ ] Allow alternative .csv file (or directory of .csv files) at command line.
- [ ] Fix "serial.serialutil.SerialException: device reports readiness" exception raised after `/stop` command in OpenBCI Python `user.py` script.
