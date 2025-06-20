#conda安装其他包
步骤一：搜索并打开 `Anaconda Prompt`
步骤二：创建独立环境(举例如下)
```bash
conda create --name my_project_env python=3.9  # 创建名为my_project_env的环境
conda activate my_project_env                  # 激活环境
```
步骤三：安装所需要的核心包(举例)
```bash
conda install pandas matplotlib seaborn  # 一次性安装三个包
```

如若下载慢，可切换国内镜像源：
```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```