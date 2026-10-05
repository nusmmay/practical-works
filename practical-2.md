# Практическое задание №2. Менеджеры пакетов
## Задача 1
Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?

### Команда:
```bash
pip3 show matplotlib
```
### Результат:
```bash
Name: matplotlib
Version: 3.10.6
Summary: Python plotting package
Home-page: https://matplotlib.org
Author: John D. Hunter, Michael Droettboom
Author-email: matplotlib-users@python.org
License: License agreement for matplotlib versions 1.3.0 and later
Location: /opt/anaconda3/lib/python3.13/site-packages
Requires: contourpy, cycler, fonttools, kiwisolver, numpy, packaging, pillow, pyparsing, python-dateutil
Required-by: ipympl, seaborn
```
### Как получить пакет без менеджера пакетов:

Зайти на сайт **PyPI** (https://pypi.org/project/matplotlib/), перейти на вкладку **Release files** и скачать нужный файл:

- **`.whl`** (wheel) — готовый бинарный пакет для конкретной системы (например, `matplotlib-3.11.2-cp313-cp313-macosx_11_0_arm64.whl` для Mac на Apple Silicon).
- **`.tar.gz`** — исходный код, который можно собрать вручную.

Затем установить вручную:

```bash
pip3 install matplotlib-3.11.2-cp313-cp313-macosx_11_0_arm64.whl
```
Или распаковать `.tar.gz` и выполнить:
```bash
python3 setup.py install
```
