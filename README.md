# Shuffle-SOAR

This is repository for my shuffle experiment

As we know, some open-source tools **need some configuration** even though they are maintained by the community.
Here are the shuffle SOAR configurations that I have tested.

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
Then we can access it on _https:(yourserverIP):3443_


## 1. Integration with Virustotal
My experience if we only follow guidance from the documentation, alert from Wazuh will never received by Webhook Shuffle.
- We need to check /var/ossec/logs/integrations.log

  Sign that your Wazuh configuration for Shuffle Integrations good is like this:
  - /tmp/shuffle-1758108926-301719090.alert  https://x.x.x.x:3443/api/v1/hooks/webhook_xxxx-xxxx-xxxx-xxxxxx
  - /tmp/shuffle-1758108926--1751902450.alert  https://x.x.x.x:3443/api/v1/hooks/webhook_xxxx-xxxx-xxxx-xxxxxx
  - /tmp/shuffle-1758108928--2010792349.alert  https://x.x.x.x:3443/api/v1/hooks/webhook_xxxx-xxxx-xxxx-xxxxxx

- We need to change **shuffle.py**, we can find that file on wazuh server (**/var/ossec/integrations**). We need to modify this :
  - Line 229
  
    > _res = requests.post(url, data=msg, headers=headers, timeout=10)_
  
    to
  
    > _res = requests.post(url, data=msg, headers=headers, timeout=10,**verify=False**)_

  - Line 230
 
    > debug('# Response received: %s' % res.json)

    to

    > debug('# Response received: %s' % res.text)
  
That's it! Webhook will receive alert from wazuh.
