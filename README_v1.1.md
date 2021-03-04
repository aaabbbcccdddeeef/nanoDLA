# nanoDLA v1.1用户手册
* [产品介绍](#产品介绍) 
* [产品特点](#产品特点)
* [软件使用](#软件安装使用)
    * [PulseView安装](#pulseview安装)
    * [驱动安装](#驱动安装)
    * [PulseView使用](#pulseview使用)
    * [协议解析](#协议解析)
* [产品链接](#产品链接)
* [FAQ](#faq)
    * [可采样多高的信号频率？](#q-可采样多高的信号频率) 
    * [支持哪些协议解析？](#q-支持哪些协议解析) 
    * [为何采样会失败？](#q-为何采样会失败) 
    * [为何无法以最大采样率采样？](#q-为何无法以最大采样率采样) 
    * [如何自行烧写固件？](#q-如何自行烧写固件) 
    * [如何获取固件源码？](#q-如何获取固件源码)
# 产品介绍
nanoDLA 是MuseLab推出硬件软件以及上位机均开源的逻辑分析仪，外观精致小巧，功能丰富，价格低廉，最高可支持24Mhz采样率，同时支持百余种协议解析。可以较好的满足电子工程师日常的开发调试需求，在问题定位、多组件的复杂系统、时序分析、性能分析等场景可以大大提升开发效率。  
<div align=center>
<img src="https://github.com/wuxx/nanoDLA/blob/master/doc/nanoDLA.jpg" width = "700" alt="" align=center />
</div>


# 产品特点
- 硬件开源，提供硬件原理图，欢迎电子爱好者自行制作
- 软件开源，提供固件源码，可自行编译固件
- 上位机开源，当前市面上的逻辑分析仪，一般使用破解上位机软件，使用上存在一些法律风险，nanoDLA依托于sigrok开源社区，使用开源的pulseview上位机，功能丰富，支持百余种协议解析，免费且开源，易于使用且功能更强
- 支持最高24Mhz采样率，8通道可同时采样，可满足日常的开发工作使用
- 支出输入电压[-0.5v, 5.25v]，其中低电平为[-0.5v, 0.8v]，高电平为[2v, 5.25v]
- 支持Windows/Linux/Mac/Android平台下使用

# 软件安装使用
在正常使用nanoDLA前，您需要为其手动安装驱动以被PulseView识别，只需先安装PulseView，然后使用PulseView自带的Zadig工具来进行安装驱动即可，具体步骤如下
## PulseView安装
本仓库的software目录下含有PulseView安装可执行文件，只需双击安装文件，连续点击下一步即可安装，在此不再赘述。
![pulseview](https://github.com/wuxx/nanoDLA/blob/master/doc/pulseview.png)

## 驱动安装
插入nanoDLA，此时会设备管理器中识别出未知设备，如图所示
![usb_device_unknown](https://github.com/wuxx/nanoDLA/blob/master/doc/usb_device_unknown.png)  
  
在开始栏中搜索zadig并打开  
![zadig_search](https://github.com/wuxx/nanoDLA/blob/master/doc/zadig_search.png)  
  
选择Options->List All Devices，上方选择对应nanoDLA的Unknown Device（USB ID为 1D50:608C），下方在驱动栏选择WinUSB驱动，点击Install Driver安装驱动即可，稍等片刻，即可成功安装驱动。  
![zadig_install1](https://github.com/wuxx/nanoDLA/blob/master/doc/zadig_install1.png)  
  
成功安装驱动后，设备可在被正常识别（尽管名字仍然为Unknown Device，然而已经被系统正常识别了）  
![usb_device_default](https://github.com/wuxx/nanoDLA/blob/master/doc/usb_device_default.png)

## PulseView使用
将nanoDLA插入PC中，然后打开PulseView，PulseView启动后，会重新对nanoDLA进行USB枚举配置，设备名也重新枚举为fx2lafw，如图所示
![usb_device_default](https://github.com/wuxx/nanoDLA/blob/master/doc/usb_device_fx2lafw.png)
PulseView使用上比较简单，在下方菜单栏中配置采样数据大小和采样率，点击左上角run按钮，即可开始采样，对于nanoDLA，最高可配置24Mhz的采样率进行工作，8通道同时进行工作
![pulseview2](https://github.com/wuxx/nanoDLA/blob/master/doc/pulseview2.png)
  
![pulseview3](https://github.com/wuxx/nanoDLA/blob/master/doc/pulseview3.png)

## 协议解析
PulseView支持百余种协议解析，采样到有效数据之后，点击菜单栏协议解析图标，在右侧窗口中选择具体的协议，点击左侧出现的协议，对协议进行具体的配置，例如以下是解析uart的例子，需要配置uart的波特率，数据奇偶校验，停止位等，配置好之后，PulseView便能解析出可视化的数据以供分析，如图所示
![pulseview_decode](https://github.com/wuxx/nanoDLA/blob/master/doc/pulseview_decode.png)

# 产品链接
[nanoDLA开源逻辑分析仪](https://item.taobao.com/item.htm?spm=a230r.1.14.4.331a393eoPAZ69&id=614150181233&ns=1&abbucket=11#detail)

# FAQ
### Q: 可采样多高的信号频率
一般来说，采样率需要至少是信号频率的五倍以上，才可采样出较完整的原始信号，所以若使用最高24Mhz采样率采样，大概可以采样出最高5Mhz左右的信号。
### Q: 支持哪些协议解析？  
支持协议列表点击[此处](https://github.com/wuxx/nanoDLA/blob/master/decoder_list.md)查看
### Q: 为何采样会失败？  
由于nanoDLA的USB工作在USB 2.0 高速模式下，带宽需求较高，假若您接在hub上进行工作，hub的质量可能无法支撑这么高的带宽需求（尤其是hub上又接了其他USB设备时），可以尝试直接接插在PC的USB上进行工作，一般均可解决。
### Q: 为何无法以最大采样率采样？
少部分windows系统可能无法以最大采样率24Mhz正常采样工作，具体表现为只能采样几百ms便停止采样，此问题与windows上的WinUSB驱动策略有关系，sigrok社区中有此问题的[bug-573](https://sigrok.org/bugzilla/show_bug.cgi?id=573)讨论。然而遗憾的是，目前最新的软件存在此问题，临时的规避方法是使用一个较低的采样率如16Mhz进行工作，此问题实验室会继续跟踪，希望能在未来的时间解决。
### Q: 如何自行烧写固件？  
nanoDLA使用的是cypress的FX2系列芯片CY7C68013A，固件存放在外置的EEPROM中，芯片支持两种启动模式C0和C2，C0模式只需在EEPROM存放8个配置字节，启动之后由上位机将最终的固件送入至FX2内部SRAM中执行，C2模式则是将固件直接存放至EEPROM中，无需外部再传入固件。目前nanoDLA采用的是C0模式（C0模式的好处是设备永远不会变砖，可随意烧录测试），只需烧录8个字节即可，具体步骤如下：  
`cd tools && source ./env.sh && cd fx2eeprom`  
`make load && make write_fx2lafw`  
具体请查看Makefile，可自行修改成不同的固件以适配其他上位机（如saleae）
### Q: 如何获取固件源码？  
请查阅 [sigrok-firmware-fx2lafw](https://github.com/wuxx/sigrok-firmware-fx2lafw)

有任何问题或者建议，请在本仓库的[Issues](https://github.com/wuxx/nanoDLA/issues)页面中提出，我们会持续跟进解决。
