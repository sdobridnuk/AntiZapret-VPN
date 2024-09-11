# AntiZapret-VPN (версия без контейнера)

Скрипт для автоматического развертывания AntiZapret VPN + обычный VPN

Через AntiZapret VPN работают только:
- Заблокированные сайты из единого реестра РФ, список автоматически обновляется раз в 6 часов
- Сайты к которым ограничивается доступ без судебного решения (например youtube.com)
- Сайты ограничивающие доступ из России (например intel.com, chatgpt.com), список предзаполнен и доступен для ручного редактирования

Все остальные сайты работают через вашего провайдера с максимальной доступной вам скоростью

**Внимание!** Для правильной работы AntiZapret VPN нужно [отключить DNS в браузере](https://www.google.ru/search?q=отключить+DNS+в+браузере)

Через обычный VPN работают все сайты, доступные с вашего хостинга

AntiZapret VPN (antizapret-\*.ovpn) и обычный VPN (vpn-\*.ovpn) работают через [OpenVPN Connect](https://openvpn.net/client)\
Поддерживается подключение по UDP и TCP\
Используются 80 и 443 порты для обхода блокировок по портам

Скрипт устанавливает последнюю версию сервера OpenVPN 2.6

При подключении используется AdGuard DNS для блокировки рекламы, отслеживающих модулей и фишинга

За основу взяты [эти исходники](https://bitbucket.org/anticensority/antizapret-vpn-container/src/master) разработанные ValdikSS

Протестировано на Ubuntu 22.04/24.04 и Debian 11/12 - Процессор: 1 core Память: 1 Gb Хранилище: 10 Gb
***
### Установка:
1. Устанавливать на чистую Ubuntu 22.04/24.04 или Debian 11/12 (рекомендуется Ubuntu 24.04 или Debian 12)
2. В терминале под root выполнить:
```sh
apt-get update && apt-get install -y git
git clone https://github.com/GubernievS/AntiZapret-VPN.git antizapret-vpn
chmod +x antizapret-vpn/setup.sh && antizapret-vpn/setup.sh
```
3. Дождаться перезагрузки сервера и скопировать файлы *.ovpn с сервера из папки /root
4. (Опционально) Включить DCO
5. (Опционально) Добавить клиентов
***
Для OpenVPN вы можете включить модуль [DCO](https://community.openvpn.net/openvpn/wiki/DataChannelOffload), он заметно снижает нагрузку на CPU сервера и клиента - это экономит аккумулятор мобильных устройств и увеличивает скорость передачи данных через VPN

Для включения DCO выполните команду:
```sh
/root/enable-openvpn-dco.sh
```
Для выключения DCO выполните команду:
```sh
/root/disable-openvpn-dco.sh
```
***
 Для добавления нового клиента выполните команду и введите имя:
```sh
/root/add-client.sh [имя_пользователя]
```
Для удаления клиента выполните команду и введите имя:
```sh
/root/delete-client.sh [имя_пользователя]
```
После добавления нового клиента скопируйте новые файлы \*.ovpn с сервера из папки /root\
Пользовательские ключи хранятся в файлах antizapret-имя_пользователя.\*
***
Изменить файл с предзаполненным списком антизапрета (include-hosts-custom.txt):
```sh
nano /root/antizapret/config/include-hosts-custom.txt
```
Потом выполнить команду для обновления списка антизапрета:
```sh
/root/antizapret/doall.sh
```
***
Обсуждение скрипта на [ntc.party](https://ntc.party/t/9270)
***
Инструкция по настройке на роутерах [Keenetic](./Keenetic.md) и [TP-Link](./TP-Link.md)
***
Хостинги для VPN принимающие рубли: [vdsina.com](https://www.vdsina.com/?partner=9br77jaat2) со скидкой 10% и [aeza.net](https://aeza.net/?ref=529527) с бонусом 15% (если пополнение сделать в течении 24 часов с момента регистрации)
