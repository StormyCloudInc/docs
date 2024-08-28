---
hidden: true
---

# 2FA

sshd

```
Include /etc/ssh/sshd_config.d/*.conf
UsePAM yes
X11Forwarding yes
PrintMotd no
AcceptEnv LANG LC_*
Subsystem       sftp    /usr/lib/openssh/sftp-server
ChallengeResponseAuthentication yes
PasswordAuthentication no
```

**`/etc/pam.d/sshd`**

```
auth required pam_google_authenticator.so
account required pam_nologin.so
@include common-account
session [success=ok ignore=ignore module_unknown=ignore default=bad] pam_selinux.so close
session required pam_loginuid.so
session optional pam_keyinit.so force revoke
@include common-session
session optional pam_motd.so motd=/run/motd.dynamic
session optional pam_motd.so noupdate
session optional pam_mail.so standard noenv # [1]
session required pam_limits.so
session required pam_env.so # [1]
session required pam_env.so user_readenv=1 envfile=/etc/default/locale
session [success=ok ignore=ignore module_unknown=ignore default=bad] pam_selinux.so open
```

1.  **Locate the Google Authenticator File**

    &#x20;

    On the original server where 2FA is set up, find the file:

    bashCopy

    ```
    ls ~/.google_authenticator
    ```
2.  **Copy the File to Other Servers**

    &#x20;

    Use `scp` to securely copy the file to another server:

    bashCopy

    ```
    scp ~/.google_authenticator user@new_server_ip:~/
    ```
3.  **Set Correct Permissions**

    &#x20;

    On the new server, ensure the file has the correct permissions:

    bashCopy

    ```
    chmod 600 ~/.google_authenticator
    ```
