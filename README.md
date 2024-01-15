SAMBA install and configure
=========

This role installs and configures SAMBA for my server.

Role Variables
--------------

The ```samba_password``` has to be set to the smb password used for the login.

The shares should be set using the ```samba_shares``` variable which is a list of dictionaries in the format shown in the example.

The main folder location for the SAMBA shares can be set using the ```samba_share_dir``` variable.

The user (name, uid, and gid) for SAMBA can be configured using the ```samba_username```, ```samba_useruid```, and ```samba_usergid```.

Example Playbook
----------------

```yaml
    - hosts: all
      vars:
        samba_shares:
          - name: file_share
            comment: private file share
            path: /share/file-share
            writable: "yes"
            browsable: "yes"
            inherit_permissions: "yes"
            force_user: sambauser
            force_group: sambauser

      roles:
         - { role: tychobrouwer.samba, samba_password: "password123", samba_username: sambauser }
         - { role: tychobrouwer.samba, samba_password: "password123", samba_username: sambauser,
             samba_useruid: 1000, samba_usergid: 1000 }
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
