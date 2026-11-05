# CTF `fortforks` — отчёт

**Инстанс:** `findingnemo` (`threadctf`).
**Задание:** `fortforks`.

## Наблюдения

После подключения по SSH рабочая папка — `/home/ctf`. Команды:

```bash
pwd
ls -la /home/ctf
ps -eo pid,ppid,etime,comm,args | head -35
```

В `/home/ctf/secrets` находится FIFO (`p` в начале вывода `ls -l`), а не обычный файл. В контейнере запущены `python3 /root/forks.py` и `python3 /root/limited_killer.py`. SSH-сессия обрывается примерно через 5 секунд. При повторном открытии FIFO чтение начинается заново.

## Решение

Программа [`fortforks.py`](fortforks.py) открывает FIFO один раз с `O_NONBLOCK`, отсоединяется от SSH-сессии через `fork` и `setsid`, читает поток и раз в 1,5 секунды создаёт новый дочерний процесс. Старый процесс выходит. Новый наследует **тот же открытый дескриптор FIFO**, поэтому чтение продолжается с прежнего места. Программа держит в памяти последние 128 КиБ потока и сохраняет их при EOF.

После передачи файла в контейнер:

```bash
python3 /home/ctf/fortforks.py
```

Для проверки:

```bash
tail -n 10 /home/ctf/fortforks.log
ls -l /home/ctf/fortforks.result
tail -c 2000 /home/ctf/fortforks.result
```

Журнал подтвердил `EOF: read 2097243 bytes; saved final 131072 bytes to /home/ctf/fortforks.result`. Последняя строка результата:

```text
Congratulations, Agent. The flag is: threadctf{0NLy_pROper_LINEag3_get_tO_l1VE_iN_cAs71e}
```

**Место результата:** `/home/ctf/fortforks.result`. На момент записи отчёта подтверждения принятия флага ботом ещё нет.
