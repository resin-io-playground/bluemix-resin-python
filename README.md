# IBM Bluemix Watson IoT device on resin.io

Implementing a basic IBM Bluemix Watson IoT device on resin.io. It shows how to send data, and receive commands. Also includes an example application that can monitor the device's data and send the appropriate commands.

For detailed explamation, and setting up IBM Bluemix with resin.io, see the [documentation](https://docs.resin.io/integrations/bluemix/)!

The sensor side of the application implements 3 readings to create interesting data streams that can be used for testing:

* CPU utilization
* Free memory
* Random number

The commandss side of the application implements 3 commands:

* `setText`: set a text value, here write to the log
* `setOff`: turn the device off using the Supervisor API
* `blinkLed`: blink the device identification LED (on those devices where it is available), using the SupervisorAPI

## Device

After setting up your device on IBM Bluemix, and save your credentials ("organization", "device type", "device name", "authentication method", and "authentication token")) create a resin.io application, and define five application-wide environment variables to hold the credential values from for the devices.

* `BLUEMIX_ORG`
* `BLUEMIX_DEVICE_TYPE`
* `BLUEMIX_DEVICE_ID`
* `BLUEMIX_AUTH_METHOD`
* `BLUEMIX_AUTH_TOKEN`

Here `BLUEMIX_ORG`, `BLUEMIX_DEVICE_TYPE`, and `BLUEMIX_AUTH_METHOD` will likely be the same for all devices within a resin.io application, so set them to the correct values. `BLUEMIX_DEVICE_ID` and `BLUEMIX_AUTH_TOKEN` will be different for all devices, so set them application-wide to `REDEFINE` or something similar to remind you to redefine them in the device-level environmental variables!

Set up your device and connect to resin. Then in the device's dashboard, redefine the environment variables ( `BLUEMIX_DEVICE_ID` and `BLUEMIX_AUTH_TOKEN`). If you have multiple devices, repeat these steps for all.

For this application other optional variables.

* `READINGS_PERIOD`: how often to read the sensor values (in seconds, default is `10`)

## Application

The application is available in the `application/` directory. Copy `application.conf.sample` to `application.conf`, update the values within with the API key and other information from the Bluemix dashboard (Dashboard of your IoT platform application > Access > API Keys).

Optional: set up virtualenv:

```bash
virtualenv venv
source venv/bin/activate
```

Install required libraries:
```bash
pip install -r requirements.txt
```

Then run the application:

* `python application.py` or `python application.py --help`: show help
* `python application getdevices`: query registered devices
* `python application monitor`: stream readings from connected devices
* `python application settext`: send "setText" command to device
* `python application setoff`: send "setOff" command to device (turn off)
* `python application blinkled`: send "blinkLed" command to the device

## License

Copyright 2016 Rulemotion Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.