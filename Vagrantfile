# https://docs.ansible.com/ansible/latest/scenario_guides/guide_vagrant.html

Vagrant.require_version ">= 1.8.0"
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.hostname = "test.hadoop.com"
    config.vm.provider "virtualbox" do |vbox|
        vbox.name = "ubuntu-20.04"
        vbox.memory = 2048
        vbox.cpus = 2
    end
end
