---
title: FTP Client 踩过的坑
tags: ftp
categories: JAVA
date: 2019-01-02 18:03:29
---
#### 目录
FTPClient的路径跳转之后，之后所做的操作都是在当前目录下，若要在其它目录下操作需要跳转到相应目录
获取当前目录：
```
client.printWorkingDirectory()
```
目录跳转:
```
client.changeWorkingDirectory(path)
```

#### 文件删除
和File处理不同，FTPClient目录删除和文件删除的命令不一样
删除目录:
```
client.removeDirectory(filePath)
```
删除文件:
```
client.deleteFile(filePath)
```

#### 文件流操作
FTPClient 返回值为InputStream或者OutputStream时必须通过调用completePendingCommand()需要流，例如retrieveFileStream()和storeFileStream()方法，完成后必须调用completePendingCommand()，并且验证是否返回success。
如：
```
if (!client.completePendingCommand()) {
    this.destroy();
    this.afterPropertiesSet();
}
```
注意：completePendingCommand()这个方法不能连续调用两次，不然程序会卡住，只有再次进行了文件流的操作的时候才需要调用

官方文档：[](https://commons.apache.org/proper/commons-net/javadocs/api-3.6/index.html)

FTPClient 的参数为InputStream或者OutputStream时，执行完操作后也要注意将流关闭，因为FTPClient的方法一般不会关闭这些流。

#### 模式设置
有的环境下文件获取以及上传都需要设置
ftpClient.listFiles()返回null, 或者返回421错误，都有可能是因为没有设置enterLocalPassiveMode模式。
我在Windows以及Linux环境下测试这些方法都没有问题，把服务放到docker上以后就报了上述问题，研究后发现是需要设置enterLocalPassiveMode这个模式，可能是docker环境导致端口号不稳定的原因。
参考：[](https://www.cnblogs.com/wqsbk/p/6526005.html)