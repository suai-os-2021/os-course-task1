# os-course-task1
Операционные системы. Лабораторная работа №1: работа с текстовыми потоками в командном интерпретаторе Bash

## Цель работы
Изучение принципов работы с командным интерпретатором GNU/Linux и основ обработки текстовых файлов с помощью команд grep, awk, sed.

## Задание на лабораторную работу
1. Подготовить операционную систему GNU/Linux к работе. При необходимости, воспользоваться средством виртуализации VMware Workstation/Player, Oracle VirtualBox или др. В качестве дистрибутива рекомендуется взять [Ubuntu](https://www.ubuntu.com/download/desktop).
2.	Создать в домашней директории пользователя `/home/user/` каталог `lab1` с помощью команды `mkdir`. Перейти в этот каталог с помощью команды `cd`. Всю дальнейшную работу вести внутри этого каталога.
3.  С помощью команды `git clone <путь_к_репозиторию_на_github>` создать локальную копию репозитория. Перейти в каталог с копией репозитория (при клонировании репозитория каталог будет иметь такое же название, как и сам репозиторий на github.com).
4.	Ознакомиться с форматом файла `dns-tunneling.log` и хранящимися в нем данными с помощью команд `cat`, `head`, `tail`, `more`, `less` и т.п.
5.	Подсчитать количество записей в файле `dns-tunneling.log`.
6.	Вычислить номер варианта задания как остаток от деления порядкового номера студента по списку в журнале на количество вариантов заданий. Если остаток равен нулю, необходимо брать последнее задание.
7.	Дописать в файл `lab1.sh` код для обработки данных из файла `dns-tunneling.log` в соответствии с вариантом задания используя исключительно команды командного интерпретатора `bash`. Использовать другие интерпретируемые или компилируемые языки запрещается. На вход скрипта должен подаваться файл `dns-tunneling.log` и все результаты должны вычисляться на его основе в реальном времени, использовать в скрипте заранее полученные значения запрещается.
8.	Сделать файлы `lab1.sh` и `test.sh` исполняемыми с помощью команды `chmod`.
9.	Отладить скрипт `lab1.sh` и убедиться, что тесты из `test.sh` выполняются без ошибок.
10.	С помощью команд `git add lab1.sh`, `git commit` и `git push` добавить файл с написанным кодом в репозиторий. Убедиться, что тест в репозитории пройден успешно.
11.	Подготовить и защитить отчет о выполнении лабораторной работы.


## Описание текстовых данных
Файл `dns-tunneling.log` содержит логи DNS-сервера, представленные в виде текстового файла, в котором каждая строка соответствует записи о поступившем на вход сервера запросе. В логах сохраняются следующие параметры запроса, разделенные символом табуляции:

1.	Название провайдера телекоммуникационных услуг: `character array`,
2.	Название узла, на котором хранятся данные: `character array`,
3.	Порядковый номер запроса: `long`,
4.	Отметка времени, когда поступил запрос: два числа `long`, разделенных точкой; первое число – количество секунд, прошедших  с 1 января 1970 года; второе число – количество микросекунд; т.е. фактически это тип данных `float`,
5.	IP-адрес пользователя: `character array`,
6.	Порт пользователя: `int`,
7.	Локальный IP-адрес, на который поступил запрос: `character array`,
8.	Локальный порт: `int`,
9.	Название оборудования DNS-сервера: `character array`,
10.	Класс запроса: `int`,
11.	Тип запроса: `int`,
12.	Код возвращаемого значения: `int`,
13.	Флаги: `int`,
14.	Вспомогательный идентификатор: `int`,
15.	Запрашиваемый URL: `character array`,
16.	Зона: `character array`,
17.	Вспомогательное поле 1: `character array`,
18.	Вспомогательное поле 2: `character array`,
19.	Вспомогательное поле 3: `character array`,
20.	Вспомогательное поле 4: `character array`,
21.	Ответ сервера: `character array`,
22.	Вспомогательное поле 5: `character array`,
23.	Вспомогательное поле 6: `character array`,
24.	Длина ответа: `int`

Варианты заданий

1.	Написать скрипт с использованием grep, sed, awk (необходимо использовать не менее одной из указанных утилит; использовать все три необязательно) для переконвертирования данных в формат XML со следующей структурой:
```<dnslog>
<row>
    <serial>Порядковый номер запроса</serial>
    <client_ip>IP адрес пользователя</client_ip>
    <url>Запрашиваемый URL</url>
</row>
<row>
    <serial>Порядковый номер запроса</serial>
    <client_ip>IP адрес пользователя</client_ip>
    <url>Запрашиваемый URL</url>
</row>
<row>
    ...
</row>
</dnslog>
```
Текст внутри тегов `<serial>`, `<client_ip>` и `<url>` необходимо заменить соответствующими значениями из логов. Для отступов использовать символ табуляции (4 пробела в примере выше = одна табуляция). Сохранить в файле `results.xml` результат применения написанного скрипта к последним 50 строкам файла `dns-tunneling.log`.

2.	Задание аналогично варианту 1, но формат XML файла иной:
```
<dnslog>
<row>
    <timestamp>Отметка времени, когда поступил запрос</timestamp >
    <client_ip>IP адрес пользователя</client_ip>
    <client_port>Порт пользователя</client_port>
</row>
<row>
    <timestamp>Отметка времени, когда поступил запрос</timestamp >
    <client_ip>IP адрес пользователя</client_ip>
    <client_port>Порт пользователя</client_port>
</row>
<row>
    ...
</row>
</dnslog>
```

3.	Сформировать список уникальных IP-адресов пользователей, присутствующих в логах, отсортировать список в порядке увеличения IP-адреса и сохранить в файле `results.txt`, записывая каждый адрес с новой строки, начиная со второй. В первой строке файла сохранить количество найденных уникальных IP-адресов пользователей.
4.	Вывести на экран в формате `"ДД-MM-ГГГГ ЧЧ:мм:СС.нс"` дату и время поступления первого и последнего DNS-запросов, где `ДД` – день, `ММ` – месяц, `ГГГГ` – год, `ЧЧ` – час, `мм` – минуты, `СС` – секунды, `нс` – наносекунды. Для этого воспользоваться командой `date` с флагом `–d`, например: `date -d @946684800`. Время и дату преобразовать в часовой пояс всемирного координированного времени (UTC). Сохранить указанные две даты в файл `results.txt`, каждую на новой строке. После этого дописать третьей строкой в файл `results.txt` число строк в файле `dns-tunneling.log`. При выполнении задания в MacOS рекомендуется использовать утилиту `gdate` (GNU date) вместо `date`.
5.	Найти количество запросов, поступивших за первую, вторую и третью секунды ведения лога. Сохранить получившиеся три числа в файл `results.txt`. При обработке данных исходить из того, что записи в логе могут быть не отсортированы в порядке увеличения отметки времени.
6.	Найти все доменные имена второго уровня, к которым обращались пользователи за все время ведения лога. Подсчитать количество запросов каждого из доменных имен второго уровня (включая поддомены). В файл `results.tsv` вывести таблицу, в которой каждая строка имеет вид:
`<доменное имя второго уровня><символ табуляции><количество запросов этого доменного имени>`
Строки в файле отсортировать в порядке убывания числа запросов к доменам второго уровня.

7.	Подсчитать количество обращений к доменам `facebook.com.` и `google.com.`. Найти суммарный объем DNS-трафика к каждому из этих доменов. Объем трафика в одном DNS-запросе равен количеству символов, из которых состоит запрашиваемое имя, включая все поддомены и точки. Найти самый длинный запрошенный URL за все время ведения лога, не ограничиваясь доменами `facebook.com.` и `google.com.`. Сформировать файл `results.txt` из трех строк в следующем виде:
```
facebook.com.;<количество обращений к facebook.com.>;<суммарный объем DNS-трафика к facebook.com.>
google.com.;<количество обращений к google.com.>;<суммарный объем DNS-трафика к google.com.>
<самый длинный запрошенный URL>
```

8.	Написать скрипт с использованием `grep`, `sed`, `awk` (необходимо использовать не менее одной из указанных утилит; использовать все три необязательно) для переконвертирования данных в формат JSON со следующей структурой:
```
{
    "dnslog": [
        "entry": {
            "timestamp": "Отметка времени, когда поступил запрос",
            "client ip": "IP адрес пользователя",
            "url": "Запрашиваемый URL"
        },
        "entry": {
            "timestamp": "Отметка времени, когда поступил запрос",
            "client ip": "IP адрес пользователя",
            "url": "Запрашиваемый URL"
        },
        ...
    ]
}
```
Взятый в кавычки русский текст необходимо заменить соответствующими значениями из логов. В формате JSON необходимо все ключи и все строковые значения помещать в двойные кавычки, числовые же значения (int, float) следует вставлять без кавычек. Для отступов использовать символ табуляции (4 пробела в примере выше = одна табуляция).
Сохранить в файле `results.json` результат применения написанного скрипта к строкам с 51 по 100-ю (включительно) файла `dns-tunneling.log`.

9.	Задание аналогично предыдущему варианту, но формат JSON файла иной:
```
{
    "Порядковый номер запроса": {
        "timestamp": "Отметка времени, когда поступил запрос",
        "client ip": "IP адрес пользователя",
        "client port": "Порт пользователя"
    },
    "Порядковый номер запроса": {
        "timestamp": "Отметка времени, когда поступил запрос",
        "client ip": "IP адрес пользователя",
        "client port": "Порт пользователя"
    },
    ...
}
```

10.	Домены второго уровня `1yf.de.` и `2yf.de.` являются DNS-туннелями. Они используются для передачи трафика по DNS-протоколу в обход HTTP (например, для обхода блокировок). Подсчитать количество обращений к каждому из доменов второго уровня `1yf.de.` и `2yf.de.`. Вычислить среднее количество запросов в секунду по всем DNS-туннелям за первый час ведения логов, округлить до пяти знаков после запятой. Сохранить полученные числа в файле `results.txt` по одному на строку: первая строка - количество обращений к домену `1yf.de.`, вторая строка - количество обращений к `2yf.de.`, третья строка - среднее количество запросов к `1yf.de.` и `2yf.de.` за первый час. Необходимо помнить, что записи в файле `dns-tunneling.log` могут идти в произвольном порядке.
11.	Подсчитать количество уникальных пользователей, использующих DNS-туннели (см. предыдущий вариант). Пользователей можно идентифицировать по их IP-адресам. Определить количество DNS–запросов, выполненных каждым из найденных пользователей. В файл `results.tsv` вывести таблицу, в которой каждая строка имеет вид:
`<IP-адрес><символ табуляции><количество запросов с использованием DNS-туннелей, выполненных с указанного IP-адреса>`  
Строки в файле отсортировать в порядке убывания числа запросов к доменам DNS-туннелей.

12.	Вычислить в процентах, какое количество DNS-запросов в приведенном логе приходится на DNS-туннели с разбивкой на `1yf.de.` и `2yf.de.` (см. предыдущие варианты), а также домены `facebook.com.` и `google.com.`. Получившиеся числа не округлять и записать в формате с плавающей запятой (разделитель целой и дробной части - точка) в файл `results.txt` по одному на строку. Порядок следования чисел должен быть такой же, как указано в задании.

## Содержание отчета

1.	Титульный лист 
2.	Цель работы
3.	Индивидуальное задание
4.	Описание входных данных
5.	Результат выполнения работы
6.	Исходный код программы с комментариями
7.	Выводы
