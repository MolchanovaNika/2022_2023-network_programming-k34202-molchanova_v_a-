University: ITMO University

Faculty: FICT

Course: Network programming

Year: 2022/2023

Group: K34202

Author: Molchanova Veronika Alexandrovna

Lab: Lab3

Date of create: 5.12.2022

Date of finished: . .2022

---

# 1. Поднятие NetBox на дополнительной VM.

> Netbox — это открытое (open source) веб приложение, разработанное для управления и документирования компьютерных сетей. 
+ Netbox был развёрнут на облачной виртуальной машине.
 
 ## Установка и настройка PostgreSQL
 
+ Установлена база данных postgresql и выполнена настройка согласно гайду https://www.vultr.com/docs/install-and-configure-netbox-on-ubuntu-20-04/

`sudo apt install postgresql`

<img src="https://user-images.githubusercontent.com/90505004/205984218-d965a48d-5e1a-40b4-ae2d-49ead76a4061.png" height="150">

+ Создана нужная база данных и привелегированный пользователь

<img src="https://user-images.githubusercontent.com/90505004/205985187-1e81d4cd-8593-44cc-9272-0656d229dccf.png" height="150">

<img src="" height="220">

## Установка Redis

+ Установлен Redis  `sudo apt install -y redis-server`

<img src="https://user-images.githubusercontent.com/90505004/205986637-7837bbdb-5fee-4da7-aac8-04c5978d347f.png" height="200"> 

<img src="https://user-images.githubusercontent.com/90505004/205986348-e7af3419-57e8-4001-b09e-d590e64398c4.png" height="30">

> Redis - это хранилище значений ключей в памяти. NetBox использует его для кэширования и постановки в очередь.

## Установка и настройка NetBox

+ Установлены все необходимые пакеты

`sudo apt install python3 python3-pip python3-venv python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev zlib1g-dev git -y`

