#Task 2   Сеть, SSH, NAT и Port Forwarding

## Цель работы
В этой работе я настроил небольшую сеть из трёх машин: Kali Linux (основная машина), Debian1 (роутер/посредник) и Debian2 (внутренний сервер). Основные задачи: настроить сеть между машинами, дать Debian2 доступ в интернет через Debian1, настроить SSH подключения, установить веб-сервер и сделать доступ к нему через port forwarding.

## Схема сети
Debian1 имеет два сетевых интерфейса: 192.168.50.2 (сеть с Kali) и 192.168.60.1 (сеть с Debian2). Debian2 находится в сети 192.168.60.0/24 и имеет адрес 192.168.60.2.

## Настройка DNS
На Debian1 был настроен DNS сервер 8.8.8.8 (файл /etc/resolv.conf).
![DNS Debian1](images/dnsdeb1nano.png)

На Debian2 был настроен DNS сервер 1.1.1.1.
![DNS Debian2](images/dnsdeb2nano.png)

## Проверка интернета
На Debian2 была выполнена команда ping google.com.
![Ping Google](images/dnsdeb2.png)


## SSH подключения
С Kali выполнено подключение к Debian1.
![SSH Debian1](images/sshcnctdeb1.png)

Далее с Debian1 выполнено подключение к Debian2.
![SSH Debian2](images/sshcnctdeb2fromdeb1.png)


## Подключение через Jump Host
Был настроен файл ~/.ssh/config, чтобы подключаться к Debian2 через Debian1 (jump host).
![SSH через jump](images/kalitodeb2.png)

Теперь можно подключаться напрямую командой ssh debian2.

## Установка веб-сервера
На Debian2 был установлен nginx.
![Установка nginx](images/startnginx.png)

Проверка статуса:
![nginx работает](images/startngix2v.png)

Сервис запущен и работает.

## Проверка локально
На Debian2 выполнена команда curl localhost.
![curl localhost](images/curlwelcomengix.png)

Была получена HTML страница nginx

## Настройка Port Forwarding (DNAT)
На Debian1 было настроено правило iptables:
![iptables правило](images/deb1-set80port.png)


С Kali выполнена команда curl 192.168.50.2:8080.
![curl через порт](images/curl8080.png)


