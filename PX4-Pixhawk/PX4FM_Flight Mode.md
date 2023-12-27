## MC Flight Mode

### Flight Mode Overview

| Main Custom Mode  | Sub Mode       | Remark                                                       |
| ----------------- | -------------- | ------------------------------------------------------------ |
| Acro              |                | rate mode                                                    |
| Altitude          |                | 姿態定高<br />yaw : yaw rate<br />thrust : speed with max rate |
| Manual/stabilized |                | 姿態不定高<br />yaw : yaw rate<br />thrust : speed without max rate |
| Position          |                | roll, pitch : acceleration over ground<br />yaw : yaw rate   |
| Auto              | Hold           | Loiter                                                       |
|                   | Mission        |                                                              |
|                   | RTL            |                                                              |
|                   | Takeoff        |                                                              |
|                   | Land           |                                                              |
|                   | Follow target  | 相對於某個東西做定高 or 定距離 or 定角度飛行                 |
|                   | Precision land |                                                              |
| Orbit             |                | 繞圈飛行                                                     |
| Offboard          |                | 機載電腦透過mavlink控制                                      |

---

### Flight Mode

Flight mode is changed in *Commander module*, it publishes `vehicle_command_s `and `vehicle_status_s` for *Navigator module* to handle the following action (e.g. handle command, do other navigation function such as avoidance or geofence).

#### 切換飛行模式

1. QGC

   ![image-20231222171128138](../../../.config/Typora/typora-user-images/image-20231222171128138.png)

2. console

   ```shell
   # e.g. 切換到acro
   nsh> commander mode acro
   ```

3. RC

   Flight Modes設定RC channel

   ![rc_fm](../../pilot4-circ-customize-px4.wiki/document/pic/FW_related/rc_fm.png)

#### Orbit說明

要解鎖起飛後才可以切換，選擇圓心和半徑，飛機會以default 1m/s速度繞圈飛行。

無法直接用RC切換到這個模式。

![orbit](https://img-blog.csdnimg.cn/c2e3bf622a44457fa8a3e5380c16844a.png)



---

### Reference

官網：https://docs.px4.io/main/en/flight_modes/

