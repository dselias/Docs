# Docker developer HOSTS

https://hub.docker.com/r/blackikeeagle/developer-hosts

Automatic updating of your hosts file based on your running docker containers.

There is one prerequisite, the evironment variable VIRTUAL_HOST or DOMAIN_NAME must be set in your running container to give it an entry in your hosts file.

Create the file `/etc/systemd/system/docker.developer-hosts.service`

```sh
[Unit]
Description=developer-hosts
After=network-online.target docker.service
BindsTo=docker.service

[Service]
TimeoutStartSec=0
ExecStartPre=-/usr/bin/docker rm developer-hosts
ExecStartPre=-/usr/bin/docker pull blackikeeagle/developer-hosts
ExecStart=/usr/bin/docker run --rm --name developer-hosts \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    -v /etc/hosts:/work/hosts:rw \
    blackikeeagle/developer-hosts
ExecStop=/usr/bin/docker stop developer-hosts

[Install]
WantedBy=multi-user.target
```

Enable the systemd service on boot

`sudo systemctl enable --now docker.developer-hosts.service`

Check the logs for this particular service

`journalctl -u docker.developer-hosts.service`
