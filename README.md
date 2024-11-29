# Домашнее задание к занятию  «Защита хоста-ZheltovIS»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Задание 1

1. Установите **eCryptfs**.
2. Добавьте пользователя cryptouser.
3. Зашифруйте домашний каталог пользователя с помощью eCryptfs.


*В качестве ответа  пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.* 

### Ответ 1
Обновляем и устаналиваем 
```bash
sudo apt update
sudo apt install ecryptfs-utils
```

Для добавления нового пользователя используйте команду adduser:
```bash
sudo adduser cryptouser
```
Далее установим lsof
```bash
sudo apt install lsof
```
Запустил модуль 
```bash
sudo modprobe ecryptfs
```

Ишифруем домашнию директорию этого юхера
```bash
sudo ecryptfs-migrate-home -u cryptouser
```
[shifr](https://github.com/ilyajeltov/sys-pattern-homework/tree/main/img/shifr.png)

### Задание 2

1. Установите поддержку **LUKS**.
2. Создайте небольшой раздел, например, 100 Мб.
3. Зашифруйте созданный раздел с помощью LUKS.

*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*

### Ответ 2

Устанавливаем gparted cryptsetup (LUKS)
```bash
apt install gparted cryptsetup
```

В esxi добавляем доп. диск размер (100 МБ)
```bash
echo "- - -" | tee /sys/class/scsi_host/host*/scan
```

проверяем
```bash
fdisk -l
Disk /dev/sdb: 100 MiB, 104857600 bytes, 204800 sectors
Disk model: Virtual disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

подготавливаем раздел
```bash
cryptsetup -y -v --type luks2 luksFormat /dev/sdb
```
Вывод
```bash
cryptsetup -y -v --type luks2 luksFormat /dev/sdb

WARNING: Device /dev/sdb already contains a 'ext4' superblock signature.

WARNING!
========
This will overwrite data on /dev/sdb irrevocably.

Are you sure? (Type 'yes' in capital letters): YES
Enter passphrase for /dev/sdb:
Verify passphrase:
Existing 'ext4' superblock signature on device /dev/sdb will be wiped.

Key slot 0 created.
Command successful.
```
Открываем устройство /dev/sdb и задаем ему имя cryptodisk
```bash
sudo cryptsetup luksOpen /dev/sdb cryptodisk
```

Проверяем

```bash
ls -al /dev/mapper/cryptodisk
lrwxrwxrwx 1 root root 7 Jun 27 20:53 /dev/mapper/cryptodisk -> ../dm-1
```

Форматируем раздел

```bash
sudo dd if=/dev/zero of=/dev/mapper/cryptodisk
sudo mkfs.ext4 /dev/mapper/cryptodisk
```

вывод
```bash
sudo dd if=/dev/zero of=/dev/mapper/cryptodisk
dd: writing to '/dev/mapper/cryptodisk': No space left on device
172033+0 records in
172032+0 records out
88080384 bytes (88 MB, 84 MiB) copied, 1.76524 s, 49.9 MB/s
root@ubuntu22-client:~# sudo mkfs.ext4 /dev/mapper/cryptodisk
mke2fs 1.46.5 (30-Dec-2021)
Creating filesystem with 21504 4k blocks and 21504 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```
Монитируем открытый раздел
```bash
mkdir .secret
sudo mount /dev/mapper/cryptodisk .secret/
```

конец
```bash
sudo umount .secret
sudo cryptsetup luksClose cryptodisk
```