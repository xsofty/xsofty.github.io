## **Windows中打开串口注意事项**

在windows操作系统中，**若COM口为10及以上时**，需要在打开COM口时转换一下名称，在COM口前加上 **`\\.\`**, 比如COM32, 应该写成 **\\.\COM32**， 这样才能正确的打开。

*微软预定义的标准设备中含有“COM1”-“COM9”。所以，“COM1”-“COM9”作为文件名传递给函数时操作系统会自动地将之解析为相应的设备。但对于COM10及以上的串口，“COM10”之类的文件名系统只视之为一般意义上的文件，而非串行设备。*