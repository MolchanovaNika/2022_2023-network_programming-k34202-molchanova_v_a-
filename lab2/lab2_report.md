University: ITMO University

Faculty: FICT

Course: Network programming

Year: 2022/2023

Group: K34202

Author: Molchanova Veronika Alexandrovna

Lab: Lab2

Date of create: 24.11.2022

Date of finished: . .2022

---

## 1.Настройка второго CHR.

+ Через VirtualBox создана вторая виртуальная машина, на ней установлен `CHR Mikrotik`.

 <img src="https://user-images.githubusercontent.com/90505004/207185105-1efe6029-5da9-445c-b940-a52d1ac5fa2a.jpg" height="300" > 

+ Вторая машины настроена как OpenVpn клиент, как и первая.

<img src="https://user-images.githubusercontent.com/90505004/207184627-9bf805a1-2a55-4695-82c3-32194c7e4559.png" height="300" >


## 2. Работа с ansible.

+ Так как ansible требует ssh-подключение для управления роутерами, необходимо его настроить. Для этого в WinBox или в консоли настроена генерацию ключей, а в VirtualBox добавлено NAT-соединение и прописаны SSH-порты.

> `Ansible` — это инструмент автоматизации работы с серверами и ПО на них.

> С помощью `Ansible` можно создавать, удалять, изменять облачные серверы, устанавливать и изменять на них ПО, управлять сетями и сетевыми настройками, и всё это делает `Ansible` самостоятельно, следуя заранее подготовленным сценариям — плейбукам (`Playbook`).


![image](https://user-images.githubusercontent.com/90505004/207187858-ec18f0a6-09aa-446e-b198-945936f64e65.png) ![image](https://user-images.githubusercontent.com/90505004/207188838-f384b5d0-15f5-4cb2-a8c1-cb9abdc8b00a.png)


### Настройка файла инвентаризации

+ На облаке создаем файл hosts.ini. Там указаны адреса машин, которые долнжны управляться Ansible. Адреса были сгруппированы в группу Routers, для каждого элемента которой назначен набор переменных.


<img src="https://user-images.githubusercontent.com/90505004/207111288-6d9515de-c164-45eb-b6fb-2b830cfed6fb.png" height="150">

+ После завершения настройки по адресу /etc/ansible создан файл playbook.yml. 

+ В него добавлено плей, в котором расположено несколько тасок, каждая из которых отвечает за конкретную задачу. Большая часть из них выполняется с помощью модуля `community.routeros.command`

> `community.routeros.command` - Запуск команд на удаленных устройствах под управлением MikroTik RouterOS. 

+ С помощью `community.routeros.command` прописаны команды для выполнения определенный задач: создан новый пользователь, настроены параметры для NTP клиента, произведена настройка OSPF маршрутизации в сети между двумя роутерами, собрана информация о конфигурации устройств

<img src="https://user-images.githubusercontent.com/90505004/207119559-15165ebf-ca75-4822-930f-9ee141d99bc8.png" height="250">


+ Результат выполнения playbook (команда ansible-playbook playbook.yml). В выводах присутствуют ошибки, так как скриншот сделан после повторного запуска playbook.

<img src="https://user-images.githubusercontent.com/90505004/205458519-dd29b745-85ed-478f-93dc-3d2dca570604.png " height="350"> <img src="https://user-images.githubusercontent.com/90505004/207130262-efee4b14-6838-473c-b3a1-c73325c2f349.png " height="350">




### Проверка на роутерах.

+ Проверка создание пользователя.

![a](https://user-images.githubusercontent.com/90505004/207200057-32d28633-bf4c-49be-b2ca-7620411ffac7.jpg)
![c](https://user-images.githubusercontent.com/90505004/207200023-ee5129eb-a358-441d-80d2-5843d3c9c6e2.jpg)


+ Активирован NTP клиент, для которого указаны первичный и вторичный сервера для настройки точного времени.

> NTP - cетевой протокол для синхронизации внутренних часов компьютера.

![d](https://user-images.githubusercontent.com/90505004/207199967-cdf9cc7e-1d8f-4585-b52c-4ad9d3447177.jpg)


+ OSPF маршрутизация настроена правильно,т.к. роутеры видят друг друга в качестве соседей в одной сети, а также между ними установлена связность адресов.

> OSPF — протокол динамической маршрутизации. 

<img src="https://user-images.githubusercontent.com/90505004/205929590-6a640867-c877-4110-90e3-84b9757feaef.png" height="100"> <img src="https://user-images.githubusercontent.com/90505004/205929635-5da26aef-2b1e-4111-b021-0831bad9c53f.png " height="100">





## Выводы:
В ходе выполнения лабораторной работы был создан еще один CHR. После чего удаленно были проведены различные настройки обоих CHR с помощью Ansible, установленного на удаленной ВМ, находящейся в YandexCloud.

![image](https://user-images.githubusercontent.com/90505004/205959711-82342480-7bd4-4523-9fbd-7574fcc9ef67.png)

