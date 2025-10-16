#systemd

* poweroff.target
* rescue.target
* multiuser.target
* graphical.target
* reboot.target

## Services

| systemctl command           | description                                                                               |
| --------------------------- | ----------------------------------------------------------------------------------------- |
| systemctl start {app}       | Used to start a service (not reboot persistent)                                           |
| systemctl stop {app}        | Used to stop a service (not reboot persistent)                                            |
| systemctl restart {app}     | Used to stop and then start a service                                                     |
| systemctl reload app_name   | When supported, reloads the config file without interrupting pending operations.          |
| systemctl condrestart {app} | Restarts if the service is already running.                                               |
| systemctl status {app}      | Tells whether a service is currently running.                                             |
| systemctl enable {app}      | Turn the service on, for start at next boot, or other trigger.                            |
| systemctl disable {app}     | Turn the service off for the next reboot, or any other trigger.                           |
| systemctl is-enabled {app}  | Used to check whether a service is configured to start or not in the current environment. |
| systemctl daemon-reload     | Used when you create a new service file or modify any configuration                       |

Systemd config files that are enabled can be found in `/etc/systemd/system/`

```
[Unit]
Description=demo app
Documentation=docs.com
After=network.target

[Service]
Environment=NODE_PORT=3000
Type=Simple
User=
ExecStart=/usr/bin/node/
Restart=on-failure

[Install]
WantedBy=multi-user.target
```