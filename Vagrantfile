Vagrant.configure("2") do |config|
    config.vm.hostname                = "skrolli-ansible"
    config.vm.box                     = "centos65-x86_64-20140116.box"
    config.vm.box_url                 = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

    config.vm.define 'front' do |machine|
        machine.vm.hostname = 'front'
        machine.vm.network "private_network", ip: "10.30.30.2"
    end

    config.vm.define 'app1' do |machine|
        machine.vm.hostname = 'app1'
        machine.vm.network "private_network", ip: '10.30.30.3'
    end

  config.vm.define 'app2' do |machine|
        machine.vm.hostname = 'app2'
        machine.vm.network "private_network", ip: '10.30.30.4'

    machine.vm.provision :ansible do |ansible|
        ansible.groups = {
            "app" => ["app1", "app2"],
            "front" => ["front"]
        }
        ansible.playbook = "site.yml"
        ansible.limit = 'all'
    end
  end
end
