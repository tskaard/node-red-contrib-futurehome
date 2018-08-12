# node-red-contrib-futurehome


![Release](https://img.shields.io/npm/v/node-red-contrib-futurehome.svg)
![npm](https://img.shields.io/npm/dm/node-red-contrib-futurehome.svg)

This module provides a set of nodes in Node-RED to controll a Futurehome system. This was made using Futurehome's public API.

## Install

To install the stable version use the `Menu - Manage palette` option and search for `node-red-contrib-futurehome`, or run the following command in your Node-RED user directory (typically `~/.node-red`):

	npm i node-red-contrib-futurehome

## Nodes
There are a total of 8 nodes. Two used for connecting to the system using websocket, three used for sending different commands to the system.


![](static/nodes.png "Nodes")


### site (connect to site)
This node is used to connect to a Futurehome site, and output the data comming from the site. The data can be anything from a device changing state, a mode change, or the temperature setpoint in a room.

### sitestate (get site info)
This node is used to fetch information about the site. This can for example be the mode of the site. Home/away/holiday etc.. No payload required.

### device (connect to device)
This node is used to connect to a device in the Futurehome system, and output changes from the device. This can be a magnet contact reporting open/close state, a motion sensor reporting motion, or a light turing on/off.


### mode
This node is used to change between the 4 modes in Futurehome.
The mode can be defined on the node, or overwritten by payload.

```javascript
// Send the following payload to use the node.
msg.payload = {"mode":"home"};		// changes to home mode
msg.payload = {"mode":"away"};		// changes to away mode
msg.payload = {"mode":"sleep"};		// changes to sleep mode
msg.payload = {"mode":"vacation"};	// changes to vacation mode
```


### change-device
This node is used to change the state of a device. Dim or turn on/off a light, or lock/unlock a door.

```javascript
// Send the following payload to use the node.
// Turn device ON or OFF:
msg.payload = "on";			// turn on a device
msg.payload = "off";		// turn off a device
msg.payload = {"power":"on"};		// turn on a device
msg.payload = {"power":"off"};	// turn off a device
// Dim a device to %:
msg.payload = 35;		// dim a device to 35%
msg.payload = {"dimValue":"75"};	// dim a device to 75%
// Lock and unlock a door:
msg.payload = "locked"; 
msg.payload = "unlocked";
msg.payload = {"lockState":"locked"};
msg.payload = {"lockState":"unlocked"};
```

### change-room (set temperature)
This node is used to change the temperature setpoint in a room.
Room ID is selected on the node.

```javascript
// Send the following payload to use the node.
// Temperatur has to be between 5.0 and 50.0 degrees.
// Set the temperature::
msg.payload = 15;
msg.payload = 16.5;
msg.payload = {"temperature":"22.0"}; // Has to be float, "22" won't work.
msg.payload = {"temperature":"19.5"};
```

### shortcut

This node is used to run a shortcut in the system.

```javascript
// Send the following payload to use the node.
// If msg.payload is an int the node will try to run the shortcut with that ID.
msg.payload = 3;		// will run shortcut with ID = 3

// Anything else will run the shortcut selected on the node.
```

### get-state
This node is used to get the state of a device or a room.

```javascript
// Send the following payload to use the node.
// Get the information from room 3:
msg.payload = {"type":"rooms","id":"3"};

// Get the information from device 2 
msg.payload = {"type":"devices","id":"2"};

// If input is something else (like timestamp) the node will get information from the selected room or device.
```