# ICSUnitSim on ESP32 board *("ICS on Chip")*

> Realtime Process Simulation of Plant Water Supply Unit

> Simulation Generates logically correct Modbus signals of Water Supply facility using ESP32 MCU board with ModbusTCP interface

> Simulation intended for HMI and DCS testing with realtime values and for ICS security research

> Developed using Arduino IDE for ESP32 (ESP 32 MCU board is <a href="https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20200516160605&SearchText=esp32">available on Aliexpress </a> for approx price of 5$)

## Version history
- Added HMI project backup for output visualisation
- V0.2 Introduced Pump AUTO functionality, adjustable setpoints, tank_drain variable on modbus
- V0.1 Initial code with manual controls only 

## Table of Contents

- [HMI Example](#HMI)
- [Simulation setup](#Simulation)
- [Virtual process P&ID](#Virtual)
- [Modbus addressing](#Modbus)
- [Follow](#Follow)
- [Credits](#Credits)
- [Version history](#Version)

## HMI Visualisation Example
HMI_Project folder contains latest backup of Ignition HMI Project, restore it to you Ignition setup for below result.

<a href="https://github.com/akiUp/ICSUnitSim"><img src="https://github.com/akiUp/ICSUnitSim/blob/master/v02/img/ICSonChip.gif" title="HMI demo" alt="HMI Demo"></a>

Current HMI Example is designed on Ignition SCADA by Inductive Automation

Free trial versions of HMI software like RapidSCADA, Ignition and Advantech is available on internet.

For simple Modbus values reading/writing you could use RMMS tool http://en.radzio.dxp.pl/modbus-master-simulator/ 

## Simulation Setup

<a href="https://github.com/akiUp/ICSUnitSim"><img src="https://github.com/akiUp/ICSUnitSim/blob/master/Simulation%20diagram.png" title="Connection diagram" alt="Connection diagram"></a>

## Virtual process's P&ID

<a href="https://github.com/akiUp/ICSUnitSim"><img src="https://github.com/akiUp/ICSUnitSim/blob/master/v02/img/ICSUnitSimP%26IDv02.png" title="Simulation P&ID" alt="Simulation P&ID"></a>

## Modbus addressing

> !Important!: Modbus library uses 0 based adressing

- ***Modbus Coils Offsets (read\write)***
```shell
mot_start, address: 100, boolean, Start button, 1 to activate, returns to 0 after activation

mot_stop, address: 110, boolean, Stop button, 1 to activate, returns to 0 after activation

valve_state, address: 120, boolean 0-Closed 1-Open (Controlled by start/stop logic)

mat_auto, address:130, boolean, 1-Pump automatic mode(by setpoints), 0 - manual mode
```
- ***Modbus input status (Discrete Inputs) Offsets(read only)***
```shell
mot_run, address: 100, boolean, 1 running, 0 stop
mot_trip, address: 110, boolean, Motor trip state, cause: Tank full, Valve closed, Random trip (1 of 10000)
```
- ***Modbus Input Register Offsets (read only)***
```shell
mot_load, address: 100; Uint16, range:0-100, random motor load simulation

flowm_flow, address: 110, Uint16, range:0-10, flow value depending on mot_load 

tank_level, address: 120, Uint16, range:0-65000, 65000 value trips the motor, has constant (random of 4) drainage flow

tank_drain,  address: 130; Uint16, Random drain by process
```
- ***Modbus Holding Register Offsets (read\write)***
```shell
tank_Hi, address: 100; Uint16, adjustable Hi level setpoint, for turning motor OFF in AUTO mode

tank_Lo, address: 110; Uint16, adjustable Lo level setpoint, for turning motor ON in AUTO mode
```

## Follow 
Follow author on twitter for project updates
https://twitter.com/supeyev/

## Credits
- Based on Alexander Emelianov (a.m.emelianov@gmail.com) Modbus library
  https://github.com/emelianov/modbus-esp8266 @emelianov
- Inductive Automation's Ignition SCADA used for HMI Design https://inductiveautomation.com/ignition/


