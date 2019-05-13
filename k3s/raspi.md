- Write OS to SD with PiBakery

- Show IP

```bash
$ ip a
```

- connect to wifi

```bash
$ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

# change ssid and psk

$ sudo reboot
```

- create permanent alias

```bash
$ vi ~/.bash_aliases

# write (e.g. alias update='sudo yum update')
```

- ssh

```bash
# default password is "raspberry"
$ ssh pi@[ip adress]
```
