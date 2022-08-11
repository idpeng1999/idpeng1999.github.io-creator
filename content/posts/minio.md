---
title: "Minio"
date: 2022-06-17T14:57:43+08:00
draft: false
categories: [工具教程]
---
## docker搭建minio单节点

1. 拉取docker镜像
```text
docker pull minio/minio
```

2. 创建挂载文件夹
```text
mkdir -p /root/minio/config /root/minio/data
```

3. 启动容器

```text
docker run -p 9000:9000 -p 1314:9001 --name minio --restart=always 
-e "MINIO_ACCESS_KEY=xxxxxx" -e "MINIO_SECRET_KEY=xxxxxxxx" 
-v /root/minio/data:/data -v /root/minio/config:/root/.minio 
-d minio/minio server /data --console-address ":9001"
```

注意：
* MINIO_ACCESS_KEY（用户名）
* MINIO_SECRET_KEY（密码，最少8位） 
* 它需要两个端口，9000为客户端连接端口，1314为Web管理端口


密码不安全报错
```text
ERROR Unable to validate credentials inherited from the shell environment: Invalid credentials
> Please provide correct credentials
HINT:
Access key length should be at least 3, and secret key length at least 8 characters
```

