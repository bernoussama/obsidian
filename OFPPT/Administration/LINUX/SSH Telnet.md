- SSH config file
`/etc/ssh/sshd_config`

```
PermitRootLogin prohibit-password
AllowUsers samir latifa
PermitEmptyPasswords no
MaxAuthTries 3
PasswordAuthentication yes
MaxSessions 10
Banner /etc/banner
AllowGroups profs
```

