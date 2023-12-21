## uORB (Micro Object Request Broker)

### Description

PX4透過pub()/sub() messaging API處理sensors和modules之間的數據傳輸，和外部的通訊則透過MAVLink進行。這篇文件主要是介紹uORB在PX4內的使用方式。

Pilot2.5 中各模塊間數據主要是透過pointer+include header file的方式來溝通，在PX4則是使用ORB的方式。ORB作為數據的"hub"，每個模塊產生的數據會publish到這個hub中，其他的模塊則可以透過hub來subscribe這個數據，優點：

1. Decoupled, highly modularized : communication和module application是分開的，比較容易維護和修改
2. 更容易track各數據的動向，e.g. 這個link可以看出各訊號publish and subscribe的關係 https://docs.px4.io/main/en/middleware/uorb_graph.html

![PX4/Pixhawk---uORB深入理解和应用-CSDN博客](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRTCfRlLBPTO2WMSD-3CKTzRT06XrEYn5ipN7PBWW7j4OLp1c-b733hyU8gpAB70p57gNg&usqp=CAU)

`*_multi`: 同一個topic可以publish不同的"channel" (e.g. 多個sensors會publish出不同的數據，但可以共用同個topic，subscriber透過multi去選擇要接收那一個channel)

---

### How to Use - 現有的Topic

#### Add topic

1. create new msg under `/msg` directory

2. add file name to `msg/CMakeLists.txt` -> 用python自動生成相應的c/c++

3. use topic in code : 

   ```c++
   #include <uORB/topics/topic_name.h>
   ```

#### Example : Position controller

##### Subscribe

##### Publish

---

### How to Use - 新增Topic



---

### Reference

https://px4.io/px4-uorb-explained-part-2/

https://mp.weixin.qq.com/s?__biz=Mzg4MjY2MDM5NQ==&mid=2247483726&idx=1&sn=b9c2c874df379c1b633a2e8bda17fd58&chksm=cf52040af8258d1c0bb3291f3ee6df8de18deca0432edb38faa0ce29023408e45785cd0192a3&scene=21#wechat_redirect

https://blog.csdn.net/qq_42955211/article/details/113666959
