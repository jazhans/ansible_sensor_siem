
![zeek](https://camo.githubusercontent.com/d8fc1510d644d4544c55e9b108372d86ea92d3e416e067e73dc62fec40678240/68747470733a2f2f7a65656b2e6f72672f77702d636f6e74656e742f75706c6f6164732f323032302f30342f7a65656b2d6c6f676f2d776974686f75742d746578742e706e67)![suricata](https://chocolatey.org/content/packageimages/suricata.2.0.2.20140625.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![arrow](https://cdn.iconscout.com/icon/free/png-256/right-arrow-439-1161082.png)![elk](https://raw.githubusercontent.com/blacktop/docker-elastic-stack/master/docs/img/el_stack_logo.png)
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