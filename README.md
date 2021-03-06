# Installation

## Agent setup

### Docker

**WIP**

1. sudo

This template requires `sudo` to be available inside the zabbix-agent container.

You can bind-mount the supplied sudoers config with `-v ./sudoers/zabbix-docker:/etc/sudoers.d/zabbix:ro`.

Bear in mind that this file should be owned by root and its permissions set to `0600`.

2. You obviously also need to make the script available as well: `-v ./zbx-reboot-required.sh:/usr/local/bin/zbx-reboot-required.sh`

3. Don't forget the config: `-v ./zabbix_agentd.conf.d/reboot-required.docker.conf:/etc/zabbix/zabbix_agentd.d/reboot-required.conf:ro`

4. To be able to chroot inside the host you need mount the rootfs like so: `-v /:/rootfs:ro`.

### OpenWRT

1. You need to install `sudo`:

```
opkg update && opkg install sudo
```

2. Copy `sudoers.d/zabbix-openwrt` to `/etc/sudoers.d/zabbix-reboot-required`

3. Copy `zbx-reboot-required.sh` to `/etc/zabbix_zabbix_agentd.d/bin/zbx-reboot-required.sh`

4. Copy `zabbix_agentd.conf.d/reboot-required.openwrt.conf` to `/etc/zabbix_zabbix_agentd.d/zbx-reboot-required.conf`

5. Restart the agent: `/etc/init.d/zabbix_agentd restart`

## Zabbix Server setup

1. Import the template `zabbix_template_reboot_required.xml`

2. Apply it to your hosts
