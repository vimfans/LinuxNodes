## UDEV
##### udev(user space /dev):
> is a device manager for the Linux kernel. Udev primarily manages device nodes in the /dev directory. At the same time, udev also handles all user space events
raised when hardware devices added into the system or moved from it.

####Rationale:
>It's an operating system's kernel that is responsible for providing an abstract interface of the hardware to the rest of the software. Being a monolithic kernel , the Linux kernel does 
exactly that, and device drivers are part of the Linux kernel , which make up more than 50% of its source code.
To be able to deal with peripheral devices that are hotplug-capable in a user-friendly way, a part of handling all of these hotplug-capable hardware devices was handled over from kernel 
to a daemon running in user-space. Running in user space serves security and stability purposes.


The udev, as a whole, is dividing into three parts:  
> 1.Library  libudev that allows access to device information.  
>
2.User space daemon udevd that manages the virtual /dev.  
>
3.Administrative command-line utility udevadm for diagnostics.


The Linux can send notifications to a user-spaces process(called udevd) upon detecting a new device on the system.
.In case a new storage device is connected over USB, udevd is notified by the kernel and itself notifies the udisksd-daemon. That daemon could then mount the file systems.
.In case a new Ethernet cable is plugged into the Ethernet NIC, udevd is notified by the kernel and itself notifies the NetkworkManager-daemon. Then NetworkManager could start dhclient
for that NIC.

