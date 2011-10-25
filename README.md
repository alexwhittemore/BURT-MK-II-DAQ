BURT Mk-II DAQ
==============

Boston University Rocket Team's Mk-II Data Acquisition and Control System.

Background
----------
The Boston University Rocket Team is currently focused on advancing hybrid rocket motor design and research. The Mk-II is a static (never leaves the ground) test bed for experimentation with various design parameters like chamber and oxidizer injector geometries.

### Sensors
The DAQ side consists of multiple sensors: pressure transducers, load cells, and thermocouples.

There are two pressure transducers, each rated at 500PSI full scale. The Oxidizer Line Transducer measures the pressure on the nitrous oxide feed line right before the injector. This should match the vapor pressure of N2O, roughly 750PSI dependent on temperature. The Combustion Chamber Transducer measures the pressure INSIDE the combustion chamber, directly after the injector. For Mk-II, the design chamber pressure is 500PSI

There are also two load cells. The Thrust Load Cell is an S-Beam, 500lbs full scale load cell. Design thrust is 75lbs. The Oxidizer Tank Cell is a canteliver 50lbs cell. This measures the weight of the Nitrous Oxide tank used to feed the motor, where change in mass of the tank can be used to calculate mass flow rate of oxidizer.

There are three thermocouples. All are K-type. One NPT-threaded, sealed TC measures oxidizer temperature before the injector. One of two silicone surface adhesive TCs measures the oxidizer tank temperature. The other of these measures the combustion chamber casing temperature. A spike in this temperature indicates a fault with the fuel grain casting and a potentially unsafe conditon that could result in a burn-through of the schedule-80 steel casing.

### Boards
All of these are read by four wheatstone bridge digitizer boards (Bridge Digitizer.sch) and three K-type thermocouple digitizer boards (Thermocouple Digitizer.sch). The outputs of these boards are read via SPI by an mbed microcontroller residing on a main board. This main board also holds a zigbee radio which forwards a UART connection to a host computer for off-site (safe distance) live monitoring of the system, as well as a USB plug for a thumb drive to log the live, real-time acquired data. Additionally, a UART is broken out on a set of .1" spaced headers to connect to a sparkfun graphical LCD for on-site monitoring. Finally, two pins are broken out on a DB-9 connector to serve as software serial to a safe distance physical control interface. This could just as easily be run exclusively via zigbee radio.

### Control
The final job of the system is to control the burn itself. This is handled by two pneumatic valves, switched by 24-volt electric solenoids in turn controlled by the mbed via a quad-half H-bridge chip on the main board. These solenoids are either open or spring-shut, and thus only require two outputs of the quad half Bridge. A third output is used to control a nichrome wire-based pyrotechnic ignitor. The fourth half bridge is implemented but unused. 
