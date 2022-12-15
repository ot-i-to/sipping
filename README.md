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

[Скачать данную версию утилиту можно тут](https://sysinfo.pro/ru/VoIP/Monitoring/sipping.tar.bz2) или с [github](https://github.com/ot-i-to/sipping).
