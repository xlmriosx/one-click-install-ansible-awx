# Pre-Requisites
- Virtual Box
- 4 CPUs -- 8 Gb RAM
- Vagrant downloaded
- Run: `PS> vagrant plugin install vagrant-vbguest; vagrant plugin install vagrant-virtualbox_WSL2`

# Start

- Clone repo:

`PS> git clone https://github.com/xlmriosx/jenkins-setup-kubernetes`

- Enter to directory

`PS> cd jenkins-setup-kubernetes`

- Aprovision virtual server

`PS> vagrant up`

- Wait around 15 minutes

- Search in your browser and look if jenkins is running

`localhost:8080`

- To enter in the platform need connect to your virtual server

`PS> vagrant ssh`

- Once inside run, to check if pod is running

`$ kubectl get all -n jenkins`

- Search in the logs of pod the password

`$ kubectl logs -n jenkins pod/<pod_id> | grep -A 3 password` E.g. 9bddff1cb32a4dc3a3b2a6b997be2bbc

- Set that password in screen of jenkins and start installation
