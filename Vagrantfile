Vagrant.configure("2") do |config|
  # Указываем базовый образ операционной системы (загружен вручную)
  config.vm.box = "ubuntu/bionic64"

  # Проброс порта для PostgreSQL
  config.vm.network "forwarded_port", guest: 5432, host: 5432

  # Настройка виртуальной машины
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
  end

  # Скрипт для установки PostgreSQL 8.4
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y wget lsb-release
    # Добавляем репозиторий для PostgreSQL 8.4
    sudo sh -c 'echo "deb http://apt-archive.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo apt-get update
    sudo apt-get install -y postgresql-8.4 postgresql-contrib-8.4
  SHELL
end
