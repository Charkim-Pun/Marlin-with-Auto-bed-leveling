# Marlin-with-Auto-bed-leveling
You just need a Servo motor AND a Switch for doing this!



-------------------------------------------------------------Tutorial-------------------------------------------------------------------<br/>
第1步:<br/>准备一个舵机和打印件，舵机的延伸臂一定要比喷头还早碰到热床并安装好（任何一个部件都一定要很牢固不能松动）不一定要和图片中的一模一样。<br/>
STEP1:<br/>Prepare a servo and printing models, the arm of the servo must reach to the bed before the nozzle.Every parts should be very sturdy.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/1.png?raw=true)<br/><br/>
第2步：<br/>舵机臂上的限位开关接到主板上的Z-min（红色框）（取代原来的Z的限位开关）<br/>
       舵机接到SERVOS的第一个（蓝色框），注意正负，通常黄色是信号线，棕色是负<br/>
       短接主板上的5V和VCC以给舵机供电（橙色框），可以用细分跳线帽。<br/>
STEP2:<br/>
   Connect swtich to the motherbord(RED)<br/>
   Connect servo to the motherbord,the yellow one is the sinal cable(BLUE)<br/>
   Short circuit 2Pins(Orange)<br/>
   ![](https://github.com/Charkim-Pun/IMAGES/blob/master/2.png?raw=true)<br/><br/>
第3步：<br/>
注释掉#define MIN_SOFTWARE_ENDSTOPS并上传固件<br/>

STEP3:<br/>
disable "#define MIN_SOFTWARE_ENDSTOPS" and upload the firmware to the board.<br/><br/>
  //#define MIN_SOFTWARE_ENDSTOPS<br/>
  //软限位<br/>
  #if ENABLED(MIN_SOFTWARE_ENDSTOPS)<br/>
    #define MIN_SOFTWARE_ENDSTOP_X<br/>
    #define MIN_SOFTWARE_ENDSTOP_Y<br/>
    #define MIN_SOFTWARE_ENDSTOP_Z<br/>
  #endif<br/><br/>
  
第4步：打开ARDUINO IDE，如图设置<br/>
STEP4:Open the ARDUINO IDE,SET UP AS THE IMAGE.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/4.png?raw=true)<br/><br/>

第5步：用    M280 P0 S角度   来获取最佳的放下和收起角度并记录起来，注意舵机臂撞车（有一定概率导致电流过大烧坏AMS1117芯片，最好10度10度调来确定方向）。
以下是我的角度，每个人的可能不一样，自己试出来。放下的时候舵机臂尽量与热床垂直，收起的话就不要低于喷头就行了。<br/>
Send M280 P0 S"degree" to get the best degree of laying down and packing up.Just like the image<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/51.png?raw=true)![](https://github.com/Charkim-Pun/IMAGES/blob/master/52.png?raw=true)
