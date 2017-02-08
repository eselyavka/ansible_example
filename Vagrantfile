Vagrant.configure("2") do |config|
  config.vm.box = "dongmyo/centos-6.5-lamp-tomcat-maven"
  config.vm.box_check_update = false
  config.vm.hostname = "ansible01"
  config.vm.post_up_message = "may be some instruction for developers"
  config.vm.provider "virtualbox" do |v|
    v.name = "Test App deploy"
    v.customize ["modifyvm", :id, "--memory", "2048", "--ostype", "RedHat_64", "--cpus", "1"]
  end
  config.vm.network :private_network, ip: "192.168.111.10"
  config.vm.network "forwarded_port", guest: 80, host: 7080, auto_correct: true
  config.vm.network "forwarded_port", guest: 8080, host: 7180, auto_correct: true
  config.vm.network "forwarded_port", guest:6379 , host: 6379, auto_correct: true
  config.vm.network "forwarded_port", guest:11211 , host: 11211, auto_correct: true
  config.vm.network "forwarded_port", guest:5432 , host: 5432, auto_correct: true
  config.vm.provision "ansible", run: "always" do |p|
    p.inventory_path = "provision/local"
    p.playbook = "provision/local.yml"
    p.verbose = "vvvv"
    p.limit = 'all'
    p.extra_vars = { ansible_ssh_user: 'vagrant', ansible_ssh_host: '192.168.111.10', ansible_ssh_port: '22' }
  end
end
