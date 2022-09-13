# RYZEN-RAM-OC-Guide

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Basics](#basics)
  - [Frequency, Latency and True Latency](#frequency-latency-and-true-latency)
  - [Primary, Secondary and Tertiary Timings](#primary-secondary-and-tertiary-timings)
    - [Primary](#primary)
    - [Secondary](#secondary)
    - [Tertiary](#tertiary)
- [Limiting Factors](#limiting-factors)
  - [Motherboard](#motherboard)
  - [Integrated Memory Controller (IMC)](#integrated-memory-controller-imc)
  - [Printed Circuit Board (PCB)](#printed-circuit-board-pcb)
  - [Integrated Circuits (ICs)](#integrated-circuits-ics)
    - [Density](#density)
    - [Logical Ranks](#logical-ranks)
    - [Voltage](#voltage) 
    - [Temperature](#temperature)

* Units:
  * Hertz: It's a unit of frequency used in the SI, it is equivalent to one cycle per second.
  * Transfer: It refers to a quantity of data that can be transferred in a second regardless of frequency. 
  * Celcius: It's the unity of temperature from the SI alongside Kelvin.

* Prefixes:
  * Nano (n): 10<sup>-9</sup>
  * Mega (M): 10<sup>6</sup>
  * Giga (G): 10<sup>9</sup>
  

# Basics:
  This section will go through the minimum knowledge required to overclock RAM. 

## Frequency, Latency and True Latency:

* RAM frequency is measured in megahertz (MHz), having your RAM operating at a higher frequency means more cycles per second, which will give you some extra performance. Having very high frequencies can make your RAM unstable and it may crash your PC.
  * **Advanced tip:** The only case witch lowering the clock will result in better performance is in tREFI since tREFI measures the timing between RAM refreshes. While your RAM refreshes, you can't write or read anything on it, so you want to make that time gap as little as possible.

* RAM Timings are the latency between various operations inside a RAM chip, having low latencies will result in better performance, so keep them as low as possible. Having very low timings will also make your RAM unstable and may result in crashes. 
  * The main timing of your ram is called CL, tCL or CAS Latency, it measures the delay between the **READ** command and the moment the data is available, this interval is specified in nanoseconds.
  
* When you buy a RAM stick, sellers usually show their transfer rate and their tCL. For example, "DDR4-3000 CL15" (3000 MT/s and tCL of 15ns) and "DDR4-3600 CL18" (3600 MT and tCL of 18ns).

* Common mistakes:

  * People usually refer to DDR4-3000 as 3000 **MHz**, but they are only 1500 **MHz**, this happens because we use DDR RAM, DDR stands for Double Data Rate, which transfers data in the rising edge of the clock and the falling edge of the clock, so the real frequency of the RAM is half the number of transfers it makes in a second. So a DDR4-3000 operates in 1500 **MHz (Megahertz)** and will transfer 3000 **MT/s (MegaTransfers per second)** of data.

  * "DDR4-3000 CL15", has a lower tCL, but "DDR4-3600 CL18" has a higher frequency, so it's necessary to evaluate how they compare.
  
  To calculate the true latency measured in nanoseconds (ns) of a given RAM's transfer rate and tCL, just use the formula: `2000 * timing / frequency`
  * DDR4-3000 CL15 = `2000 * 15 / 3000 = 10 ns`.
  * DDR4-3600 CL18 = `2000 * 18 / 3600 = 10 ns`.
  * Through this calculation it's demonstrated that they have the same RAM latency, and thus, the same performance.
  
## Primary, Secondary and Tertiary Timings:
    
* RAM timings are split into 3 categories, primary, secondary and tertiary
* Primary and secondary timings will affect latency and bandwidth, while tertiary timings affect only bandwidth

![](Images/zentimings.png)

Red (P) = Primary Timings.

Green (S) = Secondary Timings.

Blue (T) = Tertiary Timings.


### Primary

* **tCL** (Column Address Strobe): **CAS** , is the first timing listed on every memory kit.
  * measures the delay between the **RD** (read) command and the moment the data is available, this interval is specified in nanoseconds. 
* **tRCD** (Row Address to Column Address Delay): this is the second timing listed on every memory kit.
  * measures the delay between opening a row of memory and accessing columns within it.
  * Usually is divided into tRCDWR and tRCDRD
* **tRP** (Row Precharge Time): this is the third timing listed on every memory kit.
  * measures the delay between issuing the **PRE** (precharge) command and opening the next row.
* **tRAS** (Row Active Time): is the fourth timing listed on every memory kit.
  * measures the delay between a row **ACT** (activation) command and issuing the **PRE** (precharge) command.
  
### Secondary

* **tRFC** (Refresh Cycle Time): this is the only secondary timing with a three-digit number.  
  * measures the delay between two refresh cycles in nanoseconds(ns).

### Tertiary

* **tREFI** (Refresh Interval): is the tertiary timing with a five-digit number.
  * measures the time that is needed to refresh.

# Limiting Factors:  
  This section will go through components that will limit your overclocking capacities. 
 
## Motherboard
* Always prefer motherboards with 2 DIMM slots, they will let you achieve higher frequencies. However, entry-level motherboards, which usually feature 2 DIMM Slots may not overclock as well thanks to their low-quality PCBs.
* While using motherboards that use daisy chain (4 slots, usually), 2 sticks are preferred, if you use 4 sticks the performance will be impacted // ver o video do buildzoid
* Motherboards with T-topology will overclock better with 4 sticks equipped, using 2 sticks will not cap your overclocking capability that much as in a daisy chain with 4 slots. 
 
## Integrated Memory Controller (IMC)
IMCs are responsible to read and write and refresh DRAM.

* **Zen** and **Zen+** IMC won't let you hit high frequencies since they have a "bad" IMC, on the other hand, **Zen2** and **Zen3** IMCs are much better as you can see in the next table.

Expected memory frequency range for 2 single-rank DIMMs, with just the IMC bottleneck:
 
| Ryzen |                    Expected Speed (MT/s)                    |
|:-----:|:-----------------------------------------------------------:|
|  Zen  |                         3000 - 3600                         |
| Zen+  |                         3400 - 3800                         |
| Zen2  | 3600 - 3800 `(1:1 MCLK:FCLK)` <br/> 3800+ `(2:1 MCLK:FCLK)` |
 
With more DIMMs and/or dual-rank DIMMs, the expected frequency may be lower.

Terminology:
   
* GDM: Geardown mode, it will round your tCL if it's odd.
  * If you run DDR-3000 CL15 with GDM enabled, the tCL will be rounded to 16.
    * In terms of performance: GDM disabled > GDM enabled.
   
* MCLK: Memory clock, for example, DDR4-3000, the MCLK is 1500MHz.

* FCLK: Infinity Fabric clock.

* UCLK: Unified memory controller clock. 
  * If FCLK and MCLK are synchronized (1:1), `UCLK = MCLK`
  * If FCLK and MCLK are desynchronized (2:1), `UCLK = 1/2 * MCLK`. 
    * desynchronizing FCLK and MCLK usually is a bad idea.
 
* SOC voltage, is the voltage of the IMC. 
  * IMCs can degrade with high SOC voltages and higher temperatures. 
  * Higher voltages may cause instability.

| SOC | Daily Voltage (V) | Extreme Voltage (V) | 
|:---:|:-----------------:|:-------------------:|
|     |   1.00V ~ 1.20V   |    1.20V ~ 1.25V    |
  
It's not recommended to leave SOC voltage on auto, the range should be around 1.00V and 1.20V. Higher values aren't encouraged but can be acceptable and even necessary to stabilize memories with higher capacities and stabilize FCLK. 
  
If your SOC voltage is too high (1.2V-1.25V), it can also cause memory instability.  

* **(Zen2 only)** VDDG: Infinity Fabric voltage.
  * Needs to be at least 40mV under SOC voltage since it's derived from SOC voltage.  

 
# Printed Circuit Board (PCB)

// ver https://www.youtube.com/watch?v=ZJDXsoYKZaY

* A0: 
  * JEDEC stock PCB for DDR4-2133.
  * The favourite PCB for extreme overclocking.
  * Aways single rank (only one side of the PCB will have ICs).
* A1:
  * JEDEC stock PCB for DDR4-2400.
  * Not very popular in the overclocking community, since it's rarely used on high-end RAM kits.
* A2/A3:
  * JEDEC stock PCB for DDR-2666.
  * A good PCB, usually found in RGB RAM kits.
* B1:
  * JEDEC stock PCB for DDR4-2400.
  * Not good at overclocking.
  * Usually dual-rank (ICs on both sides of the PCB).
* B2:  
  * JEDEC stock PCB for DDR4-2666.
  * Not good at overclocking.
  * Usually dual-rank (ICs on both sides of the PCB).
* C0:
  * JEDEC stock PCB for DDR-2400 with bigger ICs.  
  * Little is known about its overclocking potential.

# Integrated Circuits (ICs)

Note: ICs usually are referred to as "dies"
 
* Knowing well your ICs will give you an idea of what to expect from your RAM.
* They are a wide variety of ICs which are made by Hynix, Micron, Nanya or Samsung which will perform different while overclocking.
  * Samsung B-die: The best ICs in the market, they will scale very well with voltage and will be able to achieve high clock speeds with tight timings
   
|         IC         | Expected Max Speed (MT/s) | Daily Voltage (V) | 
|:------------------:|:-------------------------:|:-----------------:|
|   Samsung B-die    |           5000+           |       1.50V       | 
| Hynix D-die (DJR)  |           5000+           |       1.50V       |
|    Micron E-die    |           5000+           |       1.45V       |
|   Samsung E-die    |           5000+           |       1.45V       | 
| Hynix C-die (CJR)  |           4133            |       1.45V       |
|   Samsung D-die    |           4000+           |       1.45V       |
| Hynix A-die (AFR)  |           3600            |       1.45V       |
  
## Density
  
* x8 configurations are faster than x16.
  * Since they have double the amount of banks and groups compared to x16 configurations. // ver https://www.youtube.com/watch?v=k6SIdxq2yxE) 
   
* Densities will determine how far your IC can go while overclocking.
  * Even having the same name, they can have different overclocking results thanks to their differences in density.
    * Micron Rev. B has 8Gb and 16Gb configurations, and the 16Gb version performs better.
      * This happens because having twice as many banks means that twice as many memory rows can be opened or closed at any time. That will save you time on RAS/RC/RCD (waiting for a closed row to open) or RP (waiting for a row to close to open another one) operations because they will be less often.
    
## Logical Ranks
  
* Single-rank sticks are used to clock higher than dual-rank sticks, but dual-rank sticks have the advantage of being able of using rank interleaving.

Rank interleaving allows the memory controller to parallelize memory requests, for example, you can write in one rank while reading or refreshing the other one.  
  
* Today on Zen3 platforms, newer BIOS and memory controllers support dual-rank better. So you may be able to make dual-rank sticks clock as high as single-rank, but you will also have the performance gains from rank interleaving.
* The downsides of dual-rank sticks are:
  * In older platforms, BIOS and memory controllers won't support rank interleaving very well.
  * As the total count of ranks in the system increases, the load of the memory controller will also increase, which will require a higher SOC voltage.   
    
## Voltage

* [JEDEC JESD79-4B (p.174)](http://www.softnology.biz/pdf/JESD79-4B.pdf) specifies that the absolute maximum is 1.50 V.
  > Stresses greater than those listed under “Absolute Maximum Ratings” may cause permanent damage to the device. This is a stress rating only, and functional operation of the device at these or any other conditions above those indicated in the operational sections of this specification is not implied. Exposure to absolute maximum rating conditions for extended periods may affect reliability.
* Even with the official value being 1.50V, the majority of the ICs cannot remain safe at this voltage, for example, Samsung C-die can start degrading with 1.35V. However, ICs like Samsung B-die have been observed with daily voltages of 1.5V for years. If you want to play it safe, research what voltages are safe for your IC, or just stick to 1.35V.
* On the majority of the ICs, tCL scales with voltage, which means that giving more voltage to the IC, will allow you to drop tCL, but tRCD, tRP and tRFC typically will not scale with voltage.
* Some bad ICs can also scale negatively with voltage, becoming unstable at higher voltages.
* Very high voltages can also overheat the ICs and make them perform worse and degrade faster.
* According to [JEDEC](https://www.jedec.org/standards-documents/dictionary/terms/output-stage-drain-power-voltage-vddq), VDDQ (Output Stage Drain Power Voltage), is tied to VDD (DRAM Voltage or VDIMM), these voltages interact with the CPU and high voltages for a long time will lead to long-term degradation of the IMC. That's why is never advised to go above 1.60V on Zen2 and Zen3.
  * CPU degradation is very difficult to measure or notice until its issues become serious. 
  
| DRAM | Daily Voltage (V) | Extreme Voltage (V) | 
|:----:|:-----------------:|:-------------------:|
|      |   1.20V ~ 1.45V   |    1.45V ~ 1.6V     | 

Voltages exceeding 1.45V for daily use are only recommended for Samsung B-die and Hynix D-die which are up to 1.50V. To use extreme voltages daily you will need good PCBs and it's also recommended to hydro-cool your sticks.
  
## Temperature
  
* Good airflow is vital to remove heat from the heat spreaders.
* If you want to overclock a RAM stick without a heat spreader I highly recommend installing an aftermarket heat spreader or your overclocking capabilities will be very low.
* Generally you want to keep your RAM below 50 °C, higher temperatures may cause instability.
* Higher voltages will make your ICs hotter.
 
# Setup:

## Identifying your RAM:

* First thing you will have to do is identify your RAM ICs and PCB, for that we will be using [Thaiphoon Burner](http://www.softnology.biz/files.html).
    * Thaipoon Burner is not the best software since sometimes it shows wrong results, but there are no alternatives.

![](Images/MicronEDie.png)

Micron E-die, 8Gb, single-rank with A2 PCB.

![](Images/Hynix%20DJR.png)

Hynix D-die (DJR), 8Gb, single-rank with A3 PCB.

![](Images/Hynix%20JJR.png)

Hynix J-die (JJR), 8Gb, single-rank with A3 PCB.

## Getting Started

* After you know your RAM, you can start by putting your VDD / VDIMM to the maximum voltage your ICs can go while not degrading yet.
* Then try to put very high timings and try discovering the highest frequencies you can get while keeping the `MCLK:FCLK`, once you start seeing any kind of instability, try desynchronizing your FCLK and keep going.
* Once you got the highest speed your RAM can get with the FCLK synchronized and desynchronized, try tightening the timings as you can get, starting with the primary, then the secondary and then the tertiary.




