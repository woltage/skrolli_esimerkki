Vagrant.configure("2") do |config|
    # Annetaan käyttöjärjestelmälle nimi
    config.vm.box                     = "centos65-x86_64-20140116.box"

    # Annetaan linkki käyttöjärjestelmä tiedostoon
 config.vm.box_url                 = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

    # Määrittele kuormantasaaja
    config.vm.define 'front' do |machine|
        # Anna kuormantasaajalle nimi
        machine.vm.hostname = 'front'

	 # Kuormantasaajalle yksityinen verkko
        machine.vm.network "private_network", ip: "10.30.30.2"
    end

    config.vm.define 'app1' do |machine|
        machine.vm.hostname = 'app1'
        machine.vm.network "private_network", ip: '10.30.30.3'
    end

  config.vm.define 'app2' do |machine|
        machine.vm.hostname = 'app2'
        machine.vm.network "private_network", ip: '10.30.30.4'

   # Ansiblea ei tarvitse määritellä joka koneen yhteydessä, koska
   # se osaa automaattisesti ajaa komennot jokaiselle koneelle.

    machine.vm.provision :ansible do |ansible|

 # Annamme ansible.groups muuttujan avulla koneille eri roolit.
        ansible.groups = {
            "app" => ["app1", "app2"],
            "front" => ["front"]
        }

	 # Mikä YAML tiedosto valitaan.
        ansible.playbook = "site.yml"

	 # Mille koneille Ansible ajetaan
        ansible.limit = 'all'
    end
  end
end
