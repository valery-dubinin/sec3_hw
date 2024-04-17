# sec3_hw

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

### Решение 1

**sudo nmap -sA < ip-адрес >**

Никаких событий в логи не попало. Собственно как nmap ничего и не собрал. Кроме того что машина запущена.

**sudo nmap -sT < ip-адрес >**

Уже заработало:

nmap:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/1.png)

логи suricata:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/2.png)

логи fail2ban: (само собой пусто)

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/3.png)

**sudo nmap -sS < ip-адрес >**

Тоже работает:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/4.png)

логи suricata:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/5.png)

логи fail2ban: (само собой пусто)

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/6.png)

**sudo nmap -sV < ip-адрес >**

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/7.png)

логи suricata:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/8.png)

логи fail2ban: (по прежнему пусто, ибо попыток влезть с паролями не было)

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/9.png)

------

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.
![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/9.png)

### Решение 2

1. Hydra справилась раньше, чем ожидалось. Быстронашлась нужная комбинация:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/10.png)   

2. Fail2Ban тем не менее все заметил:

![img](https://github.com/valery-dubinin/sec3_hw/blob/main/img/11.png)      



