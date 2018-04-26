# Data hygiene

The development of civilization always went hand-in-hand with ability of humans to communicate and store data outside their brains.

Human's brain total theoretical data capacity (not what you can actually consciously remember) is estimated at a theoretical max of 40PB (40'000 TB) - so really, our daily computers with storage capacity of 4TB are actually not that far away.

In our business of doing science, in our life times, there has been a dramatic shift away from pen-and-paper notes towards computer-only notes. Each of us is producing new files mostly every day. 

Even tough these days it is incredibly easy to create new data, making use of it is actually not that trivial. For some people, irreversibly loosing valuable electronic data is a daily experience. Even if it is not *theoretically* lost, it is often *effectively* lost if you cannot find it cheaply enough.

There is many ways in which data can be *effectively* lost. 

We now have a very real need for training and discipline in data hygiene.

This document is based on my experience.

## Firstly, consider the cost of storing data

There is two major factors to the fundamental cost of storing the data - the storage media volume, and the read/write speed of any given media. Do not underestimate the importance of the second factor. Data is *effectively* lost if it takes too long to access it.

#### Volume Cost-effectiveness of medium types:

* Strathcloud:                        zero (paid for)
	 4TB HDD:  			      47 GB / pound /  3 years   (83gbp/4000GB)
* Backblaze B2B :                 23 GB / pound / year
* Google Drive :                  5.9 GB / pound / year
	 64GB flash disk : 		  4.5 GB / pound / 2 years
* 512GB SSD:                     4.5 GB / pound / 2 years

#### Time Cost of different medium types -  how much can You read in 10 minutes:

* RAMdisk : 12'000GB

* local SSD: 300GB

* **local HDD: 36GB**

* good quality USB flashdisk - 12GB

* cheap NAS box - 12GB

* **local PC-to-PC network, if You are lucky - 9GB**

* **7zip, fastest compression,  - 9GB** + the time to decompress, and store 2nd copy of data, plus the hassle
  * Compression often doesn't save you much space cost, but takes time and is a lot of hassle. Avoid until you can consciously estimate that it will save you time/money.

* clean DVD read/write - 3GB

* **Strathcloud, day use: 3GB**

* "fast" internet service: 1GB

* floppy disk: 0.03 GB ,  but reads out entire disk in 30 seconds anyway.

  ​

  ### Technical advice for using HDDs 

  For file system: I have done a review of software options and I decide that in 2018, the best option is to use "Windows Data Spaces" with following options:


* Use mirroring, do not use RAID5:
  * 1x write speed, but 2x read speed
  * with RAID5 or Raid-Z types, you save on disk space but it makes writes much, much slower, and reads are still slower than single disk (due to the need to verify checksums). Certainly not worth it for a system with 3 or 4 disks, and probably not worth it for 5 or 6 disks. Remember, time is a cost. Only consider it if you really have >5 disks.
* Use checksumming to protect against bit rot
  * Bit rot is when the computer permamently misreads data that you gave it.
  * Without bitrot protection&scrubbing, there is approx. 10% chance that a data written to a HDD cannot be read correctly, and is permamently modified.
    * temporary errors are much more common -it is pretty much impossible to read entire HDD correctly
    * flash disks and DVDs are much, much worse than that
    * network data quality varies greatly between protocols. "Fast" protocols like "windows file sharing" are often not protected
  * Data in Your RAM is not safe - a "healthy" non-ECC PC gets 1-5 bit flips per month statistically
    * "bank" computers always use ECC memory, and still get an uncorrectable error every few years (at least it is being detected, and the software acts accordingly)
  * Data in Your GPU is way less safe. large scale GPU-based BONIC projects report up to 10% result packs coming back defective.
  * Problem is being looked into and future is bright on this, but for now, it is something to know that it can happen


* StrathCloud:
  * for small files, use "ShareFile Drive Mapper" - makes it much easier, saves You management time.
  * For large files, the use web interface - it is surprisingly reliable, more so than the DriveMapper.

## File naming scheme

This is more important than it at first appears.

I have seen many endeavors in which success or failure began with developing just-right way of naming the data - so that it can be actually found later on.

Based on experience, i propose to You the following scheme:

* For each new "topic" create a new folder

* The folder name is critical. Use the following scheme:

  * "YYYY-MM-DD theme - topic"
    * e.g. 2016-02-11 ICT hyperspectral experiment data

* File naming: whatever, as long as it is contained in a time-stamped folder. If it travels without a folder (e.g. in an email, e.g. a presentation or a single word document ) - it becomes important that it has a permament datastamp in the filename

* Why not use system data stamp? because it is not preserved when copying/moving the file


The time stamp **groups** and **orders** Your data, both of which are critically important:


* Places a natural limit on how many indyvidual things You have to manage -- you will not be starting a new folder every day.

* For most things, consider storage to be cheap. 47GB per pound. You can afford to have several, similar copies of a file BUT not to forget which one is the latest version.

* Enables you to archive and/or forget things that are old

* Naturally becomes a memory-aid for "what have I been doing 3 years ago" - this WILL COME HANDY! you have been warned.

* the files and makes it easy to divide&conquer large amounts of dispariate data




For text-editable files, use git as a way to version and fork the work. There is no good excuse to not use it.



If you really cannot categorize given file - put it into a "var" or "misc" folder, but still with date.  Do not give up the capability to order and forget things.



Desktop **is** a natural place to store files that You are working on, especially on windows machines it is already in an user-subfolder. However, over time invariably becomes a garbage yard. In such case, simply move **everything** into a date-stamped archive folder, even if it is not named.

## Software



2018 advice: For quick file-name based search, use "Everything" by void tools:

https://www.voidtools.com/

it will scan your drives, respond very quickly to enquiries, and there is a facility for searching external file lists (export/import *.efu file)

2018 advice: for accessing remote computers, use "TeamViewer"  https://www.teamviewer.com/en/ 



For real off-site data back-up, use backblaze, user-mode. 50usd / year / computer, and no limit on the volume of data or count of disks in a computer. Will not back-up "networked" drives, but there are workarounds to this (by mounting using "real drive" driver). https://www.backblaze.com/





- Why not use NTFS metadata streams? because it is not copied when copying/moving file out of NTFS, and Microsoft themselves are obsoleting this feature with their ReFS
- Why not use BRTFS? (2018 info) as promising as it sounds, it is not mature, the tools are complex and require expert knowledge, and it's future is not certain. 
  - It receives publicity because one of the original developers now works for Facebook, but Facebook does not seem to be highly invested in making it any easier for mere mortals to use. Avoid. 
  - Comparably, Windows Storage Spaces is a similar technology, but Microsoft has invested way more into making it reliable, and it has lots to loose if it doesn't work out.
- Why not use ZFS? (2018) Because it's windows implementation is literally a hobby-grade one. 

## Devices

2018 advice: when buying a laptop, prefer a lighter one. Honestly, you will not be doing advanced calculations on a laptop - we have "workstations" and a supercomputer for that.



