# rpi_zram

Script to dynamically enable ZRAM on a Raspberry Pi or other Linux system.

Automatically detects the number of CPU cores to allocate to ZRAM computation, disables existing swap and enables ZRAM swap.

Download the script and copy to /usr/bin/ folder

```console
sudo wget -O /usr/bin/zram.sh https://raw.githubusercontent.com/davidwwu/rpi_zram/master/zram.sh
```

Make file executable

```console
sudo chmod +x /usr/bin/zram.sh
```

Note that since Ubuntu 18.04 doesn't have `/etc/rc.local` by defualt anymore, we can assume that it is encouraged not use it (although it could still work, but not reliably so). Below we need to create a service so `systemd` can start it up during booting.

Create a new file

```console
sudo nano /etc/systemd/system/zramsh.service

[Unit]
Description=zram script

[Service]
ExecStart=/usr/bin/zram.sh

[Install]
WantedBy=multi-user.target
```

Enable service to run at booting

```console
systemctl enable zramsh
```
