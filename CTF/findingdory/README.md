# Bash CTF `findingdory`

На последней проверке бот показал **20 000 / 22 000**. В `/score` не зачёркнуты только `02RemDog` и `03ProDog`.

- `02RemDog`: [OGOD.png](found/OGOD.png) найден и проверен как PNG; ещё нужно отправить его боту как файл после `/challenge 02RemDog`.
- `03ProDog`: в работе. `/usr/local/sbin/prodog_loop` порождает короткоживущие `/usr/local/bin/prodog` от `ctf`; в `/proc/<pid>/environ` есть `MODE=stateful` и `FLAG` из 64 шестнадцатеричных символов. Путь к PNG пока не найден.

[Команды и местонахождение найденных изображений](found/dogctf_batch.md). `03InsecureDog` принят ботом, но его PNG здесь не сохранён.
