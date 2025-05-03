# Prusa MK4/S High Temp Mod 450°C Max
Does your Prusa MK4 have an unequenchable thirst for heat? 
Want to print PPS and other >300°C+ or even >400°C filaments? 

If so, you've found the right github repo!

This is modified firmware (currently tracking 6.3.0) that does two things:

1. Changes the hotend to one that uses a PT1000 sensor connected directly to the love board. No resistor swapping or amplifier boards or any other nonsense, just two wires spliced directly to the thermistor connector.
2. It does so **with almost no loss in temperature resolution**.

   Using the stock NTC hotend thermistor, we get a resolution of about 0.1°C.
   Normally, switching to a PT1000 with a 1K pullup (this is what the xBuddy board uses) results in considerably less, about 0.5°C resolution.

   The MK4 already uses something called oversampling to squeeze out an extra 2 bits of resolution. The great thing about oversampling is it works.
   In fact, **oversampling is like violence: if it's not working, just use more of it**.
   
   With that in mind, this firmware has been modified to use **64x oversampling** instead of the stock 16x for a resolution of about **0.2°C** resolution. This is still plenty, and close to the tolerance of the voltage reference anyway.
   
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
I advise against PEI, as cool as it seems. Aside from you needing to use a release mechanism to prevent it from fusing with the PEI print bed like a thick layer of gluestick... you really just can't print PEI on a MK4.

The limiting factor isn't the temperature, or bed adhesion. It's the magnets. 
PEI warps so hard that it will overcome the pull stength of the print bed magnets to warp while **lifting the steel sheet, still fully adhered to the print, up off the bed with it**.

So printing PEI will likely require more ...drastic... modifications. Stay tuned!😝
