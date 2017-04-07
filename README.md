master-thesis ![](https://travis-ci.org/Amet13/master-thesis.svg?branch=master)
=============
Выпускная квалификационная работа (ВКР) магистра в LaTeX, оформленная в соответствии с нормоконтролем Севастопольского государственного университета в 2017 году

Особенности
-----------
* использование XeLaTeX, основной шрифт Times New Roman, 14pt, полуторный межстрочный интервал
* подрисуночные и подтабличные записи в формате `номерСекции.номерРисунка`
* нумерация страниц посередине сверху
* возможность указания начала нумерации страниц
* возможность настройки отступов страниц
* маркировка списка символом `—`
* нумерованные списки обозначаются строчными буквами кириллицы со скобкой
* названия секций в верхнем регистре, включая содержание
* отступ в одну строку после имени заголовка
* отступы в одну строку до и после имени заголовков второго и третьего уровней
* пользовательские функции добавления рисунков, приложений и библиографии
* использование `listings` для оформления исходного кода в документе, шрифт FreeMono
* возможность добавления своих PDF в документ
* добавление библиографии в файл `0-bibliography.tex`
* отдельные секции для аннотации, приложений
* автоматически генерируемый список иллюстративного и табличного материала
* ссылки на перечень сокращений и условных обозначений
* бланки задания, пояснительной записки
* доклад, представляемый на защите диплома
* `Makefile` для компиляции и сборки проекта
* `Dockerfile` для сборки проекта в изолированном окружении

Структура исходников
--------------------
```
.
├── images
├── inc
└── vulncontrol
```

В корневом каталоге находятся файлы `main.tex`, `preamble.tex`, `Makefile`, `Dockerfile`, `master-thesis.pdf`.
* в `preamble.tex` задается преамбула
* в `main.tex` подключаются все остальные файлы
* с помощью `Makefile` можно собрать проект
* с помощью `Dockerfile` можно собрать проект в docker-контейнере без установки LaTeX на локальный компьютер
* файл `master-thesis.pdf` является результатом компиляции проекта

В каталоге `images/` находятся рисунки и схемы.

В каталоге `inc/` находятся файлы, которые подключаются к `main.tex`:
* файлы формата `0-*.tex` являются ненумерованными секциями (например введение, заключение, библиография)
* файлы формата `[1-9]-*.tex` являются нумерованными секциями (например постановка задчи, обзор литературных источников и т.д)
* файлы формата `[a-z]-app.tex` являются файлами приложений

Каталог `vulncontrol` является ссылкой на репозиторий, содержащий исходный код скрипта, используемого в ВКР.

Работа с LaTeX
--------------
Как установить нужные пакеты LaTeX в Ubuntu/Mint:
```bash
sudo apt install texlive-base texlive-latex-extra texlive-xetex texlive-lang-cyrillic latexmk texlive-fonts-extra texlive-math-extra
```

Для работы понадобятся шрифты Times New Roman и XITS-math:
```bash
sudo apt install ttf-mscorefonts-installer
sudo wget -O /usr/share/fonts/xits-math.otf https://github.com/khaledhosny/xits-math/raw/master/xits-math.otf && sudo fc-cache -f -v
```

Пример компиляции проекта с помощью Makefile:
```bash
git clone --recursive https://github.com/Amet13/master-thesis
cd master-thesis/
make || make build
```

Пример очистки сборочных файлов после компиляции (кроме PDF):
```bash
make clean
```

Docker
------
Проект можно собрать в Docker, в таком случае не придется устанавливать LaTeX на локальную машину.
Docker уже должен быть установлен на сервере или локальной машине.
```
git clone --recursive https://github.com/Amet13/master-thesis
cd master-thesis/
docker build -t master-thesis .
docker run -ti -v ../master-thesis:/master-thesis:Z master-thesis bash -c "make build && make clean"
```

Если же сборка прошла нормально, то в каталоге репозитория создасться новый файл `master-thesis.pdf`.

Лицензия
--------
[![CC BY SA](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/deed.ru)
