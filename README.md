# Pozyx-ROS
ROS node for Pozyx connected with I2C

See [https://github.com/heivi/Pozyx-Linux-library](https://github.com/heivi/Pozyx-Linux-library) for more information on installing the Pozyx library on RPi/Linux.

The Pozyx library is included as submodule, so you can either pass `--recursive` to `git clone` or run

```
git submodule init
git submodule update
```
You should change CMakeLists.txt if you don't use [pigpio](http://abyz.co.uk/rpi/pigpio/) -library.
