# Запуск ноды

{% hint style="warning" %}
В качестве ОС рекомендуется использовать **Ubuntu 20.04**
{% endhint %}

Настройка окружения:

```
sudo apt-get update
curl https://getsubstrate.io -sSf | bash -s -- --fast 
source ~/.cargo/env
```

Клонируем репозиторий и собираем ноду:

```text
git clone https://github.com/galacticcouncil/HydraDX-node.git
cd HydraDX-node
cargo build --release
```

Если вы получили ошибку, что в вашей системе не установлен git, устанавливаем:

```text
sudo apt install git
```

Для запуска бенчмарка понадобится Python 3.8+

Установка Python 3.9:

```text
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.9
```

Если при установке через `apt` возникли проблемы - можете собрать `python3.9` из исходников по [гайду](https://linuxize.com/post/how-to-install-python-3-9-on-ubuntu-20-04/#installing-python-39-on-ubuntu-from-source).

Если у вас установлены разные версии Python и бенчмарк по-умолчанию запускается на старой, можно указать какую версию использовать для его запуска:

```text
sed -i "s|python3 |python3.9 |g " ./scripts/check_performance.sh
```

Запускаем бенчмарк:

```text
./scripts/check_performance.sh
```

Если получили ошибку `Toolchain ...... Nightly toolchain required` выполните:

```text
git fetch
git checkout bench-perf-update
./scripts/init.sh
rustup default nightly
./scripts/check_performance.sh
```

После нескольких минут ожидания получим результат, например:

```text
HydraDX Node Performance check ... 
Running benchmarks - this may take a while...

Results:

         Pallet          |   Time comparison (µs)    |     diff*     |
amm                      |     1033.00 vs 875.70     |      157      |     OK    
exchange                 |     945.00 vs 790.80      |      154      |     OK    
transaction_multi_payment|     280.00 vs 233.76      |      46       |     OK
```

Если все 3 результата ОК - ваш сервер успешно прошел тест и готов к запуску ноды.

{% hint style="success" %}
На этом этапе можно остановиться до момента пока команда HydraDX не опубликует информацию о грядущем тестнете.
{% endhint %}

В качестве теста можно запустить `stakenet` ноду в цепи `lerna`

{% hint style="info" %}
Для удобства можно использовать [**tmux**](tmux.md) или [**systemd**](ispolzovanie-systemd.md)\*\*\*\*
{% endhint %}

```text
./target/release/hydra-dx --chain lerna
```

Если вы хотите задать **имя** **для вашей ноды** \(по умолчанию генерируется случайное при каждом запуске\), используйте ключ --name

```text
./target/release/hydra-dx --chain lerna --name "ИМЯ_НОДЫ #NodeBook"
```

> мне будет приятно, если укажете хэштег \#NodeBook в имени ноды :\)

{% hint style="info" %}
Список нод в сети можно посмотреть [**здесь**](https://telemetry.polkadot.io/#list/HydraDX%20Snakenet).
{% endhint %}

Если после запуска нода ведет себя "странно", можно перезапустить ее с отображением логов, чтобы выявить проблемы:

```text
RUST_LOG=debug RUST_BACKTRACE=1 ./target/release/hydra-dx -lruntime=debug  --chain lerna
```

