# Disk Utilities

### Prevent the System from Writing Data to a Disconnected Mount Point

```bash
chattr +i /mountpoint
```



### Automatic USB Mounting

There's a tool called `usbmount` that can automatically mount and unmount USBs when they are connected and disconnected from a system.