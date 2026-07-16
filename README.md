
# GateKeeper

## Hardware Version: 4.6

## Author: @timr49

## Licence: see LICENCE file

GateKeeper is designed to monitor and to control an electric gate controller. Unlike a "smart" garage door interface, as well as triggering the open/close mechanism and sensing the closed position, it also monitors and publishes:
1. whether the gate (motor) is moving;
2. if so, in which direction it is moving;
3. whether the gate is fully open, fully closed or somewhere in between;
4. whether the photoelectric beam, if fitted and connected, is interrupted or not.

In its first instantiation, it was designed and built for:
1. a heavy sliding gate approximately 5 metres long;
2. a *Centsys D2 Turbo Low Voltage* gate motor controller;
3. integration with *Home Assistant* for user interface and exception monitoring.

The *Centsys D2 Turbo Low Voltage* has:
1. a 12VDC motor;
2. external low voltage AC transformer;
3. internal backup battery.
For more information, see:
1. [D2 Turbo and D2 Turbo Low-Voltage Installation Manual](https://www.centsys.com.au/wp-content/uploads/2022/01/1195.D.01.0001-D2-Turbo-D2-Turbo-Low-V-IM-11012022MT_Web.pdf)
2. [D2 Turbo and D2 Turbo Low-Voltage User Guide](https://www.centsys.com.au/pdf/D2_Turbo/1195.D.01.0006%20D2%20Turbo%20Low-Voltage%20User%20Guide%20CENTSYS-%2029062018BM.pdf)


Unlike previous versions, this design uses two off-the-shelf devices and a custom circuit:
1. a Shelly Plus 1 provides the trigger output and one sensor input;
2. a Shelly Plus I4 DC provies four sensor inputs;
3. a simple custom circuit uses two (2) relays and diodes to convert the motor voltages into two normally open sensor inputs to suit the Shelly Plus I4 DC.

This design assumes that:
1. the voltage applied across the motor by the motor controller is zero when the motor is not moving;
2. when the motor is moving, the polarity of that voltage indicates the direction of movement;
3. the sensors for the opened and closed states, if available, are normally open and connect to ground when active;
4. the optional photoelectric beam input is normally connected to ground an opens when the beam is broken;
5. the gate motor controller's input is triggered by momentarily connecting it to ground.

Features of the design include:
1. the motor direction sensors are isolated from the remainder of the circuitry so that it doesn't matter whether the motor shares a common ground with that circuitry or not;
2. a pair of dry contacts to drive the gate controller's trigger (**TRG** on the Turbo D2);
3. the photoelectric sensor provides information only e.g. it does *not* gate the trigger output.

Design notes:
1. The motor inputs use a pair of diodes, which "decode" the direction of movement from the polarity of the voltage applied across the motor and drive the respective relays, which "invert" those voltages to provide inputs to suit the Shelly I4 DC;
2. the input of the Shelly Plus 1 is used for the optional photoelectric beam;
2. for a schematic, see the *.pdf* or EAGLE *.sch* file in the *hardware* directory.

Build notes:
1. the Shelly I4 DC and custom circuitry is housed in a 65x60x30 mm waterproof enclosure (which fits inside the cover of the Turbo D2);
2. the Shelly Plus 1 is not enclosed but rather is mounted on the top of the Turbo D2 controller, secured with a cable tie;
3. in the **Input/Output settings** for the Shelly Plus 1, the *output type for Output(0)* must be set to *Detached* and the *Action on power on for Output (0)* must be set to *Turn OFF*;
4. the 12V power and sensor wires penetrate the enclosure via an IP68 gland (size PG9);
5. for images, see the JPEG files in the *hardware* directory.

TODO:
1. A diagram showing the interconnections between this circuit and the Turbo D2 and other connections would be useful.

---

