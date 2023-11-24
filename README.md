# webhook
A webhook server written in rust.

- 通过邮件接收通知
- 通过[PushDeer](https://github.com/easychen/pushdeer)接收通知

## 接口
### email
- `/get/email`, 参数
    - `subject`: 主题
    - `body`: 正文
- `/post/json/email`, 接收`json`格式数据，参数
    - `subject`: 主题
    - `body`: 正文
- `/post/form/email`, 接收`form`格式数据，参数
    - `subject`: 主题
    - `body`: 正文

### push
- `/get/push`, 参数
    - `text`: 文本
- `/post/json/push`, 接收`json`格式数据，参数
    - `text`: 文本
- `/post/form/push`, 接收`form`格式数据，参数
    - `text`: 文本

## Docker部署
```sh
PORT=8080 # 改成你的端口号
EMAIL=xxxx@xxx.com # 改成你的邮箱
SMTP_SERVER=smtp.xxxx.com # 改成你的smtp服务器
USER_NAME=xxxxxx # 改成你的smtp服务器用户名
PASSWORD=xxxxxx # 改成你的smtp服务器密码
PUSHKEY=xxxxxx # 改成你的pushdeer的pushkey
docker run -d --name webhook -p $PORT:8080 hlf01/webhook --email $EMAIL --server $SMTP_SERVER --username $USER_NAME --password $PASSWORD --pushkey $PUSHKEY
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
