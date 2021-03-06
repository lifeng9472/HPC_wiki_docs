# caffe

### 路径

caffe 的依赖库源码路径：`/share/package/caffelib_packages`

caffe 的依赖库安装路径：`/share/apps/caffelib`

caffe 的源码和安装路径均为: `/share/package/caffe`

caffe的可执行文件所在的路径是:
`/share/package/caffe/build/tools/caffe`

### 提交 caffe 任务
由于没有指定运行时所需要的库，所以一个简单的pbs文件为
```shell
#PBS -N test_caffe
#PBS -l nodes=1:ppn=16:gpus=8
#PBS -o /home/USERNAME/logs
#PBS -e /home/USERNAME/logs_error
#PBS -q default

module load caffe # important

## write your code here
cd YOUR_SCRIPTS_PATH
sh YOUR_SCRIPTS.sh

module unload caffe
```

其中:
`YOUR_SCRIPTS_PATH`指的是你要运行的脚本
`YOUR_SCRIPTS`所在的路径。

!!! Warning
    **请注意，如果您申请的gpu数量与您实际使用的gpu数量不一致，作业会被删除** <br/>




更多关于提交作业的内容，请参考[作业系统](../jobs.md).

### pycaffe

pycaffe同样在`/share/package/caffe/python`中

如果您要运行pycaffe，那么一个pbs文件的模板为
```shell
#PBS -N test_caffe
#PBS -l nodes=1:ppn=16:gpus=8
#PBS -o /home/USERNAME/logs
#PBS -e /home/USERNAME/logs_error
#PBS -q default

module load caffe

## write your code here
cd YOUR_SCRIPTS_PATH
sh YOUR_SCRIPTS.sh

module unload caffe
```

!!! Warning
    caffe程序的命令行参数中，如果带有gpu选项指定使用的gpu，请始终从0开始写起，即使当前0号GPU已经被占用。

    例如：
    当前node1节点gpu0,gpu1已经被占用。现需要继续在node1上提交另外的caffe任务

    * 如果需要申请一个gpu
      #PBS -l 申请资源中gpus=1
      caffe命令行参数 --gpu 0

    * 如果需要申请两个gpu
      #PBS -l 申请资源中gpus=2
      caffe命令行参数 --gpu 0,1

    注意正如上面提到的，命令行参数请始终从0开始写起。集群任务调度系统能够自行调度实际GPU。



