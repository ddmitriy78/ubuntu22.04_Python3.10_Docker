### Ubuntu 22.04 Server with Python 3.10 and Docker

You can also use this file in the user data to automatically install and configure the server. 

    #!/bin/bash
    sudo apt update && sudo apt upgrade -y
    sudo apt install software-properties-common -y
    sudo add-apt-repository ppa:deadsnakes/ppa -y
    sudo apt update -y
    sudo apt install python3.10 -y
    sudo apt install python3-pip -y
    sudo apt  install awscli -y
    sudo apt-get remove docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
    sudo apt-get install -y \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    sudo mkdir -p /etc/apt/keyrings
    sudo rm -f /etc/apt/keyrings/docker.gpg
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update -y
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
    sudo systemctl restart docker
    sudo usermod -aG docker $USER
    sudo apt-get install docker-compose -y

Run this command to ensure your user has appropriate access to execute docker commands.

    newgrp docker

Additional Commands to troubleshoot your installation

    #sudo service docker start
    #sudo chown root:docker /var/run/docker.sock