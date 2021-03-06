[![CI](https://travis-ci.org/j-carpentier/ansible-haproxy-role.svg?branch=master)](https://travis-ci.org/github/j-carpentier/ansible-haproxy-role)

ansible-haproxy-role
=========

HAProxy single loadbalancer server ansible role for Centos 7

Requirements
------------

This role was developed and tested using Ansible 2.9  
Backward compatibility is currently not tested and guaranteed

Default variables values
------------------------
```
# Rsyslog log facility for HAproxy
haproxy_syslog_facility: local2

# HAProxy supports http/tcp"
haproxy_mode: http

# HAProxy stats port
haproxy_stats_port: 3000

# HAProxy stats auth username
haproxy_stats_user: admin

# HAProxy stats auth password
haproxy_stats_password: r00tme

# Port on which HAProxy should listen
haproxy_listenport: 8080

# HAProxy default backend
haproxy_default_backend: production
```

Example Playbook
----------------
```
- hosts: loadbalancer
  gather_facts: True
  become: yes
  roles:
    - role: haproxy

  vars:
    haproxy:
      backends:
        - name: production
          balance: roundrobin
          servers:
            - name: web1
              address: 10.0.0.101
              port: 80
            - name: web2
              address: 10.0.0.102
              port: 80
```

Manual testing (Vagrant)
------------------------

- Create vagrant CentOS 7 virtual machines using Vagrantfile (1 haproxy and 2 nginx)  
<em>bento box default username/password is "vagrant"</em> (https://app.vagrantup.com/bento)
```
vagrant up
```

- Deploy nginx webservers  
<em>Provided example playbook require geerlingguy.nginx role available with ansible-galaxy</em>  
```
ansible-galaxy install geerlingguy.nginx
ansible-playbook -i inventory playbook/deploy-nginx.yml -u vagrant -kK
```

- Deploy HAProxy server
```
ansible-playbook -i inventory playbook/deploy-haproxy.yml -u vagrant -kK
```

Loadbalancer: http://10.0.0.200:8080/  
Admin stats: http://10.0.0.200:3000/haproxy


License
-------

MIT


License
-------

Julien Carpentier
