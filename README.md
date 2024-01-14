SAMBA install and configure
=========

This role installs and configures SAMBA for my server.

Role Variables
--------------

The ```role_smb_password``` has to be set to the smb password used for the login.

The shares should be set using the ```role_smb_shares``` variable which is a list of dictionaries in the format shown in the example.

The main folder location for the SAMBA shares can be set using the ```role_share_dir``` variable.

The user (name, uid, and gid) for SAMBA can be configured using the ```role_username```, ```role_useruid```, and ```role_usergid```.

Example Playbook
----------------

```yaml
    - hosts: all
      vars:
        smb_password: password123
        smb_shares:
          - name: file_share
            comment: private file share
            path: /share/file-share
            writable: "yes"
            browsable: "yes"
            inherit_permissions: "yes"
            force_user: user
            force_group: user

      roles:
         - { role: samba_confgure, role_smb_password: "{{ smb_password }}", role_smb_shares: "{{ smb_shares }}" }
         - { role: samba_confgure, role_smb_password: "{{ smb_password }}", role_smb_shares: "{{ smb_shares }}", 
             role_share_dir: /share, role_username: sambauser, role_useruid: 1000, role_usergid: 1000 }
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
