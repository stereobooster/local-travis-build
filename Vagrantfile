# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty64'
  config.vm.hostname = 'rails-dev-box'

  config.vm.network :forwarded_port, guest: 3000, host: 3000

  config.vm.provision :shell, keep_color: true, inline: <<-SHELL
    function install {
        echo installing $1
        shift
        apt-get -y install "$@" >/dev/null 2>&1
    }

    echo updating package information
    apt-add-repository -y ppa:brightbox/ruby-ng >/dev/null 2>&1
    apt-get -y update >/dev/null 2>&1
    # apt-get -y update >/dev/null 2>&1

    install 'development tools' build-essential

    install Ruby ruby2.2.3 ruby2.2.3
    update-alternatives --set ruby /usr/bin/ruby2.2 >/dev/null 2>&1
    update-alternatives --set gem /usr/bin/gem2.2 >/dev/null 2>&1

    install Git git

    echo installing rbenv
    cd
    git clone git://github.com/sstephenson/rbenv.git .rbenv >/dev/null 2>&1
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
    echo 'eval "$(rbenv init -)"' >> ~/.bash_profile

    echo installing ruby-build
    git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build >/dev/null 2>&1
    echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bash_profile
    source ~/.bash_profile

    cd /home/vagrant

    rbenv rehash

    echo updating gems
    gem update --system >/dev/null 2>&1

    echo installing Bundler
    gem install bundler -N >/dev/null 2>&1
    echo installing wwtd
    gem install wwtd -N >/dev/null 2>&1

    install SQLite sqlite3 libsqlite3-dev
    # install memcached memcached
    # install Redis redis-server
    # install RabbitMQ rabbitmq-server

    install PostgreSQL postgresql postgresql-contrib libpq-dev
    sudo -u postgres createuser --superuser vagrant
    sudo -u postgres createdb -O vagrant activerecord_unittest

    debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    install MySQL mysql-server libmysqlclient-dev
    mysql -uroot -proot "CREATE USER 'rails'@'localhost'"
    mysql -uroot -proot "CREATE DATABASE activerecord_unittest  DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci"
    mysql -uroot -proot "GRANT ALL PRIVILEGES ON activerecord_unittest.* to 'rails'@'localhost'"

    # install 'Nokogiri dependencies' libxml2 libxml2-dev libxslt1-dev
    # install 'ExecJS runtime' nodejs

    # Needed for docs generation.
    update-locale LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8

    echo 'all set, rock on!'
  SHELL
end
