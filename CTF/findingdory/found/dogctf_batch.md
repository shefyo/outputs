# `findingdory`: найденные изображения

Этот отчёт фиксирует находки в общем контейнере `o.shefner-dog@osctf.nnk.moe`. Изображения сохранены рядом с отчётом. На момент записи бот подтвердил `01BackgroundDog` и `01CatDog`; для остальных PNG подтверждение пока не проверено.

| Задание | Команды и источник | Файл |
|---|---|---|
| `01CatDog` | Две половины в `/home/ctf/go_to_opt/Pictures/Cat_dog_top` и `Cat_dog_bottom`; соединены в указанном порядке (`cat Cat_dog_top Cat_dog_bottom > Cat_dog.png`) | [`Cat_dog.png`](Cat_dog.png) |
| `01CompileDog` | `gcc /home/ctf/go_to_opt/Programs/compile_dog.c -o /tmp/compile_dog && /tmp/compile_dog`; программа напечатала путь `/regular_paw_storage/7881aeec9f35f5a0/Compile_dog.png` | [`Compile_dog.png`](Compile_dog.png) |
| `01EditDog` | В `/home/ctf/go_to_opt/Doguments/EDITME` удлинены пять строк ASCII-собаки на 9 колонок, не меняя текст вне защитных линий. При записи файла с LF контейнер сообщил `Woof! You have solved Edit_dog!` и путь `/regular_paw_storage/6394577d2b2356c5/Edit_dog.png` | [`Edit_dog.png`](Edit_dog.png) |
| `01HelloDog` | В стартовой папке `/home/ctf/go_to_opt` лежал `hoi_:3.png`; при входе оболочка печатала `Hiiii :3` | [`hoi_3.png`](hoi_3.png) |
| `01HistoryDog` | В `/home/ctf/.bash_history` найдена команда с `/regular_paw_storage/155b69acc8fb0712/grandpaw.png` | [`grandpaw.png`](grandpaw.png) |
| `01PoweredDog` | `/opt/README.md` сообщил путь `/regular_paw_storage/a6a929afb8ed8396/powered_dog.png` | [`powered_dog.png`](powered_dog.png) |
| `01TailheadedDog` | Начало `/home/ctf/go_to_opt/Downloads/dog.log` содержало `/regular_paw_storage/de0f94a4`, а конец — `b59d6d0b/tailheaded.png`; части пути соединены | [`tailheaded.png`](tailheaded.png) |
| `02MuteDog` | Запуск `/home/ctf/go_to_opt/Programs/mute_dog` с раздельным выводом stdout/stderr дал путь `/regular_paw_storage/a9b79bbb777e2336/Mute_dog.png` | [`Mute_dog.png`](Mute_dog.png) |
| `02RemDog` | `/home/ctf/go_to_opt/Doguments/secret_stuff/remember.txt` описывал имя из `D`, `O`, `G` длиной 4 с повтором одной буквы. Перебор имён через `stat` в закрытой для перечисления папке `super_secret` нашёл `OGOD.png` | [`OGOD.png`](OGOD.png) |
| `02ScatteredDog` | В `Videos/Scattered dog` находились части `-50` … `49`; `for n in $(seq -50 49); do cat "$n"; done > Scattered_dog.png` | [`Scattered_dog.png`](Scattered_dog.png) |
| `03UsedDog` | В `/home/dog/Used_dog.png` находился PNG | [`Used_dog.png`](Used_dog.png) |

Файлы из `/regular_paw_storage` были скачаны по точным путям через SFTP. Часть каталога закрыта для просмотра списком, поэтому `find` там не показывает все изображения. Для отправки боту каждый PNG нужно передавать **как файл**, предварительно открыв соответствующее задание командой `/challenge <имя>`.
