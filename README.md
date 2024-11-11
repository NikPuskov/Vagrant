# Vagrant
`Обновить ядро в базовой системе`

Устанавливаем Vagrant для Windows https://hashicorp-releases.yandexcloud.net/vagrant/2.4.2/vagrant_2.4.2_windows_amd64.msi

Устанавливаем VirtualBox для Windows https://download.virtualbox.org/virtualbox/7.1.4/VirtualBox-7.1.4-165100-Win.exe

Устанавливаем VM VirtualBox Extension Pack https://download.virtualbox.org/virtualbox/7.1.4/Oracle_VirtualBox_Extension_Pack-7.1.4.vbox-extpack

Создаем папку vm на диске C (C:\vm)

Выполняем команду `vagrant init` из командной строки (cmd) в папке `c:\vm`

Редактируем созданный `Vagrantfile` в папке `c:\vm` (отредактированный файл лежит на GitHub)

1. Добавляем репозиторий  `ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'`
2. Указываем имя бокса `config.vm.box = "ubuntu/focal64"`
3. Указываем настройку сети `config.vm.network "public_network"`
4. Указываем настройки для VirtualBox (соблюдая отступы):

   `config.vm.provider "virtualbox" do |vb|`

     `vb.gui = false`

     `vb.memory = "4096"`

     `vb.cpus = "4"`

     `vb.name = "otus_vm"`

   `end`

6. Указываем Provision (соблюдая отступы):

   `config.vm.provision "shell", inline: <<-SHELL`

      `apt update`

      `apt -y full-upgrade`

      `reboot`        

   `SHELL`

`end`

Выполняем команду `vagrant up` из командной строки (cmd) в папке `c:\vm`

После выполнения `Vagrantfile` заходим в виртуальную машину командой `vagrant ssh`

Проверяем версию ядра командой `uname -r` (при установке без обновления версия `5.4.0-148-generic`, после обновления версия `5.4.0-200-generic`)
