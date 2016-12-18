Consul Demo

This repository explains the basic use for the Consul, as service Regustry tool in the microservices Architecture

uses vagrant as tool for development of Virtual environment
spins three Consul Servers, eash 64 bit Ubuntu machines categorised as:
       One BootStarp Server and two Consul Servers


Setting up the Consul using Vagrant:

Base Box used to spin the ubuntu through Vagarant:

Source for Virtual Box:
https://atlas.hashicorp.com/hashicorp/boxes/precise64

vagrant init hashicorp/precise64; 
vagrant up --provider virtualbox




Following are to be run on all Consul Servers:
sudo su
apt-get update
apt-get install git unzip -y
cd /root
wget https://releases.hashicorp.com/consul/0.6.2/consul_0.6.2_linux_amd64.zip
unzip consul_0.6.2_linux_amd64.zip
rm -f 0.6.2_linux_amd64.zip
mv consul /usr/bin/

Bootstrap / Web UI Server(The BootSTrap MAchine)
 https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip
 wget    https://releases.hashicorp.com/consul/0.7.1/consul_0.7.1_web_ui.zip(latest)
unzip 0.6.2_web_ui.zip
rm -f 0.6.2_web_ui.zip
cd /root/consul_demo

Add Consul to the PATH to all servers:
>> mv consul /usr/bin/
export PATH=$PATH:/consul


>> consul keygen

To generate the encrypted key:
Eg, Key:  f6HnfkLTGbIkFcAfCGZ4RQ==( ensure key doen’t contain /)
To be used to run command from all three servers


The same can be acheived by the following inline commands:
To execute on the Consul Server to be designated as BootStrap Server:
consul agent -dc demo -server -bootstrap -data-dir /var/vagrant -ui-dir /home/vagrant/dist -client 192.0.2.4 -node=consul-agent1 -bind=192.0.2.4 encrypt=f6HnfkLTGbIkFcAfCGZ4RQ==


to execute on other two Consul Servers:
NonBootstrapServer1
sudo consul agent -server -dc demo -data-dir /var/vagrant -node=consul-agent2 -bind=192.0.2.5 -encrypt=f6HnfkLTGbIkFcAfCGZ4RQ==

NonBootstrapServer2
sudo consul agent -server -dc demo -data-dir /var/vagrant -node=consul-agent2 -bind=192.0.2.6 -encrypt=f6HnfkLTGbIkFcAfCGZ4RQ==


where /var/vagrant = data directory, all files related to the consul gets persisted here
      /home/vagrant/dist = folder where the consul web UI is unzipped and kept i.e. UI directory
      demo = Cluster name
      consul-agent1, consul-agent2, consul-agent3 = name given to the various consul servers.       

      

where the following errors might come:
No Cluster leader despite the consul members showing all member lists
Solution: specific server as bootstrap i.e. -server -bootstrap as above.

consul monitor to be executed on Consul BootStrap Server to check for the logs, an laternative to making the og mode as DEBUG in
config file




