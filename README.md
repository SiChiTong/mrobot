# mrobot

### 主要功能：

1.电机控制

2.串口通讯

3.超声波测距

4.电池电量检测

5.蜂鸣器

6.三色LED闪烁

7.六轴传感器MPU6050

### 宏定义

_RGB：切换大小RGB-LED灯，全局定义为使用小灯，全局未定义为使用大灯，默认全局未定义

_TEST：测试按键功能，全局定义为开启测试按键功能，全局未定义为关闭测试按键功能，默认全局定义

_DOUBLE：编码器开启双精度，全局定义为开启双精度编码器，全局未定义为关闭双精度编码器，默认全局未定义

_ENABLE_MPU6050：开启MPU6050功能，全局定义为开启6050，全局未定义为关闭6050，默认全局未定义

_PRINT：串口打印信息功能，全局定义为开启通过串口打印相关信息，全局未定义为关闭打印信息，默认全局未定义（注：开启后会影响串口和车载计算机通讯功能，默认使用串口3）

_DMA_USART：DMA方式串口通讯功能，全局定义为使用DMA方式进行串口通讯，全局未定义为不使用DMA方式，默认全局定义

_REMAP：串口3重映射功能，全局定义为将串口3重映射为PC10，PC11（串口4），全局未定义为不开启串口3重映射，默认全局未定义

### 串口通信协议：

**一帧数据为：[消息头(2字节)] [命令(2字节)] [长度(1字节)] [数据(n字节，n=长度)] [校验(1字节)] [消息尾(2字节)]**

**消息头固定为[0x55 0xaa]，消息尾固定为[0x0d 0x0a]**

### 主控发送用命令参数：

(1)0x5a 0x5a：发送速度信息和电池信息

(2)0x5a 0x55：发送速度信息，电池信息和超声波信息

(3)0x5a 0xaa：发送速度信息，电池信息和六轴传感器信息

(4)0x5a 0xa5：发送速度信息，电池信息，超声波信息和六轴传感器信息

(5)0xa5 0x5a：发送速度信息

(6)0xa5 0x55：发送电池信息

(7)0xa5 0xaa：发送超声波信息

(8)0xa5 0xa5：发送六轴传感器信息

### 主控接收用命令参数：

(1)0x55 0xaa：请求发送速度信息和电池信息

(2)0x55 0x55：请求发送速度信息，电池信息和超声波信息

(3)0x55 0xa5：请求发送速度信息，电池信息和六轴传感器信息

(4)0x55 0x5a：请求发送速度信息，电池信息，超声波信息和六轴传感器信息

(5)0xaa 0xaa：请求发送速度信息

(6)0xaa 0x55：请求发送电池信息

(7)0xaa 0xa5：请求发送超声波信息

(8)0xaa 0x5a：请求发送六轴传感器信息

### 主控端发送数据段结构：

(1)0x5a 0x5a：[左轮速度（4字节浮点数），右轮速度（4字节浮点数），电池电量（4字节浮点数），电量百分比（4字节浮点数）]

(2)0x5a 0x55：[左轮速度（4字节浮点数），右轮速度（4字节浮点数），电池电量（4字节浮点数），电量百分比（4字节浮点数），前超声波（4字节浮点数），后超声波（4字节浮点数），左超声波（4字节浮点数），右超声波（4字节浮点数）]

(3)0x5a 0xaa：[左轮速度（4字节浮点数），右轮速度（4字节浮点数），电池电量（4字节浮点数），电量百分比（4字节浮点数），pitch角（4字节浮点数），roll角（4字节浮点数），yaw角（4字节浮点数），温度（4字节浮点数）]

(4)0x5a 0xa5：[左轮速度（4字节浮点数），右轮速度（4字节浮点数），电池电量（4字节浮点数），电量百分比（4字节浮点数），pitch角（4字节浮点数），roll角（4字节浮点数），yaw角（4字节浮点数），温度（4字节浮点数），前超声波（4字节浮点数），后超声波（4字节浮点数），左超声波（4字节浮点数），右超声波（4字节浮点数）]

(5)0xa5 0x5a：[左轮速度（4字节浮点数），右轮速度（4字节浮点数）]

(6)0xa5 0x55：[电池电量（4字节浮点数），电量百分比（4字节浮点数）]

(7)0xa5 0xaa：[前超声波（4字节浮点数），后超声波（4字节浮点数），左超声波（4字节浮点数），右超声波（4字节浮点数）]

(8)0xa5 0xa5：[pitch角（4字节浮点数），roll角（4字节浮点数），yaw角（4字节浮点数），温度（4字节浮点数）]

### 主控端接收数据段结构：

[左轮速度（4字节整数），右轮速度（4字节整数）]