![image](https://user-images.githubusercontent.com/90505004/205987669-aa4d3b7b-7767-44e0-a1af-bf6f2e508108.png)

+ Создана директория, в которую установлен и распакован Netbox.

`sudo wget https://github.com/netbox-community/netbox/archive/refs/tags/v3.3.9.tar.gz`

`sudo tar -xzf v3.3.9.tar.gz -C /opt`

`sudo ln -s /opt/netbox-3.3.9/ /opt/netbox`

![image](https://user-images.githubusercontent.com/90505004/205988675-028a170d-1c42-4dd1-a35a-4798a3791fbb.png)


+ Создан пользователь с предоставленными правами на все папки и файлы Netbox.

`groupadd --system netbox`

`sudo adduser --system -g netbox netbox`

`chown --recursive netbox /opt/netbox/netbox/media/`

+ Создано виртуальное окружение, где установлены все зависимости

`python3 -m venv /opt/netbox/venv`

`source venv/bin/activate`

`pip3 install -r requirements.txt`

+ Cкопирован пример файла конфигурации configuration.example.py в файл конфигурации configuration.py.

`cd netbox/netbox/`

`cp configuration.example.py configuration.py`

+ С помощью входящего в состав netbox исполнительного файла gnerate_secret_key.py сгенерирован секретный ключ.

`netbox/generate_secret_key.py`
![image](https://user-images.githubusercontent.com/90505004/207166779-072cc028-cee2-47d2-98a5-b0ac214ef840.png)

+ Открыт и отредактирован файл конфигурации configuration.py.

`nano /opt/netbox/netbox/netbox/configuration.py`

![image](https://user-images.githubusercontent.com/90505004/207167103-c8e9e10c-f5a4-4c6c-90ca-afffeb9abb19.png)

+ Выполнены миграции

`python3 manage.py migrate`

+ Внутри вирутального окружения создан superuser для дальнейшего управления netbox.

`python3 manage.py createsuperuser`

+ Собрана статика

`python3 manage.py collectstatic --no-input`



## Установка и настройка nginx и gunicorn для запуска netbox

### Настройка Gunicorn

+ Для настройка gunicorn скопирован файл

`sudo cp /opt/netbox/contrib/gunicorn.py /opt/netbox/gunicorn.py`

> Gunicorn — это Application-сервер для запуска Web-приложений написанных на Python. Основная его задача — это работа в режиме демона и поддержка постоянной работы Web-приложений.

### Настройка Systemd

+ Скопированы файлы в каталог

`sudo cp /opt/netbox/contrib/*.service /etc/systemd/system/`

+ Перезагружен демон, чтобы включить изменения Systemd

`sudo systemctl daemon-reload`

+ Запущены службы netbox и .netbox-rq

`sudo systemctl start netbox netbox-rq`

+ Включен запуск служб во время загрузки.

`sudo systemctl enable netbox netbox-rq`

### Настройка веб-сервера Nginx

> Nginx― это программное обеспечение с открытым исходным кодом, которое позволяет создавать веб-сервер. Также его используют как почтовый сервер или обратный прокси-сервер.

+ Установлен веб-сервер Nginx.

`sudo apt install -y nginx`

+ Скопирован файл конфигурации NetBox Nginx

`sudo cp /opt/netbox/contrib/nginx.conf /etc/nginx/sites-available/netbox`

+ Отредактирован файл netbox, добавлен хост и удалены https server

`sudo nano /etc/nginx/sites-available/netbox`

<img src="https://user-images.githubusercontent.com/90505004/207169776-cb88ee27-bae5-4759-b384-6d6a15c62414.png" height="350"> 

+ Создана символическая ссылка в каталоге с поддержкой сайтов netbox на файл конфигурации. Выполнен перезапуск служб. 

`sudo rm /etc/nginx/sites-enabled/default`

`sudo ln -s /etc/nginx/sites-available/netbox /etc/nginx/sites-enabled/netbox`

+ Перезапущена служба nginx, чтобы включить новые конфигурации.

`sudo systemctl restart nginx`


При переходе в браузере по ip открывается netbox. Теперь можно войти в систему, используя имя пользователя и пароль, которые установлены при создании учетной записи суперпользователя. Теперь можно приступить к настройке сетевых компонентов и управлению ими.

<img src="https://user-images.githubusercontent.com/90505004/207171818-d1bc30b7-15b7-45c7-acdc-27871741d57d.png" height="500">

## NetBox

+ Проверка работы Netbox

![image](https://user-images.githubusercontent.com/90505004/207181128-66c7aa92-fab1-413f-9aaa-7703bf442c81.png)

# Заполнение всей возможной информации о CHR в Netbox

+ Заполнены данные в Netbox. Подключение происходит по IP виртуальной машины по порту 8001. Вручную введены данные о двух устройствах. Для добавления IP адреса требуется создать интерфейс на роутере. В Netbox записаны два роутера, ID роутеров, названия роутеров, интерфейсы, IP адреса.

![205512456-20dc0e9b-8ce0-4dfb-b229-0b09606c0d7f](https://user-images.githubusercontent.com/90505004/207984774-0d9b25da-dac6-4936-9d75-5cf75e608b6d.jpg)

+ Из NetBox был скачан файл csv с данными о роутерах

# Написание сценария для настройки CHR1, CHR2

+ Файл csv перенесен на сервер с anible.

+ Создан файл playbook1.yml. Основная цель разделена на две подзадачи. Первая - спарсить csv файл и записать нужную информацию о роутере в отдельный файл. В данном случае за ключ берём UID роутера, так как это значение не будет изменяться.

<img src="https://user-images.githubusercontent.com/90505004/207989501-0314fdd9-dd8c-4079-80e8-cbd693186df8.png" height="300">
 
+ Запущен playbook1, для проверки правильности вывода.

<img src="https://user-images.githubusercontent.com/90505004/207990316-08c16dab-5ea5-4694-b915-31ae97149747.jpg" height="300">

+ В playbook1.yml добавлена часть, которая отвечает за установку названия роутера. 
 <img src="https://user-images.githubusercontent.com/90505004/207991045-8c84d2da-b2cb-413a-8d78-bd620838ed75.png" height="300">

+ Запущен playbook1 со всеми частями. В результате чего он берёт имя роутера из csv файла, сгенерированного Netbox, и присваивает  имя подключенному роутеру. Вывод результатов показывает, что всё работает корректно.

![205510886-366577b3-3f2b-4784-b701-f3b435b985ea](https://user-images.githubusercontent.com/90505004/208129703-cc5117bf-df4d-4cf7-8983-97faca4634ea.jpg)

+ В консоли роутера видно, что название поменялось

![photo_2022-12-16_18-39-21 (2)](https://user-images.githubusercontent.com/90505004/208134797-49154a9e-f2ef-485b-b5ab-9fbaf25ea608.jpg)

# Обратная задача - информацию из роутера передать в Netbox

+ Создан playbook2

<img src="https://user-images.githubusercontent.com/90505004/208139090-5c2298aa-28d3-4340-a0d8-bfc2110f2e4f.png" height="300">


![image](https://user-images.githubusercontent.com/90505004/208140522-308d1db1-f507-479a-b3e5-25e6bcd6acbb.png)







