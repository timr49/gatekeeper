
# GateKeeper

## Hardware Version: 2.10.4

## Author: @timr49

## Licence: see LICENCE file

GateKeeper is designed to monitor and to control an electric gate controller. Unlike a "smart" garage door interface, as well as triggering the open/close mechanism and sensing the closed position, it also monitors and publishes:
1. where the gate (motor) is moving;
2. in which direction it is moving;
3. whether the gate is fully open, fully closed or somewhere in between;
4. optionally, the state of the "safe" signal from a photo beam or similar, if any.

In its first instantiation, it was designed and built for:
1. a heavy sliding gate approximately 5 metres long;
2. a *Centsys D2 Turbo Low Voltage* gate controller with a 12VDC motor, backup battery and mains power adapter;
3. integrating with Home Assistant for user interface and exception monitoring;
For details of the *Centsys D2 Turbo Low Voltage* see:
1. [Installation Guide](https://www.centsys.com.au/wp-content/uploads/2022/01/1195.D.01.0001-D2-Turbo-D2-Turbo-Low-V-IM-11012022MT_Web.pdf)
2. [User Guide](https://www.centsys.com.au/pdf/D2_Turbo/1195.D.01.0006%20D2%20Turbo%20Low-Voltage%20User%20Guide%20CENTSYS-%2029062018BM.pdf)

This circuit design assumes that:
1. the voltage applied across the motor is zero when the motor is not moving;
2. when the motor is moving, the polarity indicates the direction;
3. the sensors for the opened and closed states, if available, are normally open and connect to ground when active;
4. the gate controller's input(s) are triggered by momentarily connecting the input terminal to ground.

Features of the circuit include:
1. motor direction sensors that are isolated from the remainder of the circuitry so that it doesn't matter whether the motor shares a common ground with the remainder of the circuitry;
2. there is an active-low output provided to drive the gate controller's trigger;
3. there is a second such output provided to drive the Turbo D2 "pedestrian" trigger (which opens the gate sufficiently for a pedestrian but not a vehicle);
4. both of those outputs are potential-free but do not have an isolated ground; however they are driven by (solid state) relays so the modification to do so is electrically simple but physically requires additional connectors for the second terminal of each pair;
5. A jumper controls an active-low digital input to the MCU, intended to be used to initiate provisioning.

Design notes:
1. The motor inputs use a pair of optoisolators, which isolate the motor voltages from the remainder of the circuitry. In addition, the photodiodes in the optoisolators
"decode" the direction of movement from the polarity of the voltage applied across the motor;
2. a position-sensor analog input driven by a resistor network that combines the opened and closed digital sensors into one analog input; this would have been two digital inputs except there was not quite enough input ports or cables to support the second input signal;
3. the MCU used is a *LOLIN WeMOS ESP32-C3 Pico*, chosen for its compact size and adequate number of digital and analog inputs;
4. a *TR05S3V3* 12VDC to 3.3VDC DC-DC convertor supplies 3.3VDC power to the MCU and related circuitry;
5. for a schematic, see the .pdf or EAGLE .sch file in the *hardware* directory.

Build notes:
1. the MCU and related circuitry is housed in a 60 x 65 x 30 mm waterproof enclosure;
2. a short length of UTP (CAT5/6) cable is used to expose the various inputs and outputs from the PCB to a screw terminal block external to the enclosure that provides connection
points for the gate controller power, motor, triggers, etc.
3. the UTP cable penetrates the enclosure via an IP68 gland (size PG9);
4. see the JPEG images in the *hardware* directory.

---

