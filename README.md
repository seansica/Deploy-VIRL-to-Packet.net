## Purpose
Packet.net is a bare metal cloud host that is capable of hosting Cisco VIRL servers. They provide an excellent option to create Cisco VIRl labs if you don't have access to the necessary hardware.

This project was created to simplify the creation and deletion of VIRL servers in the Packet Cloud.
---
## Prerequisites
1. You'll need to create an API key in your Packet.net account, then export that key to a system variable on the Ansible host executing this code.

2. You'll need to create two files which contain sensitive information relating to your specific Packet.net account and VIRL license:
   - roles/createServer/vars/main.yml
   - roles/deleteServer/vars/main.yml
---
## Template: roles/createServer/vars/main.yml
'''
vault_projectid: 00000000-0000-0000-0000-000000000000

vault_licensefile: some-license-prefix.virl.info.pem

vault_licensepem: |
              -----BEGIN RSA PRIVATE KEY-----

              PEM_FILE_CONTENTS_HERE

              -----END RSA PRIVATE KEY-----
---
## Template: roles/deleteServer/vars/main.yml
vault_projectid: 00000000-0000-0000-0000-000000000000


---
## Execution Steps
1. To create your VIRL server
   ansible-playbook --ask-vault-pass createServer.yml
2. To create your VIRL server
   ansible-playbook --ask-vault-pass deleteServer.yml


---
