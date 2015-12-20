Vagrant.configure "2" do |config|

  # See https://github.com/mitchellh/vagrant/wiki/Available-Vagrant-Boxes for more boxes.
  # config.vm.box     = "precise64_base"
  # config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  # config.vm.box = "hashicorp/precise64"
  config.vm.box = "bento/ubuntu-14.04"

  # change default username if needed
  # config.ssh.username = "travis"

  # requires installing a plugin with
  # vagrant gem install vagrant-vbguest
  # config.vbguest.auto_update = true

  # config.vm.provider "virtualbox" do |vm|
  #   # changing nictype partially helps with Vagrant issue #516, VirtualBox NAT interface chokes when
  #   # # of slow outgoing connections is large (in dozens or more).
  #   vm.customize ["modifyvm", :id, "--nictype1", "Am79C973", "--memory", "1536", "--cpus", "2", "--ioapic", "on"]
  #
  #   # see https://github.com/mitchellh/vagrant/issues/912
  #   vm.customize ["modifyvm", :id, "--rtcuseutc", "on"]
  # end
  # config.vm.provision :shell do |sh|
  #  sh.inline = <<-EOF
  #    sudo apt-get install ruby1.9.1-dev
  #    gem install chef --no-ri --no-rdoc --no-user-install
  #  EOF
  # end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["travis-cookbooks/community-cookbooks", "travis-cookbooks/cookbooks"]
    # chef.log_level      = :debug

    # Highly recommended to keep apt packages metadata in sync and
    # be able to use apt mirrors.
    chef.add_recipe     "apt"

    # List the recipies you are going to work on/need.
    # chef.add_recipe     "build-essential"
    # chef.add_recipe     "networking_basic"

    # chef.add_recipe     "travis_build_environment"
    # chef.add_recipe     "git"

    # chef.add_recipe     "java::openjdk7"
    # chef.add_recipe     "leiningen"

    # chef.add_recipe     "rabbitmq::with_management_plugin"

    # chef.add_recipe "rvm::vagrant"
    # chef.add_recipe "rvm::system"

    # chef.add_recipe     "rvm"
    # chef.add_recipe     "nodejs::multi"
    # chef.add_recipe     "python::multi"

    # chef.add_recipe     "libqt4"
    # chef.add_recipe     "xserver"
    # chef.add_recipe     "firefox"

    # chef.add_recipe     "memcached"
    # chef.add_recipe     "redis"
    # chef.add_recipe     "riak"
    # chef.add_recipe     "mongodb"
    # chef.add_recipe     "mysql::client"
    # chef.add_recipe     "mysql::server"
    # chef.add_recipe     "postgresql::client"
    # chef.add_recipe     "postgresql::all_packages"
    # chef.add_recipe     "couchdb::ppa"
    # chef.add_recipe     "neo4j-server::tarball"
    # chef.add_recipe     "firebird"

    # chef.add_recipe     "elasticsearch"
    # chef.add_recipe     "cassandra::datastax"
    # chef.add_recipe     "hbase::ppa"
    # chef.add_recipe     "pypy::ppa"

    # https://github.com/martinisoft/chef-rvm/issues/121
    chef.json.merge!({
      :rvm => {
        :vagrant => {
          :system_chef_solo => '/opt/vagrant_ruby/bin/chef-solo'
        },
        :gpg => {}
      }
    })

    # chef.json.merge!({
    #                    :apt => {
    #                      :mirror => :ru
    #                    },
    #                    :rvm => {
    #                      :rubies  => [
    #                        { :name => "1.8.7" },
    #                        { :name => "rbx-head", :arguments => "--branch 2.0.testing", :using => "1.8.7" },
    #                        { :name => "jruby-d19", :arguments => "--19" },
    #                        { :name => "ruby-head-s92b6597be67738490c0ab759303a0e81a421b89a" },
    #                        { :name => "1.9.3" },
    #                        { :name => "rbx-head-d19", :arguments => "--branch 2.0.testing --19", :using => "1.9.3" },
    #                        { :name => "jruby" },
    #                        { :name => "jruby-head" },
    #                        { :name => "1.9.2" },
    #                      ],
    #                      :aliases => {
    #                        "rbx"         => "rbx-head",
    #                        "rbx-2.0"     => "rbx-head",
    #                        "rbx-2.0.pre" => "rbx-head"
    #                      }
    #                    },
    #                    :mysql => {
    #                      :server_root_password => ""
    #                    },
    #                    :postgresql => {
    #                      :max_connections => 256
    #                    }
    #                  })
  end
end
