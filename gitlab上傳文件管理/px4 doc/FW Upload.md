### Description 

PX4 FW在本機端編譯和燒錄到飛控板上說明。

---

### Reference

PX4官網說明：https://docs.px4.io/main/en/dev_setup/building_px4.html

---

### Build & Upload

*手動燒錄前請先確認 `make px4_sitl`可成功，以確認Toolchain安裝正確。*

- 飛控板 Target：Pixhawk 6c

- QGC可直接從雲端抓取FW燒錄到飛控板，但若有修改FW則須手動編譯＋燒錄，指令如下：

```shell
make px4_fmu-v6c[_default] #default可加可不加
```

​	若make成功會顯示類似下面的訊息且無Error跳出：

```sh
-- Build files have been written to: /home/your_dir/Pilot4_circ_customize_px4/build/px4_fmu-v4_default
```

​	成功後即可燒錄：

```shell
make px4_fmu-v6c upload
```

Note：燒錄的Target (z.B, sitl, v6c...) 可在`/Pilot4_circ_customize_px4/boards/px4/`路徑下看到。

#### 如何確認upload成功

Upload成功的話console應該顯示如下，

```shell
Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting.

[100%] Built target upload
```

連線到QGC上確認sensor、機體是否有成功抓取到。

----

### 更新Bootloader

通常bootloader已經pre-installed，但若須更新的話可用指令：

```shell
make px4_fmu-v6c_bootloader
```

