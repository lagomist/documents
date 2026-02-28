# ESP-IDF
IDF开发框架，在Linux环境下的开发指令记录

# idf版本升级、切换
```
cd esp-idf
git pull
git checkout v5.1.3
git submodule update --init --recursive
./install.sh
. ./export.sh
```

# 环境管理

1. 环境变量别名设置  
`alias IDF='. $HOME/Workspace/esp/esp-idf/export.sh'`  



# 工程构建

1. 设置目标芯片型号运行 (初始化工程只使用一次)  
`idf.py set-target esp32`
2. 配置工程   
`idf.py menuconfig`
3. 编译工程  
`idf.py build`
4. 下载到单片机  
`idf.py -p /dev/ttyS4 -b 921600 flash`  
5. 串口监控  
`idf.py -p /dev/ttyS4 -b 115200 monitor`  
6. 运行CMAKE  
`idf.py reconfigure`  
7. 删除工程附件  
`rm -rf sdkconfig sdkconfig.old build/`

# 工程状态信息

1. 查看帮助  
`idf.py --help`  
2. 打印当前使用分区表的信息  
`idf.py partition-table`  
3. 查看本地IDF版本  
`idf.py --version`  

