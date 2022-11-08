## Method 1 – removing old key manually

1. On the source server, the old keys are stored in the file ~/.ssh/known_hosts.

2. Only if this event is legitimate, and only if it is precisely known why the SSH server presents a different key, then edit the file known_hosts and remove the no longer valid key entry. Each user in the client/source server has its own known_hosts in its home directory, just remove the entry in the file of a specific user for the destination server. For example:
– If root wants to ssh to the server, just removing entry in the /root/.ssh/known_hosts file is all right.
– If testuser wants to ssh to the server, then remove the entry in the file /home/testuser/.ssh/known_hosts.

3. In my case, I will remove the the key (highlighted in red) for the destination server 192.168.219.149 from the file /home/user01/.ssh/known_hosts.

```
# vim /home/user01/.ssh/known_hosts
172.104.9.113 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLrY91bQOihgFZQ2Ay9KiBG0rg51/YxJAK7dvAIopRaWzFEEis3fQJiYZNLzLgQtlz6pIe2tj9m/Za33W6WirN8=
192.168.219.148 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCrY/m16MdFt/Ym51Cc7kxZW3R2pcHV1jlOclv6sXix1UhMuPdtoboj+b7+NLlTcjfrUccL+1bkg8EblYucymeU=
192.168.219.149 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCrY/m16MdFt/Ym51Cc7kxZW3R2pcHV1jlOclv6sXix1UhMuPdtoboj+b7+NLlTcjfrUccL+1bkg8EblYucymeU=
```

## Method 2 – removing old key using the ssh-keygen command
```
ssh-keygen -R [hostname|IP address]
```

We shall use our IP address to delete the old key

```
$ ssh-keygen -R 192.168.219.149
# Host 192.168.219.149 found: line 3
/home/user01/.ssh/known_hosts updated.
Original contents retained as /home/user01/.ssh/known_hosts.old
```

## Verify
If the remote servers asks for a confirmation to add the new key to the ~/.ssh/known_host file, it confirms that you have successfully removed the old key. If you confirm the request, the source machine adds the new key into the ~/.ssh/known_host file.

```
$ ssh root@192.168.219.149
The authenticity of host '192.168.219.149 (192.168.219.149)' can't be established.
ECDSA key fingerprint is SHA256:V+iGp3gwSlnpbtYv4Niq6tcMMSZivSnYWQIaJnUvHb4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.219.149' (ECDSA) to the list of known hosts.
```

