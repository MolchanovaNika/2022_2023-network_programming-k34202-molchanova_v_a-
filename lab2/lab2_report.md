University: ITMO University

Faculty: FICT

Course: Network programming

Year: 2022/2023

Group: K34202

Author: Molchanova Veronika Alexandrovna

Lab: Lab1

Date of create: 24.11.2022

Date of finished: . .2022

---

## 1.Настройка второго CHR.

Через VirtualBox создана вторая виртуальная машина, на ней установлен `CHR Mikrotik`.

![photo_2022-12-03_21-16-07](https://user-images.githubusercontent.com/90505004/205455927-15d57f1f-a394-4ba7-8762-e4d0e46ddd73.jpg)
![photo_2022-12-03_21-19-45](https://user-images.githubusercontent.com/90505004/205455933-9e07b442-fed3-4d1e-a067-fd49a8a97348.jpg)

Обе машины настроены как OpenVpn клиент
![photo_2022-12-03_21-24-19](https://user-images.githubusercontent.com/90505004/205456109-b4d16973-910f-4374-9f75-36e1db2f7366.jpg)
![photo_2022-12-03_21-24-22](https://user-images.githubusercontent.com/90505004/205456115-5e89b4c9-9459-4872-a610-85f264bbb431.jpg)


## 2. Работа с ansible.

Настраиваемм ssh подключение к роутерам.

![image](https://user-images.githubusercontent.com/90505004/205456277-22739396-6792-43d9-9b97-8bd42cda1e17.png)

В VirtualBox добавим NAT соединение и пропишем SSH с портами.

![image](https://user-images.githubusercontent.com/90505004/205456431-366ce590-04f5-4de3-8942-72ea962ac427.png)

Теперь настройка облака. 

Создаем файл hosts.ini. Там указываем адреса машин.

![image](https://user-images.githubusercontent.com/90505004/205457483-6dd85966-a323-460a-a0eb-5deb2074c7fc.png)

Создан playbook.yml файл в /etc/ansible. 
![image](https://user-images.githubusercontent.com/90505004/205457686-77f8a1f0-899b-49ed-ab89-35283657f2ce.png)

Результат выполнения playbook (команда ansible-playbook playbook.yml):

![image](https://user-images.githubusercontent.com/90505004/205458519-dd29b745-85ed-478f-93dc-3d2dca570604.png)

![image](https://user-images.githubusercontent.com/90505004/205458552-3e130a64-e5f2-4a28-b805-00061bd5e959.png)

Проверка на роутерах.
Создание пользователя.

![image](https://user-images.githubusercontent.com/90505004/205458829-4e5ccf2a-4df6-4b6b-8b88-b7f7c1ddb4f7.png)

![image](https://user-images.githubusercontent.com/90505004/205458833-1ff5a044-08e7-40e3-abd5-195b90675933.png)

Установка времени.

![image](https://user-images.githubusercontent.com/90505004/205459504-f663bacb-e203-4a15-9cb7-1c08c98eaf06.png)


