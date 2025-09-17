# Shuffle-SOAR

This is repository for my shuffle experiment

As we know, some open-source tools need some configuration even though they are maintained by the community.
Here are the shuffle SOAR configurations that I have tested.


## 1. Integration with Virustotal
My experience if we only follow guidance from the documentation, alert from Wazuh will never received by Webhook Shuffle.
- We need to check /var/ossec/logs/integrations.log
  - /tmp/shuffle-1758108926-301719090.alert  https://x.x.x.x:3443/api/v1/hooks/webhook_xxxx-xxxx-xxxx-xxxxxx
  - /tmp/shuffle-1758108926--1751902450.alert  https://x.x.x.x:3443/api/v1/hooks/webhook_xxxx-xxxx-xxxx-xxxxxx
  - /tmp/shuffle-1758108928--2010792349.alert  https://x.x.x.x:3443/api/v1/hooks/webhook_xxxx-xxxx-xxxx-xxxxxx

- We need to change **shuffle.py**, we can find that file on wazuh server (**/var/ossec/integrations**)
