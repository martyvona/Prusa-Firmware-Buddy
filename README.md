# Prusa MK4/S High Temp Mod 450°C Max
Does your Prusa MK4 have an unequenchable thirst for heat? 
Want to print PPS and other >300°C+ or even >400°C filaments? 

If so, you've found the right github repo!

This is modified firmware (currently tracking 6.3.0) that does two things:

1. Changes the hotend to one that uses a PT1000 sensor connected directly to the love board. No resistor swapping or amplifier boards or any other nonsense, just two wires spliced directly to the thermistor connector.
2. It does so **with no loss in temperature resolution**.

   Using the stock NTC hotend thermistor, we get a resolution of about 0.1°C.
   Normally, switching to a PT1000 with a 1K pullup (this is what the xBuddy board uses) results in considerably less, about 0.44°C resolution.
   
   This firmware has been modified to use **256x oversampling** for 2 additional bits of resolution, allowing for 14 effective bits on the otherwise 10-bit ADC.

   These are real bits with real information, oversampling is well understood and it works. It works so well in fact, that your MK4 already uses oversampling. This just makes it use even more of it. As near as I can tell, Prusa didn't do this themselves because there was no point, 0.1°C resolution was plenty and beneath the voltage      reference variation one might see, not because there was any limitation preventing it.

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
