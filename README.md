# install_logrotate


### Variables

| Variabel                   | Type   | Value                                                                                   | Comment                                                                                              |
| -------------------------- | ------ | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| logrotate_frequency        | string | weekly                                                                                  | heufigkeit der Rotation der Log Files.                                                               |
| logrotate_keep             | int    | 4                                                                                       | Anzahl der Files die behalten werden soll                                                            |
| logrotate_compress         | bool   | yes                                                                                     | Sollen Rotierte Files kompremiert werden.                                                            |
| logrotate_dateext          | bool   | no                                                                                      | Aktiviert Date Exetension für Log Filenamen.                                                         |
| logrotate_user             | string | "{{ _logrotate_user[ansible_distribution] \| default(_logrotate_user['default'] ) }}"   | Nutzer der Verwendet werden soll um die Files zu rotieren.                                           |
| logrotate_group            | string | "{{ _logrotate_group[ansible_distribution] \| default(_logrotate_group['default'] ) }}" | Gruppe des Users der verwendet werden soll um Files zu rotieren.                                     |
| _logrotate_user            | dict   | default: root                                                                           | Default User für Logrotate.                                                                          |
| _logrotate_group:          | dict   | ```default: root```                                                                     | Default User Gruppe für Logrotate User.                                                              |
| logrotate_conf_dir         | string | "/etc/logrotate.d/"                                                                     | Pfad in dem Logroate Config Files angelegt werden sollen.                                            |
| logrotate_default_template | string | logd.j2                                                                                 | Default Template was von Ansible genutzt werden soll um Logrotate Konfigurationsdateien zu erstellen |
| logrotate_conf             | dict   | {}                                                                                      | Dict was die einzelen Logrotate Konfigurationsdateien als Dictionaries beinhaltet.                   |

Beispiel für die Variable `logrotate_conf`:

```
logrotate_conf:
    btmp:
      - path: /var/log/btmp
        missingok: yes
        frequency: monthly
        create: yes
        create_mode: "0660"
        create_user: root
        create_group: utmp
        dateext: yes
        dateformat: "-%Y-%m-%d"
        keep: 1
```
