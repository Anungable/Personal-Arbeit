### Description 

PX4編譯環境建立說明，包含本機端及使用docker建置。

---

### Reference

(中文版翻譯和英文有出入，請以英文版為準)

PX4官網說明如何本機端建置：https://docs.px4.io/main/en/dev_setup/dev_env_linux_ubuntu.html

PX4官網說明如何使用docker：https://docs.px4.io/main/en/test_and_ci/docker.html

---

### 本機端 PX4 Toolchain 安裝

- 系統：支援Ubuntu 16.04以上

#### 安裝程序
參考官網教學，這裡整理如下：

1. clone `Pilot4 circ customize px4` repo

2. 自動安裝所有相關套件

   ```shell
   bash ./Pilot4_circ_customize_px4/Tools/setup/ubuntu.sh
   ```

   Note: 若有要求特定版本 (z.B, arm-none-eabi-gcc, java...) 的套件須先安裝後再bash。

3. Reboot

4. 安裝地面站QGroundControl (穩定版) 或QGroundControl Daily (快速更新版) 

#### 如何確認安裝成功

- 試執行SITL

  1. 開啟QGC

  2. make，`<simulator_name> (optional)`填入要使用的模擬器，z.B, gazebo, jmavsim

     ```shell
     make px4_sitl_default <simulator_name>
     ```

  3. make成功後回到QGC，若看到介面顯示Ready To Fly即表示成功。

---

### 使用Docker

- 系統：支援Ubuntu 16.04以上

#### 建置流程：

參考官網教學，這裡整理如下：

1. 安裝docker

2. PX4 docker container：https://github.com/PX4/PX4-containers/tree/master，可連結到docker hub找要的tag

3. 執行docker有兩種方法，分別說明如下：

   - 使用script (easy to use)，下面兩個分別為接入Linux及NuttX

     ```shell
     cd PX4_repo #cd到repo根目錄
     ./Tools/docker_run.sh 'make px4_sitl_default' #Linux
     ./Tools/docker_run.sh 'bash' #NuttX
     ```

   - 手動建置 （建議使用這個）

     指令模板如下，須更改處：

     1. `<host_src>，<container_src>`填入PX4 FW路徑`~your_dir/pilot4-circ-customize`
     2. `<-p>`後接指定UDP，須注意避免confilct，也可更改成host避免衝突，但接QGC時要更改成本地IP而非docker IP
     3. `<local_container_name>`請自己取名
     4. `<container>:<tag>`可至第二項的網址裡面連結至docker hub選擇compatible to ubuntu版本的image
     5. `<build_command>`打上bash開啟console

     ```shell
     # enable access to xhost from the container
     xhost +
     
     # Run docker
     docker run -it --privileged \
         --env=LOCAL_USER_ID="$(id -u)" \
         -v <host_src>:<container_src>:rw \
         -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
         -e DISPLAY=:0 \
         -p 18550:18550/udp \
         --name=<local_container_name> <container>:<tag> <build_command>
     ```
     

4. 手動接上QGC

   到Comm Links內新增UDP，
   
   port：14550 (填上make出來的remote port，應該會是14550)
   
   Server address：`docker_ip:udp_port`，填上docker IP，如果用host則是本機IP。
   
   Note：udp_port要和build出來的值double check `(build/px4_sitl_default/etc/init.d-posix/px4-rc.mavlink檔案內找udp_gcs_port_local)`，應該會是18570，不能直接套用官網上的14550。

#### 如何確認安裝成功

- 試執行SITL

  1. 開啟QGC
  
  2. make，`<simulator_name> (optional)`填入要使用的模擬器，z.B, gazebo, jmavsim
  
     ```shell
     make px4_sitl_default <simulator_name>
     ```
  
  3. make成功後回到QGC，若看到介面顯示Ready To Fly即表示成功。

---

### 建置過程Troble-shooting

1. 軟模擬`make`失敗顯示`ninja: error: unknown target 'simulator_name'`

   退回舊版本後remake，記得清除殘留檔再進行

   ```shell
   make clean
   make distclean
   # v1.14 前的版本
   make px4_sitl gazebo
   make px4_sitl jmavsim
   
   # v1.14 後的版本
   make px4_sitl gazebo-classic
   ```

   make指令記得依版本而定，ubuntu20.04用`gazebo`, ubuntu22.04用`gazebo-garden`

   Note：docker若要接上模擬器，container選擇`px4-dev-simulation~<ubuntu distribution>`

3. make with Gazebo顯示錯誤訊息：`FAILED: external/Stamp/sitl_gazebo/sitl_gazebo-configure`

   run `sudo apt-get install libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-bad gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-ugly -y`



