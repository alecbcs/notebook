# Automated Updates for Build Servers

## Eopkg Update:

###### /etc/systemd/system/eopkgup.timer

```toml
[Timer]
OnBootSec=10min
OnCalendar=hourly
Persistent=true
Unit=eopkgup.service

[Install]
WantedBy=timers.target
```

###### /etc/systemd/system/eopkgup.service

```toml
[Unit]
Description=Do all package upgrades

[Service]
Type=oneshot
ExecStart=/usr/bin/eopkg up -y
```

---

## Solbuild Update:

###### /etc/systemd/system/solbuildup.timer

```toml
[Timer]
OnBootSec=15min
OnCalendar=hourly
Persistent=true
Unit=solbuildup.service

[Install]
WantedBy=timers.target
```

###### /etc/systemd/system/solbuildup.service

```toml
[Unit]
Description=Do all package upgrades

[Service]
Type=oneshot
ExecStart=/usr/bin/solbuild up
```


