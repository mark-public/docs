
### 阿里云docker仓库
#### 登录实例
获取临时密码或固定密码后，可通过密码登录镜像服务实例：   
- 1. 获取访问域名，基于当前的网络环境，选择对应的专有网络、公网或经典网络域名。  
- 2. 在终端中输入访问凭证，登录Registry实例  
```shell
$ sudo docker login --username=用户名 --password=密码 registry.cn-hangzhou.aliyuncs.com
```

#### 命名空间
| 命名空间    | 权限 | 命名空间状态 | 自动创建仓库 | 默认仓库类型 |
| ----------- | ---- | ------------ | ------------ | ------------ |
| mark-public | 管理 | 正常         | 开启         | 公开         |
| mark02      | 管理 | 正常         | 开启         | 私有         |


#### 镜像加速器
一、**加速器地址：**  https://gyvdwe4d.mirror.aliyuncs.com

二、**操作说明：**

+ **Ubuntu/CentOs**

  + **1）安装／升级Docker客户端**
    推荐安装1.10.0以上版本的Docker客户端，参考文档docker-ce

   + **2）配置镜像加速器**
     针对Docker客户端版本大于 1.10.0 的用户
        您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

     ```shell
     sudo mkdir -p /etc/docker
     sudo tee /etc/docker/daemon.json <<-'EOF'
     {
       "registry-mirrors": ["https://gyvdwe4d.mirror.aliyuncs.com"]
     }
     EOF
     sudo systemctl daemon-reload
     sudo systemctl restart docker
     ```

+ **Macos**

  + **1) 安装／升级Docker客户端**
    对于10.10.3以下的用户 推荐使用Docker Toolbox
    Mac安装文件：http://mirrors.aliyun.com/docker-toolbox/mac/docker-toolbox/
    对于10.10.3以上的用户 推荐使用Docker for Mac
    Mac安装文件：[http://mirrors.aliyun.com/docker-toolbox/mac/docker-for-mac/](http://mirrors.aliyun.com/docker-toolbox/mac/docker-for-mac/?spm=5176.8351553.0.0.4c1e1991HDNW8p)

  + **2) 配置镜像加速器**
    针对安装了Docker Toolbox的用户，您可以参考以下配置步骤：
    创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。  

    ```bash
    docker-machine create --engine-registry-mirror=https://gyvdwe4d.mirror.aliyuncs.com -d virtualbox default
    ```

    查看机器的环境配置，并配置到本地，并通过Docker客户端访问Docker服务。
    ```bash
    docker-machine env defaulteval "$(docker-machine env default)"docker info
    ```

    针对安装了Docker for Mac的用户，您可以参考以下配置步骤：
    在任务栏点击 Docker Desktop 应用图标 -> Perferences，在左侧导航菜单选择 Docker Engine，在右侧输入栏编辑 json 文件。将

    https://gyvdwe4d.mirror.aliyuncs.com加到"registry-mirrors"的数组里，点击 Apply & Restart按钮，等待Docker重启并应用配置的镜像加速器。


+ **Window**

   + **1) 安装／升级Docker客户端**
      对于Windows 10以下的用户，推荐使用Docker Toolbox
      Windows安装文件：http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/
      对于Windows 10以上的用户 推荐使用Docker for Windows
      Windows安装文件：http://mirrors.aliyun.com/docker-toolbox/windows/docker-for-windows/

  +  **2) 配置镜像加速器**
      针对安装了Docker Toolbox的用户，您可以参考以下配置步骤：  
      创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。
      查看机器的环境配置，并配置到本地，并通过Docker客户端访问Docker服务。
  
        ```bash
        docker-machine env default
        eval "$(docker-machine env default)"
        docker info
        ```
  
    针对安装了Docker for Windows的用户，您可以参考以下配置步骤：
    在系统右下角托盘图标内右键菜单选择 Settings，打开配置窗口后左侧导航菜单选择 Docker Daemon。编辑窗口内的JSON串，填写下方加速器地址：
  
    ```
    {
      "registry-mirrors": ["https://gyvdwe4d.mirror.aliyuncs.com"]
    }
    ```
  
    编辑完成后点击 Apply 保存按钮，等待Docker重启并应用配置的镜像加速器。
    **注意： **Docker for Windows 和 Docker Toolbox互不兼容，如果同时安装两者的话，需要使用hyperv的参数启动。
  
    ```bash
    docker-machine create --engine-registry-mirror=https://gyvdwe4d.mirror.aliyuncs.com -d hyperv default
    ```
  
    Docker for Windows 有两种运行模式，一种运行Windows相关容器，一种运行传统的Linux容器。同一时间只能选择一种模式运行。
  
  
  

