---
title: Bash Variables
weight: 210
menu:
  notes:
    name: Variables
    identifier: notes-bash-variables
    parent: notes-bash
    weight: 10
---

<!-- Variable -->
{{< note title="Variable" >}}

```bash
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}
```

{{< /note >}}

<!-- Condition -->
{{< note title="Condition" >}}

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

{{< /note >}}

<!-- Install Qemu -->
{{< note title="Install Qemu" >}}

```bash
#!/bin/bash
  echo -e "\n----------------------------------- update packages\n"
  sudo apt update -y && sudo apt upgrade -y
  sleep 5
  echo -e "\n----------------------------------- update timezone\n"
  sudo timedatectl set-timezone Asia/Manila
  date
  sleep 3
  echo -e "\n----------------------------------- install qemu agent\n"
  sudo apt install qemu-guest-agent -y
  sleep 2
  sudo systemctl enable qemu-guest-agent
  sleep 2
  sudo systemctl restart qemu-guest-agent
  sleep 2
  sudo systemctl status qemu-guest-agent
  echo -e "\n----------------------------------- done\n"
```

{{< /note >}}

<!-- Install Docker -->
{{< note title="Install Docker" >}}

```bash
#!/bin/bash

  echo -e "\n----------------------------------- install docker dependencies\n"
  sudo apt install apt-transport-https ca-certificates curl software-properties-common -y 
  sleep 5
  echo -e "\n----------------------------------- add GPG Key\n"
  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sleep 5
  echo -e "\n----------------------------------- add docker repository\n"
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  sleep 5
  echo -e "\n----------------------------------- install docker-ce\n"
  sudo apt install docker-ce -y
  sudo systemctl restart docker
  sudo systemctl enable docker
  sleep 3
  sudo systemctl status docker
  sleep 3
  echo -e "\n----------------------------------- add user to docker group\n"
  sudo usermod -aG docker ${USER}
  sleep 3
  echo -e "\n----------------------------------- done\n"
```

{{< /note >}}

<!-- Install Portainer -->
{{< note title="Install Portainer" >}}

```bash
docker run -d \
   -p 8000:8000 \
   -p 9443:9443 \
   --name do-portainer \
   --restart=always \
   -v /var/run/docker.sock:/var/run/docker.sock \
   -v /opt/docker-data/portainer/data:/data \
   portainer/portainer-ce:latest
```

{{< /note >}}

<!-- Install Portainer Agent -->
{{< note title="Install Portainer Agent" >}}

```bash
docker run -d \
  -p 9001:9001 \
  --name do-portainer-agent \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /opt/docker-data/portainer-agent/volumes:/var/lib/docker/volumes \
  portainer/agent:2.19.5
```

{{< /note >}}