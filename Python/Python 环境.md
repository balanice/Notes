# Python 环境

## Anaconda

* 查看当前 python 环境:
    ```shell
    conda env list
    ```
* 激活某个环境, 如 base:
    ```shell
    conda activate base
    ```
* 升级所有包:
    ```shell
    conda upgrade --all
    ```
* 安装包:
    ```shell
    conda install xxx
    ```
* 安装包时候指定包的版本:
    ```shell
    conda install xxx=0.1
    ```
* 卸载包:
    ```shell
    conda remove xxx
    ```
* 输出当前环境配置到 yaml 文件中:
    ```shell
    conda env export > environments.yaml
    ```
* 根据 yaml 文件创建环境:
    ```shell
    conda env create -f xxx.yaml
    ```
## --help, man 大法好

## pip 管理 python 包
