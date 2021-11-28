# Python GetKey
> A powerful beta __keypress detection module__

## Quick Start

```python
from getkey import getkey, keys

key = getkey()

if key == keys.UP:
  ...  # Handle the UP key
elif key == keys.DOWN:
  ...  # Handle the DOWN key
elif key == 'a':
  ...  # Handle the `a` key
elif key == 'Y':
  ...  # Handle `shift-y`
else:
  # Handle other text characters
  buffer += key
  print(buffer)
  ```
  
## Philosophy
Keys will be returned as strings representing the received key codes, however as some keys may have multiple possible codes on a platform, the key code will be canonicalized so you can test ```key == keys.UP``` instead of key in keys.UP. This means non-control keys will be returned just as the text they represent, and you can just as easily test ```key == 'a'``` to see if the user pressed a.
>
In addition, by default we will throw KeyboardInterrupt for Ctrl-C which would otherwise be suppressed. However, it is possible to disable this if you wish:
```python
from getkey import plaform

my_platform = platform(interrupts={})
my_getkey = my_platform.getkey
```
Now ```my_getkey``` will be a function returning keys that won't throw on Ctrl-C. __Warning!__ This may make it difficult to exit a running script.

# Documentation

## Installation
```python
pip install getkey
```
```python
pip3 install getkey
```
The getkey library is compatible with python 3.2 to 3.10+ (tested and worked).
>
## Usage
```python
from getkey import getkey, keys

key = getkey()

if key == keys.UP:
  ...  # Handle the UP key
elif key == keys.DOWN:
  ...  # Handle the DOWN key
... # Handle all other desired control keys
else:  # Handle text characters
  buffer += key
  print(buffer)
```
Please consult ```tools/keys.txt``` for a full list of key names available on different platforms, or ```tools/controls.txt``` for the abridged version just containing control (normally non-printing) characters.
>
## Non-Blocking Usage (Non-Blocking function)
__```getkey(Blocking=False)```__
>
This will prevent getkey to wait for the input.
```python
from getkey import getkey, keys

key = getkey(Blocking=False)

if key == keys.UP:
  ...  # Handle the UP key
elif key == keys.DOWN:
  ...  # Handle the DOWN key
... # Handle all other desired control keys
else:  # Handle text characters
  buffer += key
  print(buffer)
```
__Note:__ This will greatly consume CPU resources if its on loop.

## API Blocking Usage
There is one primary method:
>
__```getkey(blocking=True)```__
>
Reads the next key-stroke from __```stdin```__, returning it as an string.
>
A key-stroke can have:
>
- 1 character for normal keys: ```'a', 'z', '9'...```
- 1 character for certain control combinations: ```'x01'``` as ```Ctrl-A```, for example
- more for other control keys (system dependent, but with portable names)
- check ```tools/keys.txt``` for keys available on different systems.
>
## keys
Interpreting the keycode response is made easier with the __```keys```__ object:
>
Contains portable names for keys, so that ```keys.UP``` will mean the up key on both Linux or Windows, even though the actual key codes are different.
>
Because the list of key names is generated dynamically, please consult ```tools/keys.txt``` for a full list of key names. It is not necessary to use key names for single characters: if the user pushes a the key returned is very portably just that single character a itself.
>
## keys.name(code)
Returns the canonical name of the key which yields this key code on this platform. One key code may have multiple aliases, but only the canonical name will be returned. The canonical names are marked with an asterisk in ```tools/keys.txt```.
>

## OS Support
This library has been tested on both Mac & Windows, & the Mac keys should work much the same on Linux. If planning to use more esoteric control keys, please verify compatibility by checking
>
## Manual Installation
```bash
git clone https://github.com/TheIceBergBot/getkey.git
cd getkey
```
```bash
pip install -r requirements-dev.txt
pip3 install -r requirements-dev.txt
```
```bash
sudo python setup.py install
sudo python3 setup.py install
```
## License
__Copyright__ (c) 2014, 2015 Miguel Ángel García (@magmax9).
>
__Copyright__ (c) 2016 K.C.Saff (@kcsaff)
>
Based on previous work on gist [getch()-like unbuffered character reading from stdin on both Windows and Unix (Python recipe)](http://code.activestate.com/recipes/134892/), started by [Danny Yoo](http://code.activestate.com/recipes/users/98032/).
>
Licensed under the [MIT license](http://opensource.org/licenses/MIT).


