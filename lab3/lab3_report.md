University: ITMO University

Faculty: FICT

Course: Network programming

Year: 2022/2023

Group: K34202

Author: Molchanova Veronika Alexandrovna

Lab: Lab3

Date of create: 24.11.2022

Date of finished: . .2022

---

*Поднятие NetBox на дополнительной VM.*
Netbox — это открытое (open source) веб приложение, разработанное для управления и документирования компьютерных сетей. 
Netbox был развёрнут на облачной виртуальной машине.
Была установлена база данных postgresql

\\ команда \\

![image](https://user-images.githubusercontent.com/90505004/205699942-7171d883-1dd5-47c5-929a-9794b4e70798.png)

Создана нужная база данных и привелегированный пользователь

![image](https://user-images.githubusercontent.com/90505004/205699973-8ce917bd-e5ca-4d48-8476-7d58afc97464.png)

Также требуется установить Redis - СУБД для баз данных NoSQL

\\ и дальше как у Макса \\
![image](https://user-images.githubusercontent.com/90505004/205700210-1b8b5cb1-bda7-4426-8665-45a4b378c6a0.png)

![image](https://user-images.githubusercontent.com/90505004/205700264-e2414ed5-ff9d-400d-b444-bdc5b508846a.png)


*Заполнить всю возможную информацию об имеющихся CHR в Netbox.*

![image](https://user-images.githubusercontent.com/90505004/205700424-e11ee880-966d-4ba7-b803-d0857b9675b7.png)
\поменять имя\

![image](https://user-images.githubusercontent.com/90505004/205700621-555afe34-87e4-4e79-a78f-fba9a26c9966.png)
\поменять айпишники\

*Используя Ansible и роли для Netbox в тестовом режиме сохранить все данные из Netbox в отдельный файл*

![image](https://user-images.githubusercontent.com/90505004/205700839-3f08bb20-7aaa-49b5-b0cb-01705be609db.png)
\поменять путь\

![image](https://user-images.githubusercontent.com/90505004/205700972-3e2f1cb1-0d4a-457b-8710-1fbc9545b853.png)



*Написать сценарий, при котором на основе данных из Netbox можно настроить 2 CHR, изменить имя устройства, добавить IP адрес на устройство.*

![image](https://user-images.githubusercontent.com/90505004/205702865-77daf7e7-e44d-423d-a546-6318632a8c57.png)

![image](https://user-images.githubusercontent.com/90505004/205702943-436f0cec-c1ae-4879-b720-8effb9163d30.png)


*Написать сценарий, позволяющий собрать серийный номер устройства и вносящий серийный номер в Netbox.*
![image](https://user-images.githubusercontent.com/90505004/205702996-94eb3775-2317-468c-af11-ec03800e0b0c.png)
\поменять имя\

![image](https://user-images.githubusercontent.com/90505004/205703148-74a78f60-dd67-4457-a25e-6afa0a8cfd7d.png)
\сама поймёшь\

![image](https://user-images.githubusercontent.com/90505004/205703213-9c71389f-9d76-4ae5-8466-50fa783fcfe3.png)

![image](https://user-images.githubusercontent.com/90505004/205703240-abad78c5-84d1-4ff3-8079-233b59b3a96d.png)

\схема\
