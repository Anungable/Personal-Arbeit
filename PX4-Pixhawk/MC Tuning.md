## MC Tuning

### Description

---

### Prerequisite

打開QGC，在Autotune前確認以下：

1. 選擇airframe，設定motor mapping、最大最小PWM值、軸距
2. 執行sensor、ESC校正
3. 關掉`MC_AIRMODE` (PID tuning頁面內)，若在tuning階段打開可能會導致還不穩定的控制器發散

---

### 注意事項

1. ESC校正時要用usb供電，不可用電池 (QGC會有指示)
1. 落地後才更改參數 (微幅調整的話不一定要落地，但大幅度調整的話response會有spike，保險起見請降落)

---

### How To Tune 

分兩部份著手：1. PID  2.trajectory generator

#### 1. PID  

(flight controller結構紀錄在`MC Flight Contoller.md`)

##### 內圈Rate control loop

- 有兩種PID form可以選擇：parallel和standard (兩者等價)

<img src="https://docs.px4.io/v1.11/images/mc_pid_tuning/PID_algorithm_Mixed.png" alt="PID_Mixed" style="zoom:67%;" />

​	設定$ K=1 $ 調整PID或設定$P=1$調整KID。

- 用acro mode來調整

  Disable stick expo：

  - `MC_ACRO_EXPO` = 0, `MC_ACRO_EXPO_Y` = 0, `MC_ACRO_SUPEXPO` = 0, `MC_ACRO_SUPEXPOY` = 0
  - `MC_ACRO_P_MAX` = 200, `MC_ACRO_R_MAX` = 200
  - `MC_ACRO_Y_MAX` = 100

- 可調整參數

  - Roll rate control (`MC_ROLLRATE_P`,` MC_ROLLRATE_I`, `MC_ROLLRATE_D`, `MC_ROLLRATE_K`)
  - Pitch rate control (`MC_PITCHRATE_P`, `MC_PITCHRATE_I`, `MC_PITCHRATE_D`, `MC_PITCHRATE_K`)
  - Yaw rate control (`MC_YAWRATE_P`, `MC_YAWRATE_I`, `MC_YAWRATE_D`, `MC_YAWRATE_K`)

- 先調整PD再調整I

  - P gain

    太高：高頻震盪

    太低：slow response, 在acro模式下機體無法level

  - D gain

    太高：馬達會發燙

    太低：overshoot

    gain值通常會落在這個區間：

    - standard form (**P** = 1): between 0.01 (4" racer) and 0.04 (500 size), for any value of **K**
    - parallel form (**K** = 1): between 0.0004 and 0.005, depending on the value of **P**

  - I gain

    太高：低頻震盪

    太低：穩態誤差

    gain值通常會落在這個區間：

    - standard form (**P** = 1): between 0.5 (VTOL plane), 1 (500 size) and 8 (4" racer), for any value of **K**
    - parallel form (**K** = 1): between 0.3 and 0.5 if **P** is around 0.15. The pitch gain usually needs to be a bit higher than the roll gain.

##### 外圈Attitude control loop

- 用manual/stabilized mode來調整
- 可調整參數
  - Roll control (`MC_ROLL_P`, `MC_ROLLRATE_MAX`)
  - Pitch control (`MC_PITCH_P`, `MC_PITCHRATE_MAX`)
  - Yaw control (`MC_YAW_P`, `MC_YAWRATE_MAX`)

##### 最外圈Velocity and position control loop

- 可用autotune後進行微調

#### 2. Trajectory generator模式選取

Trajectory generator影響setpoint的設定，模式有以下3種，透過`MPC_POS_MODE`調整：

- Jerk-limited trajectory (Default) : smooth command
- Slew-rate trajectory : quicker response than jerk-limited since jerk and acceleration are not limited
- Simple position control : RC指令直接map到速度指令，可以用來tune velocity loop

注意事項：

- mission mode只使用Jerk-limited trajectory
- postion和altitude (只有高度向平滑化) 支援全部
- 其他模式不適用

### Filter Tuning



---

### PX4改Siras調參+設定紀錄

- PWM最小值落在1110~1120之間，最大值1900

- 馬達異音＋發熱

  主要原因是yaw rate D gain太大，實際值應該落在0.0005以下

  次要原因是roll and pitch rate D gain

- 

---

### Reference

https://github.com/PX4/PX4-user_guide/blob/main/en/config_mc/filter_tuning.md
