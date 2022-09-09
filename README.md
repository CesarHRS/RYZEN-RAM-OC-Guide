# AMD-RAM-OC-Guide
# General RAM Info:

* Units:
  * Hertz: It is a unity of frequency used in the SI, it is equivalent to one cycle per second.
  * Transfer: It refers to a quantity of data that can be transferred in a second. 

* Prefixes:
  * Nano: 10^-9
  * Mega: 10^6
  * Giga: 10^9
  

## Basics:
* RAM frequency is measured in megahertz (MHz), having your RAM operating at a higher frequency means more cycles per second, which will give you some extra performance. Having very high frequencies can make your RAM unstable and it may crash your PC.
  * **Advanced tip:** The only case witch lowering the clock will result in better performance is in tREFI, since tREFI measures the timing between RAM refreshes. While your RAM refreshes, you can't write or read anything on it, so you want to make that time gap as little as possible.

* RAM Timings are the latency between various operations inside a RAM chip, having low latencies will result in better performance, so keep them as low as possible. Having very low timings will also make your RAM unstable and may result in crashes. 
  * The main timing of your ram is called CL or CAS Latency, it measures the delay between the **READ** command and the moment the data is available, this interval is specified in nanoseconds.
  
* When you buy a RAM stick, sellers usually show their clock speed and their CL. For example, DDR4-3000 CL15 and DDR4-3600 CL18.

  * 3000MHz CL 15, has a lower CAS, but 3600 CL 18 has a higher frequency, so it's necessary to find out how they compare.
  
  To calculate the time in nanoseconds (ns) of a given frequency and CL, just use the formula: `2000 * timing / frequency`
  * DDR4-3000 CL15 = `2000 * 15 / 3000 = 10 ns`.
  * DDR4-3600 CL18 = `2000 * 18 / 3600 = 10 ns`.
  * Thus it's demonstrated that they have the same performance 

* Common mistakes:

  * People usuary refer to DDR4-3000 as 3000 **MHz**, but they are only 1500 **MHz**, this happens because we use DDR RAM, DDR stands for Double Data Rate, which transfers data in the rising edge of the clock and in the falling clock edge, so the real frequency of the RAM is half the number of transfers it makes in a second. So a DDR4-3000 operates in 1500 **MHz (MegaHertz)** and will transfer 3000 **MT/s (MegaTransfers per second)** of data.
  
## Primary, Secondary and Tertiary Timings:

* AMD
    
image here
    
* RAM timings are split into 3 categories, primary, secondary and tertiary
* Primary and secondary timings will affect latency and bandwidth, while tertiary timings affect only bandwidth
  
# Limiting Factors:  
  This section will go through components that will limit your overclocking capacities. 
  * Motherboard
  * Always prefer motherboards with 2 DIMM slots, they will let you achieve higher frequencies.
    * While using motherboards that use daisy chain, 2 sticks are preferred, if you use 4 sticks the performance will be impacted
    * Motherboards with T-topology will overclock better with 4 sticks equipped, using 2 sticks will not cap your overclocking capability that much as in a daisy chain with 4 slots. 
  * Entry-level motherboards may not overclock as well thanks to their low-quality PCB.  
  
  
  * Integrated Circuits (ICs)
  * Integrated Memory Controller (IMC)
