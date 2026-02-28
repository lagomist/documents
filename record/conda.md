# conda

## 一、管理conda：  

- （1）检查conda版本  
	`conda --version`  
	
- （2）获取版本号  
	`conda --version`  
	`conda -V`
	
- （3）列出所有的环境  
	`conda env list` 查看conda创建的所有虚拟环境  
	`conda list` 查看conda下的包
	
- （4）查看环境管理的全部命令帮助  
	`conda env -h`
	
- （5）conda升级  
	`conda update conda`  
	`conda update --all` 升级所有包
	
- （6）conda升级后释放空间  
	`conda clean -p` 删除没有用的包  
	`conda clean -t` 删除保存下来的压缩文件（.tar）
	
## 二、管理环境

- （1）创建环境  

	`conda create -n env-name [list of package]`  
	-n env-name是设置新建环境的名字，  
	list of package是可选项，选择要为该环境安装的包。

	指定安装python的版本  
	`conda create -n env-name python=3.6`

- （2）激活、进入环境  

	`source activate env-name`  

    `conda activate env-name`

- （3）退出当前环境  

    `conda deactivate`

- （4）切换到base环境  

	`conda source deactivate`

- （5）复制一个环境  
	通过克隆来复制一个环境。这儿将通过克隆snowfllakes来创建一个称为flowers的副本。  
	
	`conda create -n flowers --clone snowflakes`

- （6）删除一个环境

	`conda env remove -n env-name`
	
## 三、管理包

- （1）安装包 或 安装特定版本的包  
	`conda install package-name`  
	`conda install package-name==version`
	
- （2）查看所有已安装包  
	`conda list` 
	
- （3）卸载包  

	`conda remove package-name`
	
- （4）更新包  

	更新一个包  
	`conda update package-name`  
	更新所有包  
	`conda update --all`
	
- （5）搜索包  
	`conda search search-term` 可以模糊搜索

# 安装

## 官方下载
[官方文档](https://docs.anaconda.com/miniconda/)

## 环境配置

去除默认环境激活
```bash
conda config --set auto_activate_base false
```
