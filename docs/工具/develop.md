# 开发相关工具

## 设置git ssh代理
设置 `~/.ssh/config`
```text
Host github.com
Hostname ssh.github.com
Port 443
ProxyCommand ncat --proxy ${proxy_host}:${proxy_port} --proxy-type socks5 %h %p
```

## ssh远程执行
例如本网页就是通过如下脚本发布的
```shell
#!/bin/sh

SECRET=''
SERVER_HOST=''
SERVER_USER=''
CUR_DIR=$(pwd)
BLOG_PROJECT_DIR=""
REMOTE_DIR=""

npm run build


cd ${BLOG_PROJECT_DIR}
npm run build

sshpass -p "${SECRET}" ssh -t ${SERVER_USER}@${SERVER_HOST} "rm -rf ${REMOTE_DIR}/*"
sshpass -p "${SECRET}" scp -r ${BLOG_PROJECT_DIR}/build/* ${SERVER_USER}@${SERVER_HOST}:${REMOTE_DIR}/

echo "update blog success..."

cd ${CUR_DIR}
```