---
id: install_milvus
title: Install Milvus
sidebar_label: Install Milvus
---
# 安装 Milvus

点击 [版本发布](../release/v0.4.0.md) 了解最新版本的功能。

## 硬件要求

| 组件 | 建议配置                          |
| ---- | --------------------------------- |
| CPU  | Intel CPU Haswell 及以上          |
| GPU  | NVIDIA Pascal series 及以上       |
| 内存 | 8 GB + （取决于具体向量数据规模） |
| 存储 | SATA 3.0 SSD 及以上               |

## 安装前提

1. 请确保您的 Linux 系统符合以下版本：

| Linux 操作系统平台 | 版本             |
| :----------------- | :--------------- |
| CentOS             | 7.5 and higher   |
| Ubuntu LTS         | 18.04 and higher |

2. 请确保您已经安装以下软件包：

   - NVIDIA driver 418 及以上
   
     若要安装 NVIDIA driver 418，在电脑桌面，进入 **Software & Updates** -> **Additional Drivers**。选择 **Using NVIDIA driver metapackage from nvidia-driver-418**，然后点击 **Apply Changes**。
   
   - [Docker 19.03 及以上](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/)
   
   - [nvidia-docker2](https://github.com/NVIDIA/nvidia-docker/wiki/Installation-(version-2.0))
   
   > 注意：您无需单独安装 CUDA 环境，它已经包含在 Milvus Docker 容器里。
   
## 使用 Docker

1. 确认后台已经运行 Docker daemon：

   ```
   docker version
   ```

   如果没有看到相关服务器，请启动 **Docker** daemon.

   > 提示：在 Linux 上，Docker 需要带 sudo。

2. 拉取 Milvus 0.5.0 版本的镜像：

   ```
   sudo docker pull milvusdb/milvus:latest
   ```

3. 下载 Milvus 源文件。

   ```shell
   # Create Milvus file
   $ mkdir /home/$USER/milvus
   $ cd /home/$USER/milvus
   $ mkdir conf
   $ cd conf
   $ wget https://raw.githubusercontent.com/milvus-io/docs/master/assets/server_config.yaml
   $ wget https://raw.githubusercontent.com/milvus-io/docs/master/assets/log_config.conf
   ```

4. 启动 Milvus server。

   ```shell
   # Start Milvus
   $ nvidia-docker run -td --runtime=nvidia -e "TZ=Asia/Shanghai" -p 19530:19530 -p 8080:8080 -v /home/$USER/milvus/db:/opt/milvus/db -v /home/$USER/milvus/conf:/opt/milvus/conf -v /home/$USER/milvus/logs:/opt/milvus/logs milvusdb/milvus:latest
   ```

5. 确认 Milvus 运行状态。

   ```shell
   # Confirm Milvus status
   $ docker ps
   ```
   
   如果 Milvus 服务没有正常启动，您可以执行以下命令查询错误日志。
   
   ```shell
   # Get Milvus container id
   $ docker ps -a
   # Check docker logs
   $ docker logs <milvus container id>
   ```

## 接下来您可以

- 如果您刚开始了解 Milvus：

  - [运行示例程序](example_code.md)
  - [了解更多 Milvus 操作](milvus_operation.md)
  - [体验 Milvus 在线训练营](https://github.com/milvus-io/bootcamp)

- 如果您已准备好在生产环境中部署 Milvus：

  - [向 Milvus 导入数据](import_data.md)
  - 创建 [监控与报警系统](monitor.md) 实时查看系统表现
  - [设置 Milvus 参数](../reference/milvus_config.md)