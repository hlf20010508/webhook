# webhook
A webhook server written in rust.

- 通过邮件接收通知
- 通过[PushDeer](https://github.com/easychen/pushdeer)接收通知

**不需要使用的功能无需填写对应的配置参数**

## 接口
### email
- `/get/email`, 参数
    - `title`: 主题
    - `body`: 正文
- `/post/json/email`, 接收`json`格式数据，参数
    - `title`: 主题
    - `body`: 正文
- `/post/form/email`, 接收`form`格式数据，参数
    - `title`: 主题
    - `body`: 正文

### push
- `/get/push`, 参数
    - `title`: 主题
    - `body`: 正文（选填）
- `/post/json/push`, 接收`json`格式数据，参数
    - `title`: 主题
    - `body`: 正文（选填）
- `/post/form/push`, 接收`form`格式数据，参数
    - `title`: 主题
    - `body`: 正文（选填）

## Docker部署
```sh
PORT=8080 # 改成你的端口号
# email
EMAIL=xxxx@xxx.com # 改成你的邮箱
SMTP_SERVER=smtp.xxxx.com # 改成你的smtp服务器
USER_NAME=xxxxxx # 改成你的smtp服务器用户名
PASSWORD=xxxxxx # 改成你的smtp服务器密码
# push
PUSHKEY=xxxxxx # 改成你的pushdeer的pushkey
# 部署
docker run -d --name webhook -p $PORT:8080 hlf01/webhook --email $EMAIL --server $SMTP_SERVER --username $USER_NAME --password $PASSWORD --pushkey $PUSHKEY
```

## Docker Compose部署
```yml
version: '3.8'
services:
  webhook:
    container_name: webhook
    image: hlf01/webhook
    restart: always
    network_mode: bridge
    ports:
      - 8080:8080 # 改成你的端口号
    # 以下改成你自己的配置
    command: >
      --email xxxx@xxx.com
      --server smtp.xxxx.com
      --username xxxxxx
      --password xxxxxx
      --pushkey xxxxxx
```

## Docker构建
```sh
docker build --tag webhook --no-cache .
```

## Rust构建
```sh
cargo build --release
# 运行
./target/release/webhook
```
