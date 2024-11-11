# Задание 1
## Узнать IP-адрес интерфейса, подключенного к сети Интернет
### Используя команду 'ip addr, ip address, ip addr show, ip a' в консоль выводится сетевой интерфейс и его ip-адрес
*[root@server ~]# ip a*

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
       
2: ***enp0s5***: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether ca:0b:83:0e:f9:5a brd ff:ff:ff:ff:ff:ff
    ***inet 93.183.74.88/24*** brd 93.183.74.255 scope global noprefixroute enp0s5
       valid_lft forever preferred_lft forever
       
**Loopback игнорируется, необходимый интерфейсом является enp0s5, а его ip: 93.183.74.88**
       
## Также можно воспользоваться командой 'hostname -I'(опция 'I' выводит ip-адреса а не имя хоста), так как на сервере один сетевой интерфейс не считая loopback интерфейса 
*[root@server ~]# hostname -I*

*93.183.74.88*

**С помощью этой команды получаем тот же ip-адрес, который получили при использовании первой команды**

# Задание 2
## Создать именованный пайп ( named pipe ). Вывести в файл через созданный pipe вывод команды ss -plnt
### Используя команды 'mkfifo' создается именнованный пайп, с помощью которого можно будет вывести в файл определенную информацию
*[root@server ~]# mkfifo named_pipe*

### 'ss -plnt' колманда для просмота сетевых сокетов(опция 'p' показывает процессы, связанные с сокетами, опция 'l' показывает listening сокеты, опция 'n' показывает числовые адреса и порты, опция 't' показывает тип сокета)
### Команда '>' перенаправляет стандартный вывод ss в файл(канал) named_pipe
### named_pipe, именованный пайп созданный ранее
### Команда & запускает команду ss в фоновом режиме
### [1] 23817, PID ранее запущенной команды
*[root@server ~]# ss -plnt > named_pipe &*

*[1] 23817*

### Используя команду 'touch' создаем файл output.txt для дальнейшей записи в него через пайп результата выполнения команды

*[root@server ~]# touch output.txt*

### С помощью команды 'cat' считываем данные из канала ***named_pipe*** и записываем данные в "output.txt"
*[root@server ~]# cat named_pipe > output.txt*

### Результат выполнения команды можно проверить в ранее созданном файле
![Screenshot From 2024-11-12 00-20-41](https://github.com/user-attachments/assets/518fdeff-8202-4db3-b0d6-c72e6e79e02a)

### Также, что бы не засорять каталог можно удалить пайп с помощью команды 'rm'
*[root@server ~]# rm named_pipe*

# Задание 3
