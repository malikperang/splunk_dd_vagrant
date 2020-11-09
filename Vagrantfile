# -*- mode: ruby -*-
# vi: set ft=ruby :

servers = [
    {
        :name => "searchead1",
        :type => "searchead",
        :box => "centos/7",
        :eth1 => "192.168.20.21",
        :mem => "2048",
        :cpu => "2",
        :guess_port => "8001",
        :host_port => "8001"
    },
    {
        :name => "indexer01",
        :type => "indexer",
        :box => "centos/7",
        :eth1 => "192.168.20.22",
        :mem => "2048",
        :cpu => "2"
    },
    {
        :name => "indexer02",
        :type => "indexer",
        :box => "centos/7",
        :eth1 => "192.168.20.23",
        :mem => "2048",
        :cpu => "2"
    }
]

$configBox = <<-SCRIPT
    echo 'Installing WGET'
    sudo yum install wget net-tools vim -y
    wget -O splunk-8.1.0-f57c09e87251-linux-2.6-x86_64.rpm 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.1.0&product=splunk&filename=splunk-8.1.0-f57c09e87251-linux-2.6-x86_64.rpm&wget=true'
    chmod 644 splunk-8.1.0-f57c09e87251-linux-2.6-x86_64.rpm
    rpm -i splunk-8.1.0-f57c09e87251-linux-2.6-x86_64.rpm
    # sudo ln -s /opt/splunk/bin/splunk /usr/bin/splunk
    # sudo splunk start
    sudo yum install net-tools
SCRIPT

$startup = <<-SCRIPT
    sudo splunk start
SCRIPT

Vagrant.configure("2") do |config|

    servers.each do |opts|
        config.vm.define opts[:name] do |config|

            config.vm.box = opts[:box]
            config.vm.hostname = opts[:name]
            config.vm.network :private_network, ip: opts[:eth1]

            config.vm.provider "virtualbox" do |v|
                v.name = opts[:name]
                v.customize ["modifyvm", :id, "--groups", "/splunk"]
                v.customize ["modifyvm", :id, "--memory", opts[:mem]]
                v.customize ["modifyvm", :id, "--cpus", opts[:cpu]]
            end
          
            #config.vm.network :forwarded_port, guest:opts[:guess_port], host:opts[:host_port]

            # Only Enable on initial
            # config.vm.provision "shell", inline: $configBox
            config.vm.provision "shell", inline: $startup
          
        end
    end
end 