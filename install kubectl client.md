### Accessing kubernetes master /controller from client using kubectl
  1. install kubectl
      ```
      curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
      chmod +x ./kubectl
      sudo mv ./kubectl /usr/local/bin/kubectl
      kubectl version --client
      ```
  3. config kubectl\
     create config directory in local (client)
     ```
     mkdir -p $HOME/.kube
     ```
     copy config file from```master cluster``` but please make sure ```config``` file is there (master cluster)
     ```
     ls $HOME/.kube
     ```
     if config file is there then copy it to local(client)
     ```
     scp master@192.168.1.20:/home/master/.kube/config $HOME/.kube/
     ```
