Python Bravia TV
=====================

Python Bravia TV is a Python library to perform remote communication via http protocol with Sony Bravia TVs 2013 and newer. For more information on the api used in this library, refer to [BRAVIA Professional Display Knowledge Center](https://pro-bravia.sony.net/develop/index.html)

This library was forked from [BraviaRC](https://github.com/aparraga/braviarc) and is primarily being developed with the intent of supporting [home-assistant](https://github.com/home-assistant/home-assistant)

Installation
------------

    # Installing from PyPI
    $ pip install bravia-tv
    # Installing latest development
    $ pip install git+https://github.com/dcnielsen90/python-bravia-tv@master

Initializing and Connecting
===========================
```python
from bravia_tv import BraviaRC

ip_address = '192.168.1.2'
mac_address = 'XX:XX:XX:XX:XX:XX'
subnet_mask = '255.255.255.0'

# IP address is required.
# MAC address can be found dynamically and therefore does not need to be specified. It is useful to specify mac address when a bravia instance is created when the TV is in the OFF state.
# Subnet Mask is only required when the TV and the device you are running your script from are on different subnets. Without specifying subnet mask, the wake on lan packet will only broadcast over the the local subnet.
braviarc = BraviaRC(ip_address, mac_address, subnet_mask)


# The pin can be a pre-shared key (PSK) or you can
# receive a pin from the tv by making the pin 0000
pin = '1878'

# Connect to TV
braviarc.connect(pin, 'my_device_id', 'my device name')
```
Command Examples
================
```python
# Check connection
if braviarc.is_connected():

    # Get power status
    power_status = braviarc.get_power_status()
    print (power_status)

    # Get playing info
    playing_content = braviarc.get_playing_info()

    # Print current playing channel
    print (playing_content.get('title'))

    # Get volume info
    volume_info = braviarc.get_volume_info()

    # Print current volume
    print (volume_info.get('volume'))

    # Change channel
    braviarc.play_content(uri)
  
    # Get app list
    app_info = braviarc.load_app_list()
    print (app_info)
  
    # Start a given app
    braviarc.start_app("Netflix")

    # Turn off the TV
    braviarc.turn_off()
```
