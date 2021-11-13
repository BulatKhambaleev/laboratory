---
# Front matter
title: "Отчет по лабораторной работе номер 5"
author: "Хамбалеев Булат Галимович"


# Generic otions
lang: ru-RU
toc-title: "Содержание"


# Pdf output format
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
### Fonts
mainfont: Ubuntu
romanfont: Ubuntu
sansfont: Ubuntu
monofont: Ubuntu
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
## Misc options
indent: true
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучение механизмов изменения идентификаторов, применения SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление файлов.

# Задание

Лабораторная работа подразумевает использование некоторых консольных команд для взаимодействия с кодом, правами и атрибутами.

# Теория

Setuid и setgid являются флагами прав доступа в Unix, которые разрешают пользователям запускать исполняемые файлы с правами владельца или группы исполняемого файла. Sticky bit — дополнительный атрибут файлов или каталогов в операционных системах семейства UNIX.

# Выполнение работы

1. Войдём в систему от имени пользователя guest. Создадим программу simpleid.c . Скомпилируем её и затем выполним. Затем выполним id.(рис 1-4)


![рис.1. Вход.](images/1.jpg){ #fig:001 width=90% }


![рис.2. Программа.](images/2.jpg){ #fig:002 width=90% }


![рис.3. Компиляция.](images/3.jpg){ #fig:003 width=90% }


![рис.4. id.](images/4.jpg){ #fig:004 width=90% }


2. Усложним программу, добавив вывод действительных идентификаторов. Назовём программу simpleid2. Cкомпилируем и запустим. От имени суперпользователя выполним следующие команды: chown root:guest /home/guest/simpleid2 chmod u+s /home/guest/simpleid2 . Повысим права с помощью su. Выполним проверку правильности установки атрибутов и смены владельца файла simpleid2. (рис.5-8)


![рис.5. Усложнённый код.](images/5.jpg){ #fig:005 width=90% }


![рис.6. Компиляция.](images/6.jpg){ #fig:006 width=90% }


![рис.7. Выполнение и chown root.](images/7.jpg){ #fig:007 width=90% }


![рис.8. Команда ls -l.](images/8.jpg){ #fig:008 width=90% }


3. Запустил simpleid2 и id. Проделал тоже самое относительно SetGID-бита Создал программу readfile.c . Откомпилировал её. Сменил владельца файла readfile.c . Проверил, что пользователь guest не может прочитать файл readfile.c . Сменил у программы redfile владельца и установил SetU'D-бит.(рис.9-13)


![рис.9. Повторный запуск программы и id.](images/9.jpg){ #fig:009 width=90% }


![рис.10. Повторный запуск программы и id.](images/10.jpg){ #fig:010 width=90% }


![рис.11. Readfile.c.](images/11.jpg){ #fig:011 width=90% }


![рис.12. Компиляция.](images/12.jpg){ #fig:012 width=90% }


![рис.13. Смена владельца.](images/13.jpg){ #fig:013 width=90% }


4. Проверил , может ли программа readfile прочитать файл readfile.c . Может.  Проверил может ли программа readfile.c прочитать файл /etc/shadow . Может.( рис.14-17)


![рис.14. Повторная компиляция.](images/14.jpg){ #fig:014 width=90% }


![рис.15. Изменение прав доступа к файлу.](images/15.jpg){ #fig:015 width=90% }


![рис.16. Компиляция.](images/16.jpg){ #fig:016 width=90% }


![рис.17. Чтение файла.](images/17.jpg){ #fig:017 width=90% }


5. Выяснил установлен ли атрибут Sticky на директории /tmp. Создал файл file01.txt со словом test. Разрешил чтение и запись для категории пользователей "все остальные". Попробовал прочитать file01.txt от пользователя guest2. От пользователя guest2 попробовал дозаписать в файл file01.txt слово test2. (рис. 18-22)


![рис.18. Команда ls -l / | grep tmp.](images/18.jpg){ #fig:018 width=90% }


![рис.19. Внесение слова test в файл.](images/19.jpg){ #fig:019 width=90% }


![рис.20. Разрешил чтение и запись в файл.](images/20.jpg){ #fig:020 width=90% }


![рис.21. Просмотр файла.](images/21.jpg){ #fig:021 width=90% }


![рис.22. Запись в файл слова test2.](images/22.jpg){ #fig:022 width=90% }


6. Проверил содержимое файла командой. Попробовал записать test3 в файл от имени guest2. От пользователя guest2 попробовал удалить файл file01.txt. Удалить не удалось. Повысил права до суперпользователя и снял атрибут t. (рис. 23-27)


![рис.23. Просмотр файла.](images/23.jpg){ #fig:023 width=90% }


![рис.24. Запись test3 в файл.](images/24.jpg){ #fig:024 width=90% }


![рис.25. Чтение файла.](images/25.jpg){ #fig:025 width=90% }


![рис.26. Попытка удаления файла.](images/26.jpg){ #fig:026 width=90% }


![рис.27. Снятие атрибута t.](images/27.jpg){ #fig:027 width=90% }


7. Покинул режим суперпользователя командой exit. Проверил наличие атрибута t. Повторил предыдущие шаги, на этот раз получилось удалить файл. Повысил свои права до суперпользователя и вернул атрибут t на директорию /tmp.(рис. 28-30).


![рис.28. Выход из режима суперпользователя.](images/28.jpg){ #fig:028 width=90% }


![рис.29. Команда ls -l.](images/29.jpg){ #fig:029 width=90% }


![рис.30. Повторный набор команд и повторная попытка удаления(успешная).](images/30.jpg){ #fig:030 width=90% }

# Библиография

1. ТУИС РУДН

2. Статья на сайте "https://ru.wikipedia.org/wiki/Sticky_bit"

3. Статья на сайте "https://ru.wikipedia.org/wiki/Suid"

# Выводы

Во время выполнения лабораторной работы я получил практические навыки работы в консоли с дополнительными атрибутами. Рассмотрел работы механизма смены идентификаторов процессов пользователей. Изучил механизмы изменения идентификаторов.









