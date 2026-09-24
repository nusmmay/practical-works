# Практическое занятие №1. Введение, основы работы в командной строке

Выполнил: Могутова Анастасия
Группа: ИКБО-17-25

## Задача 1
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd.

### Команда:
```bash
cut -d: -f1 /etc/passwd | sort
```

### Результат:
```text
bin
daemon
mail
nobody
operator
root
sync
sys
www-data
```


## Задача 2
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов.

### Команда:
```bash
cat /etc/protocols | sort -n -k2 | tail -n 5
```
### Результат:
```text
manet    138                     # MANET Protocols [RFC5498]
hip      139       HIP           # Host Identity Protocol
shim6    140       Shim6         # Shim6 Protocol [RFC5533]
wesp     141       WESP          # Wrapped Encapsulating Security Payload
rohc     142       ROHC          # Robust Header Compression
```


## Задача 3
Написать программу banner средствами bash для вывода текстов, как в примере (размер баннера должен меняться!).

### Код скрипта (файл banner):
```bash
#!/bin/bash
TEXT="$*"
if [ -z "$TEXT" ]; then
    echo "Использование: $0 <текст>"
    exit 1
fi
LEN=${#TEXT}
LINE=$(printf '%*s' $((LEN + 2)) '' | tr ' ' '-')
echo "+${LINE}+"
echo "| ${TEXT} |"
echo "+${LINE}+"
```
### Результат:
```text
+----------------------+
| Hello from RTU MIREA! |
+----------------------+
```

## Задача 4
Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

### Код скрипта (файл identifiers):
```bash
#!/bin/bash
if [ -z "$1" ]; then
    echo "Использование: $0 <файл>"
    exit 1
fi
tr -c '[:alnum:]_' '\n' < "$1" | grep -E '^[a-z_][a-z0-9_]*$' | sort -u
```

### Результат:
```text
h
hello
include
int
main
n
printf
return
stdio
world
```

## Задача 5
Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

### Код скрипта (файл reg):
```bash
#!/bin/bash
if [ -z "$1" ]; then
    echo "Использование: $0 <файл>"
    exit 1
fi
chmod +x "$1"
cp "$1" /usr/local/bin/
echo "Файл $1 успешно зарегистрирован в /usr/local/bin/"
```

### Результат:
```text
[root@localhost ~]# sh reg banner
Файл banner успешно зарегистрирован в /usr/local/bin/

[root@localhost ~]# ls -l /usr/local/bin/banner
-rwxr-xr-x 1 root root 52 Sep 24 11:31 /usr/local/bin/banner
```


## Задача 6
Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

### Код скрипта (файл check_comment):
```bash
#!/bin/bash
if [ -z "$1" ]; then echo "Использование: $0 <файл>"; exit 1; fi
filename="$1"
first_line=$(head -n 1 "$filename")
case "$filename" in
  *.c|*.js)
    if echo "$first_line" | grep -q "^//"; then echo "В файле $filename есть комментарий в первой строке."; else echo "В файле $filename нет комментария в первой строке."; fi
    ;;
  *.py)
    if echo "$first_line" | grep -q "^#"; then echo "В файле $filename есть комментарий в первой строке."; else echo "В файле $filename нет комментария в первой строке."; fi
    ;;
  *)
    echo "Неизвестный тип файла: $filename"
    ;;
esac
```

### Результат:
```text
В файле test.c есть комментарий в первой строке.
В файле test.js есть комментарий в первой строке.
В файле test.py есть комментарий в первой строке.
```

## Задача 7
Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

### Код скрипта (файл find_duplicates):
```bash
#!/bin/bash
if [ -z "$1" ]; then echo "Использование: $0 <директория>"; exit 1; fi
find "$1" -type f -exec md5sum {} + | sort | awk '{count[$1]++; files[$1]=files[$1]"\n"$0} END {for (h in count) if (count[h]>1) print files[h]}'
```

### Результат:
```text
09f7e02f1290be211da707a266f153b3  testdir/file1.txt
09f7e02f1290be211da707a266f153b3  testdir/file2.txt
09f7e02f1290be211da707a266f153b3  testdir/subdir/file4.txt
```

## Задача 8
Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента, и архивирует все эти файлы в архив tar.

### Код скрипта (файл archive_files):
```bash
#!/bin/bash
if [ -z "$1" ] || [ -z "$2" ]; then echo "Использование: $0 <каталог> <расширение>"; exit 1; fi
dir="$1"
ext="$2"
archive="archive_$(date +%s).tar"
find "$dir" -type f -name "*$ext" | tar -cvf "$archive" -T -
echo "Архив $archive создан."
```

### Результат:
```text
testdir/subdir/file3.txt
testdir/subdir/file4.txt
testdir/file1.txt
testdir/file2.txt
testdir/unique.txt
Архив archive_1790241374.tar создан.
```


## Задача 9
Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.

### Код скрипта (файл replace_spaces):
```bash
#!/bin/bash
if [ -z "$1" ] || [ -z "$2" ]; then echo "Использование: $0 <входной_файл> <выходной_файл>"; exit 1; fi
sed "s/    /\t/g" "$1" > "$2"
echo "Замена выполнена. Результат в файле $2"
```

Замена выполнена. Результат в файле output.txt


### Результат:
```text
# Содержимое output.txt (посимвольно):
Hello\tWorld
This\tis\ta\ttest
NoSpacesHere
```
