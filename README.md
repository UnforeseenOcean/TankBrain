# TankBrain
Official repository for TankBrain, a replacement board for Academy and other motorized vehicle models

# What is this?
This is an Arduino-compatible* board with remote controller that replaces either the old 30/40MHz band remote control or wired remote on models from Academy Plastic Models or other companies.
Currently it supports Academy's wired motorized tank models (the benchmark being their ROK K1A1 tank model), but with some support it should be easy to make it support nearly all models.

\*: Arduino-compatible in this context means "Arduino IDE compatible". The board in no way, shape or form can support peripherals made for Arduino Uno and other boards.

# Goals
- To create a universal board that fits into most models, including some toy vehicles (such as tanks or cars)
- To make a firmware that handles most functions called by signals through 433MHz ASK/OOK module

# Information
This board currently uses GoodRF SRX887 and STX887 pair, which has a good range of operation with least amount of latency (due to it not containing any signal-to-binary conversion) from the online reviews.

The operating state table is as follows:
```
ABCD (AIN1,AIN2,BIN1,BIN2)
0000 (Stop)
0001 (Backwards Left Strafe)
0010 (Right Strafe)
0011 (Invalid/Unused)
0100 (Backwards Right Strafe)
0101 (Backward)
0110 (Right Turn In Place)
0111 (Invalid/Unused)
1000 (Left Strafe)
1001 (Left Turn In Place)
1010 (Forward)
1011 (Invalid/Unused)
1100 (Invalid/Unused)
1101 (Invalid/Unused)
1110 (Invalid/Unused)
1111 (Brake)
```
Simulation for engine starting and firing is handled by switching the movement state through this table:
```
1010 (Start of "Engine start" movement set)
0101
1010
0101
1010
0101 (Start of "Fire" movement set)
1010
0101
1111
0000 (End)
```
There is a plan to add support for external sound modules (DFPlayer Mini / Serial MP3 player modules)

The board needs some revision and quality/function check, as it has not been made yet. However this is what the board could look like if the current design is made:
![IMG1630331590](https://user-images.githubusercontent.com/11834016/131350370-ea361070-b381-45ae-9f61-9ed486dc4f7a.png)
![IMG1630331605](https://user-images.githubusercontent.com/11834016/131350399-ea78d039-bd0e-4c0c-a015-98a4eade9e0e.png)

Believe it or not this is the second big revision -- the first one was... not good.

# Credits
Pololu - DRV8833 circuit design
