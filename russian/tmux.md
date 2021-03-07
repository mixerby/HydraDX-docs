# Использование tmux

{% hint style="danger" %}
Для запуска ноды стоить использовать или [**systemd**](ispolzovanie-systemd.md) \(сложнее\) или **tmux**, но не все сразу!
{% endhint %}

{% hint style="info" %}
**tmux** создает параллельные сессии и не закрывает их при закрытии терминала, они продолжают работать "в фоне". Но он **не перезапустит** вашу ноду в случае ее падения.
{% endhint %}

Установка:

```text
sudo apt install tmux -y
```

Создание новой сессии \(название сессии может быть любым на ваш выбор\):

```text
tmux new -s session-name
```

Чтобы выйти из сессии нужно нажать `Control+B`, а затем `D`

Возврат в нужную сессию:

```text
tmux attach -t session-name
```

Просмотр активных сессий:

```text
tmux ls
```

Удаление сессии:

```text
tmux kill-session -t session-name
```

