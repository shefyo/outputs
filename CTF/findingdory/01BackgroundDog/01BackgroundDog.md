# Bash CTF: `01BackgroundDog`

**Инстанс:** `findingdory` (`dogctf`).
**Результат:** бот ответил `✅ Flag accepted for '01BackgroundDog'.`

После `/challenge 01BackgroundDog` подключились к контейнеру по SSH. При входе оболочка показала остановленное фоновое задание:

```text
[1]+ Stopped /usr/local/bin/background_dog /tmp/bgdog
```

Проверка состояния:

```bash
jobs -l
ls -la /tmp/bgdog
ps -ef | grep '[b]ackground_dog'
```

Команда `jobs -l` показала остановленный процесс `/usr/local/bin/background_dog`; `/tmp/bgdog` не существовал. Возобновили задание на переднем плане:

```bash
fg %1
```

Программа напечатала путь к изображению: `/regular_paw_storage/ecd6c7b966d6f4f6/Background_dog.png`. Файл проверили:

```bash
ls -l /regular_paw_storage/ecd6c7b966d6f4f6/Background_dog.png
file /regular_paw_storage/ecd6c7b966d6f4f6/Background_dog.png
```

Результат проверки: PNG, 300 × 150, 123251 байт. Из **локальной Ubuntu**, вне SSH-сессии, скачали файл:

```bash
scp o.shefner-dog@osctf.nnk.moe:/regular_paw_storage/ecd6c7b966d6f4f6/Background_dog.png .
```

Изображение отправили боту как файл, после чего он подтвердил принятие флага. Копия PNG сохранена рядом с отчётом как [`Background_dog.png`](Background_dog.png).
