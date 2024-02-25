---
---

# Computer Hardware

In this page, we'll recap the basics of what the various elements of your computer are used for. This will be important to understand for you to shop for appropriate hardware, understand what resources are being under/over utilized on your home setup, and to know when it's time to upgrade. We'll keep it brief!

## CPU

Your CPU (Central Processing Unit) is what handles all computational tasks in your machine. Evaluating a good CPU from a bad one goes far beyond "which one is faster." Despite that, you can get a quick numerical comparison of CPUs at [Passmark](https://www.cpubenchmark.net/cpu.php?cpu=AMD+Ryzen+Embedded+R1600&id=5117). For instance, the CPU in the Synology DS923+ is a AMD Ryzen Embedded R1600, which scores with a 3281.

Here are some aspects to use to compare CPUs:

### Single Threaded Performance

This is how quickly your CPU can crunch through a single threaded task. A single threaded task is a task that cannot be split up into multiple parallel tasks. An example of a task that cannot be multi-threaded would be the compressing a file. Your computer reads in a bit of the file, compresses it, and sticks it at the next slot in storage at the destination. Since the exact destination of each compressed chunk depends on the size of the chunks before it, you can't have multiple processors tackling this task at the same time. The process is therefore handled by only one core of the processor. More cores does not equal faster performance in single threaded tasks! If you expect lots of single threaded operations, you'd be better off with faster/better individual cores instead of more cores.

### Multi Threaded Performance

Conversely, this is how fast your computer can handle tasks that can be split up into parallel tasks. An example of this is transcoding videos. Your CPU needs to crunch numbers on each frame of the video to translate the video into a different format. If you've got 24 cores, you could have each core working on a separate frame and get the job done 24 times as fast as a single core-processor. For parallel tasks, more cores generally correlate to faster processing.

## GPU

A GPU is a variant of a CPU that is uniquely optimized for graphical processing. In a sense, you can think of it as a CPU that has many (thousands) of cores, but they're all pretty wimpy. What's the correlation to graphical processing? Let's say you're playing a video game that has 100 cubes on the screen. Each cube is drawn on your screen with a series of lines. Based on where you're viewing the cubes from, simple geometry is used to calculate the angle, length and position of the line. It's simple/quick math, but there are a ton of simple calculations that need to be done all at the same time. A CPU could do it, but it doesn't have many cores, so despite each individual core being capable of easily doing that math very quickly, it takes a long time to render the image since so much time is wasted on each core moving from one object to the next.

GPUs are useful for rendering graphics in video games, certain image processing operations, and fast transcoding. Fast transcoding may be useful to you if you have a large video in one format, but you want to watch it real time while converting it to another format. This sort of transcoding is called **Hardware Transcoding**. While it is *much* faster than traditional transcoding, it lacks the accuracy of regular transcoding. The GPU's thousands of "cores" are not very powerful, so more estimations need to be made in the transcoding process which reduces the overall quality of the transcode.

## Storage

Storage is where you keep your bulk data and filesystem. It is meant to be "persistent"/"non-volatile", meaning the data doesn't go away when the computer loses power. It is measured in bytes and is often accompanied by a (decimal) metric or (binary) IEC prefix. A byte (B) is eight bits (b). A bit is a single "digit" of memory, where that "digit" can be a one or a zero. So a bit can be 1 or 0, but a byte could be 00010000, 00000011, 11110011, etc.

(Decimal) metric prefixes:

 - kB - kilobyte - 10^3 B  - 1,000 bytes
 - MB - megabyte - 10^6 B  - 1,000,000 bytes
 - GB - gigabyte - 10^9 B  - 1,000,000,000 bytes
 - TB - terabyte - 10^12 B - 1,000,000,000,000 bytes

(Binary) IEC prefixes:

 - kiB - kibibyte - 2^10 B - 1024 bytes
 - MiB - mebibyte - 2^20 B - 1,048,576 bytes
 - GiB - gibibyte - 2^30 B - 1,073,741,824 bytes
 - TiB - tebibyte - 2^40 B - 1,099,411,627,776 bytes

Here's the confusing part: When you buy a hard drive, they list the storage capacity in metric prefixes and they actually mean it! When your computer shows the size of the drive, it says it's displaying the metric value (TB) but it's actually displaying the IEC value (TiB) and using the wrong unit (TB)! Very frustrating. That is unless you're using mac or linux, where they don't lie. Storage capacity is displayed with the correct units (TiB).

Why do you care? What's the point besides a fun trivia fact you can bore your friends with at parties and silly words that are fun to say? Plug a 1TB hard drive in your computer and you'll see that the capacity is listed as 931GB. Your computer really means 931GiB!

Here's how you can save yourself the mental gymnastics: Just know we're always talking IEC (kiB, MiB, GiB, TiB) prefixes, even if there are metric prefixes being displayed (kB, MB, GB, TB). The only time we're not talking IEC prefixes is when you're buying the hard drive. So the actual capacity of that hard drive is going to be a little less than what you'd expect based on the packaging.

### Characteristics to look for in storage

#### Capacity

A 4TB is twice as good as a 2TB hard drive! More storage capacity more better!

#### SSD vs. HDD Technology

A Hard Disk Drive (aka HDD, aka spinning disks, aka hard disks, aka "spinning rust") is cheap but slow to access. It's a series of disks, so they consume more power to spin them and take more time to move motors and disks into place before the requested data can be read.

A Solid State Drive (aka SSD) is expensive but fast. It's just transistors in there, so your computer can quickly ask for data at an address and get it back. No need to spend the power or time to spin up.

#### Access Speed

In the case of HDDs, this is normally a consequence of the speed the disk can spin (in RPM) and the interface technology. But obviously, faster access to your data is better for you!

Access speed is typically measured in bits per second (bps), with metric prefixes like Mbps, Gbps, etc. Note that we're talking "bits per second" (bps), not "bytes per second" (Bps). Remember that a byte has eight bits. So 8Mbps = 1MBps = 1MB transferred every second.

#### Interface technology

For HDDs, common interfaces are SAS (industry standard for rack-mount servers) and SATA (more consumer grade). While SATA is standard among consumers, if you're setup supports SAS then you have the advantage of buying **very** cheap used hard drives from companies that need to get rid of their hard drives. Depending on your motherboard, you'll have some number of available SAS or SATA connections. If you're working in a PC, you might be able to get a card that fits in an empty PCIe slot to give you more SAS or SATA connections! Both SAS and SATA have different "versions" of their technology. SATA has SATA I (speeds up to 1.5Gbps), SATA II (speeds up to 3Gbps) and SATA III (speeds up to 6Gbps). All of the SATA technologies are physically backwards compatible with one another. So you can buy a SATA I drive to plug into your SATA III motherboard slot, it just will be capped at 1.5Gbps.

#### Physical form factor

Hard drives are popular in a 3.5" size (typical in PC towers), 2.5" size (typical in portable drives and laptops). SSDs are common in the same 2.5" form factor, as well as M.2, mSATA, and PCIe. M.2 has grown quite common, and is a bare circuit board profile that slots into your motherboard. Be careful with the M.2 profile, though: motherboards will only support certain lengths of M.2 cards!

## RAM

RAM (Random Access Memory) is also referred to as "Memory" in computers. This is data storage that is specifically optimized to be read/written to as fast as possible and is "non-persistent"/"volatile", meaning it doesn't retain its memory when you power down your computer. Since your computer can store/retrieve data so quickly from RAM, it's used as as a sort of "scratch space" to help the computer handle its current tasks. If storage is your notebook where you take notes in class that you want to keep, RAM is the piece of scratch paper that you use to work out a homework problem and then throw it away when you're done with it.

This means, the more RAM you have, the more things your computer can do at the same time. You may notice that you start some tasks and see RAM increase, then you end some tasks and don't see the RAM decrease. That's because in some cases your computer decides to "cache" things in memory just in case it needs to access it again. But if there are more necessary uses of RAM at hand, it will start removing things from the cache to make room.

And when I say it's faster than storage, I mean it's *much* faster. We're talking something like 300x faster than an SSD or 1000x faster than a HDD.

#### Swap

If your computer runs out of RAM, it can utilize something called "Swap". If you have set up your computer with a partition of storage dedicated to "swap" space, that means the computer will treat that storage space as spillover RAM if it needs it. Storage is waaaay slower to read/write than RAM, so if your computer starts using swap you'll likely feel it!

### Characteristics to look for in RAM

#### Capacity

More capacity = more concurrent things your computer can do at once.

Oh, and remember when we said that when it comes to storage your computer actually measures things in GiB (but it says GB) and you buy storage in GB (which is actually GB)? Well when it comes to RAM, the computer measures it in GiB (but says GB), and when you buy RAM it's actually in GiB (but the package says GB). So there's no discrepancy like there is with storage. If you buy 16GB of RAM, your computer will tell you it's got 16GB of RAM. Everyone *actually* means GiB, but hey, at least we're being consistent this time!

#### Technology

RAM technology evolves over time, and therefore there are different standards for RAM. Commonly on the market today you'll find "DDR3" and "DDR4". DDR4 is newer than DDR3, meaning it supports faster speeds and higher capacities. However, beware that your motherboard needs to be able to support the technology of your RAM. Old motherboards might only support DDR3, and the different technologies have different physical form factors to avoid you plugging in an incompatible RAM technology.

#### Speed

RAM is all about speed! Slow RAM will slow down your whole computer. RAM slots on motherboards are rated up to a certain speed. Common DDR4 speeds are 2133MHz, 2400MHz, 266MHz, 3000MHz, and 3200MHz. If your motherboard only supports up to 2400MHz and you stick a 2666MHz RAM stick in, it will run the RAM at 2400MHz (meaning you wasted some money on paying for higher performance that you can't use with this motherboard).

#### Physical form factor

RAM comes in a number of types of "Dual Inline Memory Module" (DIMM) form factors. DIMM, Small Outline DIMM (SODIMM; common in laptops), MicroDIMM, etc. Each of those form factors have sub-variants to accommodate for different pin counts, so double check before you buy!
