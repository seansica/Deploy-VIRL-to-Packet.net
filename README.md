## Overview
Packet.net is a bare metal cloud host that is capable of hosting Cisco VIRL servers. They provide an excellent option to create Cisco VIRl labs if you don't have access to the necessary hardware.
## Purpose
This project was created to simplify the creation and deletion of VIRL servers in the Packet Cloud. It leverages the **packet_device** Ansible module that handles variables as defined by Packet's API: https://www.packet.com/developers/api/. You can also read more informatio about the Packet module here: https://docs.ansible.com/ansible/latest/scenario_guides/guide_packet.html.

---

## Prerequisites
1. Install the Ansible package for Packet: `pip install packet-python`

2. Create an API key in your Packet account via the Packet Portal (https://app.packet.net).  

3. Export the key to a system variable on the Ansible host executing this code: `$ export PACKET_API_TOKEN=Bfse9F24SFtfs423Gsd3ifGsd43sSdfs`

4. Acquire your Project ID where you want the server to be installed via the Packet Portal (https://app.packet.net).

5. Acquire your VIRL license file. You'll need to extra multiple pieces of information from it.

6. Create two files per the following templates:
   - roles/createServer/vars/main.yml
   - roles/deleteServer/vars/main.yml

7. The templates contain sensitive information relating to your specific Packet.net account and VIRL license. It is highly recommended that you encrypt both of these files using ansible-vault: `ansible-vault encrypt path-to-main\main.yml`

### Template: roles/createServer/vars/main.yml
    vault_projectid: 00000000-0000-0000-0000-000000000000

    vault_licensefile: some-license-prefix.virl.info.pem

    vault_licensepem: |
                      -----BEGIN RSA PRIVATE KEY-----

                      PEM_RUBBISH_HERE

                      -----END RSA PRIVATE KEY-----

### Template: roles/deleteServer/vars/main.yml
    vault_projectid: 00000000-0000-0000-0000-000000000000

---

## Execution Steps
1. To create your VIRL server:
   `ansible-playbook --ask-vault-pass createServer.yml`
2. To create your VIRL server:
   `ansible-playbook --ask-vault-pass deleteServer.yml`
---
