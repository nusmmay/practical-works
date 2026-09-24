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
