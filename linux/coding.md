##### 安装docker

* 乌班图

  * ```bash
    sudo apt update  # 更新系统
    sudo apt install docker.io -y # 安装docker.io
    sudo usermod -aG docker $USER # 将本用户加入docker的组
    newgrp docker                 # 创建新组docker
    ```

* `manjaro`

  * 

##### 配置镜像环境

* 乌班图
  * ```bash
    docker pull ubuntu:latest # 拉取乌班图镜像
    
    sudo apt-get install x11-xserver-utils # 非必要，安装x11服务器工具包
    xhost +                   # 让任何ip都能使用本机显示功能
    
    # 开启一个容器
    $ docker run -d \
      -v [hostpath]:/root \
      -v /tmp/.X11-unix:/tmp/.X11-unix \
      -e DISPLAY=unix$DISPLAY \
      -e GDK_SCALE \
      -e GDK_DPI_SCALE \
      --name [containername] \
      [yourimage] \
      /bin/bash
    ```

  * 此时进入了容器的`bash`环境

    * ```bash
      apt update    # 更新系统
      apt install vim 
      apt install x11-utils
      ```

  * 调试`xev`功能即可

  
