# Home theater calibration

This is a work-in-progress document regarding my upcoming journey to get the
most out of my so-called "Home theater".

## Goal

My home theater is a small room, with an (open) double door into our main
living room. While I am not able to make it a 100% dedicated home theater room, I
want to make the most out of it, while also making it a integrated part of our
primary living space. This means I am limited regarding the placement of
speakers, couch and subs, in addition to installing sound treatments.

Another goal is to make a good balance of time/effort and result. In other
words, I want my room to sound really good, but I do not want to spend endless
hours chasing the near impossible.

## Prerequisite

1. Make this document :-)
2. Read *nathan_h* excellent [reply](https://www.avsforum.com/posts/63725174/) to
   my post about bass management
3. For each step in this document, write a detailed plan on what to do,
   measurements to preform, and goal of the step.

## Step 1 - Placement of subs

I have to subwoofers:
- Arendal Sound 1723 Subwoofer 1S
- Arendal Sound 1723 Subwoofer 1.5 (Legacy product)

I will abbreviate those to Sub1S and Sub1.5 in this document.

### Goal

While Sub1S will remain where its located, I will find the optimal placement for
Sub1.5 so they have a combined frequency response which will have no dips and
preferably no peaks.

### Plan

1. Seal the port on Sub1.5
2. Put the Sub1.5 on a [moving
   trolley](https://www.biltema.no/en-no/car---mc/workshop-equipment/lifting-equipment/trolleys/moving-trolley-200-kg-2000040831)
3. Attach a active speaker to the miniDSP, port 4.
4. Ensure Sub1.5 is connected to miniDSP port 2, and Sub1S is connected to miniDSP port 1.
5. Note the gain setting on each sub.
6. Connect the PC to miniDSP via USB.
7. Choose a slot on the miniDSP with no filters, settings, crossover, etc.
8. Note the volume on the PC, the input gain on miniDSP.
9. Mute/Disable Sub1.5/Output 2 in miniDSP
9. Play sweep for Sub1S from 20-200Hz via REW, using the active speaker as
   acoustic timing reference
10. Mute/Disable Sub1S/Output 1, unmute/enable Sub1.5/Output 2 in miniDSP
11. Repeat until all possible locations are measured:
    1. Move Sub1.5 to a new location
    2. Note the location and orientation in a document
    3. Play sweep for Sub1.5 from 20-200Hz via REW, using the active speaker as
       acoustic timing reference
12. In REW, I use the "Alignment tool" between the first measurement and all the
    rest to figure out the best location for Sub 2. The best location is where
    there are no/fewest dips/nulls and no/fewest negative summations.
13. Physically place the sub in the optimal position, enter the delay in
    miniDSP and take a new measurement to verify REWs calculations.

### Notes

- Mic (UMIK-1) volume in Windows: 80%
- Sound card (miniDSP) volume in Windows: 90%
- REW Pink Random Noise and volume for sweeps: -15,00 dBFS
- Master volume in miniDSP control panel (input): -5dB
- Gain on Arendal Sound Subwoofer 1.5: +6dB (ca)
- Gain on Arendal Sound Subwoofer 1S: +6.0dB
- No crossover, PEQ, delay, gain in miniDSP, slot 3 (which is used for measurements)

With the settings above, the SPL in MLP:
- Sub1.S: 100-110dB depending on position
- Sub1S: 100dB
- Active speaker: 72dB

### Files

- [20241230 - Best position of Sub1_5.mdat](https://github.com/SitronNO/HT-calibration-plan/blob/main/Step%201/20241230%20-%20Best%20position%20of%20Sub1_5.mdat) - REW Measurements of every position of Sub1.5 from MLP
- [20241230 - Best position of Sub1_5 - With alignments.mdat](https://github.com/SitronNO/HT-calibration-plan/blob/main/Step%201/20241230%20-%20Best%20position%20of%20Sub1_5%20-%20With%20alignments.mdat) - Same as above, but with some manual REW calculations regarding alignments (time delay) of Sub1.5

### Conclusion

Without time alignment, these seems like the best options:
- Pos 11: Sub1.5 position is left back, back-panel against back wall
    - Adding a 14ms delay gives nice response. PP: 112dB - 93dB = 19dB
- Pos 3: Right of couch, back against right wall
    - About 18ms. PP: 113dB - 85dB = 28dB

**Position 11 it is!**


## Step 2 - Multi-Sub Optimizer (MSO) and miniDSP

### Goal

By utilizing [Multi Sub Optimizer](https://www.andyc.diy-audio-engineering.org/mso/html/index.html) and miniDSP I can try to get the best response for both my MLP, and other listening position - while maintaining a high SPL for my subs.

### Plan

1. Attach a active speaker to the miniDSP, port 4.
2. Ensure Sub1.5 is connected to miniDSP port 2, and Sub1S is connected to miniDSP port 1.
3. Note the gain setting on each sub.
4. Connect the PC to miniDSP via USB.
5. Choose a slot on the miniDSP with no filters, settings, crossover, etc.
6. Note the volume on the PC, the input gain on miniDSP.
7. For each listening position:
    1. Mute Sub1S, unmute Sub1.5
    2. Run a sweep from 10-300Hz in REW, using the active speaker as a acoustic timing reference
    3. Unmute Sub1S, mute Sub1.5
    4. Run a sweep from 10-300Hz in REW, using the active speaker as a acoustic timing reference
8. In REW, use "A + B" trace arithmetic function to verify the measurements. [Reference in MSO manual](https://www.andyc.diy-audio-engineering.org/mso/html/reference-manual/getting-started-mso.html)
9. Follow [Getting started with MSO](https://www.andyc.diy-audio-engineering.org/mso/html/reference-manual/getting-started-mso.html) until the "Configuration Wizard" is completed.
10. Follow and copy the steps from Dave Boswell's [Tutorial video for MSO version 2](https://youtu.be/yrrE6Ygh67Q)
11. Apply the config from MSO into miniDSP
12. Take measurements to verify which config gives the best response and sound.

### Notes

- In MSO, I have called the project "New year"
- Mic (UMIK-1) volume in Windows: 80%
- Sound card (miniDSP) volume in Windows: 90%
- REW Pink Random Noise and volume for sweeps: -15,00 dBFS
- Master volume in miniDSP control panel (input): -10dB
- Gain on Arendal Sound Subwoofer 1.5: +6dB (ca)
- Gain on Arendal Sound Subwoofer 1S: +6.0dB
- No crossover, PEQ, delay, gain in miniDSP, slot 3 (which is used for measurements)
(All settings as in step 1, but reduced "Master volume" in miniDSP by 5dB)

### Files

- [20241230 - MSO measurements.mdat](https://github.com/SitronNO/HT-calibration-plan/blob/main/Step%202/20241230%20-%20MSO%20measurements.mdat) - REW measurements for MSO: Sub1S and Sub1.5 individually, from LLP, MLP and RLP.
- [New year.msop](https://github.com/SitronNO/HT-calibration-plan/blob/main/Step%202/New%20year.msop) - MSO project file with the config and calculations
- [New Year - Config 4 - Multistage](https://github.com/SitronNO/HT-calibration-plan/tree/main/Step%202/New%20Year%20-%20Config%204%20-%20Multistage) - The filter report from MSO, and Biquads for miniDSP
- [New Year - Config 5 - Higher SPL penalty](https://github.com/SitronNO/HT-calibration-plan/tree/main/Step%202/New%20Year%20-%20Config%205%20-%20Higher%20SPL%20penalty) - The filter report from MSO, and Biquads for miniDSP
- [20250104 - After MSO New year config.mdat](https://github.com/SitronNO/HT-calibration-plan/blob/main/Step%202/20250104%20-%20After%20MSO%20New%20year%20config.mdat) - REW measurments from MLP, LLP and RLP via miniDSP, with MSOs "New Year" config 4 and 5

### Conclusion

## Step 3 - Fronts: Placement and plugged or vented?
## Step 4 - Anthem ARC
## Step 5 - Final measurements
