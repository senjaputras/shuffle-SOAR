# Shuffle-SOAR

This is repository for my shuffle experiment

## IMPORTANT NOTE
> As we know, some open-source tools **need some configuration** even though they are maintained by the community.
Here are the shuffle SOAR configurations that I have tested.


Another Resouce on this repo

If you can skip installation Shuffle and have trouble with some integration, just go through this section:
- [Wazuh Shuffle Integration](/Shuffle-Wazuh.md).


In this experiment the workflow look like this

<img width="953" height="367" alt="image" src="https://github.com/user-attachments/assets/a09de894-2ae4-474a-b17c-f27bc9c3e274" />





## Shuffle Installation / Configuration 

### Requirement : Docker and Docker compose installed
- do this to install Docker 

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl start docker
```
- do this to install Docker Compose

```
curl -SL https://github.com/docker/compose/releases/download/v2.39.3/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

If the command docker-compose fails after installation, check your path. You can also create a symbolic link to /usr/bin or any other directory in your path. For example:
```sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose```

- do this to instal Shuffle
```
git clone https://github.com/Shuffle/Shuffle
cd Shuffle
mkdir shuffle-database                    # Create a database folder
sudo chown -R 1000:1000 shuffle-database  # IF you get an error using 'chown', add the user first with 'sudo useradd opensearch'
sudo swapoff -a                           # Disable swap
sudo sysctl -w vm.max_map_count=262144             # https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html
docker-compose up -d
```
Then we can access it on **https://(yourserverIP):3443**



