安装命令行工具前请确保您的系统已经安装了 Python 环境, 具体应安装Python2.7和python-pip。

## 1. 安装腾讯云命令行工具 CLI	
### I. 确认已经**通过内测申请**
否则在使用命令行工具的 Batch 相关命令时会提示没有访问权限。

### II. 安装命令行工具 CLI：
* 没安装 CLI：通过 pip 可以快速安装腾讯云命令行工具 CLI。
```
$ sudo pip install qcloudcli
```

* 已安装 CLI：通过 pip 可以快速升级，命令见下
```
$ sudo pip install --upgrade qcloudcli
```

### III. 检验命令行工具 CLI 是否安装成功，并包含 Batch 相关能力：
```
$ qcloudcli batch help
You should use the qcloudcli as follow format:
qcloudcli <module> <action> [options and parameters]
The action name you input is error! The module [batch] support the valid action as follows:

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

## 2. 获取 SecretID 和 SecretKey。
### I. 登录腾讯云[API 密钥控制台](https://console.cloud.tencent.com/capi)。

### II. 新建密钥或使用现有云 API 密钥。单击云 API 密钥 ID进入详情页，获取 SecretID 及 SecretKey。
![Alt text](https://mc.qcloudimg.com/static/img/ab7aea426d53f31f6bb1fc84bd2ce177/1.png)

## 3. 准备 COS 目录
### I. 创建 Bucket 和子文件夹
![](https://mc.qcloudimg.com/static/img/ecb3282f6cf12b371925743d9efa3874/COS_1.png)
创建一个 Bucket，命名随意，在 Bucket 里再创建 3 个文件夹以便后续使用，文件夹名字见上图。

### II. 记好 COS 访问的地址
![](https://mc.qcloudimg.com/static/img/0a0a2a781ed55febaecc2531fbe4f592/COS_2.png)

先通过上图指示查看 COS Bucket 的访问域名，然后通过域名 + 文件夹名称拼凑出 3 个文件夹的访问域名，刚才官方帐号创建的 3 个文件夹的访问地址分别是

* cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/input/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/output/

``` 请务必根据您自己的 Bucket 访问域名拼凑出文件夹访问地址 ```

## 4. 下载 Batch Demo 文件

[下载地址](http://batchdemo-1251783334.cosgz.myqcloud.com/demo/BatchDemo.zip)，解压后目录结构如下，后续请按照下列顺序逐个体验 Batch 的使用和能力

* [1_SimpleStart](https://cloud.tencent.com/document/product/599/10551)
* [2_RemoteCodePkg](https://cloud.tencent.com/document/product/599/10552)
* [3_StoreMapping](https://cloud.tencent.com/document/product/599/10983)

``` Demo 以 Python + Batch 命令行工具 的形式提供，Batch 的能力和可配置项较多，通过 Python 脚本可以更便捷的操作。```

## 5. Demo 自定义信息通用部分说明
以『1_SimpleStart』的自定义信息部分为例，

```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```

* imageId：内测期间需要使用包含 Cloud-init 服务的镜像，官方在云市场提供了 CentOS 7.2 版本的可直接使用镜像，镜像 ID **img-31tjrtph**，自定义镜像需要基于此镜像来制作
* StdoutRedirectPath、StderrRedirectPath：请填写第三步里准备的 COS 目录里的 logs 文件夹完整访问地址，比如示例中则是 cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/，请替换成您自己的访问地址
* Application：启动命令行，暂时不用修改
