# RAM Card for Sharp Pocket PC-E500

Disclaimer: use it at your own risk. I am programmer, not an electronics engineer. The DIY card works for me but can damage your device.

256 KB RAM card with battery.

![Overview](./_img/card.jpg?raw=true)

## Circuit Diagram

![Circuit diagram](./_img/circuit-diagram.png?raw=true)

[Download as PDF](./ram-card-256k/ram-card-256k.pdf)

[KiCad Project](./ram-card-256k/)

## PCB

PCB: 41.9 x 54.1 x 0.8 mm

![Address lines](./_img/pcb.jpg?raw=true)

## Bill of Materials

| Reference | Part | Size | Comments |
| --------- | ---- | ---- | -------- |
| R1,R2 | 47K | 1206 | Pull resistor |
| R3 | 470K | 1206 | Pull resistor |
| C1 | 330 nF | 1812 | Decoupling capacitor |
| D1 | RB160M | SOD-123 | Schottky diode prevents card battery trying to power E500 when it's switched off |
| D2 | 1N4148W | SOD-123 | Fast switching diode - reverse battery protection, prevents cell battery loading from E500 |
| U1 | HC138 | SOIC-16 | Address decoder |
| U2, U3 | KM681000BLG | SSOP-32 | 128K x 8-bit low power CMOS static RAM |
| S1 | Slider switch | 6.7 x 2.7 mm | Write protection |
| BT1 | CR1216 | 12.5 x 1.6 mm | 3 volts lithium cell |

## Usage

Power off Pocket Computer, insert card, power on.

The following message should appear:
```
S2(CARD):NEW CARD

   PF1 --- INITIALIZE
   PF2 --- DO NOT INITIALIZE
```

Press **PF1** to initialize.

To use card as an additional memory space for Basic program and variables type:

```
MEM$="B"
```

To use internal RAM for storing programs and variables

```
MEM$="S1"
```

To use RAM card for storing programs and variables

```
MEM$="S2"
```

### Device names

- **X:** Pocket disk drive
- **Y:** Another disk in the disk drive. Used for disk-to-disk copy
- **E:** RAM disk internal RAM
- **F:** RAM disk external RAM
- **G:** ROM storing engineering programs
- **CAS:** Cassette tape
- **COM:** Serial I/O device


### Partitioning RAM card

The card space is used for storing data and variables.

Allocate **data** storage space in the RAM disk F: 

```
INIT "F:100K"
```

*Allowable size can be from 2 to RAM card capacity minus 1.*


### Usage example

```BASIC
REM use internal RAM for BASIC programs and variables
MEM$="S1"

REM reserve 254K for data on external RAM drive F:
INIT "F:254K"     

REM check free variables space (internal RAM)
FRE 0

REM check free disk space on external RAM card
DSKF "F:"

REM check what files are delivered with E500 on built-in ROM
FILES "G:"

REM copy pre-installed program with periodic table of chemical elements from ROM to F:
COPY "G:PERIOD.221" TO "F:"

REM check that file is now present on drive F:
FILES "F:"

REM check the remaining free disk space (must be ~8K less then on a newly initialized card)
DSKF "F:"

REM test if information is preserved on the RAM card when not inserted in E500 (CR1216 cell should provide enough power to store data for few months)

REM turn off Pocket Computer
REM take out the RAM card
REM turn on Pocket computer
FILES "F:"
--> Bad drive name

REM turn off Pocket Computer
REM put the RAM card back into E500
REM turn on Pocket computer
FILES "F:"
--> you should see list of files

REM load file from F:
LOAD "F:PERIOD.221"

REM switch to PROG mode clicking green BASIC button
REM check that file was loaded
LIST

REM switch back to RUN mode clicking BASIC button again
REM execute the program
RUN
```
