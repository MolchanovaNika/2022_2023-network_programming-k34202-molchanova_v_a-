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

<img src="https://user-images.githubusercontent.com/90505004/205455927-15d57f1f-a394-4ba7-8762-e4d0e46ddd73.jpg" height="200" > <img src="https://user-images.githubusercontent.com/90505004/205455933-9e07b442-fed3-4d1e-a067-fd49a8a97348.jpg" height="200">


+ Обе машины настроены как OpenVpn клиент

<img src="https://user-images.githubusercontent.com/90505004/205456109-b4d16973-910f-4374-9f75-36e1db2f7366.jpg" height="200" > <img src="https://user-images.githubusercontent.com/90505004/205456115-5e89b4c9-9459-4872-a610-85f264bbb431.jpg" height="200">



## 2. Работа с ansible.

+ Так как ansible требует ssh-подключение для управления роутерами, необходимо его настроить. Для этого в WinBox или в консоли настроена генерацию ключей, а в VirtualBox добавлено NAT-соединение и прописаны SSH-порты.

> `Ansible` — это инструмент автоматизации работы с серверами и ПО на них.

> С помощью `Ansible` можно создавать, удалять, изменять облачные серверы, устанавливать и изменять на них ПО, управлять сетями и сетевыми настройками, и всё это делает `Ansible` самостоятельно, следуя заранее подготовленным сценариям — плейбукам (`Playbook`).

<img src="https://user-images.githubusercontent.com/90505004/205456277-22739396-6792-43d9-9b97-8bd42cda1e17.png" height="200" > <img src="https://user-images.githubusercontent.com/90505004/205456431-366ce590-04f5-4de3-8942-72ea962ac427.png" height="300">


### Настройка облака. 

+ На облаке создаем файл hosts.ini. Там указаны адреса машин, которые долнжны управляться Ansible. Адреса были сгруппированы в группу Routers, для каждого элемента которой назначен набор переменных.

<img src="https://user-images.githubusercontent.com/90505004/205457483-6dd85966-a323-460a-a0eb-5deb2074c7fc.png" height="150">

+ После завершения настройки по адресу /etc/ansible создан файл playbook.yml. 

+ В него добавлено плей, в котором расположено несколько тасок, каждая из которых отвечает за конкретную задачу. Большая часть из них выполняется с помощью модуля `community.routeros.command`

> `community.routeros.command` - Запуск команд на удаленных устройствах под управлением MikroTik RouterOS. 

+ С помощью `community.routeros.command` прописаны команды для выполнения определенный задач: создан новый пользователь, настроены параметры для NTP клиента, произведена настройка OSPF маршрутизации в сети между двумя роутерами, собрана информация о конфигурации устройств
 
<img src="https://user-images.githubusercontent.com/90505004/205457686-77f8a1f0-899b-49ed-ab89-35283657f2ce.png" height="250">


+ Результат выполнения playbook (команда ansible-playbook playbook.yml). В выводах присутствуют ошибки, так как скриншот сделан после повторного запуска playbook.

<img src="https://user-images.githubusercontent.com/90505004/205458519-dd29b745-85ed-478f-93dc-3d2dca570604.png " height="350"> <img src="https://user-images.githubusercontent.com/90505004/205458552-3e130a64-e5f2-4a28-b805-00061bd5e959.png " height="350">



### Проверка на роутерах.

+ Проверка создание пользователя.

<img src="https://user-images.githubusercontent.com/90505004/205458829-4e5ccf2a-4df6-4b6b-8b88-b7f7c1ddb4f7.png" height="90"><img src="https://user-images.githubusercontent.com/90505004/205458833-1ff5a044-08e7-40e3-abd5-195b90675933.png " height="90">

+ Активирован NTP клиент, для которого указаны первичный и вторичный сервера для настройки точного времени. IP-адреса серверов были получены из DNS-имен 1.ru.pool.ntp.org и 2.ru.pool.ntp.org.

> NTP - cетевой протокол для синхронизации внутренних часов компьютера.


<img src="https://user-images.githubusercontent.com/90505004/205928188-f5e82a49-7630-458f-8d4c-8869626dc5a8.png" height="250">

+ OSPF маршрутизация настроена правильно,т.к. роутеры видят друг друга в качестве соседей в одной сети, а также между ними установлена связность адресов.

> OSPF — протокол динамической маршрутизации. 

<img src="https://user-images.githubusercontent.com/90505004/205929590-6a640867-c877-4110-90e3-84b9757feaef.png" height="100"> <img src="https://user-images.githubusercontent.com/90505004/205929635-5da26aef-2b1e-4111-b021-0831bad9c53f.png " height="100">


## Выводы:
В ходе выполнения лабораторной работы был создан еще один CHR. После чего удаленно были проведены различные настройки обоих CHR с помощью Ansible, установленного на удаленной ВМ, находящейся в YandexCloud.

![image](https://user-images.githubusercontent.com/90505004/205959711-82342480-7bd4-4523-9fbd-7574fcc9ef67.png)

