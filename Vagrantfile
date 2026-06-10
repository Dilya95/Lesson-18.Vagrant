# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-26.04"
  config.vm.hostname = "otus-homework"


  # выделение памяти 
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
  end


  # Дополнительные диски — Vagrant Disks API.
  # name: обязательно (чтобы при vagrant reload диск не пересоздавался).
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.disk :disk, size: "1GB", name: "extra1"
  config.vm.disk :disk, size: "1GB", name: "extra2"


  # Проброс портов: запрос к http://localhost:8080 на хосте уйдёт
  # на 80-й порт внутри VM. Аналог `docker run -p 8080:80`.
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Provision: формат, монтирование, fstab, + бонус nginx
  config.vm.provision "shell", inline: <<-'SHELL'
    set -euo pipefail
    apt-get update
    apt-get install -y nginx
    echo "<h1>Hello from Vagrant + shell provision</h1>" > /var/www/html/index.html

    # --- Найти добавленные диски ---
    # Имена устройств варьируются: на amd64-VBox обычно /dev/sdb, /dev/sdc,
    # на ARM-VBox или с другим контроллером — могут быть /dev/vdb, /dev/nvme*.
    # Поэтому ищем не по имени, а по характеристикам:
    #   TYPE = disk (не partition, не loop, не rom)
    #   нет точки монтирования (системный диск занят корнем)
    #   размер ≈ 1ГБ (Vagrant Disks API "1GB" = 1073741824 байт)
    #
    # Используем -b (bytes) для численного сравнения — без зависимости от
    # локали (в ru_RU lsblk может показать "1,0G" вместо "1G").
    # Диапазон 1.0–1.2 ГБ на случай если provider создаст немного больше.
    echo "=== Настраиваем диски ==="

    # Определяем новые диски (обычно /dev/sdb и /dev/sdc)
    DISKS=($(ls /dev/sd? | grep -v /dev/sda | sort))

    if [ ${#DISKS[@]} -ne 2 ]; then
      echo "Ошибка: найдено ${#DISKS[@]} новых дисков, ожидалось 2"
      ls /dev/sd*
      exit 1
    fi

    DISK1=${DISKS[0]}
    DISK2=${DISKS[1]}

    echo "Диски: $DISK1 и $DISK2"

    # Форматируем (только если не отформатированы)
    if ! blkid $DISK1 | grep -q ext4; then
      echo "Форматируем $DISK1 → ext4"
      mkfs.ext4 -F $DISK1
    fi

    if ! blkid $DISK2 | grep -q ext4; then
      echo "Форматируем $DISK2 → ext4"
      mkfs.ext4 -F $DISK2
    fi

    # Создаём точки монтирования
    mkdir -p /mnt/disk1 /mnt/disk2

    # Монтируем
    mount $DISK1 /mnt/disk1 || true
    mount $DISK2 /mnt/disk2 || true

    # Добавляем в /etc/fstab (используем UUID — надёжнее)
    if ! grep -q "/mnt/disk1" /etc/fstab; then
      UUID1=$(blkid -s UUID -o value $DISK1)
      UUID2=$(blkid -s UUID -o value $DISK2)
      echo "UUID=$UUID1  /mnt/disk1  ext4  defaults  0  2" >> /etc/fstab
      echo "UUID=$UUID2  /mnt/disk2  ext4  defaults  0  2" >> /etc/fstab
      echo "Записи в fstab добавлены"
    fi
  SHELL
end
