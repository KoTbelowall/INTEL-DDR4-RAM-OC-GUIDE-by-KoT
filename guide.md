# INTEL DDR4 RAM OC GUIDE by KoT#3421


### **Introduction** 


This guide does not aim to be a comprehensive tutorial on DDR4 RAM overclocking, as there are already many such tutorials available on the internet. Instead, the purpose of this guide is to complement those existing resources and correct any errors that may be present. The guide will be updated over time. 
If you have any complaints, please contact me.



### **Understanding the goal** 


The available RAM OC guides are quite good, but they share the same problem. These guides are authored by people who are not concerned enough about stability. The main goal in RAM overclocking for competitive gaming is 100% stability, not just maximum performance and it is important to always keep this in mind. Although unstable RAM can give better avg fps/benchmark results, it is not suitable for us, as it can increase input lag, degrade smoothness and cause stutters. As a result, most gamers who attempt RAM overclocking end up with an unstable system. The aim of this guide is to address this issue. Once you've read all the guides/forums ([links at the bottom](https://github.com/KoTbelowall/INTEL-DDR4-RAM-OC-GUIDE-by-KoT/blob/main/guide.md#links)) and gained a basic understanding of RAM overclocking, you can use this guide to correct your timings and other flaws. You can also check your RAM config before and after this guide against each other, testing by feel/fps/etc.



### **RAM OC impact** 


