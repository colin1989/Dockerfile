# gitlab docker使用ssh访问失败问题

> fatal: Could not read from remote repository. 
> 
> Please make sure you have the correct access rights and the repository exists.

查看 `sshd` 日志文件 `logs\sshd\current` 


## 原因
> Permissions 0777 for '/etc/gitlab/ssh_host_xxxx_key' are too open. \
> It is required that your private key files are NOT accessible by others. \
> This private key will be ignored. \
> key_load_private: bad permissions \
> Could not load host key: /etc/gitlab/ssh_host_xxxx_key

# 解决办法

```
chmod 700 ssh_host_ecdsa_key # 权限设置为只有拥有者能访问，其他组员和其他用户不能访问
chmod 700 ssh_host_ed25519_key
chmod 700 ssh_host_rsa_key
```



## docker assets文件
将 `/assets/sshd_config` 文件中的 Port 22 改为 Port 30022 即可。