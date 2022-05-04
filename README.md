# modep for Raspberry Pi 4 / 400

## Introduction

Use it at you own risk. It will overclock your Pi 4/400 to 4x 2.0 GHz. Be sure to use a heatsink on the Pi 4. The Pi 400 should be fine without (mine is around 38°C while modep is running).

It requires the 64-bit version of Raspberry OS.

### Install modep

Follow official instructions.

### Adjust file systemd/jackd.service

Make sure to set the right name and config for your USB or I2S audio interface. You can figure it out by using aplay -l.
My config is made for a Tascam Model 12, which gives me 12 channels multitrack out and 10 channels input via USB, which comes very handy.

### Add systemd unit files and activate services

```
sudo cp systemd/* /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable jackd.service
sudo systemctl enable mod-host.service
sudo systemctl enable mod-ui.service
```

afterwards start the services using systemctl start <service_name>

### Optional.: Overclock CPU from 1.8GHz to 2.0GHz

```
sudo cp config.txt /boot/
```

### Fetch my 64-bit Kernel with Realtime (preempt-rt) patches

```
wget https://bittunnel.org/rpi/rt-kernel/linux-headers-5.15.36-rt41-v8+_5.15.36-rt41-v8+-3_arm64.deb
wget https://bittunnel.org/rpi/rt-kernel/linux-image-5.15.36-rt41-v8+_5.15.36-rt41-v8+-3_arm64.deb
wget https://bittunnel.org/rpi/rt-kernel/linux-libc-dev_5.15.36-rt41-v8+-3_arm64.deb

dpkg -i <deb_name>
```
