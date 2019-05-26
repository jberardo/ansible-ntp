# NTP Ansible Role

Installs NTP on Ubuntu.

Two main tasks are:
- Creation of personal user with ssh key, etc
- Tries to remove apt lock files so other roles can use apt and not run into errors

## Requirements

None.

## Variables

See `defaults/main.yml`.

`ntp_enabled`: Enable or disable role

`ntp_manage_config`: Enable or disable copying the template file (insisde `templates`) to the server

`ntp_timezone`: Server timezone (type `timedatectl list-timezones` to see all time zones)

NTP server area configuration
`ntp_servers`: NTP servers to use (http://support.ntp.org/bin/view/Servers/NTPPoolServers)

`ntp_restrict`: List of hosts to restrict NTP access.

## Example

```yml
- hosts: host1
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - ntp
```

Variables example:

```yml
ntp_enabled: true
ntp_manage_config: yes
ntp_timezone: America/New_York

ntp_servers:
  - "0.us.pool.ntp.org iburst"
  - "1.us.pool.ntp.org iburst"
  - "2.us.pool.ntp.org iburst"
  - "3.us.pool.ntp.org iburst"

ntp_restrict:
  - "127.0.0.1"
  - "::1"
```