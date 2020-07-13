## npm常用指令

### 配置

| 指令                                                         | 说明                            |
| ------------------------------------------------------------ | ------------------------------- |
| npm config list                                              | 列举已有npm配置                 |
| npm config set registry 镜像源地址                           | 设置镜像地址                    |
| npm install -g cnpm --registry=https://registry.npm.taobao.org | 使用cnpm                        |
| cnpm install package-name                                    | 使用 `cnpm` 命令代替 `npm` 命令 |

### 安装模块

| 指令                                 | 说明                 |
| ------------------------------------ | -------------------- |
| npm install 模块名 -g                | 全局安装             |
| npm install 模块名                   | 本地安装             |
| npm install 模块名 --save            | 安装运行时依赖包     |
| npm install 模块1 模块2 模块n --save | 一次性安装多个依赖包 |
| npm install 模块名 --save-dev        | 安装开发时依赖包     |

### 更新模块

| 指令                 | 说明         |
| -------------------- | ------------ |
| npm update 模块名    | 更新本地模块 |
| npm update -g 模块名 | 更新全局模块 |

### 卸载模块

| 指令                    | 说明         |
| ----------------------- | ------------ |
| npm uninstall 模块名    | 卸载本地模块 |
| npm uninstall -g 模块名 | 卸载全局模块 |

### 查看安装

| 指令               | 说明                       |
| ------------------ | -------------------------- |
| npm root           | 查看本地安装的目录         |
| npm root -g        | 查看全局安装的目录         |
| npm ls --dept 0    | 查看当前目录下已安装的模块 |
| npm ls -g --dept 0 | 查看已安装的全局模块       |
| npm info 模块名    | 查看模块的信息             |

### 其他

| 指令           | 说明                                                     |
| -------------- | -------------------------------------------------------- |
| npm help       | 查看npm命令                                              |
| npm init       | 初始化一个基于node的项目，会创建一个配置文件package.json |
| npm init --yes | 全部使用默认配置                                         |

