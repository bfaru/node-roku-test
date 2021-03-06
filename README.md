# node-roku-test
---

Roku channel testing tool for node.  This is aimed at developers who are using a Roku in development mode and want to verify channel behavior.  

This module can:

* Install a channel zip
* Launch a channel with arbitrary arguments
* Send ECP commands to a Roku device (e.g. key presses)
* Listen for data on the debug console


Based on [node-roku](https://github.com/TheThingSystem/node-roku).



## Install

`npm install veeta-tv/node-roku-test`


## Module Initialization

Pass in the Roku device ip address, developer password, and port to debug on

`device = new RokuTest('192.168.1.100', 'passw0rd', RokuTest.MAIN)`

The following port constants are available:


* `RokuTest.MAIN` 8085
* `RokuTest.SG` 8089
* `RokuTest.TASK1` 8090
* `RokuTest.TASK2` 8091
* `RokuTest.TASK3` 8092
* `RokuTest.TASK4X` 8093
* `RokuTest.PROFILER` 8080

## api

### type(string [, fn])

Types the provided string into a field

### press(button)

Simulates a button press on the remote control

### delay(ms)

Add a delay into the command queue to allow the roku to keep up with what you want to do.

### input(obj)

Pass arguments into the currently running app. see [test/input.js](https://github.com/tmpvar/node-roku/blob/master/test/input.js)

### apps(function(err, array) {});

list the installed apps on the roku

### createIconStream(appId)

create a PNG stream

### launch(string)

Using the `launch` command you can open application or allow a development application handle the protocol.

see the example code in [test/launch.js](https://github.com/tmpvar/node-roku/blob/master/test/launch.js) and [test/dev-video.js](https://github.com/tmpvar/node-roku/blob/master/test/dev-video.js)

### launch(Object)

Launch the development roku channel, passing the key/value pairs from Object as URL query params.


### info(function(err, obj) {});

returns an object of information about the roku

example object:

```

{ major: '1',
  minor: '0',
  deviceType: 'urn:roku-com:device:player:1-0',
  friendlyName: 'Roku Streaming Player',
  manufacturer: 'Roku',
  manufacturerURL: 'http://www.roku.com/',
  modelDescription: 'Roku Streaming Player Network Media',
  modelName: 'Roku Streaming Player 4200X',
  modelNumber: '4200X',
  modelURL: 'http://www.roku.com/',
  serialNumber: '1GH35D054697',
  UDN: 'uuid:31474833-3544-a9d5-0000-05006d1f0000',
  serviceType: 'urn:roku-com:service:ecp:1',
  serviceId: 'urn:roku-com:serviceId:ecp1-0',
  SCPDURL: 'ecp_SCPD.xml' }

```

### install(zip)

Install the channel `zipfile` to a Roku device with development password `password`.

### connectDebug(port)

Start listening for data on the console.  The `port` argument is optional.  If no port is specified, the port specified at module initialization will be used.

### destroyDebug()

Stop listening for data on the console.


## Node Events

### debugData

The `debugData` event is emitted when the debug socket has data on it.  This will not be emitted for old data which the Roku "replays" on initial connection to the debug port.

## license

[MIT](http://tmpvar.mit-license.org)
