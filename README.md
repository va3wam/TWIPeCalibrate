# TWIPeCalibrate
This is embedded code that run on the TWIPe robot to calibrate its MPU6050

## Getting Started

There is a [VA3WAM wiki page](https://github.com/va3wam/va3wam.github.io/wiki) that has been created containing information common to all VA3WAM projects. Everything that you need to set up a VA3WAM compatable work space can be found in the wiki. Alternativey, you can follow the instructions and links below to set up your environment.  

### Prerequisites

The VA3WAM development environment used to make the code in this repository is documented [here](https://github.com/va3wam/va3wam.github.io/wiki/Tools).

### Installing

To get a copy of this project up and running on your local machine for development and testing purposes please follow these [instructions](https://github.com/va3wam/va3wam.github.io/wiki/Software-Version-Control).

## Running the tests

Run these tests over a serial connection between you computer and the robot. Use the green RESET button once you have serial data showing up to make sure that you see all the output. When you run this test it takes about 5 mintes because it is using two methods  and averaging a lot of readings to narrow down what calibration values you should use. Here is some example output that you get in your console window:

```Initializing I2C devices...
Testing device connections...
MPU6050 connection successful
PID tuning Each Dot = 100 readings
>**......>......
at 600 Readings

//           X Accel  Y Accel  Z Accel   X Gyro   Y Gyro   Z Gyro
//OFFSETS    -4016,     714,    5400,     134,     -10,     -81

>.>.700 Total Readings

//           X Accel  Y Accel  Z Accel   X Gyro   Y Gyro   Z Gyro
//OFFSETS    -4018,     714,    5400,     140,     -17,     -81

>.>.800 Total Readings

//           X Accel  Y Accel  Z Accel   X Gyro   Y Gyro   Z Gyro
//OFFSETS    -4020,     714,    5398,     135,     -12,     -81

>.>.900 Total Readings

//           X Accel  Y Accel  Z Accel   X Gyro   Y Gyro   Z Gyro
//OFFSETS    -4022,     714,    5400,     135,     -11,     -82

>.>.1000 Total Readings

//           X Accel  Y Accel  Z Accel   X Gyro   Y Gyro   Z Gyro
//OFFSETS    -4022,     712,    5400,     134,     -10,     -81


 Any of the above offsets will work nice 

 Lets proof the PID tuning using another method:
averaging 1000 readings each time
expanding:
....    XAccel                  YAccel                          ZAccel                  XGyro                   YGyro                   ZGyro
 [0,0] --> [32734,32767]        [0,0] --> [-6048,-6056] [0,0] --> [-32718,-32767]       [0,0] --> [-534,-534]   [0,0] --> [40,39]       [0,0] --> [324,326]
.... [-1000,0] --> [25296,32760]        [0,1000] --> [-6057,2421]       [0,1000] --> [-32767,-25408]    [0,1000] --> [-534,3453]        [-1000,0] --> [-3949,29]        [-1000,0] --> [-3663,314]
.... [-2000,0] --> [16913,32751]        [0,1000] --> [-6062,2418]       [0,2000] --> [-32760,-15919]    [0,1000] --> [-522,3450]        [-1000,0] --> [-3945,26]        [-1000,0] --> [-3660,312]
.... [-3000,0] --> [8520,32744] [0,1000] --> [-6062,2417]       [0,3000] --> [-32752,-6456]     [0,1000] --> [-526,3449]        [-1000,0] --> [-3949,26]        [-1000,0] --> [-3659,313]
.... [-4000,0] --> [181,32734]  [0,1000] --> [-6065,2418]       [0,4000] --> [-32741,3055]      [0,1000] --> [-526,3453]        [-1000,0] --> [-3950,30]        [-1000,0] --> [-3663,317]
....    XAccel                  YAccel                          ZAccel                  XGyro                   YGyro                   ZGyro
 [-5000,0] --> [-8186,32726]    [0,1000] --> [-6063,2421]       [0,5000] --> [-32731,12548]     [0,1000] --> [-522,3451]        [-1000,0] --> [-3946,28]        [-1000,0] --> [-3659,315]
.... [-5000,0] --> [-8182,32727]        [0,1000] --> [-6062,2418]       [0,6000] --> [-32724,21989]     [0,1000] --> [-527,3449]        [-1000,0] --> [-3946,25]        [-1000,0] --> [-3659,313]

closing in:
..      XAccel                  YAccel                          ZAccel                  XGyro                   YGyro                   ZGyro
 [-5000,-2500] --> [-8182,12706]        [500,1000] --> [-1819,2418]     [3000,6000] --> [-6379,21989]   [0,500] --> [-527,1467] [-500,0] --> [-1955,25] [-500,0] --> [-1665,313]
.. [-5000,-3750] --> [-8182,2253]       [500,750] --> [-1819,302]       [4500,6000] --> [7826,21989]    [0,250] --> [-527,465]  [-250,0] --> [-962,25]  [-250,0] --> [-675,313]
.. [-4375,-3750] --> [-2996,2253]       [625,750] --> [-766,302]        [5250,6000] --> [14960,21989]   [125,250] --> [-35,465] [-125,0] --> [-462,25]  [-125,0] --> [-174,313]
.. [-4062,-3750] --> [-377,2253]        [687,750] --> [-243,302]        [5250,5625] --> [14960,18516]   [125,187] --> [-35,210] [-62,0] --> [-208,25]   [-125,-62] --> [-174,78]
.. [-4062,-3906] --> [-377,934] [687,718] --> [-243,31] [5250,5437] --> [14960,16735]   [125,156] --> [-35,86]  [-31,0] --> [-84,25]    [-93,-62] --> [-44,78]
..      XAccel                  YAccel                          ZAccel                  XGyro                   YGyro                   ZGyro
 [-4062,-3984] --> [-377,279]   [702,718] --> [-104,31] [5343,5437] --> [15843,16735]   [125,140] --> [-35,22]  [-15,0] --> [-20,25]    [-93,-77] --> [-44,19]
.. [-4023,-3984] --> [-51,279]  [710,718] --> [-36,31]  [5390,5437] --> [16291,16735]   [132,140] --> [-10,22]  [-15,-7] --> [-20,11]   [-85,-77] --> [-11,19]
.. [-4023,-4003] --> [-51,114]  [714,718] --> [-1,31]   [5390,5413] --> [16291,16504]   [132,136] --> [-10,6]   [-11,-7] --> [-4,11]    [-85,-81] --> [-11,4]
.. [-4023,-4013] --> [-51,24]   [714,716] --> [-1,13]   [5390,5401] --> [16291,16396]   [134,136] --> [-1,6]    [-11,-9] --> [-4,3]     [-83,-81] --> [-3,4]
.. [-4018,-4013] --> [-3,24]    [715,716] --> [-1,13]   [5395,5401] --> [16336,16396]   [134,135] --> [-1,2]    [-10,-9] --> [0,3]      [-82,-81] --> [0,4]
..      XAccel                  YAccel                          ZAccel                  XGyro                   YGyro                   ZGyro
 [-4018,-4015] --> [-3,12]      [715,716] --> [-4,13]   [5398,5401] --> [16376,16396]   [134,135] --> [-2,2]    [-10,-9] --> [0,3]      [-82,-81] --> [0,4]
averaging 10000 readings each time
.................... [-4018,-4016] --> [-3,13]  [715,716] --> [-2,13]   [5399,5401] --> [16376,16396]   [134,135] --> [-1,2]    [-10,-9] --> [0,3]      [-82,-81] --> [0,4]
.................... [-4017,-4016] --> [-3,13]  [715,716] --> [-2,13]   [5399,5400] --> [16376,16396]   [134,135] --> [-1,2]    [-10,-9] --> [0,3]      [-82,-82] --> [0,1]
.................... [-4017,-4016] --> [-3,13]  [715,716] --> [-3,13]   [5399,5400] --> [16376,16396]   [134,135] --> [-1,2]    [-10,-9] --> [-1,3]     [-82,-82] --> [0,1]
-------------- done --------------
```
For our robot we only care about the XGyro, YGyro and ZGyro values. In this example we see these numbers:

<ul>
<li>XGyro show the range of values [134,135]. Pick the middle of the range which we will call 134 in this case.</li> 
<li>YGyro show the range of values [-10,-9]. Pick the middle of the range which we will call -10 in this case.</li> 
<li>ZGyro show the range of values [-82,-82]. Pick the middle of the range which we will call -82 in this case.</li> 
</ul>

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
