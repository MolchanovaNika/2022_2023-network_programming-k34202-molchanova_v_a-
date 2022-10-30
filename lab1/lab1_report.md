University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2022/2023

Group: K34202

Author: Molchanova Veronika Alexandrovna

Lab: Lab1

Date of create: 16.10.2022

Date of finished: xx.xx.2022

Ход работы:
1.	Создана виртуальная машина в Яндекс.Облаке на операционной системе Ubuntu.
2.	Выполнено подключение к ВМ по ssh.![1](https://user-images.githubusercontent.com/90505004/198903288-79eeb7db-92ef-4300-88c3-af6e7427fdb6.jpg)
3.	Установлен ansible.![3](https://user-images.githubusercontent.com/90505004/198903314-4082714c-a571-4329-9312-fcbb43fc572b.jpg)
 
4.	Выполнена проверка установки ansible.![4 check](https://user-images.githubusercontent.com/90505004/198903321-edf60b45-ae21-4c34-b49a-03d022ae7239.jpg)

5.	В VirtualBox установлен MikroTik 7 версии, это будет важно для дальнейшей работы. Здесь имеет смысл обратить внимание на то, что после загрузки в настройках VirtualBox необходимо отключить загрузочный диск вручную, тогда как на установке более привычных операционных систем это происходит автоматически.
![вм](https://user-images.githubusercontent.com/90505004/198903340-fdea8537-9e04-4f86-b4db-c9081eb4a896.jpg)
![микротик](https://user-images.githubusercontent.com/90505004/198903346-240d1ba4-a44c-4b82-9e2d-a1258c766dc0.jpg)

6.	После этого устанавливаем Wireguard на удалённую машину. ![5](https://user-images.githubusercontent.com/90505004/198903357-edc22cc6-deeb-4749-ae82-850029b30cda.jpg)
7.	Прописываем в Wireguard в файл условий интерфейса. Создаём пару ключей.
8.	После этого начинаем работу с MikroTik. Было обнаружено, что большая часть инструкций по его использованию объясняют работу при помощи графического интерфейса WinBox. 
9.	С помощью Winbox получилось подключиться к виртуальной машине MikroTik.
![винбокс](https://user-images.githubusercontent.com/90505004/198903377-dc580dcc-2883-4cdc-aec1-846d46bdd163.jpg)

10.	Поскольку в качестве VPN был выбран WireGuard, и установлен MikroTik последней версии, заходим в настройку Wireguard и создаём там новый интерфейс
11.	Заполняем конфиг файл wg0.conf.
![144](https://user-images.githubusercontent.com/90505004/198903386-8d2bfb3c-2f63-4680-8c1f-c74ac43b6662.jpg)

12.	Создан интерфейс.  
![пирс](https://user-images.githubusercontent.com/90505004/198903395-19547f3a-218e-4ef1-9419-a781d842607d.jpg)

13.	Создана пара ключей для интерфейса
![ключи](https://user-images.githubusercontent.com/90505004/198903404-924e662b-10f0-4f28-a25b-16e3d6881029.jpg)

14.	Узнали ListenPort через команду открытия файла /etc/wireguard/wg0.conf , 
чтобы создать интерфейс 
![14](https://user-images.githubusercontent.com/90505004/198903419-fab32d2b-06c7-4eb0-ab46-2f1b6da130b3.jpg)


15.	Переходим во вторую вкладку, там создаём Peer - указываем только что созданный интерфейс, указываем публичный ключ сервера, его публичный IP, указанный ранее порт и сеть адресов, по которым будет идти подключение.  
![10](https://user-images.githubusercontent.com/90505004/198903432-f48717b0-a409-4953-b577-aecdfb96d421.jpg)
16.	В настройке IP - Addresses указываем выбранную сеть и созданный интерфейс.
![11](https://user-images.githubusercontent.com/90505004/198903438-f60eb531-1152-4eee-b283-062439df0782.jpg)
17.	В настройке IP - Firewall создаём NAT Rule masquerade, Masquerade NAT позволяет преобразовывать несколько IP-адресов в другой одиночный IP-адрес. Можно использовать маскарадный NAT, чтобы скрыть один или несколько IP-адресов во внутренней сети за IP-адресом, который нужно сделать общедоступным.
![12](https://user-images.githubusercontent.com/90505004/198903441-75d4a485-354c-4025-a37f-549cd21c3249.jpg)
18.	Теперь для проверки работоспособности запускаем ping к виртуальной машине по заданному IP адресу. Пинг идёт - следовательно, все настройки выполнены корректно
![15](https://user-images.githubusercontent.com/90505004/198903461-36e69ca9-6d98-4701-b77e-aaf03a82c786.jpg)
19.	В результате получаем связь по следующей схеме.
![photo_2022-10-31_01-11-28](https://user-images.githubusercontent.com/90505004/198903991-d0828caa-0a05-4ae3-a6c7-3519c6917518.jpg)

Выводы: При помощи WireGuard возможно настроить VPN туннель между виртуальной машиной с операционной системой RouterOS и удалённой виртуальной машиной. Для работы с RouterOS достаточно удобно использовать графический интерфейс.
