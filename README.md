# lib8relind

This is the python library to control the [8-RELAYS Stackable Card for Raspberry Pi](https://sequentmicrosystems.com/product/raspberry-pi-relays-stackable-card/).

## Preinstall

Raspberry Pi I2C Config

```bash
# checking i2c enabled.
~$ i2cdetect -y 1
# enable i2c
~$ sudo raspi-config
3 Interface Options -> I5 I2C -> Yes

OR 

~$ sudo bash -c 'echo "dpparam=i2c_arm=on" >> /boot/config.txt'
# effectuate
~$ sudo reboot
```

## Install

For python3.x:
```bash
~$ sudo apt-get update
~$ sudo apt-get install build-essential python-pip python-dev python-smbus git
~$ sudo pip install lib8relind==0.1
```

## Usage

Now you can import the lib8relind library and use its functions. To test, read relays status from the board with stack level 1:

```bash
~$ python
Python 3.9.2 (default, Mar 12 2021, 04:06:34)
[GCC 4.9.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import lib8relind
>>> lib8relind.get_all(1)
0
>>>
```

## Functions

### set(stack, relay, value)
Set one relay state.

stack - stack level of the 8-Relay card (selectable from address jumpers [0..7])

relay - relay number (id) [1..8]

value - relay state 1: turn ON, 0: turn OFF[0..1]

example:
```python
>>> lib8relind.set(1, 1, 1)
```


### set_all(stack, value)
Set all relays state.

stack - stack level of the 8-Relay card (selectable from address jumpers [0..7])

value - 8 bit value of all relays (ex: 255: turn on all relays, 0: turn off all relays, 1:turn on relay #1 and off the rest)

example:
```python
>>> lib8relind.set_all(1, 255)
```

### get(stack, relay)
Get one relay state.

stack - stack level of the 8-Relay card (selectable from address jumpers [0..7])

relay - relay number (id) [1..8]

return 0 == relay off; 1 - relay on

example:
```python
>>> lib8relind.get(1, 1)
```

### get_all(stack)
Return the state of all relays.

stack - stack level of the 8-Relay card (selectable from address jumpers [0..7])

return - [0..255]

example:
```python
>>> lib8relind.get_all(1)
```
