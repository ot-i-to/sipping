#### Утилита диагностики VoIP использующая протокол SIP сообщения OPTIONS в качестве ping для анализа состояния носта.

> Для работы утилиты SIP Ping требуется работающая среда Python 2.x., но возможно заработает и на Python 3.x (не провералось).  
> Хост, который вы пингуете, должен отвечать на пакеты OPTIONS. Неважно, что он отвечает - 200, 403, даже 501 все в порядке, если что-то возвращается с неповрежденным Call-ID. Если вы пингуете устройство, которое фильтрует SIP-трафик по доменному имени (например, принимает только пакеты вида From: user@\*\*company.com\*\*), вам может потребоваться использовать опцию “-d” для установки правильного доменного имени.  
>   
> SIP Ping работает только по UDP и не может работать с TCP или TLS.  
>  

Утилита является модернизаций утилиты  [cathoderaydude/sip-ping](https://github.com/cathoderaydude/sip-ping) , но внесены следующие изменения: 

-   исправлено неработающая опция “-с”
-   добавлены опции позволяющие выполнять произвольный скрипт в системе при достижения порога неудачных пингов:

` --crun count   `   Count lost the run shell script (default 0 - off)

` --cnew count   `   Number of successful attempts to reset the failure  counter(default 10, 0 - off)

` --run script   `   Path/Name lost shell script (./script.sh))

` --pause timeout `  Pause after script execution (.default 60 sec.))

#####   
Пример запуска:  
`/usr/share/sipping/sipping.py -p 5060 -i 10.15.1.154:5099 10.15.1.154 -I 60000 -t 10000 -w '/var/log/asterisk/sipping.log' --pause 300 --crun 10 --run '/usr/share/sipping/script.run' -q`

[Скачать данную версию утилиту можно тут](https://sysinfo.pro/ru/VoIP/Monitoring/sipping.tar.bz2).


##### Справка:

```plaintext
usage: sipping.py [-h] [-I interval] [-u userid] [-i ip] [-d domain] [-p port]
                 [--ttl ttl] [-w file] [-t timeout] [-c count] [-x [X]]
                 [-X [X]] [-q [Q]] [-S [S]] [--crun count] [--cnew count]
                 [--run script] [--pause timeout]
                 host

Send SIP OPTIONS messages to a host and measure response time. Results are
logged continuously to CSV.

positional arguments:
 host             Target SIP device to ping

optional arguments:
 -h, --help       show this help message and exit
 -I interval      Interval in milliseconds between pings (default 1000)
 -u userid        User part of the From header (default sipping)
 -i ip            IP to send in the Via header (will TRY to get local IP by
                  default)
 -d domain        Domain part of the From header (needed if your device
                  filters based on domain)
 -p port          Destination port (default 5060)
 --ttl ttl        Value to use for the Max-Forwards field (default 70)
 -w file          File to write results to. (default sipping-logs/[ip] - * to
                  disable.
 -t timeout       Time (ms) to wait for response (default 1000)
 -c count         Number of pings to send (default 0 infinite)
 -x [X]           Print raw transmitted packets
 -X [X]           Print raw received responses
 -q [Q]           Do not print status messages (-x and -X ignore this)
 -S [S]           Do not print loss statistics
 --crun count     Count lost the run shell script (default 0 - off)
 --cnew count     Number of successful attempts to reset the failure
                  counter(default 10, 0 - off)
 --run script     Path/Name lost shell script (./script.sh))
 --pause timeout  Pause after script execution (.default 60 sec.))
```

