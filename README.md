# Shuffle-SOAR

This is repository for my shuffle experiment

## IMPORTANT NOTE
> As we know, some open-source tools **need some configuration** even though they are maintained by the community.
Here are the shuffle SOAR configurations that I have tested.


Outline this repo

Link to the helpful section: [Installation Shuffle](/Wazuh-Integration.md).


In this experiment the workflow look like this

<img width="953" height="367" alt="image" src="https://github.com/user-attachments/assets/a09de894-2ae4-474a-b17c-f27bc9c3e274" />

## Configuration 
Just follow official Shuffle documentation.
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



