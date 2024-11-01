# MERN 项目部署指南

# 前提条件
## 1. Ubuntu 服务器
安装 Node.js 和 npm连接到您的服务器，运行以下命令安装 Node.js 和 npm。
  ```
  sudo apt update
  sudo apt install nodejs npm
  ```
## 2. 安装mongodb
参考网站 https://www.mongodb.com/zh-cn/docs/manual/tutorial/install-mongodb-on-ubuntu/

安装 MongoDB Community Edition
按照以下步骤使用 apt 软件包管理器安装 MongoDB Community Edition。

### 1. 导入公钥
   
从终端安装 gnupg 和 curl（如果尚未安装）：
  ```
  sudo apt-get install gnupg curl
  ```
  - 要导入 MongoDB 公共 GPG 密钥，请运行以下命令：
  ```
  curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
     sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
     --dearmor
  ```
 ### 2. 创建列表文件
    
为您的 Ubuntu 版本创建列表文件 /etc/apt/sources.list.d/mongodb-org-8.0.list。
  
  为Ubuntu 22.04 (Jammy) 创建列表文件：
  ```
  echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
  ```
 ### 3. 重新加载包数据库
    
发出以下命令以重新加载本地软件包数据库：
  ```
  sudo apt-get update
  ```
### 4. 安装 MongoDB Community Server
   
 您可以安装最新稳定版本的 MongoDB 或指定版本的 MongoDB。
要安装最新的稳定版本，请执行以下命令：
```
sudo apt-get install -y mongodb-org
```
在 Ubuntu 中安装 MongoDB 时，如需对过程中遇到的错误进行故障排查，请参阅故障排查指南。

## 3.连接到github目录
 使用 SSH 进行身份验证。这是推荐的方式，特别适用于服务器环境。
  
  生成 SSH 密钥 在服务器上生成一个新的 SSH 密钥对：
  ```
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```
  按提示操作即可，通常密钥会保存在 ~/.ssh/id_ed25519 中。
  
  添加 SSH 密钥到 GitHub

  运行以下命令查看生成的公钥：
  ```
  cat ~/.ssh/id_ed25519.pub
  ```
  复制显示的公钥内容。
  登录 GitHub，进入「Settings」->「SSH and GPG keys」->「New SSH Key」，粘贴公钥并保存。

## 部署步骤
1. 安装 Node.js 和 MongoDB
2. 克隆项目仓库并安装依赖
3. 构建前端项目
4. 配置 Nginx 和 PM2
