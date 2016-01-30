# VPN-Services
Открытый исходный код коммерческого VPN-сервиса

Скрипт для автоматизированного развертывания OpenVPN сервера.
Данный скрипт представляет собой сценарий для автоматизированного развертывания OpenVPN сервера на серверах с операционной системой Debian или Ubuntu (для тестирования скрипта использовалась система Ubuntu Server 14.04.3 LTS). Для запуска развертывания необходимо скачать все файлы и запустить скрипт «start.sh» с привилегиями «root».
Сценарий реализует следующий функционал:
- изменяет стандартный порт ssh (по умолчанию 22) на порт 5729;
- реализует режим бана на 15 минут после 5 неверных попыток входа по ssh (для предотвращения brute force атак);
- устанавливает и настраивает для работы OpenVPN SSL;
- устанавливает и настраивает OpenVPN сервер;
- настраивает  межсетевой экран закрывая все неиспользуемые порты кроме порта ssh и OpenVPN;

Особенности сервера:
На сервера используется двухфакторная авторизация. Помимо стандартной авторизации по средствам сертификатов, реализована дополнительная возможность подтверждения привилегий пользователя через сторонний сервис. Алгоритм работы следующий:
1) клиент пытается подключиться к серверу для чего отправляет свой публичный ключ;
2) сервер из публичного ключа извлекает login пользователя;
3) сервер, зная login пользователя, совершает запрос к стороннему сервису на право подключения пользователя к VPN серверу с таким login;
4) сторонний сервер, руководствуюсь своей бизнес логикой одобряет или не одобряет подключение пользователя к VPN серверу;
5) сервер получив одобрение или неодобрение подключает или не подключает пользователя.
Таким образом, помимо стандартной  TLS авторизация используется еще и биллинговая система.
