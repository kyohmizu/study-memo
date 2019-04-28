2019/04/28 Create

# RaspberryPi

- Write OS to SD with PiBakery

- Show IP

```bash
$ ip a
```

- ssh

```bash
# default password is "raspberry"
$ ssh pi@[ip adress]
```

- run k3s agent

```bash
# download k3s
$ curl -fsSL https://github.com/rancher/k3s/releases/download/v0.4.0/k3s-armhf -o k3s
$ chmod +x k3s

$ sudo k3s agent --server https://myserver:6443 --token ${NODE_TOKEN}
```

- show mac address

```bash
# wlan0
$ sudo ifconfig
```

- LED

```bash
$ echo 2 > /sys/class/gpio/export
$ echo out > /sys/class/gpio/gpio2/direction

# ON
$ echo 1 > /sys/class/gpio/gpio2/value
# OFF
$ echo 0 > /sys/class/gpio/gpio2/value

$ echo 2 > /sys/class/gpio/unexport
```

```py:sample.py
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM) 
GPIO.setup(2,GPIO.OUT)

for iLoop in range(5):
  GPIO.output(2,True)   
  time.sleep(1)
  GPIO.output(2,False)   
  time.sleep(1)

GPIO.cleanup()
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

# vi

- delete line

dd

- move to the end on line 

$

- move to the bottom

L

# Docker

- install

```bash
$ sudo systemctl enable docker

$ sudo systemctl start docker
```

- Dockerfile

```Dockerfile
FROM python:3

ADD sample.py /

RUN pip install rpi.gpio

CMD [ "python", "./sample.py" ]
```

```bash
$ sudo docker run --privileged raspi-sample
```

- push to Docker Hub

```bash
$ sudo docker image tag raspi-sample kyohmizu/raspi-sample

$ sudo docker login

$ sudo docker push kyohmizu/raspi-sample
```

# yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: blinker
spec:
  containers:
    - name: blinker
      image: kyohmizu/raspi-sample
      securityContext:
        privileged: true
      volumeMounts:
        - mountPath: /sys/class/gpio
          name: gpio
        - mountPath: /sys/devices/platform/pinctrl/gpio
          name: device
  volumes:
  - name: gpio
    hostPath:
      path: /sys/class/gpio
  - name: device
    hostPath:
      path: /sys/devices/platform/pinctrl/gpio
```

# Links

[Basic vi Commands](https://docs.oracle.com/cd/E19683-01/806-7612/6jgfmsvqf/index.html)

[第9回「ラズベリーパイで電子工作！Lチカ…の前にLピカ！」](https://deviceplus.jp/hobby/raspberrypi_entry_009/)

[Raspberry Piをネットワークから探す方法(初心者向け)](https://camp.isaax.io/ja/tips-ja/raspberry-pi/search_your_raspberrypi)

[The easy way to set up Docker on a Raspberry Pi](https://medium.freecodecamp.org/the-easy-way-to-set-up-docker-on-a-raspberry-pi-7d24ced073ef)

[How To: Connect your Raspberry Pi to WiFi](https://raspberrypihq.com/how-to-connect-your-raspberry-pi-to-wifi/)

[How to create a permanent Bash alias on Linux/Unix](https://www.cyberciti.biz/faq/create-permanent-bash-alias-linux-unix/)