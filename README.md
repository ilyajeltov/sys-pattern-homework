# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Приведите ответ в свободной форме........`

1. `Обновляем КЭШ репозиториев и обновляем зависимости`
2. `Устанавливаем posttgres`
3. `Скачиваем репу`
4. `Ставим репозитории и опять обновляем кэш репозиториев что бы появились репозитория zabbix`
5. `Создаем юзера для БД и создаем саму БД`
6. `Копируем задержимое в БД`
7. `Прописываем юзера БД и пароль в настройках zabbix сервера` 
8. `Рестартуем, включаем, проверяем что apache и zabbix server запустились`

```
sudo apt update
sudo apt upgrade
sudo apt install postgresql postgresql-contrib

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"' 

su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"' 

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf 

systemctl restart zabbix-server  apache2

systemctl enable zabbix-server apache2

systemctl status zabbix-server  apache2

```

При необходимости прикрепитe сюда скриншоты
[Окно Авторизации](https://ru.paste.pics/1dda3d290162d2c82283ae29b459aa67)


---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Заходим на WEB -> Configuration->Hosts->Create hos`
2. `Далее прописываем имя хоста, добавляем группы(может сделать свои), добавляем интерфейс и настраиваем подключение по IP или DNS(на ваш выбор если есть DNS у сервера)`
3. `Добавляем и когда Status будет Enabled, а Availability гореть зеленом`
4. `И конечно что бы все получилось нужно в самом агенте прописать IP(нашего сервреа) или повесть, к кому он может подключаться`
5. `В данный момент я подключил два агента, один стоит на отдельной машине второй на самом сервере`
6. 

```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb

dpkg -i zabbix-release_6.0-4+debian11_all.deb

apt update apt install zabbix-agent

systemctl restart zabbix-agent

systemctl enable zabbix-agent

systemctl status zabbix-agent
```

При необходимости прикрепитe сюда скриншоты
[Скриншот что zabbix агенты подключены](https://ru.paste.pics/87ceb3b9b1ae787b746b2655d5e62b37)
[Скриншот что все работает как нужно](https://ru.paste.pics/83d123bfb565c98f53fb191560e48473)
[Скриншот Monitoring->Latest Data](https://ru.paste.pics/c5149a9fbf9e06c8d82f439b0e940ac1)


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`




# Домашнее задание к занятию "`Система мониторинга Zabbix. Часть 2`" - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста`

1. `Заходим в Configuration -> Templates`
2. `Нажимаем Create Templates`
3. `Указываем Template name, Groups, `
4. `Далее настроил макрос {$UPDATE_INTERVAL_TIME}`
5. `Добавил свои items в Templat,  proc.cpu.util и proc.mem`


При необходимости прикрепитe сюда скриншоты
[Скрин templates](https://ru.paste.pics/e37f4b901964110ea04b456162750112)
[Скрин items](https://ru.paste.pics/e0d190c98a9aeca2fc79e7cc15709386)


---

### Задание 2

`Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>. Например: ivanovii-1 и ivanovii-2`

1. `Поднял две вертуальные машине с именами iszheltov-1 и iszheltov-2`
2. `Установил на ни zabbix агентов и в конфигах прописал ip сервера (код по установке нижк)`
3. `закрепил за каждый агентов шаблон Linux by Zabbix Agent`
4. `Проверил что в разделе Latest Data начали появляться данные с добавленных агентов`

```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb

dpkg -i zabbix-release_6.0-4+debian11_all.deb

apt update 

apt install zabbix-agent

systemctl restart zabbix-agent

systemctl enable zabbix-agent

systemctl status zabbix-agent
```

При необходимости прикрепитe сюда скриншоты
[Скриншот что мой шаблон привязан к двух хостам iszheltov-1 и iszheltov-2](https://ru.paste.pics/0e05077b061cc9ea4d06e42557705e0c)
[Скрин что они активны](https://ru.paste.pics/dfb07ec642e73ebbbf67bcceb3d14a46)
[Скрин моего itema CPU](https://ru.paste.pics/bf242460629822218afe7c4343881e85)
[Скрин моего itema MEMORY](https://ru.paste.pics/ab509708575df8eb00071b9011cf6ae5)


---

### Задание 3

`Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent`

1. `Зашле в настройки каждого хоста и в разделы Templates и прикрепил к этим хостам мой шаблон`
2. `Привязал им Linux by Zabbix Agent`
3. `Проверил что в разделе Latest Data начали появляться данные с добавленных агентов` 

[Название скриншота](ссылка на скриншот)
[Скриншот что мой шаблон привязан к двух хостам iszheltov-1 и iszheltov-2](https://ru.paste.pics/0e05077b061cc9ea4d06e42557705e0c)
[Скрин что они активны](https://ru.paste.pics/dfb07ec642e73ebbbf67bcceb3d14a46)
[Скрин моего itema CPU](https://ru.paste.pics/bf242460629822218afe7c4343881e85)
[Скрин моего itema MEMORY](https://ru.paste.pics/ab509708575df8eb00071b9011cf6ae5)


### Задание 4

`Создайте свой кастомный дашборд`

1. `Зашел и создал свой шаблон`
2. `на шаблоне расместил все свои тачки и так же разместил метрики со своими items`

При необходимости прикрепитe сюда скриншоты
[скрин дашборда](https://ru.paste.pics/32bba9f8cd4de6a9a476140c3a5b1d5a)



# Домашнее задание к занятию "`Система мониторинга Prometheus`" - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Установите Prometheus`


При необходимости прикрепитe сюда скриншоты
[Скрин Prometheus](https://ru.paste.pics/2e67388e4ea1aa6f7c6b99729260b7e8)


---

### Задание 2

`Установите Node Exporter`


При необходимости прикрепитe сюда скриншоты
[Скрин exporete](https://ru.paste.pics/f41cbc3b172899591b651e8b63138205)


---

### Задание 3

`Подключите Node Exporter к серверу Prometheus` 

[Название скриншота](ссылка на скриншот)
[Скриншот что мой шаблон привязан к двух хостам iszheltov-1 и iszheltov-2](https://ru.paste.pics/0e05077b061cc9ea4d06e42557705e0c)
[Скрин 1](https://ru.paste.pics/cb5edb4f1bf3fe3da847fcc89fc0d331)
[Скрин 2](https://ru.paste.pics/6b7f0c330b3874d2a65e00b3a3a90edc)


### Задание 4

`Установите Grafana`

При необходимости прикрепитe сюда скриншоты
[скрин garafana](https://ru.paste.pics/42b8fd8ec9f8e9f1c60235d13ab91967)



### Задание 5

`Интегрируйте Grafana и Prometheu`

При необходимости прикрепитe сюда скриншоты
[Интеграция](https://ru.paste.pics/df36ddc79b1a814a82ac8a3c05a94e13)




# Домашнее задание к занятию "`Система мониторинга Prometheus часть 2`" - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Создайте файл с правилом оповещения, как в лекции, и добавьте его в конфиг Prometheus`


При необходимости прикрепитe сюда скриншоты
[статус pending](https://ru.paste.pics/850aa0961ea8c17723d2e2f0737db7fb)


---

### Задание 2

`Установите Alertmanager и интегрируйте его с Prometheus`


При необходимости прикрепитe сюда скриншоты
[Скрин Fireing](https://ru.paste.pics/d007049a44c71bc8aefb751b47ba79ae)
[Правило оповещения](https://ru.paste.pics/6ec02dcafa957ac2ce6a9e24d76fa5ac)


---

### Задание 3

`Активируйте экспортёр метрик в Docker и подключите его к Prometheus` 

[Название скриншота](ссылка на скриншот)
[endpoint](https://ru.paste.pics/2d4ac0bc28a839ab8da35c47a38ab0e0)
[prom](https://ru.paste.pics/0b11f60d3ee5527e966bb4ae9048b8a4)


### Задание 4

`Установите Grafana`

При необходимости прикрепитe сюда скриншоты
[скрин garafana docker](https://ru.paste.pics/fa659988ec1bae284569de85cc95a452)










# Домашнее задание к занятию "`Disaster recovery и Keepalived`" - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---


### Задание 1

`Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.`
`На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)`
`Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).`
`Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.`
`На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.`

1. `С помощью команды sho standby можно увидеться выполненые настройки`
2. `При разрве любого соединения пакет дайдет в нужном напарвлении`


При необходимости прикрепитe сюда скриншоты
[скрин конфигурвции](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/dz1.png)
[схема](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/dz1.pkt)


### Задание 2

`Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.`
`Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах`
`Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.`
`Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script`
`На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html`

1. `Поднял две машины на Debian и настроил Keepalived`
2. `Поднял два сервира nginx на каждой машине`
3. `Скрипт реализован на Bash`
4. `Настроил итервал в 3 секунды что было ip перемещался на другую ноду в случа недоступности`

[скрин запущенныйх служб keepalived](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/1k.png)
[скрин запущенныйх служб keepalived](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/2k.png)
[nginx1](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/1n.png)
[nginx2](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/2n.png)
[настройка keepalived1](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/master.png)
[настройка keepalived2](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/back.png)
[скрипт](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/script.png)
[Демонстрация работы 1](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/1-1.png)
[продолжение скрипта](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/1-2.png)


# Домашнее задание к занятию "`Домашнее задание к занятию 2 «Кластеризация и балансировка нагрузки»`" - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---


### Задание 1

Запустите два `simple python` сервера на своей виртуальной машине на разных портах
Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
Настройте балансировку `Round-robin` на 4 уровне
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к `HAProxy`.

1. Запускаю ВМ и создаю две директории
 ```bash
mkdir http1
``` 
```bash
mkdir http2
``` 

2. Установил haproxy
 ```bash 
sudo apt-get install haproxy
```

3. Установил haproxy
 Запустил два python-сервера с разными портами. Один с портом 8888
 ![Запуска сервер 1](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/sr1.png)

 Запустил два python-сервера с разными портами. Один с портом 9999
 ![Запуск сервера 2](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/sr2.png)


4. Из материалов к лекции выполнил настройку конфигурационного файла для балансировки на L4
```bash
global
        log /dev/log    local0
        log /dev/log    local1 notice
        chroot /var/lib/haproxy
        stats socket /run/haproxy/admin.sock mode 660 level admin
        stats timeout 30s
        user haproxy
        group haproxy
        daemon

        # Default SSL material locations
        ca-base /etc/ssl/certs
        crt-base /etc/ssl/private

        # See: https://ssl-config.mozilla.org/#server=haproxy&server-version=2.0.3&config=intermediate
        ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RS>
        ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256
        ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets

defaults
        log     global
        mode    http
        option  httplog
        option  dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000
        errorfile 400 /etc/haproxy/errors/400.http
        errorfile 403 /etc/haproxy/errors/403.http
        errorfile 408 /etc/haproxy/errors/408.http
        errorfile 500 /etc/haproxy/errors/500.http
        errorfile 502 /etc/haproxy/errors/502.http
        errorfile 503 /etc/haproxy/errors/503.http
        errorfile 504 /etc/haproxy/errors/504.http

listen stats
        bind                    :888
        mode                    http
        stats                   enable
        stats uri               /stats
        stats refresh           5s
        stats realm             Haproxy\ Statistics

frontend example
        mode http
        bind :8088
        default_backend web_servers

backend web_servers
        mode http
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8888 check
        server s2 127.0.0.1:9999 check

listen web_tcp

        bind :1325

        server s1 127.0.0.1:8888 check inter 3s
        server s2 127.0.0.1:9999 check inter 3s

```

5. Проверил в браузере страницу со статистикой .

![Стата](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/stat.png)

### Задание 2

Запустите три `simple python` сервера на своей виртуальной машине на разных портах
Настройте балансировку `Weighted Round Robin` на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
HAproxy должен балансировать только тот `http-трафик`, который адресован домену example.local
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена `example.local` и без него.


1. Я добавил 3-ю диркторию `http3`, в ней  создал файл `index.html` вот с такими данными `Server 3 :6666` и запустил в ней Python-server
2. Открываю  конфигурационный файл `haproxy`
--
```bash
sudo nano /etc/haproxy/haproxy.cfg
```
--
и в пунктах `forntend` и `backend` изменил следующие настройки

![Скрин изменений](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/zdz.png)
--

перезагружаем `HaProxy`
И попробуем отправить запрос домену `example.com`

```bash
curl -H 'Host:example.local' http://127.0.0.1:8088
```
![Чекаем по домену](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/zapros.png)

и получаю балансировку по весу серверов: 
- 4 запроса на 888
- 3 запроса на 666
- 2 запроса на 999

![Скрин запросов](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/final.png)
--

Если сделать запрос без указания хоста , то мы получим ошибку

![Скрин](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/error.png)
--

Файл конфигурации
[Файл конфигурации](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/haproxy.cfg)




# Домашнее задание к занятию `Домашнее задание к занятию 3 Резервное копирование` - `Zheltov Ilya`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

----

### Задание 1
Составьте команду `rsync`, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию `/tmp/backup`
Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
Необходимо сделать так, чтобы `rsync` подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
На проверку направить скриншот с командой и результатом ее выполнения

1. Прилагаю скриншот своей команды 
---
 ![Команда rsync](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/rsync.png)

- `a` Архивный режим (сохраняет права, символьные ссылки и временные метки)
- `c` Заставляет rsync использовать контрольные суммы (хэши) для проверки файлов
- `progress` Наблюдаем за прогрессом выполнения
- `exlude` Исключаем файлы которые не сенхронизируются
- `delete` копирование в режиме заркалирования
---
![Выполнение команды](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/rsync_done.png)
 Убрал `--progress` что бы наглядно показать
---

### Задание 2

Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью `rsync` и `cron`.
Резервная копия должна быть полностью зеркальной
Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции
Резервная копия размещается локально, в директории `/tmp/backup`
На проверку направить файл `crontab` и скриншот с результатом работы утилиты.


1. Написал скрипт на bash который.
```bash
#!/bin/bash

SOURCE="/home/iszheltov/"
DEST="/tmp/backup_iszheltov/"
LOG_TAG="backup_iszheltov"

# Создаём директорию назначения, но сначала проверим существует или нет
if [ ! -d "$DEST" ]; then
    mkdir -p "$DEST"
fi


rsync -av --delete "$SOURCE" "$DEST"

if [ $? -eq 0 ]; then
    logger -t "$LOG_TAG" "Backup успешно выполнен для $SOURCE в $DEST"
else
    logger -t "$LOG_TAG" "Ошибка при выполнении backup для $SOURCE"
    exit 1
fi
```
---
- Делае зеркалированное резервное копирование
- Добавил задачу в cron для ежедневного выполнения
- Добавил лог фаил который все это логирует
- Копия складывается локально в `/tmp/backup_iszheltov`
---
![Crontab -L](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/cron.png)

Для проверки работы дерним скрипт вручную

![result](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/result.png)

Для наглядности выполнения отключил `verbous`e в скрипте.

### Задание 3

Настройте ограничение на используемую пропускную способность `rsync` до 1 Мбит/c
Проверьте настройку, синхронизируя большой файл между двумя серверами
На проверку направьте команду и результат ее выполнения в виде скриншота

Для ограниче на пропускную способность нужно использовать `bwlimit`
Расчитаем сначала более точно что бы выставить ограничения
`1 Мбит/с = 1024 Кбит/с = 1024 / 8 КБ/с ≈ 128 КБ/с`. Для точности и меньшего потребления возьмем 125 КБ/с

![bwlimit](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/bwlimite.png)
---
![2-й сервер](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/server2.png)
---
Как мы видим скорость передачи была не выше 125.

