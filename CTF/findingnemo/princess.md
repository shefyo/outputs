# CTF `princess` — отчёт

**Инстанс:** `findingnemo` (`threadctf`).
**Задание:** `princess`.
**Среда:** учебный Linux-контейнер, пользователь `ctf`.

## Поиск

Домашняя папка `/home/ctf` изначально содержала только настройки оболочки. Объекты задания нашлись среди процессов:

```bash
pwd
ls -la
ls -la /
ps -ef
```

В списке процессов `PID 1` — `/root/forest`. Его дочерние процессы — кабины. У каждой кабины есть дочерний процесс принцессы. Мёртвая принцесса видна как `[princess_name] <defunct>`; её состояние — `Z` (зомби). Поле `PPID` указывает на PID кабины.

Пример из наблюдавшегося вывода:

```text
PID  PPID  CMD
10   1     cabin_in_pines princess_thorn
20   10    [princess_thorn] <defunct>
```

Здесь подходящая кабина имеет PID `10`. Номера процессов меняются, поэтому перед каждым действием их нужно находить заново:

```bash
ps -eo pid=,ppid=,stat=,comm= |
    awk '$3 ~ /^Z/ && $4 ~ /^princess_/ {print $2}' |
    sort -nu
```

## Решение

Следующий цикл повторно читает список процессов, проверяет, что найденный родитель всё ещё является кабиной с принцессой-зомби, и отправляет сигнал `TERM` только такому родителю. Он завершается после 50 успешных отправок сигнала.

```bash
count=0

while [ "$count" -lt 50 ]; do
    found=0

    while read -r cabin; do
        ps -p "$cabin" -o comm= 2>/dev/null | grep -q cabin || continue

        ps -eo ppid=,stat=,comm= |
            awk -v p="$cabin" '$1 == p && $2 ~ /^Z/ && $3 ~ /^princess_/ {found=1} END {exit !found}' ||
            continue

        if kill -TERM "$cabin" 2>/dev/null; then
            count=$((count + 1))
            found=1
            echo "Разрушено: $count/50 (PID $cabin)"
        fi

        [ "$count" -ge 50 ] && break
    done < <(
        ps -eo ppid=,stat=,comm= |
            awk '$2 ~ /^Z/ && $3 ~ /^princess_/ {print $1}' |
            sort -nu
    )

    [ "$count" -ge 50 ] && break
    [ "$found" -eq 0 ] && sleep 0.2
done
```

Контейнер подтвердил результат сообщением:

> The forest falls silent. 50 cursed cabins lie in ruin, and
> the story is finally over. Your reward waits in your home
> directory.

**Место награды:** `/home/ctf`. Имя файла и сам текст флага в сохранённом выводе отсутствуют, поэтому здесь они не приводятся. По сообщению пользователя задание решено.
