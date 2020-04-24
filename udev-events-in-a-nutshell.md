---
title: "UDEV Event Handling In A Nutshell"
---

**Identify events** of interest via `udevadm monitor -u -p`. 
```sh
udevadm monitor -u -p
# *plugs in HDMI cable* ...
UDEV  [3120.101110] change   /devices/pci0000:00/0000:00:02.0/drm/card0 (drm)
ACTION=change
DEVPATH=/devices/pci0000:00/0000:00:02.0/drm/card0
SUBSYSTEM=drm
HOTPLUG=1
DEVNAME=/dev/dri/card0
DEVTYPE=drm_minor
SEQNUM=8367
USEC_INITIALIZED=4351142
ID_PATH=pci-0000:00:02.0
ID_PATH_TAG=pci-0000_00_02_0
ID_FOR_SEAT=drm-pci-0000_00_02_0
MAJOR=226
MINOR=0
DEVLINKS=/dev/dri/by-path/pci-0000:00:02.0-card
TAGS=:seat:snap_spotify_spotify:master-of-seat:uaccess:
```

**Register the event** by adding a udev-rule to an existing *.rules*-file or create a new one named *[PRIONUM]-[NAME].rules*.

```sh
# /etc/udev/rules.d/99-myevents.rules
ACTION=="change", SUBSYSTEM=="drm", RUN="/usr/local/bin/udev-trigger.sh change drm"
```

Rules are cached. **Reload** via `sudo udevadm control --reload`.

To **run user scripts** the environment has to be recreated manually.

```sh
RUN="/usr/bin/su stan -c 'source ~/.profile; export DISPLAY=:0; sleep 1; ~/myscript.sh
```