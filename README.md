nRF51822-cli
============

Provides a minimal GCC based build system for [nRF51822](https://www.nordicsemi.com/eng/Products/Bluetooth-R-low-energy/nRF51822) projects. Avoids [make](https://www.gnu.org/software/make/) in favour of simple shell scripts. Includes JLink flash and erase scripts.

Handles:
- Compilation
- SoftDevices
- Flash Programming

Includes blink-test file.

Heritage
---------

There are several similar projects available such as [this](https://github.com/hlnd/nrf51-pure-gcc-setup), [that](https://github.com/pauloborges/nrf51822-linux-template), and the [other](https://github.com/EarthLord/nrf51Demo). Each has their own merits. [This guide](http://www.funwithelectronics.com/?id=168) was also helpful.

This project aims to be simple and well documented, for example, the [very concise](https://github.com/pauloborges/nrf51822-linux-template/blob/master/scripts/erase.jlink) JLink shorthand commands are expanded and [written more naturally](https://github.com/hughobrien/nRF51822-cli/blob/master/flash).

Version 6 of the S110 SoftDevice currently recommended, and for simplicity is hardcoded into this project; this can easily be modified.

Usage
-----

Since we know the included 'main.c' blinker compiles successfully, we can test with <pre>./compile; ./erase; ./flash; ./clean</pre>

compile:
- Calls GCC directly on all .c files, including the necessary NRF SDK templates.
- Avoids 'make' complexity by forcing [tabula rasa](https://en.wikipedia.org/wiki/Tabula_rasa) builds.
- Links with the correct offsets for the S110 softdevice.

flash:
- The application is checked to see if it was linked against a SoftDevice.
- Both are then flashed to the chip.

erase:
- Erases both region0 and region1 areas, if defined.
- Erases the User Information Configuration Registers.

clean:
- Remove object files

Tests
-----
Using the [Nordic NRFGo Studio](http://www.nordicsemi.com/chi/node_176/2.4GHz-RF/nRFgo-Studio) both the SoftDevice and the application binaries were read from the flashed chip and successfully verified against the original hexfiles.

Requirements
------------

- [nRF51 SDK](https://www.nordicsemi.com/eng/Products/Bluetooth-R-low-energy/nRF51822)
- [An S110 SoftDevice, v6 preferred](https://www.nordicsemi.com/eng/Products/Bluetooth-R-low-energy/nRF51822)
- [SEGGER JLink](http://www.segger.com/jlink-software.html)
- [nRF51822 Evaluation Kit board PCA1001](http://www.nordicsemi.com/eng/Products/Bluetooth-R-low-energy/nRF51822-Evaluation-Kit)
- [GNU Tools for ARM](https://launchpad.net/gcc-arm-embedded)

In each case, there are multiple versions of these available. The code should be easily modifiable to support them.
