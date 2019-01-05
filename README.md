bvansomeren.haproxy
=================

Installs HAProxy from ports and configures frontends and backends as required.
Sets up its own self signed cert to bootstrap the proxy https.
Recommended to use the haproxy\_cert\_folder and place certificates through other means

Requirements
------------

FreeBSD 11.2+

Role Variables
--------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
- hosts: lbs
  become: True
  vars:
    letsencrypt_host: "10.0.0.1"
  handlers:
    - name: Reload syslog
      service:
        name: syslogd
        state: reloaded
  roles:
  - role: bvansomeren.pf
    pf_skip:
    - vtnet1
    - vtnet2
    pf_tcp_pass_in:
    - 80
    - 443
  - role: bvansomeren.haproxy
    sites:
    - name: site-prd
      domains:
      - site.example.nl
      servers:
      - id: application00
        hostname: 10.0.1.1
      - id: application01
        hostname: 10.0.1.2
    - name: site-acc
      domains:
      - site-acc.example.nl
      servers:
      - id: accept00
        hostname: 10.0.0.1

```


License
-------

BSD

Author Information
------------------

Just reach out via Github
