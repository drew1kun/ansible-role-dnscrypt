Ansible role: pihole
=========

[![MIT licensed][mit-badge]][mit-link]
[![Galaxy Role][role-badge]][galaxy-link]

Ansible role which installs and configures [DNSCrypt-proxy2][dnscrypt-proxy2-link].

The role achieves the following:
 - Installs dnscrypt-proxy 2
 - Configures dnscrypt-proxy to be run as unprivileged user [ for security purposes ]
 - If distro uses systemd init: configures systemd socket activated dnscrypt-proxy.service
 - If distro does not use systemd: configures built in dnscrypt-proxy service

Requirements
------------

NOTE: Role requires Fact Gathering by ansible!

One of the following distros (or derivatives) required:
 - Debian | Raspbian | [Minibian][minibian-link]
    - jessie
    - stretch

Role Variables
--------------

| Variable | Description | Default |
|----------|-------------|---------|
| **dnscrypt_arch** | System architecture. See [available architectures][dnscrypt-arch-link]. Check [`defaults/main.yml`](defaults/main.yml) | `linux-arm64` |
| **dnscrypt_on_pihole** | Is it dnscrypt on [pihole][pihole-link] installation? If `yes` then it will modify pihole config | `no` |
| **dnscrypt_force_upgrade** | Force reinstall `dnscrypt-proxy2` even if it's already installed | `no` |
| **dnscrypt_proxy2_link** | url of the latest `dnscrypt-proxy2` version. Must be updated manually | `https://github.com/jedisct1/dnscrypt-proxy/releases/download/2.0.8/dnscrypt-proxy-linux_arm-2.0.8.tar.gz` |
| **dnscrypt_bin** | Where to put dnscrypt-proxy binary | `/usr/local/bin/dnscrypt-proxy` |
| **dnscrypt_config** | Where to store dnscrypt config | `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` |
| **dnscrypt_socket_only** | Use ONLY socket activation of dnscrypt-proxy.service | `yes` |

### Config-related vars

| Variable | Description | Default |
|----------|-------------|---------|
| **dnscrypt_ipv4_address** | IPv4 address for `dnscrypt-proxy` to listen on | `127.0.0.1` |
| **dnscrypt_port** | Port for `dnscrypt-proxy` to listen on | `41` |
| **dnscrypt_ipv4_servers** | Use servers reachable over IPv4 | `'true'` |
| **dnscrypt_ipv6_servers** | Use servers reachable over IPv6. Do not enable if you don't have IPv6 set | `'false'` |
| **dnscrypt_dc_servers** | Use servers implementing the DNSCrypt protocol | `'true'` |
| **dnscrypt_doh_servers** | Use servers implementing the DNS-over-HTTPS protocol | `'true'` |
| **dnscrypt_require_dnssec** | Server must use DNSSEC validation | `'true'` |
| **dnscrypt_require_nolog** | Server must not log user queries (declarative) | `'true'` |
| **dnscrypt_require_nofilter** | Server must NOT enforce its own blacklist (for parental control, ads blocking) | `'true'` |
| **dnscrypt_force_tcp** | Always use TCP to connect to upstream servers. Useful for TOR. | `'false'` |
| **dnscrypt_fallback_resolver** | non-encrypted fallback resolver. Only used if DNS config doesn't work. `114.114.114.114:53` for people in China | `9.9.9.9:5` |

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: raspberrypi
      gather_facts: yes
      roles: drew-kun.dnscrypt

License
-------

[MIT][mit-link]

Author Information
------------------

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[role-badge]: https://img.shields.io/badge/role-drew--kun.dnscrypt-green.svg
[galaxy-link]: https://galaxy.ansible.com/drew-kun/dnscrypt/
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew-kun/ansible-dnscrypt/master/LICENSE
[minibian-link]: https://minibianpi.wordpress.com/
[pihole-link]: https://pi-hole.net/
[dnscrypt-proxy2-link]: https://github.com/jedisct1/dnscrypt-proxy
[dnscrypt-arch-link]: https://github.com/jedisct1/dnscrypt-proxy/releases/latest

