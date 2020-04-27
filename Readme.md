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
注释掉#define MIN_SOFTWARE_ENDSTOPS并上传固件
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
STEP5:Send M280 P0 S"degree" to get the best degree of laying down(vertical) and packing up.Just like the image<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/51.png?raw=true)<br/>![](https://github.com/Charkim-Pun/IMAGES/blob/master/52.png?raw=true)<br/><br/>


第6步：在热床尽量靠中心的地方贴一张纸画一个小点。<br/>
STEP6:Stick a piece of paper in the middle of the bed and draw a little point.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/6.png?raw=true)<br/><br/>

第7步：输入M280 P0 S（放下舵机臂的角度）<br/>
STEP7:Send M280 P0 S"LAYING DOWN"<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/51.png?raw=true)<br/><br/>

第8步：把Z降到小点的正上方后，在显示屏选择运动——关闭步进电机，手动把XY移动到如图所示位置。<br/>
STEP8:Lower the Z over the point, shutdown the Steper and move manually XY to the point.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/8.png?raw=true)<br/><br/>

第9步：回到显示屏的移动Z轴，一次一次地慢慢-0.025mm，直到听到限位开关被按压的声音为止。<br/>
STEP9:Lower the Z by 0.025mm,til you can hear the switch pressed sound.<br/><br/>

第10步：输入G92 X0 Y0 Z0，再输入输入M280 P0 S（收起舵机臂的角度）<br/>
STEP10:Send G92 X0 Y0 Z0,M280 P0 S(Packing Up)<br/><br/>

第11步：通过显示屏或者上位机来移动XYZ，使得喷头刚刚好处于小点的上面一点点（不能贴到热床，如果没把握就高一点点，不需要太精准，后续再调），输入M114并记录下来。<br/>
STEP11:Move the Nozzle over the point by the Software or the LCD. The nozzle cant touch the bed. Send M114 to record the location.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/11.png?raw=true)<br/>![](https://github.com/Charkim-Pun/IMAGES/blob/master/11-1.png?raw=true)<br/><br/>

第12步：回到固件，填入刚刚记录下来的舵机角度和偏移量，并去掉软限位的注释符。重新上传固件，上传完了输入M502(重置EEPROM)<br/>
STEP12:Open the firmware and fill in the Degree and Offset,enable "#define MIN_SOFTWARE_ENDSTOPS".Then upload the firmware and Send M502 to reset the EEPROM.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/12.png?raw=true)<br/><br/>

第13步：在显示屏选择调平热床，调平结束后，然后选择保存设置，然后按一下RAMPS上的RESET按钮重启系统。<br/>
STEP13:Select Leveling Bed on the LCD, after that Select Save.The Press REBOOT botton on the motherboar.<br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/13.png?raw=true)<br/><br/>

第十四步：在切片软件打印机的设置起始G-code添加命令<br/>
M420 L <br/>
M420 S <br/>
M420 V <br/>
STEP14:Edit the starting G-code in the cutting software,add:<br/>
M420 L <br/>
M420 S <br/>
M420 V <br/><br/><br/>

Finished!<br/><br/><br/><br/><br/>



你可以在这里设置喷头的高度差，然后保存重启。-往下 +往上<br/>
You can set the Z offset here then save and reboot  *- down + up <br/>
![](https://github.com/Charkim-Pun/IMAGES/blob/master/145.png?raw=true)<br/><br/><br/>

你可以在固件这里设置探测热床的点数(点数越多调平越精准)<br/>
You can set the point of Probe point here(More points better)<br/>

#if EITHER(AUTO_BED_LEVELING_LINEAR, AUTO_BED_LEVELING_BILINEAR)<br/>

  // Set the number of grid points per dimension.<br/>
  #define GRID_MAX_POINTS_X 10 //数量<br/>
  #define GRID_MAX_POINTS_Y 10<br/>
