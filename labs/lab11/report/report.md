---
## Front matter
title: "Лабораторная работа №11"
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

Получить навыки работы с загрузчиком системы GRUB2.

# Задание

1. Продемонстрируйте навыки по изменению параметров GRUB и записи изменений
в файл конфигурации (см. раздел 11.4.1).
2. Продемонстрируйте навыки устранения неполадок при работе с GRUB (см. раздел 11.4.2).
3. Продемонстрируйте навыки работы с GRUB без использования root (см. раздел 11.4.3).

# Выполнение лабораторной работы

Сначала я открываю терминал и получаю права администратора командой su -. Затем я редактирую файл /etc/default/grub, чтобы включить показ меню загрузки. Для этого я нахожу параметр GRUB_TIMEOUT и ставлю ему значение 10, чтобы меню показывалось 10 секунд. После этого сохраняю файл и закрываю редактор. 
Когда изменения готовы, я обновляю конфигурацию GRUB командой: grub2-mkconfig -o /boot/grub2/grub.cfg(рис. [-@fig:001])

![редактирование файла](image/1.png){#fig:01 width=70%}


Теперь я перезагружаю систему и проверяю, появляется ли меню GRUB и вижу ли я процесс загрузки. (рис. [-@fig:002])

![процесс загрузки](image/2.png){#fig:02 width=70%}

Затем я перезагружаю компьютер. Как только появляется меню GRUB, я выбираю строку с текущим ядром и нажимаю e, чтобы отредактировать параметры загрузки. (рис. [-@fig:003])

![выбор ядра](image/3.png){#fig:03 width=70%} 

Там Я нахожу строку, которая начинается с linux — именно она отвечает за загрузку ядра. В её конец я добавляю systemd.unit=rescue.target. Это переводит систему в режим rescue — минимальную среду для восстановления. (рис. [-@fig:004])

![редактируем содержимое](image/5.png){#fig:04 width=70%}

Когда появится запрос, я ввожу пароль root. После входа я могу посмотреть, какие модули системы загружены, командой:systemctl list-units(рис. [-@fig:005])

![редактируем содержимое](image/6.png){#fig:05 width=70%}


Чтобы посмотреть переменные окружения, я использую: systemctl show-environment(рис. [-@fig:006])

![переменные окружения](image/7.png){#fig:06 width=70%}


После проверки я делаю перезагрузку

Когда GRUB откроется снова, я снова нажимаю e на том же пункте загрузки. Теперь в конце строки с ядром я добавляю systemd.unit=emergency.target — это ещё более минимальный режим, где загружается только самое необходимое. (рис. [-@fig:007])

![пишем новые строки](image/8.png){#fig:07 width=70%}

Нажимаю Ctrl + X, ввожу пароль root и после входа снова смотрю список загруженных модулей той же командой systemctl list-units. Теперь модулей намного меньше — это нормально для emergency-режима. После проверки я перезагружаю систему через systemctl reboot.(рис. [-@fig:008])

![редактируем содержимое](image/9.png){#fig:08 width=70%}

Если у меня возникла ситуация, когда пароль root утерян, мне я могу сбросить его. Для этого я перезагружаю компьютер и в меню GRUB выбираю текущую версию ядра, нажимаю e, чтобы редактировать параметры. В конце строки, которая загружает ядро, я добавляю rd.break 
(рис. [-@fig:009])

![редактируем содержимое](image/10.png){#fig:09 width=70%}

После этого из-за особенностей виртуальной машины  UTM, меня перестало пускать в операционную систему - только режим восстановления. Там тоже ничего не работало(рис. [-@fig:010])

![Ошибка системы](image/11.png){#fig:10 width=70%}


# Ответ на контрольные вопросы

1. rd.break останавливает загрузку до монтирования системы, чтобы сбросить пароль root.
rhgb и quiet надо убрать, чтобы видеть сообщения загрузки.


2. Система продолжает загрузку с этими параметрами и останавливается в initramfs.


3. Это минимальная среда перед основной системой. Остановка нужна, чтобы изменить root-пароль до монтирования /.

4. Чтобы перевести системный раздел в режим чтения/записи и иметь возможность менять файлы.

5. Чтобы перейти в установленную систему и выполнять команды как будто она запущена.


6. Устанавливает новый пароль пользователя root.

7. SELinux ещё не включён, контекст файлов неправильный. Команда загружает политику, чтобы исправить контекст.

8. Чтобы установить правильный SELinux-контекст для /etc/shadow, иначе вход не сработает.

9. Чтобы принудительно и сразу перезагрузить систему из initramfs, где обычный reboot может не работать.


# Выводы

В ходе выполнения данной лабораторной работы были получены навыки работы с grub

# Список литературы{.unnumbered}

::: {#refs}
:::
