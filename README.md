# Домашнее задание к занятию "`Защита хоста`" - `Белолипецкий Леонид`

---

### Задание 1

`Так как WSL2 модуль eCryptfs недоступен из-за ограничений ядра Windows, выполнил шифрование альтернативным способом`

До шифрования:

![img](img/img1.png)

Был введён код для шифрования:
```bash

sudo dd if=/dev/zero of=/home/crypted_home.img bs=1M count=100 status=progress
sudo losetup -f /home/crypted_home.img
LOOP_DEV=$(losetup -a | grep crypted_home | cut -d: -f1)
echo "Loop device: $LOOP_DEV"
echo "password123" | sudo cryptsetup luksFormat $LOOP_DEV --key-file=-
echo "password123" | sudo cryptsetup luksOpen $LOOP_DEV crypted_home --key-file=-
sudo mkfs.ext4 /dev/mapper/crypted_home
sudo mkdir -p /mnt/crypted_home
sudo mount /dev/mapper/crypted_home /mnt/crypted_home
sudo cp -r /home/cryptouser/* /mnt/crypted_home/
sudo chown -R cryptouser:cryptouser /mnt/crypted_home/
sudo ls -la /mnt/crypted_home/

```

После шифрования шифрования:

![img](img/img2.png)

---

### Задание 2

![img](img/img3.png)

![img](img/img4.png)

![img](img/img5.png)

---