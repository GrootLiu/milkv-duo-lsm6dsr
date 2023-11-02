# milkv-duo 适配 lsm6dsr 陀螺仪
## 清单

- [milkv-duo 开发板](https://item.taobao.com/item.htm?spm=a1z10.1-c.w4004-24811212567.2.1f7913b5Y8K002&id=707976817589)
- [lsm6dsr 陀螺仪](https://item.taobao.com/item.htm?spm=a1z10.1-c.w4004-24811212567.2.1f7913b5Y8K002&id=707976817589)
- [官方 SDK 仓库](https://github.com/milkv-duo/duo-buildroot-sdk)
## 第一步：修改设备树

克隆官方仓库到本地之后，进入 `duo-buildroot-sdk/build/boards/cv180x/cv1800b_milkv_duo_sd/u-boot` 文件夹中修改 `cv1800b_milkv_duo_sd.dts` 文件

```dts
// duo-buildroot-sdk/build/boards/cv180x/cv1800b_milkv_duo_sd/u-boot/cv1800b_milkv_duo_sd.dts: 23

//&i2c1 {
//       status = "okay";
//       clock-frequency = <100000>;
//};

&i2c1 {
    status = "okay";
    lsm6dsr:lsm6dsr@6b {
        compatible = "litchicheng,lsm6dsr";
        reg = <0x6b>;
        status = "okay";
    };  
};
```

## 第二步：编译镜像
进入  `duo-buildroot-sdk/` 执行命令
```bash
$ ./build_milkv.sh
```

编译过程需要很久，可以喝杯茶歇歇。

## 第三步：编译内核模块和测试程序

克隆仓库
```shell
$ git clone -b i2c-module git@github.com:GrootLiu/milkv-duo-lsm6dsr.git
$ cd milkv-duo-lsm6dsr/i2c-module
```

进入仓库后，阅读 `i2c-module/` 文件下面的 README.md 文件

