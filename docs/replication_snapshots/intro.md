
The UNICell system allows you to manualy create ZFS snapshots or schedule snapshot creation. 

##Snapshots
A description of ZFS snapshots from [Aaron Topence's ZFS guide](https://pthree.org/2012/12/19/zfs-administration-part-xii-snapshots-and-clones/) follows..

"A snapshot is a first class read-only filesystem. It is a mirrored copy of the state of the filesystem at the time you took the snapshot. Think of it like a digital photograph of the outside world. Even though the world is changing, you have an image of what the world was like at the exact moment you took that photograph. Snapshots behave in a similar manner, except when data changes that was part of the dataset, you keep the original copy in the snapshot itself. This way, you can maintain persistence of that filesystem.

You can keep up to 2^64 snapshots in your pool. ZFS snapshots are persistent across reboots, and they don't require any additional backing store; they use the same storage pool as the rest of your data. Creating snapshots is near instantaneous, and they are cheap. However, once the data begins to change, the snapshot will begin storing data. If you have multiple snapshots, then multiple deltas will be tracked across all the snapshots. However, depending on your needs, snapshots can still be exceptionally cheap."

##Replication
The UNICell system uses ZFS's send and receive functionalities to send consistent file system images of a dataset to another UNICell system. A description of ZFS send from [Aaron Topence's ZFS guide](https://pthree.org/2012/12/20/zfs-administration-part-xiii-sending-and-receiving-filesystems/) follows..

"Now that you're a pro at snapshots, we can move to one of the crown jewels of ZFS- the ability to send and receive full filesystems from one host to another. This is epic, and I am not aware of any other filesystem that can do this without the help of 3rd party tools, such as "dd" and "nc".

Sending a ZFS filesystem means taking a snapshot of a dataset, and sending the snapshot. This ensures that while sending the data, it will always remain consistent, which is crux for all things ZFS. By default, we send the data to a file. We then can move that single file to an offsite backup, another storage server, or whatever. The advantage a ZFS send has over "dd", is the fact that you do not need to take the filesystem offilne to get at the data."
