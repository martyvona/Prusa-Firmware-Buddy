# Prusa MK4/S High Temp Mod 450°C Max
Does your Prusa MK4 have an unequenchable thirst for heat? 
Want to print PPS, PEI, and other >300°C+ or even >400°C filaments? 

If so, you've found the right github repo!

This is modified firmware (currently tracking 6.3.0) that does two things:

1. Changes the hotend to one that uses a PT1000 sensor connected directly to the love board. No resistor swapping or amplifier boards or any other nonsense, just two wires spliced directly to the thermistor connector.
2. It does so **with almost no loss in temperature resolution**.

   Using the stock NTC hotend thermistor, we get a resolution of about 0.1°C.
   Normally, switching to a PT1000 with a 1K pullup (this is what the xBuddy board uses) results in considerably less, about 0.5°C resolution.

   However, the ADC on the xBuddy is actually a 12-bit ADC, and being used in 12-bit mode, but the Prusa MK4 firmware simply discards the last 2 bits to make it compatible with the Marlin codebase it is based upon, which expects a 10-bit ADC value.
   Prusa then uses 16x oversampling to regain those lost 2 bits.
   
   This branch, besides switching out the hotend thermistor for a PT1000, modifies the Marlin so it can support a 12-bit ADC, and keeps Prusa's 16x overssampling.

   This gets us a full 14-bits of real resolution (oversampling is not a gimmick, it really gets you better accuracy/resolution at the trade off lower sampling rate)!

   And as any good engineer will tell you, **bits are like violence: if it's not working, just use more**.
   
   Ultimately, this modification gets us a resolution of about **0.2°C** resolution with a PT1000 with no side effects or downsides. While still slightly less than the 0.1°C with the stock hotend thermistor, it's still plenty.
   
## Hardware
*Note: none of these are affiliate links, just the raw amazon links. These are simply what I used, but certainly not the only options.*

### Necessary hardware modifications:
- Grab a PT1000 thermistor like [this one](https://www.amazon.com/dp/B09TT1NHSY) and splice it onto the wires of the old thermistor connector.
- Swap out your nextruder heater block for a nickel-plated solid copper one like [this](https://www.amazon.com/POLISI3D-Temperature-Compatible-Nextruder-Accessories/dp/B0CZDL8LTW)
- Brass nozzles can no longer be used. You'll need to switch to hardened steel/copper/tungsten/etc.
  - I recommend using a bimetal heatbreak adapter like [this one](https://www.amazon.com/POLISI3D-Heatbreak-Compatible-Nextruder-Heaterblock/dp/B0CW91V1TJ/) and using whatever nozzle you like (that isn't brass).
 
That's it! Well, and you'll have to [modify](https://help.prusa3d.com/article/flashing-custom-firmware-core-one-mk4-s-mk3-9-s-mk3-5-s_814967) your xBuddy board to accept custom firmware if you haven't already. 
Make the swaps, then flash this firmware (you can always go back to stock if things aren't working for you) and print away!

I highly recommend PPS for your first try. It's relatively easy to print and fairly forgiving. It is prone to warping so be sure to use a wide (5-10mm or even more) brim if your print has corners or other sharp angles on the bottom.

PEI is harder but possible. Be sure to use a release agent (hot glue stick, magigoop, some other adhesive) to prevent the PEI from fusing with the PEI print surface.
The primary issue wth PEI is its a drippy dribbly boi. And for larger objects, it can warp hard enough that it will lift the steel sheet off the print bed. 
Meaning it can overpower the strength of the magnets holding the steel sheet onto the bed. In those cases, printing on something like a glass sheet is non-optional. 
