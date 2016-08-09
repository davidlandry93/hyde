---
title: Writing udev rules
layout: post
---

To me, udev rules have been shrouded in mystery until recently. Fortunately, I came across
a situation where I had to write one, so I finally dug into the subject. And it turns out it's pretty simple after all.

The understanding I built is as follows:

> udev rules are a mapping from a type of device to actions. Typical actions are 
> changing the permissions, creating symlinks to the device, and so on.

With that in mind, a typical udev rule becomes much clearer.

```
SUBSYSTEMS=="usb", KERNEL=="ttyACM[0-9]*", ACTION=="add", ATTRS{idVendor}=="15d1", ATTRS{idProduct}=="0000", MODE="0666", PROGRAM="/opt/ros/hydro/lib/urg_node/getID /dev/%k q", SYMLINK+="sensors/hokuyo_%c", GROUP="dialout"
```

The above `SUBSYSTEMS`, `KERNEL` and `ATTRS` fields are used to define what kind
of devices you want this rule to apply to. Finally `MODE` and `GROUP` change the
permissions of the device, `PROGRAM` and `SYMLINK` are used to create a symlink
to it, while `ACTION` is a way of detecting if the device is being plugged in or
out when using the `PROGRAM` command.

To include this rule in your system you would add this line to a file named
`/etc/udev/rules.d/90-hokuyo.rules`.

So that's the basic understanding. For more explanations, the people at
[Clearpath](https://www.clearpathrobotics.com/) wrote a nice
[tutorial](https://www.clearpathrobotics.com/assets/guides/ros/Udev%20Rules.html)
on the subject. A more detailed documentation can be found
[here](http://www.reactivated.net/writing_udev_rules.html).

Before you go on and start writing your own rules, you should be aware of two
commands. The first one allows you to list the attributes of a given device.
It's useful when you want to write a rule that will match it. You just have to
replace `<devpath>` by a path to the device, something like `/dev/ttyACM0`.

```
$ udevadm info -a -p $(udevadm info -q path -n <devpath>)
```

This second command will allow you to test your current set of rules to debug it.

```
$ udevadm test $(udevadm info -q path -n <devpath>) 2>&1
```

Good luck!

/David
