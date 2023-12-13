# Demo2024
## 1.
**Цель задания:**
1. Выполнить базовую настройку всех устройств:  
  a. Собрать топологию согласно рисунку. Все устройства работают на OC Linux - Debian  
  b. Присвоить имена в соответствии с топологией  
  c. Рассчить IP-адресацию IPv4 и IPv6. Необходимо заполнить таблицу №1. При необходимости отредактировать таблицу.  
  d. Пул адресов для сети офиса BRANCH - не более 16. Для IPv6 пропустить этот пункт.  
  e. Пул адресов для сети офиса HQ - не более 64. Для IPv6 пропустить этот пункт.  




## Топология
![image](https://github.com/MaximSSA39/Demo2024---1/assets/148869340/0d18022d-4e35-4e69-b9cf-7bf3ebfd7eb9)



## Таблица сети
| Имя устройства | Интерфейс      | IPv4/IPv6      | Маска/Префикс       | Шлюз           |
| -------------- | -------------- | -------------- | ------------------- | -------------- |
| ISP            |      ens192    | 10.12.19.55    | /24                 |                |
|                |      ens224    | 192.168.0.162  | /30                 |                |
|                |      ens256    | 192.168.0.166  | /30                 |                |
| HQ-R           |      ens192    | 192.168.0.165  | /30                 | 192.168.0.166  |
|                |      ens224    | 192.168.0.2    | /25                 |                |
| BR-R           |      ens192    | 192.168.0.161  | /30                 | 192.168.0.162  |
|                |      ens224    | 192.168.0.130  | /27                 |                |
| HQ-SRV         |      ens192    | 192.168.0.1    | /25                 | 192.168.0.2    |
| BR-SRV         |      ens192    | 192.168.0.129  | /27                 | 192.168.0.130  |
---



**IP-адрес машин**  
```
nano /etc/network/interfaces  
```

ISP:  
```
auto ens192  
iface ens192 inet static  
address 10.12.19.55  
gateway 10.10.200.200  
netmask 255.255.255.0  
  
auto ens224  
iface ens224 inet static  
address 192.168.0.162  
netmask 255.255.255.252  

auto ens256  
iface ens256 inet static  
address 192.168.0.166  
netmask 255.255.255.252  
```

HQ-R:
```
auto ens192  
iface ens192 inet static  
address 192.168.0.165  
netmask 255.255.255.252  

auto ens224  
iface ens224 inet static  
address 192.168.0.2  
netmask 255.255.255.224  
```
BR-R:
```
auto ens192  
iface ens192 inet static  
address 192.168.0.161  
netmask 255.255.255.252  

auto ens224  
iface ens224 inet static  
address 192.168.0.130  
netmask 255.255.255.128  
```
HQ-SRV:
```
auto ens192  
iface ens192 inet static  
address 192.168.0.2  
netmask 255.255.255.224  
gateway 192.168.0.2  
```
BR-SRV
```
auto ens192  
iface ens192 inet static  
address 192.168.0.129  
netmask 255.255.255.224
```
