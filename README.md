# Python CAN bus monitor

This script allows you to read live data from a CAN bus or offline CAN data from a file and display it in an easy-to-read table.

## Live

It's primarily meant to be used in conjunction with an Arduino and a CAN bus shield. You'll need this [Arduino sketch](https://github.com/alexandreblin/arduino-can-reader.git) to make it work.

You can also use any serial device capable of reading a CAN bus. It expects data in this format:

    FRAME:ID=X:LEN=Y:ZZ:ZZ:ZZ:ZZ:ZZ:ZZ:ZZ:ZZ

where `X` is the CAN frame ID (decimal), `Y` is the number of bytes in the frame, and `ZZ:ZZ...` are the actual bytes (in hex).

## Offline

You can also read CAN frames from a text file.
This is designed to read log files generated by `candump` (from [can-utils](https://github.com/linux-can/can-utils/blob/master/README.md)) with `-l` option.

The log must contain one message per line.
Messages must be stored in this format:

    [(<timestamp>)] <interface> <frame_id>#<frame_data>

where frame id and data are in hex (upper case letters).

Example:

    (1499430972.167877) can0 12E#C77FFE7FD0FFFF00

## Usage
Install the dependencies (preferably in a virtualenv)

    pip install -e .

Launch the script

    canmonitor <serial device> <baud rate>

Or

    canmonitor -f <file name>

Press Q at any time to exit the script.

## Example

    canmonitor /dev/tty.usbmodem1451 115200
    canmonitor -f can_log.log
    
![Screenshot](http://i.imgur.com/1nqCQKz.png)

