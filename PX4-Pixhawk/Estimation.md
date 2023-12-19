Mahony (互補濾波)

用磁力計校正陀螺儀的偏航誤差，加速計校正陀螺儀的pitch和roll誤差。

EKF (擴展卡爾曼濾波)

---

### Yaw alignment using IMU and GPS

- EKF (Extended Kalman Filter)
- UKF (Unscented Kalman Filter)
- EKF-GSF (Gaussian Sum Filter using states from multiple EKF’s)
- UKF-GSF (Gaussian Sum Filter using states from multiple UKF’s)
- EKF-IMM (Interacting Multiple Model Filter using states from multiple EKF’s)
- UKF-IMM (Interacting Multiple Model Filter using states from multiple UKF’s)
- Particle Filter

---

### State Vector

$$
x^{(24\times1)}=[q\space\space \vec{v}\space\space  \vec{p}\space\space  \Delta\theta_b\space\space  \Delta v_b\space\space  m_{O}\space m_b\space\space  m_{wind}]^T
$$

$q$ : O->B quaternion

$\vec{v}$ : velocity in NED frame

$\vec{p}$ : position in NED frame

$m_O$ : 地磁 （磁場在NED frame下）(gauss)

$m_b$ : 飛機磁力計和磁北極差角 (bias)，修正這個差角後得到磁航向

$m_{wind}$ : 東北向風速 (m/s)

$\Delta\theta_b$ : IMU angle bias (increment)

$\Delta v_b$ : IMU velocity bias

---

## Reference

ECL 推導https://github.com/ericzzj1989/matlab_px4_msf/blob/master/Analysis%20of%20PX4%20ECL.pdf

天芎https://github.com/Ewenwan/ShiYanLou/tree/master/MCU/px4