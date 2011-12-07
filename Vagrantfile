Vagrant::Config.run do |config|
  aptdir = "#{ENV['HOME']}/aptcache/"
  config.vm.box = "milli-ubuntu-11-10-32-bit"
  config.vm.network "33.33.33.20"
  # config.vm.boot_mode = :gui
  
  # config.vm.forward_port "http", 80, 8080
  # config.ssh.max_tries = 50
  # config.ssh.timeout   = 300
  
  config.vm.share_folder("v-apt", "/var/cache/apt", aptdir)
  config.vm.customize do |vm|
    vm.name = "GitlabHQ"
    vm.memory_size = 384
  end

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  # config.vm.share_folder "v-data", "/vagrant_data", "../data"

  config.vm.provision :chef_solo do |chef|
    chef.log_level = :debug
    chef.cookbooks_path = ["~/chef-repo/cookbooks"]
    # chef.roles_path = 'chef/roles'
    # chef.add_role "nerd_factory"
    chef.add_recipe "base"
    chef.add_recipe "sudo"
    chef.add_recipe "python"
    chef.add_recipe "sqlite"
    chef.add_recipe "rvm::ruby_192"
    chef.add_recipe "nginx"
    chef.add_recipe "unicorn"
    chef.add_recipe "gitlabhq"
    
    # chef.add_recipe "mysql::client"
    # chef.add_recipe "mysql::server"
    #chef.add_recipe "milli-redis"

    # chef.add_recipe "redis2::default"
    # chef.add_recipe "redis2::default_instance"

    # chef.add_recipe "app"
    # chef.add_recipe "app::deploy"

    # chef.json.merge!({ 
    #   :base => {
    #     :system_packages => ["tree", "htop", "vim-nox"]
    #   }
    # })
    chef.json.merge!({
      "authorization" => {
        "sudo" => {
          "groups" => ["admin", "wheel", "sysadmin"],
          "users" => ["vagrant", "git"],
          "passwordless" => true
        }
      }
    })
    end

    # config.vm.provision :chef_client do |chef|
    #   chef.chef_server_url = "https://api.opscode.com/organizations/sprout"
    #   chef.validation_key_path = "/Users/millisami/chef-repo/.chef/sprout-validator.pem"
    #   chef.validation_client_name = "sprout-validator"
    #   
    #    chef.add_recipe "base"
    #    chef.add_recipe "rvm::install"
    #    chef.add_recipe "rvm::ruby_192"

    # chef.add_recipe "mysql::client"
    # chef.add_recipe "mysql::server"
    # # chef.add_recipe "rails"
    #   
    # chef.add_recipe "app"
    #   
    # chef.json = { 
    #     :base => {
    #       :system_packages => ["tree", "htop", "vim-nox"]
    #     },
    #     :app => {
    #       :repository => "https://github.com/millisami/NerdFactory.git"
    #     },
    #     :db => {
    #       :adapter => "mysql"
    #     },
    #     :mysql => {:server_root_password => "dbpassword"}
    #   }    
    # end
end
