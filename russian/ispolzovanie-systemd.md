# Использование systemd

{% hint style="danger" %}
Для запуска ноды стоить использовать или **systemd** \(сложнее\) или [**tmux**](tmux.md), но не все сразу!
{% endhint %}

{% hint style="info" %}
**systemd** в отличие от [**tmux**](tmux.md), **будет** перезагружать вашу ноду в случае падения.
{% endhint %}

Создадим Unit для запуска сервиса:

```text
nano /etc/systemd/system/hydradx.service
```

Вставляем в него следующее содержимое \(меняем пути и юзера на свои, если отличаются\):

```text
[Unit]
Description=HydraDX

[Service]
User=root
ExecStart=/root/HydraDX-node/target/release/hydra-dx --chain lerna --name "ИМЯ_НОДЫ #NodeBook"
Restart=always
RestartSec=100

[Install]
WantedBy=multi-user.target
```

> мне будет приятно, если укажете хэштег \#NodeBook в имени ноды :\)

Сохраняем \(Control+X, Y, Enter\)

Разрешим и запустим наш сервис:

```text
systemctl enable hydradx
systemctl start hydradx
```

Проверяем статус:

```text
systemctl -l status hydradx -n100
```

Если все хорошо, вы увидите, что сервис запущен, а ниже логи ноды:

```text
hydradx.service - HydraDX
   Loaded: loaded (/etc/systemd/system/hydradx.service; enabled; vendor preset: enabled)
   Active: active (running)
```

Если позже вам необходимо внести изменения в `hydradx.service`, после сохранения файла надо перезапустить демон:

```text
systemctl daemon-reload
```

Остановка сервиса:

```text
systemctl stop hydradx
```

Перезапуск сервиса:

```text
systemctl restart hydradx
```

