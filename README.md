# TWIPeCalibrate
This is embedded code that run on the TWIPe robot to calibrate its MPU6050

## Getting Started

There is a [VA3WAM wiki page](https://github.com/va3wam/va3wam.github.io/wiki) that has been created containing information common to all VA3WAM projects. Everything that you need to set up a VA3WAM compatable work space can be found in the wiki. Alternativey, you can follow the instructions and links below to set up your environment.  

### Prerequisites

The VA3WAM development environment used to make the code in this repository is documented [here](https://github.com/va3wam/va3wam.github.io/wiki/Tools).

### Installing

To get a copy of this project up and running on your local machine for development and testing purposes please follow these [instructions](https://github.com/va3wam/va3wam.github.io/wiki/Software-Version-Control).

## Running the tests

When you run this test it takes a few minutes. When done capture the values given  to seed yor TWIPe robot balance numbers.

## Deployment

At this time the embedded code in this repository is uploaded via a serial connection using PlatformIO. 

## Built With

* [Visual Studio Code](https://code.visualstudio.com/) - Enhanced text editor
* [PlatformIO](https://platformio.org/) - Embedded programming IDE
* [Sea Monkey](https://www.seamonkey-project.org/) - Internet Application Suite
* [Mosquito](https://mosquitto.org/) - MQTT Broker
* [MQTTfx](http://mqttfx.org/) - MQTT client
* [Doxygen](http://www.doxygen.nl/) - Source code documentation generator

## Contributing

At the present time this code is only done by close friends so no process for becomming a contibutor has been worked out.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/va3wam/TWIPe/tags).

## Authors

* **Jeff Rowberg** - *Initial code available [here](https://github.com/jrowberg/i2cdevlib/tree/master/Arduino/MPU6050)*
* **va3wam** - *Modified to work on ESP32* 

See also the list of [contributors](https://github.com/va3wam/TWIPe/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Jeff Rowberg for the MPU6050 DMP logic
