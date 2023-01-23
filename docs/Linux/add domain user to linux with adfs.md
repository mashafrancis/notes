### Giving access to users with adfs

```
vim /etc/sssd/sssd.conf
```

Add the name to the following line
```
simple_allow_users = fmasha, newusername
```

```
systemctl restart sssd
```

Give sudo rights

```
vim /etc/sudoers.d/ad_server_admins
```

Add the following line
```
newusername@domain.net      ALL=(root)      ALL
```
