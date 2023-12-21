## MC Flight Mode

### Flight Mode Overview

| Main Custom Mode  | Sub Mode       | Description                                                  |
| ----------------- | -------------- | ------------------------------------------------------------ |
| Acro              |                | angular rate                                                 |
| Altitude          |                | 姿態＋定高<br />yaw : yaw rate<br />thrust : speed with max rate |
| Manual/stabilized |                | 姿態＋定高<br />yaw : yaw rate<br />thrust : speed without max rate |
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

### Flight Mode Command Flow



---

### Flight Mode

Flight mode is changed in *Commander module*, it publishes `vehicle_command_s `and `vehicle_status_s` for *Navigator module* to handle the following action (e.g. handle command, do other navigation function such as avoidance or geofence).

Position mode: RC input mapped to either velocity or position control loop

commander.run()->handle_command()->publish vehicle_status

navigator->subscribe vehicle_status

#### Flight mode activation flag



---

### Reference

https://docs.px4.io/main/en/flight_modes/

https://blog.csdn.net/qq_38768959/article/details/127763019

