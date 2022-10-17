# Sharp Pocket Computer PC-E500

## Internal RAM upgrade from 32K to 128K

The internal RAM (HM62256A) can be easily replaced with 128K CMOS static RAM.

1. Solder out 32K chip
2. Solder the new chip on the same contact pads. The old chip had 28 pins while the new one has 32. Pins 1, 2, 31 and 32 stay not connected (yet).
3. Connect pin 32 to VCC. The VCC voltage can be taken from a contact pad on PCB or from the pin 30.
4. Connect pin 31 to A15 address line
5. Connect pin 2 to A16 address line

Signals A15 and A16 can be found on contact pads near CPU SC62015B01.

Overview:
![Overview](./_img/ram-upgrade.jpg?raw=true)

Address lines
![Address lines](./_img/address-pads.jpg?raw=true)

**M5M51008DFP-55HI** 128K RAM chip
![Address lines](./_img/ram-chip.jpg?raw=true)

