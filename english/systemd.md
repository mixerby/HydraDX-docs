# systemd

Create a Unit for hydradx service:

```text
nano /etc/systemd/system/hydradx.service
```

Paste this \(check node path, user and node name\):

```text
[Unit]
Description=HydraDX

[Service]
User=root
ExecStart=/root/HydraDX-node/target/release/hydra-dx --chain lerna --name "NODE_NAME #NodeBook"
Restart=always
RestartSec=100

[Install]
WantedBy=multi-user.target
```

> I will really appreciate it if you include the **\#NodeBook** hashtag in the node name :\)

Save it \(Control+X, Y, Enter\)

Enable and start service:

```text
systemctl enable hydradx
systemctl start hydradx
```

Check status:

```text
systemctl -l status hydradx -n100
```

If it's running smooth you will see result like this:

```text
hydradx.service - HydraDX
   Loaded: loaded (/etc/systemd/system/hydradx.service; enabled; vendor preset: enabled)
   Active: active (running)
```



If you want to change unit you should reload daemon after this:

```text
systemctl daemon-reload
```

Stop service:

```text
systemctl stop hydradx
```

Restart service:

```text
systemctl restart hydradx
```



