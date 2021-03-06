## Disk Partition
 We need to format the drive before write something to it. Formatting (usually known as "making a file system") writes information to the drive,
create order out of the empty space in an unformatted drive.

A small percentage of the drive's available space is used to store file system-related data and can be considerable as overhead.
A file system splits the remaining space into small, consistently-sized segments. For Linux , these segments are known as blocks.


Disk drives can be divided into  partitions. Each partition can be accessed as if it was a separate disk. This is done through the addition of
a partition table.
There are several reasons for allocating disk space into separate disk partitions.
> 1.Logical separation of the operating system data from user data
>
 2.Ability to use the different file systems
> 
3.Ability to run multiple operating systems on one machine
>
4.Once a disk is divided into several partitions, directories and files of different categories may be stored in different partitions.
>
5.Preventing overflow of temporary files.

**Notes: There is a critical difference between partitioning and file manipulation. The partition table defines simple boundaries on 
the disk, whereas a filesystem is a much more involved data system.** 

LBA(logical block addressing): address a location on the disk by a block number



### Filesystem
The filesystem is a form of database; It supplies the structure to transform a simple block device into the sophisticated hierarchy of files
and subdirectories that user can understand.  

### Virtual File System
VFS ensures that all user-space applications access files and directories in the same manner.

*Creating a Filesystem*

`mkfs -t ext4 /dev/sdb1`

### Mounting a Filesystem
  On Unix , the process of attaching a filesystem is called mounting. When the system boots, the kernel reads some configuration data and mounts
root(/) based on the configuration data.
In order to mount a filesystem, you must know the following:
>  1.The filesystem's device(such as a disk partition; where the actual filesystem data resides)
>
   2.The filesystem type
 >
 3.The mount point. The place in the current system's directory hierarchy where the filesystem will be attached.The mount point is always a normal
directory.

To mount a filesystem, use the mount command as follows with the filesystem type, device, and desired mount point:

` mount -t type device mountpoint`  

or  

` mount UUID='' mountpoint`  
you can use `blkid` command to find uuid of the device.


### /etc/fstab
> 1.first column: The device or UUID
>
2.second column: The mount point
>
3.third column: The filesystem type
>
4.fourth column: options
>
5.fifth column: Backup information for use by the dump command
>
6.sixth column: The filesystem integrity test order(To ensure that fsck always runs on the root first, always set this to 1 for the root filesystem and 2 for 
any other filesystems on a hard disk. Use 0 to disable the bootup check for everything else.Including CD-ROOM drives, swap, and the /proc filesystem.)


### Filesystem Capacity
To view the size and utilization of your currently mounted filesystems, use the df command.   
` df -h`  
`du`

### Checking and Repairing Filesystems
`fsck`  
You should never use fsck on a mounted filesystem because the kernel may alter the disk data as you run the check.


### Special-purpose filesystems  
Not all filesystems represent storage on physical media. Specifically, most versions of Unix have filesystems that serve as system interfaces.
a filesystem can represent system information such as process IDs and kernel diagnostics.  
> proc: Mounted on /proc. The name proc is actually an abbreviation for process. Each numbered directory inside /proc is actually the process ID of current process on the system.
>
sysfs: Mounted on /sys
>
tmpfs: Mounted on /run and other locations.With tmpfs, you can use your physical memory and swap space as temporary storage.


### Swap space
`free`

Using a disk partition as swap space
> 1. Make sure the partition is empty.
2. Run ` mkswap dev`   , where dev is the partition's device. This commands puts a swap signature on the partition.
3. Execute swapon dev to register the space with the kernel.
After creating a swap partition, you can put a new swap entry in your /etc/fstab file to make the system use the swap space as soon as the machine 
boots.
