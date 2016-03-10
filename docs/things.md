# Things

IOTDB in and off itself is pretty bare-bones: it doesn't know how to talk to anything. 
To get IOTDB to talk your Things, you install the appropriate **Module** that has that functionality.
Modules include a [Bridge](bridge) that has the code to do the work,
and one or more [Models](model) that semantically describe how to use a Thing.
We use this architecture so you don't need to have more functionality installed than you are using.

NOTE: use <code>homestar install</code> and not
<code>npm install</code> to install Modules. This does two Things:

* it modifies <code>.iotdb/keystore.json</code> so that IOTDB knows the Module (and its associated Things) should be used.
* it does some complicated management of IOTDB-related dependencies so that there's not different versions of the same code running in a single installation

# Modules

Please click on the links for further documentation, including what specific devices are supported, how to configure, and limitations (if any):

## [Chromecast](https://github.com/dpjanes/homestar-chromecast)

	$ homestar install homestar-chromecast

## [Bluetooth Low Energy](https://github.com/dpjanes/homestar-ble)

	$ homestar install homestar-ble

## [Feeds (Atom and RSS)](https://github.com/dpjanes/homestar-feed)

	$ homestar install homestar-feed

## [Denon Audio/Video Receiver](https://github.com/dpjanes/homestar-denon-avr)

	$ homestar install homestar-denon-avr

## [ITach Infrared](https://github.com/dpjanes/homestar-itach-ir)

	$ homestar install homestar-itach-ir

## [Johnny-Five / Arduino](https://github.com/dpjanes/homestar-johnny-five)

	$ homestar install homestar-lifx

## [KNX](https://github.com/dpjanes/homestar-knx)

	$ homestar install homestar-lifx

## [LG Smart TV](https://github.com/dpjanes/homestar-lg-smart-tv)

	$ homestar install homestar-lg-smart-tv

## [LIFX](https://github.com/dpjanes/homestar-lifx)

	$ homestar install homestar-lifx

## [Nest](https://github.com/dpjanes/homestar-nest)

	$ homestar install homestar-rest

## [Philips Hue](https://github.com/dpjanes/homestar-hue)

	$ homestar install homestar-hue
	$ homestar configure homestar-hue

## [REST](https://github.com/dpjanes/homestar-rest)

Talk to REST interfaces

	$ homestar install homestar-rest

## [Samsung Smart TV](https://github.com/dpjanes/homestar-samsung-smart-tv)

	$ homestar install homestar-samsung-smart-tv

## [SmartThings](https://github.com/dpjanes/homestar-smartthings)

Note there's a ton of configuration required.

	$ homestar install homestar-smartthings
	$ homestar configure homestar-smartthings

## [Sonos](https://github.com/dpjanes/homestar-sonos)

We need a tester

	$ homestar install homestar-tcp

## [TCP Lighting](https://github.com/dpjanes/homestar-tcp)

	$ homestar install homestar-tcp
	$ homestar configure homestar-tcp

## [WeMo](https://github.com/dpjanes/homestar-wemo)

	$ homestar install homestar-wemo

