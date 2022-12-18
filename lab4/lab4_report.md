University: ITMO University

Faculty: FICT

Course: Network programming

Year: 2022/2023

Group: K34202

Author: Molchanova Veronika Alexandrovna

Lab: Lab4

Date of create: 7.12.2022

Date of finished: . .2022
<img src="" height="220">
## 1. Установка Vagrant, VirtualBox, vm-ubuntu-20.04.

+ Vagrant и VirtualBox предварительно установлены на компьютер
>  Для использования Vagrant в России нужно включить vpn. 

>  Vagrant - свободное и открытое программное обеспечение для создания и конфигурирования виртуальной среды разработки. Является обёрткой для программного обеспечения виртуализации, например VirtualBox.

+ Склонирован репозиторий на диск с помощью команды `git clone https://github.com/p4lang/tutorials`
> Для клонирования с помощью команды git предварительно была установлена программа git

+ В папке vm-ubuntu-20.04 выполнена команда `vagrant up`, которая запустила установку виртуальной машины

<img src="https://user-images.githubusercontent.com/90505004/208214846-d7081861-b6ee-446f-976d-d0e92025e7ca.png" height="220">

+ Далее выполнена комнада `vagrant provision` и в VurtualBox для созданной виртуальной машины изменен тип графического контроллера на VMSVGA, для того чтобы отобразился графический интерфейс.
+ В результате чего запущена виртуальная машина P4 Tutorial Release 2022-12-18. Выполнен вход в пользователя p4.

<img src="https://user-images.githubusercontent.com/90505004/208272459-030c4ff8-b192-4e3c-9640-33ea9841c395.png" height="400">

## 2. Реализация базовой переадресации. 
> Цель задания - дописать программу P4, реализующиую базовую переадресацию. 
### Запуск начального кода
+ Выполнен вход в папку задания. 
+ Затем выполнена команда, которая скомпилирует basic.p4

```
make run
```
+ После этого запускается Mininet
> Mininet — это эмулятор компьютерной сети

<img src="https://user-images.githubusercontent.com/90505004/208278357-5710d9f4-fc66-412b-a1c2-a9a43c61ca08.png" height="400">

+ По умолчанию все коммутаторы просто сбрасывают все приходящие к ним пакеты. Поэтому после пинга не было получена ответа, как и ожидалось.

<img src="https://user-images.githubusercontent.com/90505004/208278358-25dd0a53-3f59-43d7-b0a1-5a109c7d6030.png" height="400">

<img width="406" alt="image_2022-12-18_05-28-21" src="https://user-images.githubusercontent.com/90505004/208278511-e2c25f78-9935-485e-8a6d-8fd57b649109.png">


<img width="399" alt="image_2022-12-18_05-11-49" src="https://user-images.githubusercontent.com/90505004/208278358-25dd0a53-3f59-43d7-b0a1-5a109c7d6030.png">
<img width="396" alt="image_2022-12-18_05-13-01" src="https://user-images.githubusercontent.com/90505004/208278359-f9700e34-8847-4da7-a992-accf6c5bea87.png">
<img width="400" alt="image_2022-12-18_05-13-14" src="https://user-images.githubusercontent.com/90505004/208278360-cc482369-e515-4d14-818b-50015229d0bd.png">
<img width="400" alt="image_2022-12-18_05-17-18" src="https://user-images.githubusercontent.com/90505004/208278362-96176d9a-082e-4fa1-b019-d0742e31449b.png">
<img width="400" alt="image_2022-12-18_05-20-30" src="https://user-images.githubusercontent.com/90505004/208278363-1df97215-91f9-44ce-82fb-8ab228f200e1.png">
<img width="400" alt="image_2022-12-18_05-25-28" src="https://user-images.githubusercontent.com/90505004/208278437-9d221cff-2b84-42a3-80b4-4ee1a5d3c296.png">
<img width="402" alt="image_2022-12-18_05-26-41" src="https://user-images.githubusercontent.com/90505004/208278439-71aee41e-843c-4123-8479-9416bbde5fe2.png">
<img width="400" alt="image_2022-12-18_05-25-28" src="https://user-images.githubusercontent.com/90505004/208278470-c3114fa1-62eb-4141-94a0-47d5f04da238.png">
<img width="402" alt="image_2022-12-18_05-26-41" src="https://user-images.githubusercontent.com/90505004/208278472-e6fbb0f2-65ac-4bd4-8be4-35a544839e4f.png">
