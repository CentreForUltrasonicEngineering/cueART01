Data management tips

* Cost-effectiveness of data storage method:
  * Strathcloud:                        zero (paid for)
  * 4TB HDD:  			      47 GB / pound /  3 years   (83gbp/4000GB)
  * Backblaze B2B :                 23 GB / pound / year
  * Google Drive :                  5.9 GB / pound / year
  * 64GB flash disk : 		  4.5 GB / pound / 2 years
  * 512GB SSD:                     4.5 GB / pound / 2 years
* Time Cost of data read -  you have 10 minutes:
  * RAMdisk : 12'000GB
  * local SSD: 300GB
  * **local HDD: 36GB**
  * good quality USB flashdisk - 12GB
  * cheap NAS box - 12GB
  * **local PC-to-PC network, if You are lucky - 9GB**
  * **7zip, fastest compression,  - 9GB** + the time to decompress, and store 2nd copy of data, plus the hassle
    * Compression often doesn't save you much space cost, and is a lot of hassle. Avoid. Many "easy to compress" data types are already compressed internally.
  * clean DVD read/write - 3GB
  * **Strathcloud, day use: 3GB**
  * "fast" internet service: 1GB
  * floppy disk: 0.03 GB ,  but reads out entire disk in 30 seconds anyway.
* For file system: use "Windows Data Spaces":
  * Use mirroring, do not use RAID5:
    * 1x write speed, but 2x read speed
    * with RAID5, you save on disk space but it makes writes very slow. Not worth it.
  * Use checksumming to protect against bit rot
    * Bit rot is when the computer permamently misreads data that you gave it.
    * Without bitrot protection&scrubbing, there is approx. 10% chance that a data written to a HDD cannot be read correctly, and is permamently modified.
      * temporary errors are much more common -it is pretty much impossible to read entire HDD correctly
      * flash disks and DVDs are much, much worse than that
      * network data quality varies greatly between protocols. "Fast" protocols like "windows file sharing" are often not protected
    * Data in Your RAM is not safe - a "healthy" non-ECC PC gets 1-5 bit flips per month statistically
      * "bank" computers always use ECC memory, and still get an uncorrectable error every few years (at least it is being detected, and the software acts accordingly)
    * Data in Your GPU is way less safe. GPU-based SETI@home estimates up to 10% result packs are wrong
    * Problem is being looked into and future is bright on this, but for now, it is something to know that it can happen
* Misc tips:
  * StrathCloud:
    * for small files, use "ShareFile Drive Mapper" - makes it much easier
    * For large files, the use web interface - it is surprisingly reliable
* File naming scheme:
  * Put each new work in new folder
    * YYYY-MM-DD theme - topic
      * e.g. 2016-02-11 ICT hyperspectral experiment data
  * This groups and orders 
  * Places a natural limit on how many indyvidual things You have to manage -- you will not be starting a new folder every day.
  * For most things, consider storage to be cheap. 47GB per pound. You can afford it.
  * Enables you to archive and/or forget things that are old
  * Naturally becomes a memory-aid for "what have I been doing 3 years ago" - this WILL COME HANDY!
  * the files and makes it easy to divide&conquer large amounts of dispariate data
  * For text-editable files, use git. There is no excuse.
  * If you really cannot categorize given file - put it into a "var" or "misc" folder, but still with date.  Do not give up the capability to order and forget things.
* Desktop **is** a natural place to store files that You are working on - but over time invariably becomes a garbage yard. In such case, simply move **everything** into a date-stamped archive folder, even if it is not named