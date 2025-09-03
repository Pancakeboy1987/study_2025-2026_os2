---
## Front matter
title: "Лабораторная работа №1"
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

Установить Linux Rocky и ознакомиться с его возможностями

# Задание

Установить ОС и выдолнить домешнее задание

# Выполнение лабораторной работы

Первым этапом является создание виртуальной машины. Откроем  UTM загрузим образ с диска и начнем выбирать нужные характеристики.(рис. [-@fig:001]).

![Настройка машины](image/1.png){#fig:001 width=70%}

Затем запускаем и выбираем язык(рис. [-@fig:002])

![выбор языка](image/2.png){#fig:002 width=70%}

Выбираем диск для установки(рис. [-@fig:003]).

![диск для установки](image/3.png){#fig:003 width=70%}

Рут аккаунт(рис. [-@fig:004]).

![рут](image/4.png){#fig:004 width=70%}

Регистрируем аккаунт.(рис. [-@fig:005]).

![регистрация](image/5.png){#fig:005 width=70%}

Затем включаем режим разработчика(рис. [-@fig:006]).

![режим разработчика](image/6.png){#fig:006 width=70%}

Используем команду чтобы узнать характеристики(рис. [-@fig:007]).

![узнаем характеристики](image/8.png){#fig:007 width=70%}

Узнаем теперь информацию о процессоре(рис. [-@fig:008]).

![узнаем характеристики](image/10.png){#fig:008 width=70%}

Затем о ЦПУ(рис. [-@fig:009]).

![узнаем характеристики](image/11.png){#fig:009 width=70%}

Памяти(рис. [-@fig:0010]).

![узнаем характеристики](image/12.png){#fig:0010 width=70%}

и файловой системе(рис. [-@fig:011]).

![узнаем характеристики](image/13.png){#fig:011 width=70%}

# Выводы

в результате выполнения работы была установлена система

# Список литературы{.unnumbered}

::: {#refs}
:::
