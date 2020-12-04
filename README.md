# Suricata Zeek Sensor + ELK SIEM

## Prerequisites:

**Control Node**
- Ansible installed
- Sudo SSH Key access to Sensor & SIEM box
- Python3
 
**Sensor Node:**
- Ubuntu 18 Server
- User with SSH Key Access and Sudo
- 8 GB RAM +
- 4 CPU +
- 50-100 GB HD + (Suricata & Zeek logs)

**SIEM Node:** 
- Ubuntu 18 Server
- User with SSH Key Access and Sudo
- 8 GB RAM +
- 4 CPU +
- 500 GB + (Elasticsearch data)

## Setup Code for Ansible Playbook
Changes:
ansible.cfg (remote user & ssh private key)
inventory.yml (setup appropriate hosts, ips for sensor and siem)
roles/sensor_ids/vars
- home_dir (add your home dir or chosen directory)
- sniff_interface (interface that will sniff traffic)
- log_location (place to store zeek and suricata logs) 
- siem_ip (tell sensor where to send logs)

roles/siem_ids/vars
- home_dir (add your home dir or chosen directory)

## Install
**1. Install SIEM First:**
```bash
# Run in directory with inventory and cfg files
ansible-playbook install_siem.yml --ask-become-pass
# Grab a coffee, this will take a hot minute
```
- Verify that the system is installed and running properly 
- Go to http://yoursiemip:5601 to see Kibana

**2. Install Sensor Second:**
```bash
# Run in directory with inventory and cfg files
ansible-playbook install_sensor.yml --ask-become-pass
# Grab more coffee...
```
- Ensure the Suricata and Zeek (filebeat) logs are populating Elasticsearch
- Import Synlite Suricata Dashboards

### References 
https://github.com/robcowart/synesis_lite_suricata
https://github.com/zeek/zeek