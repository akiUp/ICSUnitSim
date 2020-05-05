# ICSUnitSim
Simulation of Industrial process unit on ESP32 board with ModbusTCP interface
Simulation intended to for HMI testing with realtime values and ICS security research

For Modbus signals testing you could use http://en.radzio.dxp.pl/modbus-master-simulator/ 

Example of HMI design is below
https://twitter.com/supeyev/status/1257664325659082758

Free trial versions of HMI software like RapidSCADA, Ignition and Advantech is available on internet.

Developed using Arduino IDE for ESP32

//-----Modbus Coils Offsets (read\write)

mot_start, address: 100, boolean, Start button, 1 to activate, returns to 0 after activation

mot_stop, address: 110, boolean, Stop button, 1 to activate, returns to 0 after activation

valve_state, address: 120, boolean 0-Closed 1-Open (Controlled by start/stop logic)

//-----Modbus input status (Discrete Inputs) Offsets(read only)

mot_run, address: 100, boolean, 1 running, 0 stop

mot_trip, address: 110, boolean, Motor trip state, cause: Tank full, Valve closed, Random trip (1 of 10000)


//-----Modbus Input Register Offsets (read only)

mot_load, address: 100; Uint16, range:0-100, random motor load simulation

flowm_flow, address: 110, Uint16, range:0-10, flow value depending on mot_load 

tank_level, address: 120, Uint16, range:0-65000, 65000 value trips the motor, has constant (random of 4) drainage flow

Based on Alexander Emelianov (a.m.emelianov@gmail.com) Modbus library
  https://github.com/emelianov/modbus-esp8266
