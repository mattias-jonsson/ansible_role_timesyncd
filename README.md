Ansible Role: ansible_role_timesyncd
=========

Installs and configures timesyncd on the following Linux distributions:

<ul>
<li>Debian 11
<li>Ubuntu 18/20/22
</ul>

Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values where applicable (see `defaults/main.yml`):

| Variable | Required | Default | Comments |
| -------- | -------- | ------- | -------- |
| `ansible_role_timesyncd_connectionretrysec` | No | 30 | On supported distributions (currently Ubuntu 22) this specifies the minimum delay before subsequent attempts to contact a new NTP server are made. Default value is to 30 seconds and it must not be smaller than 1 second. |
| `ansible_role_timesyncd_fallback_time_server` | No | [] | A list of NTP server host names or IP addresses to be used as the fallback NTP servers. Any per-interface NTP servers obtained from systemd-networkd.service take precedence over this setting. |
| `ansible_role_timesyncd_pollintervalmaxsec` | No | 2048 | The maximum poll intervals for NTP messages. The default unit is seconds, default value is 2048 seconds and it must be larger than `ansible_role_timesyncd_pollintervalminsec`. |
| `ansible_role_timesyncd_pollintervalminsec` | No | 32 | The minimum poll intervals for NTP messages. The default unit is seconds, default value is 32 seconds and must not be smaller than 16 seconds. |
| `ansible_role_timesyncd_rootdistancemaxsec` | No | 5 | Maximum acceptable root distance, i.e. the maximum estimated time required for a packet to travel to the server we are connected to from the server with the reference clock. If the current server does not satisfy this limit, systemd-timesyncd will switch to a different server. |
| `ansible_role_timesyncd_time_servers` | Yes | [] | A list of NTP server host names or IP addresses. During runtime this list is combined with any per-interface NTP servers acquired from systemd-networkd.service. |


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers

      vars:
        ansible_role_timesyncd_connectionretrysec: 30
        ansible_role_timesyncd_fallback_time_servers:
          - ntp3.localdomain
          - ntp4.localdomain
        ansible_role_timesyncd_pollintervalmaxsec: 2048
        ansible_role_timesyncd_pollintervalminsec: 32
        ansible_role_timesyncd_rootdistancemaxsec: 5
        ansible_role_timesyncd_time_servers:
          - ntp1.localdomain
          - ntp1.localdomain

      roles:
         - role: ansible_role_timesyncd

License
-------

MIT

Author Information
------------------

Mattias Jonsson
