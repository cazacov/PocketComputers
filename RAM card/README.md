# RAM Card for Sharp Pocket PC-E500

256 KB RAM card with battery.

![Overview](./_img/card.jpg?raw=true)

[Download schematic](./ram-card-256k/ram-card-256k.pdf)

## PCB

PCB: 41.9 x 54.1 x 0.8 mm

![Address lines](./_img/pcb.jpg?raw=true)

## Bill of Materials

| Reference | Part | Size | Comments |
| --------- | ---- | ---- | -------- |
| R1,R2 | 47K | 1206 | Pull resistor |
| R3 | 470K | 1206 | Pull resistor |
| C1 | 330 nF | 1812 | Decoupling capacitor |
| D1 | RB160M | SOD-123 | Schottky diode |
| D2 | 1N4148W | SOD-123 | Fast switching diode |
| U1 | HC138 | SOIC-16 | Address decoder |
| U2, U3 | KM681000BLG | SSOP-32 | 128K x 8-bit low power CMOS static RAM |

## Usage

Power of Pocket Computer, insert card, power on.

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

To use card as a RAM disk **F** type:

```
MEM$="S1"
```