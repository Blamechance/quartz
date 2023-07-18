## **RAID 0:**

* Files are all striped across the array, increasing performance but providing ZERO redundancy or FAULT TOLERANCE.
* If you lose a single drive, you lose ALL your data.
* Read and Write speeds are enhanced due to the accessibility of the tapes (since they are striped).

## **RAID 1 (mirror):**

* This allows FULL fault tolerance between drives, as there is always a mirror copy of a drive's contents on another drive -- however, it means your capacity is limited since you are allocating so much to fault tolerance.
  * i.e 2 drives of 500 GB in RAID 1 will ultimately only provide the user 500gb of capacity, as opposed to 1 TB.
* Losing a single disk will allow your full data still available on the other (mirrored) disk.
* Good **read performance**, with decent write performance.

## **RAID 5:**

* This format stripes the data similar to RAID 0, however, each drive also includes sections of ***parity data***, which is used as backups to other drives.
  
  When a drive is down, the state of the raid is considered "degraded" -- as it is reconstructing data through parity data, leading to **less fault tolerance and poorer performance**.
  
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/00ba3e0c-30a3-4809-9a8a-34733efa991e/Untitled.png)

* To remediate this, we "rebuild the array", which will be done through the parity data.
  
  This process can take a while and also impacts performance, however when finished will restore fault tolerance and the RAID.

* Notes:
  
  * **There is still less disk capacity in RAID 5, allocated to parity data.**
  * RAID 5 can be enhanced through use of "hot spares" -- standby drives which are on standby for when the RAID degrades.
  * Slower write performance, due to need to write to parity blocks too -- however, read performance is decent as you can read off the multiple disks.
  * *Minimum 3 disks, with logically, one used for parity (spread across).*

## **RAID 10:**

* This format is essentially a **mirror of stripes**.
