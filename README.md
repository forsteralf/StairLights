# StairLights
# This project is a small controller to turn on/off some led lights when a PIR sensor picks someone up. It has a manually adjustable period and will restart the timeout whenever the PIR sensor picks someone up.
# This project is more for me mucking around than functionality, there are many ways to implement the above statement.
#
# Contents:
#  README.md - This file
#  stairs.S  - PIC Source code
#  Schematic_StairLights_2023-10-06.pdf - Schematic diagram of controller board
#  pic10F_programmer - source code for a programmer that i created.
#  pic10F_simulator - source code for the simulation of the controller board
#
# Overall System consistes of 12VDC power plug, LED light strip, controller, PIR Sensor. 
#  The 12VDC power supplies the controller and LED lights. 
#  The PIR sensor has a set of contacts that trigger when someone is picked up. 
#  The controller has a MOSFET that drives the LED circuit
# 
# Controller Circuit:
#  I decided to use one of the smallest PIC ucontroller, the PIC10F222. This chip has only 4 IO pins, 512 instructions memory, 23 working registers. 
#  I decided to add a FRAM chip and and IO chip using I2C interface so that it had some more capability.
# 
# SENSOR --->--------------------------------------------
#                  -------------                         |
#  -------         |   uP    GP0|----------------------  |
# | Reset |--->----|GP3         |           --------   | |
# | Cntl  |        |         GP1|---*-SCL --|  IO   |  | |
#  -------         |            |   |       |    INT|->  |
#                  |         GP2|-----SDA-*-|      7|-<--
#                  -------------    |     | |      6|------> to led lights
#                                   |     | |       |     -----------
#                  ----------       |     | |      3|-<---|  BDC    |
#                  |   FRAM  |------      | |      2|-<---| switch  |
#                  |         |            | |      1|-<---|         |
#                  |         |------------  |      0|-<---|         |
#                  ----------               --------      -----------
#
# PIC Software:
#  The PIC source code, being so small in resources, is written in ASM and compiled using Microchips xc8 assembler using the following command:
#   "C:\Program Files\Microchip\xc8\v2.41\pic-as\bin\pic-as.exe" -mcpu=10F222 -Wl,-Map=stairs.map -Wl,-presetVec=0h -Wl,-pcode=1h stairs.S
#
# Testing the PIC Source Code:
#  I wrote a quick and dirty simulation of the PIC uProcessor and analysied the code.
#
# Programming the PIC:
#  Use a PICKit. Or in my case, I developed my own programmer using a raspberry pi and a small circuit to interface to the PIC10F222.
#
# Building the circuit board:
#  I used EasyEda to create a circuit board.
