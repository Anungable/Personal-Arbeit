## Architecture

**Modularity in PX4：**

1. All the flight tasks are specified at the top level (called APP in PX4) and all of them use the same position/attitude controller. But of course, each airframe has its own control schemes thus had developed in different files.

   (Ref path： /src/modules).

2. Class

3. Template

4. uORB

## Parameter

Ref: https://docs.px4.io/main/en/advanced/parameters_and_configurations.html

### Define

e.g. `PARAM_DEFINE_FLOAT(MC_ROLLRATE_MAX, 220.0f);`

```c++
/**
 * Max roll rate
 *
 * Limit for roll rate in manual and auto modes (except acro).
 * Has effect for large rotations in autonomous mode, to avoid large control
 * output and mixer saturation.
 *
 * This is not only limited by the vehicle's properties, but also by the maximum
 * measurement rate of the gyro.
 * 以下是這個參數定的設定，會顯示在QGC上
 * @unit deg/s
 * @min 0.0
 * @max 1800.0
 * @decimal 1
 * @increment 5
 * @group Multicopter Attitude Control //group會顯示在QGC中參數的sidebar
 * //把這裡的source code寫到QGC上是透過Metadata
 */
PARAM_DEFINE_FLOAT(MC_ROLLRATE_MAX, 220.0f);
```

### Access

1. access

```c++
// include
#include <px4_platform_common/module_params.h> //get DEFINE_PARAMETERS macro
#include <uORB/topics/parameter_update.h> //access to parameter_update
#include <uORB/Subscription.hpp> //access to uORB 訂閱API
```

定義參數：derived class from `ModuleParams`

```c++
class MyModule : public ModuleParams //derived class
{
public:
	...

private:

	/**
	 * Check for parameter changes and update them if needed.
	 */
	void parameters_update();

	DEFINE_PARAMETERS( //使用macro
		(ParamInt<px4::params::SYS_AUTOSTART>) _sys_autostart,   /**< example parameter */
		(ParamFloat<px4::params::ATT_BIAS_MAX>) _att_bias_max  /**< another parameter */
	)

	// Subscriptions
	uORB::SubscriptionInterval _parameter_update_sub{ORB_ID(parameter_update), 1_s};

};

```

2. check param有無更新

```c++
void Module::parameters_update()
{
	if (_parameter_update_sub.updated()) { //check if there is any update to param_update 
		parameter_update_s param_update;
		_parameter_update_sub.copy(&param_update); //有更新個話將更新的數據copy到param_update

		// If any parameter updated, call updateParams() to check if
		// this class attributes need updating (and do so).
		updateParams(); //更新DEFINE_PARAMETERS list
	}
}
```

## Task and Work Queue Task

Ref: https://docs.px4.io/main/en/modules/module_template.html

PX4有提供template，可直接套用：src/examples/work_item **&** src/templates/template_module 

### Task

有自己的stack和priority，使用時機：

- Accessing parameters and reacting to parameter updates.

- uORB subscriptions and waiting for topic updates.

- Controlling the task that runs in the background via `start`/`stop`/`status`.

- Command-line argument parsing.

- Documentation: the `PRINT_MODULE_*` methods serve two purposes

  They are used to print the command-line usage when entering `module help` on the console.

  They are automatically extracted via script to generate the [Modules & Commands Reference](https://docs.px4.io/main/en/modules/modules_main.html) page.

<font color='orange'>使用方式：</font>

建立新task : `px4_task_spawn_cmd()`

### Work queue task 

For lower consumption on CPU and RAM, suitable for regular task (e.g. sensor data reading)
Work queue 中的所有task (thread) 共享priority，無法切換對方->所以無法使用`sleep()`, `poll()` ....。可以按週期或透過uORB更新數據。

<font color='orange'> 使用方式：</font>

1. 若某個module要使用work queue task，需要在這個module的cmakelist裡面增加depends :

```txt
px4_add_module(
	MODULE modules__manual_control
	MAIN manual_control
	COMPILE_FLAGS
	SRCS
	ManualControl.cpp
		ManualControl.cpp
		ManualControl.hpp
		ManualControlSelector.hpp
		ManualControlSelector.cpp
	DEPENDS
		hysteresis
		px4_work_queue 
	)
```

2. 在declare module class時也需要derived from **px4::ScheduleWorkItem**

```c++
class ManualControl : public ModuleBase<ManualControl>, public ModuleParams, public px4::ScheduledWorkItem
```

## Module

Moduels are derived from `ModuleBase`來管理module中共通的一些函數 (e.g. start, stop, status...)

下圖是啟動機制：
Ref: https://blog.csdn.net/m0_58880384/article/details/123462988

<img src="https://img-blog.csdnimg.cn/7905cb8e66cd47089ba2360a8750082d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAbTBfNTg4ODAzODQ=,size_14,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:67%;" />





