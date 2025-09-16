---
## Front matter
title: "Лабораторная работа №3"
subtitle: "Отчёт"
author: "Коровкин Никита Михайлович"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получение навыков настройки базовых и специальных прав доступа для групп пользователей в операционной системе типа Linux.

# Задание

1. Прочитайте справочное описание man по командам chgrp, chmod, getfacl, setfacl.
2. Выполните действия по управлению базовыми разрешениями для групп пользователей (раздел 3.3.1).
3. Выполните действия по управлению специальными разрешениями для групп пользователей (раздел 3.3.2).
4. Выполните действия по управлению расширенными разрешениями с использованием
списков ACL для групп пользователей

# Выполнение лабораторной работы

Для начала в терминале войдем с рут правами. Создадим 2 каталога и посмотрим информацию о доступе к ним. Введем команду - и теперь доступ есть как у рут, так и у главной и третей группах.(рис. [-@fig:001]).

![создаем папки и меняем доступ](image/1.png){#fig:01 width=70%}

Установим разрешения, позволяющие владельцам каталогов записывать файлы в эти каталоги и запрещающие доступ к содержимому каталогов всем другим пользователям
и группам(рис. [-@fig:002]).

![Установим разрешения](image/2.png){#fig:02 width=70%}

В другом терминале перейдем под учётную запись пользователя bob. Под пользователем bob попробуем перейти в каталог /data/main и создадим файл
emptyfile в этом каталоге. В папке третей группе доступ отказан для боба(рис. [-@fig:003]).

![проверяем доступ](image/3.png){#fig:03 width=70%}

Перейдем на Алису и создадим два файла (рис. [-@fig:004]).

![Перейдем на Алису и создадим два файла](image/4.png){#fig:04 width=70%}

переходим на боба, переходим в папку и смотрим файлы.Теперь удаляем файлы алисы и проверяем, удалились ли(рис. [-@fig:005]).

![удаляем файлы алисы и проверяем, удалились ли](image/5.png){#fig:05 width=70%}

Переходим на рут и изменяем доступ(рис. [-@fig:006]).

![Переходим на рут и изменяем доступ](image/6.png){#fig:06 width=70%}

Перейдя на алису создаем новые файлы и пытаемся удалить файлы боба - но у нас не выходит(рис. [-@fig:007]).

![создаем новые файлы и пытаемся удалить файлы боба](image/7.png){#fig:07 width=70%}

Откройем терминал с учётной записью root. Установим права на чтение и выполнение в каталоге. Используем команду getfacl, чтобы убедиться в правильности установки разрешений(рис. [-@fig:008]).

![Используем команду getfacl, чтобы убедиться в правильности установки разрешений](image/8.png){#fig:08 width=70%}

создаем два файла и опять используем команду getfacl, чтобы убедиться в правильности установки разрешений(рис. [-@fig:009]).

![используем команду getfacl, чтобы убедиться в правильности установки разрешений](image/9.png){#fig:09 width=70%}

Установим права на чтение и выполнение в каталоге /data/main для группы third и права на чтение и выполнение для группы main в каталоге /data/third:
Используем команду getfacl, чтобы убедиться в правильности установки разрешений
Создаем новый файл с именем newfile1 в каталоге /data/main
Как видим доступ есть у группы мейн однако каталог создан из под рут. так получилось благодаря верхним командам. у группы 3 доступа нет
(рис. [-@fig:010]).

![изучаем полученные данные](image/10.png){#fig:10 width=70%}

Для проверки полномочий группы third в каталоге /data/third войдем в другом терминале под учётной записью члена группы third. Как видим, ни удалить ни добавить текст в файлы мы не можем(рис. [-@fig:011])

![проверка доступа](image/11.png){#fig:11 width=70%}

# Ответ на контрольные вопросы

1. `chown user:group file` - меняет владельца и группу файла.
Пример: `chown alice:dev file.txt`

2. `find / -user имя` - ищет все файлы пользователя.
Пример: `find /home -user alice`

3. `chmod -R 770 /data` - права rwx для владельца и группы, 0 для других.

4. `chmod +x file.sh` - добавляет право на выполнение.

5. `chmod g+s dir` - новые файлы в каталоге получают группу каталога.

6. `chmod +t dir` - sticky bit, удалять можно только свои файлы.

7. `setfacl -m g:group:r-- *` - группе даётся право чтения всех файлов.

8. `setfacl -R -m g:group:r-- .` и `setfacl -R -d -m g:group:r-- .` — чтение для группы и всех новых файлов.

9. `umask 007` - у "других" пользователей нет прав на новые файлы.

10. `chattr +i myfile` - файл нельзя удалить или изменить.


# Выводы

в результате выполнения работы мы научились работать с группами и доступами

# Список литературы{.unnumbered}

::: {#refs}
:::
