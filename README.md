# qemu-sec

基于qemu v2.7.0源码修改，简单实现了qemu用户模式的NX、ASLR、PIE、W^X安全机制


## Usage

`build`目录里面有docker构建文件，默认以静态链接的方式构建所有架构的用户模式qemu-sec程序

`qemu-sec`目录下是已经构建好的程序，可以直接拿去使用

加以下参数可实现
```shell
-nx           QEMU_NX           enable NX implementation
-pie          QEMU_PIE        enable PIE randomization
-aslr         QEMU_ASLR       enable ASLR randomization
-wxorx        QEMU_WXORX        enable W^X implementation
```

其中 `W^X` 开启后，程序不允许mmap分配同时存在`PROT_EXEC`与`PROT_WRITE`属性的内存 或是通过mprotect更改内存为同时存在`PROT_EXEC`与`PROT_WRITE`属性

                                                                                  commit by b0ldfrev