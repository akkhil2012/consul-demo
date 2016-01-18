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
unzip 0.6.2_linux_amd64.zip
rm -f 0.6.2_linux_amd64.zip
mv consul /usr/bin/

Bootstrap / Web UI Server
wget https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip
unzip 0.6.2_web_ui.zip
rm -f 0.6.2_web_ui.zip
cd /root/consul_demo

Add Consul to the PATH to all servers:
>> mv consul /usr/bin/
export PATH=$PATH:/consul


>> consul keygen

To generate the encrypted key:
Eg, Key:  lcLuo15MxnC4PpMPwuTkwQ==( ensure key doen’t contain /)
To be used to run command from all three servers



