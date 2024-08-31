Vagrant.configure("2") do |config|
    config.vm.provider "virtualbox"
    config.vm.box = "alvistack/ubuntu-23.10"
    config.vm.hostname = "awx"

    config.vm.define "vm" do |vm|
        vm.vm.network "private_network", ip: "10.0.0.100"
        vm.vm.network "forwarded_port", guest: 30000, host: 8080
    end

    # Configurating keys to enter server
    config.vm.provision "file", source: "~/.ssh", destination: "/home/vagrant/.ssh"
    config.vm.provision "shell", inline: "chmod 700 -R /home/vagrant/.ssh"
    
    # Mount repo to development
    config.vm.synced_folder ".", "/home/vagrant/workdir"

    # Installing Ansible, Molecule
    config.vm.provision "shell", inline: <<-SHELL
        HOME=/home/vagrant
        sudo usermod -aG sudo vagrant
        sudo chmod -R g+rwx /var
        # Actualiza todos los paquetes
        apt upgrade -y && apt update -y
        curl -sfL https://get.k3s.io | sh -
        kubectl get all
        export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
        sudo chmod +r /etc/rancher/k3s/k3s.yaml
        
        # Install kustomize
        curl -s "https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh"  | bash
        sudo mv kustomize /usr/local/bin/
        
        # Install awx
            # Apply kustomize to install operator
            cd $HOME/workdir && kustomize build . | kubectl apply -f - 
            # Sleep 120 seconds
            echo -e "\033[33mWaiting for operator is ready...\033[0m"
            sleep 120

            # Apply k to deploy components awx
            kubectl apply -f awx.yaml
                # Sleep 45 seconds
            echo -e "\033[33mWaiting for web is ready...\033[0m"
            sleep 120

        # Show creds to access platform
        PASS=$(kubectl get secret awx-admin-password -o jsonpath="{.data.password}" --namespace awx | base64 --decode)
        echo -e "\033[32mAccess to http://localhost:8080 with \nusername: admin \npassword: $PASS\033[0m"
    SHELL
end