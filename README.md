# raspberry-mixxx


## SD Card

I installed Raspbian bookworm lite using Raspberry Imager.

I setup my user (the initial boot takes care of this), setup wifi, ensured that I was using wayland, and setup autologin.

Then:

```
sudo apt update
sudo apt upgrade
```

## Boot setup

I wanted the boot sequence to be as quiet as possible so I made the following changes.


```
/boot/firmware/cmdline.txt

console=serial0,115200 console=tty9 loglevel=3 root=PARTUUID=850b8d9a-02 rootfstype=ext4 fsck.repair=yes rootwait cfg80211.ieee80211_regdom=FR video=HDMI-A-1:1920x1080M@60

```

`console=tty9 loglevel=3` sends all of the bootup text to `tty9` leaving `tty1` empty.

I also made the following changes to prevent text from displaying before the command prompt appears.

```
/etc/systemd/system/getty@tty1.service.d/autologin.conf

[Service]
ExecStart=
ExecStart=-/sbin/agetty --skip-login --nonewline --noissue --autologin murray --noclear %I $TERM
```

Obviously you'll need to change `murray` to whatever username you chose.


## Other software that we will need

`sudo apt install sway blah blah blah`
