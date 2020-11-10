elastic-beats-modules
=========

Module for configuring elasticsearch beats modules

Requirements
------------

The targeted beat must already be installed and the following and `filebeat.config.modules.path` must be set e.g.,:

```yaml
filebeat.config.modules.path: ${path.config}/modules.d/*.yml
```

Role Variables
--------------


| Variable name                     | Type       | Default                                            | Description                                   |
| --------------------------------- | ---------- | -------------------------------------------------- | --------------------------------------------- |
| elastic_beats_modules_beat        | string     | filebeat                                           | The beats type to configure the modules for\* |
| elastic_beats_modules_executable  | path       | /usr/bin/"{{ elastic_beats_modules_beat }}"        | The beats executable to use                   |
| elastic_beats_modules             | list[dict] | []                                                 | The modules to enable/disable                 |
| elastic_beats_modules_tmp         | path       | /tmp/                                              | Dir to save package file to                   |
| elastic_beats_modules_destination | path       | /usr/share/{{ elastic_beats_modules_beat }}/module | Module install dir                            |
| elastic_beats_modules_config_dir  | path       | /etc/{{ elastic_beats_modules_beat }}/modules.d    | Module config dir                             |
| &nbsp;&nbsp;&nbsp;&nbsp;∟.module  | string     |                                                    | The name of the module                        |
| &nbsp;&nbsp;&nbsp;&nbsp;∟.enabled | bool       | true                                               | If the module should enabled or not           |
| &nbsp;&nbsp;&nbsp;&nbsp;∟.url     | uri        |                                                    | Source URL to install from a remote source    |
| &nbsp;&nbsp;&nbsp;&nbsp;∟.package | filename   |                                                    | Source package archive name                   |
| &nbsp;&nbsp;&nbsp;&nbsp;∟.config  | dict       |                                                    | Custom module config\*\*                      |


*\*Note that not all beats support modules via module directory.*
*\*\*Note that this must be set for remotely installed modules*

### elastic_beats_modules

Example Playbook
----------------

```yaml
    - hosts: servers
      roles: 
         - role: elastic-beats-modules
           vars:
            elastic_beats_modules_beat: "filebeat"
            elastic_beats_modules:
              - module: system
              - module: suricata
                enabled: false
```
License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
