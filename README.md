# My specs
- S.O.: Windows11 V(23H2)
- MicroPrc: Ryzen5-1600-3.20GHz
- RAM: 16GB-3200MHz
- IDE: VSCode

# Pre-Requisites
- VirtualBox. V(7.0.18)
> Download: https://www.virtualbox.org/wiki/Downloads 

- Vagrant. V(2.4.1)
> Download: https://developer.hashicorp.com/vagrant/install?product_intent=vagrant

- Vagrant plugins.
> Run: `PS> vagrant plugin install vagrant-vbguest; vagrant plugin install vagrant-virtualbox_WSL2`

# Instructions

- Clone repo:

`PS> git clone https://github.com/xlmriosx/start-zero-awx.git`

- Enter to directory

`PS> cd start-zero-awx`

- Aprovision virtual server

`PS> vagrant up`

- Wait around 15 minutes

- Search in your browser

`http://localhost:8080`

# Inspect deploy

- Enter in server

`PS> vagrant ssh`

- Once inside run, to check if pod is running

`~$ kubectl get all -n awx`

# Extra

> If you lose the admin password can recover by enter in server and run: 
`~$ kubectl get secret awx-admin-password -o jsonpath="{.data.password}" --namespace awx | base64 --decode`
