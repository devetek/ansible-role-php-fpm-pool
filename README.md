Ansible role: PHP FPM Pool Configuration
=========

This role creates a PHP-FPM pool configuration.

Requirements
------------

This role creates PHP-FPM pool configurations. It depends on the PHP role to ensure PHP is installed and configured beforehand.

You can use the same Ansible roles listed below to maintain consistency across your setup.
* [geerlingguy.php]

Role Variables
--------------

List of variables in ansible-role-php-fpm-config:

```sh
---
# PHP-FPM pool default configuration.
phpfpm_pool_conf_path: "/etc/php-fpm.d/dpanel.conf"
phpfpm_pool_user: "www-data"
phpfpm_pool_group: "www-data"
phpfpm_listen: "127.0.0.1:9000"
phpfpm_listen_allowed_clients: "127.0.0.1"
phpfpm_pm_max_children: 50
phpfpm_pm_start_servers: 5
phpfpm_pm_min_spare_servers: 5
phpfpm_pm_max_spare_servers: 5
phpfpm_pm_max_requests: 0

# PHP-FPM pools configuration.
phpfpm_pools:
  - pool_name: dpanel
    pool_template: www.conf.j2
    pool_listen: "{{ phpfpm_listen }}"
    pool_listen_allowed_clients: "{{ phpfpm_listen_allowed_clients }}"
    pool_pm: dynamic
    pool_pm_max_children: "{{ phpfpm_pm_max_children }}"
    pool_pm_start_servers: "{{ phpfpm_pm_start_servers }}"
    pool_pm_min_spare_servers: "{{ phpfpm_pm_min_spare_servers }}"
    pool_pm_max_spare_servers: "{{ phpfpm_pm_max_spare_servers }}"
    pool_phpfpm_pm_max_requests: "{{ phpfpm_pm_max_requests }}"
```

Dependencies
------------

It depends on the `php_installer` Ansible role, which installs and configures PHP. Make sure the `php_installer` role is available and configured before using this role.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - devetek.php-fpm-pool
```

License
-------

GNU General Public License v3.0 or later

Author Information
------------------

[Nedya Prakasa]. Role created for [dPanel].

[dPanel]: https://cloud.terpusat.com/
[Nedya Prakasa]: https://github.com/prakasa1904
[devetek]: https://github.com/devetek
[geerlingguy.php]: https://galaxy.ansible.com/ui/standalone/roles/geerlingguy/php/