Overclocking your RAM is worth considering, as it can lead to a [significant performance improvement](https://kingfaris.co.uk/blog/intel-ram-oc-impact). Even if your game's fps doesn't increase, you may experience better overall consistency, mouse responsiveness and smoothness.


## Physical setup


#### RAM cooling


Before you begin, it's important to understand that you can't overclock your RAM without proper cooling, since [the temperature changes can strongly impact the RAM stability](https://github.com/BoringBoredom/PC-Optimization-Hub#temperature) due to its capacitor-based structure.

1) Remove the heat spreaders if present, as this [significantly degrades the temperatures of the RAM](https://media.discordapp.net/attachments/898074377407574018/936765203243237386/unknown.png). 
2) Be sure to install one or more fans so that they blow over the RAM chips (even bad fans are better than no fans at all; 140mm is preferred; [example of temp reduction](https://media.discordapp.net/attachments/898074377407574018/1011084065409081355/unknown-114.png)).
3) Disable any RGB/lightning on your RAM as it generates heat and creates interference.


#### **Correct RAM installation**


1) Make sure that there is no dust/hair/etc in the DIMM slots, as well as on the RAM itself there is no any [dirt on the pins](https://cdn.discordapp.com/attachments/903249065226149959/1106262302484865154/image.png), because poor contact can degrade signal integrity = degrade RAM overclocking.
2) On most modern 4 DIMM boards, [the best slots for installing RAM are 2 and 4](https://media.discordapp.net/attachments/898074377407574018/951203012376936458/unknown.png?width=1440&height=599) (but you can always check the manual and sometimes see [hints on the motherboard itself](https://cdn.discordapp.com/attachments/903249065226149959/1102246713286197318/image.png)).
3) Proper installation of RAM sticks to each other; check how RAM is trained at different freqs (3200MHz+; 2-3 reboots at the same frequency), then write down these values and swap the RAM sticks with each other.
Do the same and compare the results (on the same freqs). The option where tRTLs differ by a smaller value (i.e. **67/68** vs 67/69 for example) is correct and you should use it. 


## **BIOS setup** 


- Disable unused RAM slots/PowerDown/Command Rate Support.

    - Disable SelfRefresh (highly recommend testing this; causes problems with rebooting)

- General rule: don’t touch unused or unknown timings/settings. 

   - Don't set unused timings to lowest possible, leave them at auto (also _sg/_dg/_dr/_dd sometimes bugged and mixed up).

- Always gear 1 (11th gen or higher).

- 100:133 can be easier for IMC and requires lower voltages, also can help push high freqs in some cases.

- Check different bios versions/microcode updates in terms of RAM OC, some versions will allow better freq/stability/cr1/etc.




## **Timing things and formulas:**

**Disclaimer**: While some formulas may be wrong (tRAS for example)/”meme” for some people, they are proven over time and work best after all. I don’t recommend going below recommended/possible values. Overtight means the timing value that comes right after the value that had errors in RAM stress tests.



- **tCL**
    - doesn't affect performance much

    - affects tRTL

    - i don't recommend lowering it if you are increasing the voltages too much to do so

- **tCWL** 
    - tCWL=tCL (or tCWL=tCL-1/+1 if tCL is uneven)

    - possible values: 9/10/11/12/14/16/18/20

    - tRDWR dependent

- **tRCD/tRP**
    - don't overtight these on b-die

    - temperature sensitive

    - affects performance a lot

- **tRAS**
    - tRAS=tCL+tRCD+4

- **Command Rate**
    - use CR1 (MSI: Real 1N) if possible (which can't be said about dual rank at high frequencies, there you most likely want cr2 in most cases)

    - affects overall stability/mouse feeling/smoothness a lot

    - 3800cr1>4200cr2 / 4000cr2>3200cr1 in terms of performance

    - affects tRTL

- **tWR/tRTP**
    - tWR=2*tRTP (tRDPRE=tRTP, tWRPRE=4+tCWL+tWR)

    - don't overtight these

    - recommended tWR values: 20/24/28

    - can affect smoothness; doesn't affect performance much

- **tRRD_S**
    - tRRD_S=4 for max RAM perf (if tFAW=16)

    - affects performance/RAM temperature a lot

    - setting this to 5 and higher is a huge RAM nerf

    - can “hide” instability if set too high (because ram is getting too slow)
    
    - can't be lower than 4

- **tRRD_L**
    - recommended values: 6-8

    - can't be lower than 4

- **tFAW**
    - tFAW=16 for max RAM perf

      - i suggest to test higher values (20-40) after RAM tuning with tFAW=16

    - affects performance/RAM temperature a lot (if tRRD=4)

    - can “hide” instability if set too high (because ram is getting too slow)
   
    - can't be lower than 16

- **tRFC**
    - start point: add +15-30ns to the minimum boot value and round up to 16

    - see [tRFC list by Reous](https://cdn.discordapp.com/attachments/903249065226149959/1101086029097734174/tRFC_v26.png)

    - don’t overtight this (especially don't go lowest "stable" on b-die)
    
- **tREFI**
    - any value applies, however i recommend these:

      - 16256/32512/65024 (tREFIx9=127)
      - 32640/43520/52224/65280 (tREFIx9=255)

    - temperature sensitive

    - i strongly don't recommend going above 65k

- **tREFIx9**
    - tREFIx9=8xtREFI/1024 ([from intel datasheet](https://media.discordapp.net/attachments/898074377407574018/1075947541708931113/image.png))

    - 127 or 255 mostly

- **tCCD_L**
    - tCCD_L=tRDRD_sg=tWRWR_sg(=_dr=_dd)

- **tCCD_S**
    - tCCD_S=tRDRD_dg=tWRWR_dg=4 (setting this to 5 and higher is a huge RAM nerf)

- **tRDWR**
    - start point: auto-2

    - recommended values: 8/10/12/14/16/18/20/etc 

    -  _sg=_dg=_dr=_dd

    - tCWL dependent (inverse relationship, higher tRDWR allows lower tCWL in a nutshell)

    - don't overtight this

- **tWTR_L**
    - recommended values: 8-14

    - doesn't affect performance much

    - tCWL dependent

    - change it via tWRRD_sg=6+tCWL+tWTR_L

- **tWTR_S**
    - recommended values: 4-6

    - doesn't affect performance much

    - tCWL dependent

    - change it via tWRRD_dg=6+tCWL+tWTR_S

- **tIOL**
    - if you're on the 10th gen or lower

    - don't overtight this

- **tRTL**
    - if it differs by more than 2, you are probably unstable

- **t_MR** (if MSI motherboard)
    - t_MR = t (for example: tCWL=tCWL_MR)


## **RAM Stress Testing**

For additional stability i highly recommend running RAM stress tests with GPU load to create extra heat. You can use [Furmark](https://geeks3d.com/furmark/) or [MSI Combustor](https://www.geeks3d.com/furmark/kombustor/) for this. Recommended GPU temperatures for such testing are 60-70c. To create even more stress and higher temperatures, you might consider lowering the RAM fan(s) speed in addition to the GPU load.



## **Useful info/quotes:**

- if you are going to use cr2 if possible make cr1 stable first and only then use cr2
- stability>frequency>timings
- stable without fan > stable only with fan
- XMP doesn't guarantee stability
- [IMLC GUI](https://github.com/FarisR99/IMLCGui/) is trash
- before you start doing any RAM OC, get a fan to blow over them, either with zipties or other methods, best RAM OCs are gained from lower temperatures
- 1 degree C temperature lower means much more than you think because: 1. it applies through time, 2. it applies as a single measure of temperature currently and 3. it applies at 0.1% lows (or 99% edge case load) not just in one state of PC load(idle)
what this means is that u do ( TEMPERATURE GAIN ) *  ( TEMPERATURE GAIN ) *  ( TEMPERATURE GAIN )  to get real temp reduction (current/load/through time) so temp_diff ^ 3 = real temp gain from observing temp reduction property
- 1 degree C lower RAM temperature is worth ~ 15-30% in performance (latency/smoothness/fps), depending on how good your RAM OC/cpu OC is
- tRC/tRCD/tRAS/tRP are worth far more than tCL for RAM OC
- AIDA is a dogshit scam tool for CES reviewers, use IMLC(Intel Memory Latency Checker) and read the manual, its worth it
- IMLC loaded latency is what matters (up to ~ 10GB/s bandwidth used) as well as L2 hit/L2 miss latency(uncore dependant)
- AIDA latency numbers are useless metric for anything in real life and due to broken benchmark [it doesn't even reflect changes for all timings](https://www.youtube.com/watch?v=GHfXRUPLj1I)
- true knowledge/info can only be found in scientific papers/research
- everything you read on any overclocking forum or reddit is as wrong as it can possibly be
- RAM latency and RAM temperature are the biggest bottlenecks in modern computer systems (by far, like 1:30000000000 over anything else)
- when tuning RAM timings aim for higher fps backed by better consistency in ultra high FPS menu, this translates into better responsiveness/smoothness, even if you lose a bit ns of latency
- dedicate 2 weeks of your life to overclock your RAM properly,do it for all RAM timings, most people cba to do it, but it's worth it far more than you can imagine (OC RAM benchmark vids on yt dont show u latency/smoothness of proper RAM OC related to input)
- tightening RAM timings is very hard, some timings may be lower but perform worse, some might be higher but also worse, test across different loads (ultra high menu fps, ingame, high cpu load, high gpu load,memtests)
- your tight RAM timings might have error correction, higher timings perform better and have no stutters due to no error correction
- finding the proper RAM timings takes time, but worth it in the end
- measuring things can be done based on how it feels,but make sure you have proper monitor(low input lag/response time/high Hz) and clear mental state without any bias before doing so, confirm with actual benchmarks!
- Don't chase aida lowest latency number, tuning RAM is much more complex than that, you need to aim to find the best out of lowest latency possible without error correction AS WELL as without any clock/timing correction.
- Clock/timing correction of RAM happens when you drop some timing far below than its supposed to be, tFAW (Four activate window) or tRAS in most of the cases,just because it boots, works and gives you some lower latency in aida, doesnt mean its actually better in game, if you are on win10 use liblava fps example demo or something with really high FPS to see how reducing timings affects your FPS, look at 0.1% 1% lows, and frame consistency, a lot of people dumped their tRAS/tFAW just to chase 0.3ns RAM latency reduction, but having proper timings derived out of formulas will give you far better consistency/smoother feeling
- stress test and actual real memory access is different, different ways of accessing, temps etc, something with the cells too



## **Theories to discuss/test (for fps benchmark or something):**

1) [different tREFIx9/tREFI values](https://cdn.discordapp.com/attachments/867774526196678656/1145338856103755776/image.png) (tREFIx9=(tREFI+1)/1024)
2) [read to write burst gap](https://media.discordapp.net/attachments/903249065226149959/1098881770365132800/image.png)
3) cr2>cr1 on bad 4 DIMM boards (even if you can run cr1 with “no problems”)
4) 100:100 vs 100:133 in terms of mouse feeling/smoothness
5) stability vs row hammer (prevention)/memory scrambler 


## **Links:**

#### RAM OC guides:

* https://github.com/integralfx/MemTestHelper/blob/oc-guide/DDR4%20OC%20Guide.md#table-of-contents

* https://cdn.discordapp.com/attachments/898074377407574018/1094783462755536926/DDR4_Memory_Guide_V1.0.0.pdf

#### Forums:

* https://forums.overclockers.ru/viewtopic.php?f=4&t=578879

* https://www.hardwareluxx.de/community/threads/intel-ddr4-RAM-oc-thread-guides-und-tipps.1230518/

* https://www.overclock.net/threads/official-intel-ddr4-24-7-memory-stability-thread.1569364/

#### Other/useful info:

* https://calypto.us (check RAM section)

* https://github.com/sieger/handbook/ (check RAM section)

* https://www.systemverilog.io/

* https://docs.google.com/document/d/1JSqt9TP_VeihjAXtfq7LDQ9vmakzaYqJP48rnVC9rzo/mobilebasic (RAM IC rating by prev)

* https://www.anandtech.com/show/3851/everything-you-always-wanted-to-know-about-sdram-memory-but-were-afraid-to-ask

* http://www.softnology.biz/pdf/DDR4-For-Dummies-4thEd-4AA6-6217ENW.pdf

* https://www.youtube.com/watch?v=105IJiGbGsg (by buildzoid; check other “ram timings explained” vids)

* https://github.com/RAMGuide/TheRamGuide-WIP-/blob/main/Advanced%20Timings.md 


#### Papers/research:

* https://cdn.discordapp.com/attachments/898074377407574018/1095863260537966642/DDR4_Spec_JESD79-4C.pdf (JEDEC)

* https://research.ece.cmu.edu/safari/thesis/dlee_dissertation.pdf

* https://people.inf.ethz.ch/omutlu/pub/adaptive-latency-dram_donghyuk_hpca15-talk.pdf

* https://arxiv.org/pdf/2005.13121.pdf (row hammer)

* https://www.mdpi.com/2072-666X/10/9/590

* https://www.pdl.cmu.edu/PDL-FTP/NVM/chargecache_low-latency-dram_hpca16.pdf

* https://research.ece.cmu.edu/safari/pubs/kim-isca14.pdf

* https://www.jedec.org/sites/default/files/JS_Choi_DDR4_miniWorkshop.pdf

* https://cdn.discordapp.com/attachments/1075405865974243378/1085482975141036062/ieeetc65-1.pdf

* https://cdn.discordapp.com/attachments/1075405865974243378/1085487999107739658/mutlu_dram-refresh_extreme-scale-computing14.pdf

* https://www.micron.com/-/media/client/global/documents/products/technical-note/dram/tn4007_ddr4_power_calculation.pdf

* https://users.ece.cmu.edu/~omutlu/pub/dram-access-refresh-parallelization_hpca14.pdf





