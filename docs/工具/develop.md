# 开发相关工具

## 设置git ssh代理
设置 `~/.ssh/config`
```text
Host github.com
Hostname ssh.github.com
Port 443
ProxyCommand ncat --proxy ${proxy_host}:${proxy_port} --proxy-type socks5 %h %p
```