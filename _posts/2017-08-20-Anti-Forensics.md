---
title:  "Anti-Forensics"
date:   2017-08-20
published: true
---

It is difficult to start with a specific point when talking about **"Anti-Forensic "**, the idea is to give various tips and advice to execute or hinder a forensic work to our data, computer, devices and others in order to preserve the illusion of privacy.

First we must begin by defining what is [Computer Forensics](https://en.wikipedia.org/wiki/Computer_forensics). So with this simple definition of what this branch of computer science does, we will proceed to understand a little more in detail certain characteristics.

First of all we must know that electromagnetic storage devices such as hard disks, pendrives, memories among others, store/save/record information or data in a peculiar way.

Before starting we should know that depending on the operating system and the type of disk things may vary, but in general. The Windows operating system tracks files (user data) using either a File Allocation Table or a Master File Table.  In simple terms, the FAT or MFT tells the computer where the file begins and ends.
Macintosh uses a similar system known as Nodes. When a file is deleted, the operating system deletes the pointers to the file and in the FAT or MFT the space occupied by the file is mark as available.  The computer does not delete the actual data that was contained in the file.
What really happens is that the reference to it is deleted so that it is invisible to the operating system, but the file will still exist in the same sector of the disk where it was located, without being modified. 
In short, the file still exists but the operating system stops indexing it.


# **Understanding this, let's look at some interesting things.**

Listo!. Entendida la teoría ahora con ella digamos que sabemos de manera básica que si borro un archivo en realidad se mueve, pero no lo indexa el S.O y de paso puede ser recuperado por herramientas, técnicas y metodologías de Informática Forense.


# What do we do?

**First technique**: [Steganography](https://en.wikipedia.org/wiki/Steganography)

  Simple but easy to discover (unless you use a lot of creativity).

**Second technique**: Secure data deletion.

  One of the best (explained below).

**Third technique**: Overwriting Metadata.

  Bbasically because when you create a file X is stored in its metadata the program that made the exact time, the creation software and many more things including in some cases the username of the account with which you access the host.

**Fourth technique**: Avoiding data creation.

  If the data never existed you will never be able to recover something that never existed, simple but effective! 

**Fifth technique**: Encrypted data.

  An "easy" to implement alternative and can be applied at the disk, software and application level.

**Sixth technique**: Data Hiding.

  Data may also be hidden in unassigned or otherwise unreachable locations that are ignored by forensic tools

Besides these simple techniques there are also some tools such as

* [Starfish](https://www.digitrace.de/forschung/starfish)
* [usbkill](https://github.com/hephaest0s/usbkill)
* [Usbdeath](https://github.com/trpt/usbdeath) -> Inspired by usbkill
* [DBAN](http://www.dban.org/) -> A very good one.

Other cool techniques.

**Hiding in the echo.**

  The echo of a discrete signal is used and extra sound is added. The echo has three parameters that will be seen in the original signal to hide information: amplitude, decay speed and delay time. These variations apply
always below the threshold of the human ear. The remarkable thing is that unlike the other methods, the original audio can be improved.

**Spectrum Dispersion.**

  The secret data are dispersed in the frequency spectrum at random, as much as possible. The data are modulated and the resulting signal occupies a higher bandwidth than actually required. The disadvantage is that noise is added to the original audio file.
  
**Spatial Domain.**

 The secret data is embedded in the intensity of the pixels. This means that some pixel values change while the data is being hidden. And it should be noted that it has categories: 

* Coding of the least significant bit (LSB).
* Pixel Value Differentiation (PVD).
* Segmentation of complexity on the bit plane (BPCS-steganography (Bit-Plane Complexity Segmentation steganography)).
* Edge-based data embedding (EBE).
* Pixel mapping to secret data.
* Distortion.
* Masking and filtering.

Additionally, there are other techniques such as:

**Sanitizacion:** It is known as a process of erasing all or part of the data on a digital storage device in such a way that it cannot be recovered and it also consists of 3 types: 

**Clearing:** The user rewrites or deletes the entire file or disk. In Linux there is a powerful tool called shred.

**Wipping:** Data wiping makes data unreadable, but it does not remove the data. Instead, data wiping is the process of overwriting the data on a particular hard drive to such an extent that the original data is unreadable.

**Analogical:** Or purging degaussing , is basically a degradation of the analog signal that encodes the bits representing the data.

Of course there is physical destruction (incineration, cutting, disintegration, demagnetization and pulverization) which is another section for a complete post due to its complexity.

![](/images/genrico.png "Simple Steganographic Process")

Additionally I will present a table of possible defenses against a computer expert (based on the chain of custody which is not mentioned in this post).

| **Stage**        | **Description**           | **Attack**  |
| :-------------: |:-------------:| :-----:|
| Identification      | Method by which the expert determines if there is an incident to be investigated | Obscuring the incident and unlinking the related device |
| Preservation      | Steps to safeguard the integrity of the evidence     |   Interrupting the chain of custody or questioning the integrity (based on the [Hash](https://en.wikipedia.org/wiki/Hash_function)) |
| Collection | Process by which data is extracted from evidence      |    Avoiding data collection, questioning software, hardware and applied methodologies |
| Analysis | Phase in which the expert draws conclusions from the evidence. It is based on the tools, the expert's skill and the rest of the non-digital evidence that was found.| If the case is based only on digital evidence, the interpretation will be the most likely to be attacked.|

Thank you for reading the article!.

> If you want a post about Forensic Analysis in Windows, Linux environment, procedures, techniques, tools and or any challenge do not hesitate to write me.

~~~R
HACKED!
~~~
