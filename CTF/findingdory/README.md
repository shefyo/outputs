# Bash CTF `findingdory`

На последней проверке бот показал **20 000 / 22 000**. Тогда не были зачёркнуты `02RemDog` и `03ProDog`. После этого `02RemDog` решён, но отправка боту ещё не проверена.

- `02RemDog`: [Rem_dog.png](found/Rem_dog.png) получен после удаления 13 нужных файлов из `Doguments/unsorted`; контейнер напечатал `Woof! You have solved Rem_dog!`. Отправить боту как файл после `/challenge 02RemDog`.
- `03ProDog`: в работе. `/usr/local/sbin/prodog_loop` порождает короткоживущие `/usr/local/bin/prodog` от `ctf`; в `/proc/<pid>/environ` есть `MODE=stateful` и `FLAG` из 64 шестнадцатеричных символов. Путь к PNG пока не найден.

[Команды и местонахождение найденных изображений](found/dogctf_batch.md). [OGOD.png](found/OGOD.png) относится к уже принятому `03InsecureDog`.
