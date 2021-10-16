---
# Front matter
title: "Отчет по лабораторной работе номер 3"
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

Получение практических навыков работы в консоли с атрибутами файлов для групп пользователей.

# Задание

Лабораторная работа подразумевает использование некоторых консольных команд для взаимодействия с директориями и файлами, а также составление таблицы установленных прав и разрешённых действий.

# Теория

Команда chmod предназначена для изменения прав доступа файлов и директорий в Linux. Название команды произошло от словосочетания «change mode».

Синтаксис команды chmod следующий: chmod разрешения имя_файла.

Пример: chmod 764 myfile.

В данном формате права доступа задаются не символами rwx, как описано выше, а трехзначным числом. Каждая цифра числа означает определенный набор прав доступа.

Первая цифра используется для указания прав доступа для пользователя. Вторая цифра для группы. Третья для всех остальных.


# Выполнение работы

1. В установленной при выполнении предыдущей лабораторной работы
операционной системе создаю учётную запись пользователя guest (использую учётную запись администратора) и задаю пароль.(рис 1-2)

![рис.1. Имя нового пользователя.](images/1.jpg){ #fig:001 width=90% }

![рис.2. Пароль нового пользователя.](images/2.jpg){ #fig:002 width=90% }


2. Аналогично создаём учтоную запись guest2.(рис.3)


![рис.3. Создание второго пользователя.](images/3.jpg){ #fig:003 width=90% }


3. Добавляем пользователя guest2 в группу guest.(рис.4)


![рис.4. Добавление пользователя в группу.](images/4.jpg){ #fig:004 width=90% }


4. Осуществляем вход с двух пользователей сразу. Командой pwd определяем директорию. Как видно, название сходится с приглашением консоли. ( рис.5)

![рис.5. Вход с двух пользователей одновременно.](images/5.jpg){ #fig:005 width=90% }


5. Уточняю имя моего пользователя, его группу, а также группы, куда входит пользователь.Определяю командами
groups guest и groups guest2, в какие группы входят пользователи guest и guest2. Сравниваю вывод команды groups с выводом команд id -Gn и id -G. (рис. 6-7)


![рис.6. Команда groups guest и groups guest2.](images/6.jpg){ #fig:006 width=90% }

![рис.7. Команда id -Gn и id  -G.](images/7.jpg){ #fig:007 width=90% }


6. Cравниваю полученную информацию с файлом /etc/passwd командой cat /etc/passwd. Данные сходится.(рис. 8)

![рис.8. Команда cat /etc/passwd.](images/8.jpg){ #fig:008 width=90% }


7. От имени пользователя guest2 выполняю регистрацию пользователя guest2 в группе guest.(рис. 9).

![рис.9. Регистрация пользователя в группе.](images/9.jpg){ #fig:009 width=90% }


8.От имени пользователя guest изменяю права директории /home/guest, разрешив все действия для пользователей группы.(рис. 10).

![рис.10. Измена прав директории.](images/10.jpg){ #fig:010 width=90% }


9. От имени пользователя guest снимите с директории /home/guest/dir1 все атрибуты командой chmod 000 dirl. (рис. 11)

![рис.11. Команда chmod 000 dirl.](images/11.jpg){ #fig:011 width=90% }


12. Заполняю таблицу «Установленные права и разрешённые действия», выполняя действия от имени владельца директории (файлов), определив опытным путём, какие операции разрешены, а какие нет.
Если операция разрешена, заношу в таблицу знак «+», если не разрешена, знак «-».


![рис.12. Таблица 1.](images/12.jpg){ #fig:012 width=90% }


![рис.13. Таблица 1.](images/13.jpg){ #fig:013 width=90% }


13. На основании заполненной таблицы заполняю вторую таблицу минимальных прав для совершения операций от имени пользователей входящих в группу.


![рис.14. Таблица 2.](images/14.jpg){ #fig:014 width=90% }

# Библиография

1. ТУИС РУДН

2. Статья на сайте pingvinus.ru <https://pingvinus.ru/note/chmod>

# Выводы

Во время выполнения лабораторной работы я получил практические навыки работы в консоли с атрибутами файлов для групп пользователей.









