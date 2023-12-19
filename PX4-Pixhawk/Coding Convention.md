### Naming Convention

1. `__Underscore`

   表示這是一個class的private member， *e.g. _gain_vel_p*

2. `_s`

   uORB message 的結尾都是 _s， *e.g. vehicle_command_s*

3. `_pub / _sub`

   uORB publish and subscribe topic 會用這兩個 postfix 表示， *e.g. vcmd_pub (vehicle command publish)*

4. 參數

   最長16字元且全大寫，定義在`"<Module_name>_params.c"`的文件內，*e.g. MC_PITCH_P (multicopter pitch p gain)*

5. 變數

   變數用snake case，*e.g. rate_setpoint*

6. 函數

   函數用camel case， *e.g. setProportionalGain()*

---

### PX4 Build-in Functions

1. __PX4_INFO : 等同printf()
1. __EXPORT : 函數輸出到linker
1. __PX4_ERR : print error message 
