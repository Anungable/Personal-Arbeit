```shell
docker run -it --privileged \
--env=LOCAL_USER_ID="$(id -u)" \
-v /home/inungshen/inung/PX4-Autopilot-ins:/home/inungshen/inung/PX4-Autopilot-ins/:rw \
-v /tmp/.X11-unix:/tmp/.X11-unix:ro \
-e DISPLAY=:0 \
-p 18550:18550/udp \
--name=px4-test px4io/px4-dev-base-focal:latest bash
```

```shell
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' 5bf03990760b
```

<sup style="display: inli

```bash
docker run -it --privileged \
--env=LOCAL_USER_ID="$(id -u)" \
-v /home/inungshen/inung/PX4-Autopilot-ins:/home/inungshen/inung/PX4-Autopilot-ins/:rw \
-v /tmp/.X11-unix:/tmp/.X11-unix:ro \
-e DISPLAY=:0 \
-p 18550:18550/udp \
--name=px4-test px4io/px4-dev-simulation-focal bash
```

---

- QGC設定

  ```bash
  docker run -it --privileged \
  --env=LOCAL_USER_ID="$(id -u)" \
  -v /home/van/inung/px4-autopilot:/home/van/inung/px4-autopilot/:rw \ 
  -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
  -e DISPLAY=:0 \
  -p 18550:18550/udp \
  --name=px4-test1 px4io/px4-dev-simulation-focal bash
  ```

  

  ![docker SITL setting](/home/inungshen/Pictures/docker SITL setting.png)

```bash
INFO  [init] PX4_SIM_HOSTNAME: localhost
INFO  [simulator_mavlink] Waiting for simulator to accept connection on TCP port 4560
INFO  [simulator_mavlink] Simulator connected on TCP port 4560.
INFO  [lockstep_scheduler] setting initial absolute time to 5440000 us
INFO  [commander] LED: open /dev/led0 failed (22)
```

