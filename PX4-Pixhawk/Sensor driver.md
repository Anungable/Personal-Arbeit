### ID decode

IST8310: 000001100 0001100 00100 001
decode to : 0x06 0xC bus4 I2C

```c++
// device_id: 396321
device::Device::DeviceId device_id_mag{};
device_id_mag.devid_s.bus_type = device::Device::DeviceBusType_I2C;
device_id_mag.devid_s.bus = 4; //from 
device_id_mag.devid_s.address = 0xc; //internal address
device_id_mag.devid_s.devtype = DRV_MAG_DEVTYPE_IST8310;
```

====================================================================================
Kevin:  000001100 0001110 00001 001
0x06 bus1 I2C

====================================================================================
IST8303: 0000011010 0001110 00001 001
slave address: 0x0E
ID: 0x0D
0x0D bus1 I2C

855561

====================================================================================
MS5611: 001111010 1110111 00100 001 
0xF4 bus4 I2C

ID decimal->binary
sparse it according to rules, the first segment is the sensor ID
but we need to shift it rightwards for 1 bit to get the real ID defined in `drv_sensor.hpp`

---

**GPS nsh調閱**

```bash
nsh> gps status
INFO  [gps] Main GPS
INFO  [gps] protocol: UBX
INFO  [gps] status: OK, port: /dev/ttyS0, baudrate: 115200
 sensor_gps
    timestamp: 2646955303 (0.176477 seconds ago)
    timestamp_sample: 0
    latitude_deg: 0.000000
    longitude_deg: 0.000000
    altitude_msl_m: -17.000000
    altitude_ellipsoid_m: 0.000000
    time_utc_usec: 0
    device_id: 11010053 (Type: 0xA8, SERIAL:0 (0x00))

```

