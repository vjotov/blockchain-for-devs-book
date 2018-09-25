# Mining Equipment

Bitcoin mining hardware has evolved throughout the years:

- **CPU**
- **GPU**: Graphics Processing Unit; don't be fooled by the name, they can do much more than graphics!
- **FPGA**: Field-Programmable Gate Array; used to coexist with GPU mining for a while
- **ASIC**: Application-Specific Integrated Circuit

The least efficient, but also simplest way, was **CPU mining**; you just use some SHA-256 library and that's it. You can use multi-threading to more fully utilize multi-core CPUs.

Then eventually some programmer[^1] figured out a way to do the calculations on the programmable **GPUs** that were entering the market at the time, which allowed for a huge boost due to the parallel nature of the GPUs and the "embarrassingly parallel" nature of the mining problem (a problem is said to be "embarrassingly parallel" when the solutions don't depend on each other, and you easily search for solutions simultaneously).

Then came **FPGAs**, which are basically "reconfigurable chips" - you develop a chip in a language like Verilog or VHDL, and upload it to the "blank". They were more power-efficient than GPUs, but not by much (even though they can be quite a bit faster).

The last stage of the evolution, and what BTC miners are currently using, are **ASICs**: fully custom silicon developed for one purpose - mining! When it comes to performance per Watt, the newest ASICs are around 50 *million* times more efficient than the CPUs where it all started.

While mining hardware has evolved quite a lot, the mining **business** also has: it's not just hobbyists with one or two graphics cards anymore, there are farms that have thousands of machines and are managed like professional data centers:

![](/content/part-1-blockchain-networks-concepts/mining-and-mining-pools/Cryptocurrency_Mining_Farm.jpg)
*(picture by Marco Krohn, published on Wikimedia Commons)*

In an attempt to try to prevent things from becoming **too** serious, some coins, like Ethereum, use mining algorithms that are **ASIC-resistant**: they use memory-heavy algorithms that cannot be optimized much by the use of custom chips. This is done so that mining is more widely accessible to people, because many people have GPUs already, while an ASIC is something you have to purchase specifically for mining. Here is a table that shows the potential efficiency gains from going to an ASIC for various algorithms:

| PoW algorithm     | Potential ASIC efficiency gain |
|-------------------|--------------------------------|
| SHA256 (BTC, BCH) | 1000X                          |
| Scrypt (LTC)      | 1000X                          |
| X11 (Dash)        | 1000X                          |
| Equihash (ZEC, BTG) | 100X                         |
| Cuckoo Cycle (AE) | 100X                           |
| CryptoNight (XMR) | 50X                            |
| ETHash (ETH)      | 2X                             |

(*Source: https://github.com/ifdefelse/ProgPOW*)

[^1]: This programmer was Laszlo Hanyecz, the same person that famously bought two pizzas for 10,000 BTC in the first Bitcoin transaction that involved physical goods.