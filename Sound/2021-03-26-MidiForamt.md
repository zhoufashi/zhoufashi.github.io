# Midi的格式解析  <文件头块> + <音轨块数据>
 <https://www.jianshu.com/p/31d02765e1ec>
 <https://blog.csdn.net/lchunli/article/details/5765138?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_baidulandingword-1&spm=1001.2101.3001.4242>
文件头块：
<标志符串>(4字节) + <头块数据区长度>(4字节) + <头块数据区>(6字节)
MThd ＜数据长度＞ ＜Header数据＞    //首部块
音轨块
<标志符串>(4字节) + <音轨块数据区长度>(4字节) + <音轨块数据区>(多个MIDI事件构成)
 Mtrk ＜数据长度＞ ＜Track数据＞     //音轨块
 
 MIDI事件 一个状态字节 + 多个数据字节 构成
  状态字节可以理解为方法，数据字节可以理解为这个方法的参数。状态字节的最高位永远为1，因为它的范围介于128~ 255之间，而数据字节最高位永远为0

消息根据性质可分成通道消息和系统消息两大类
通道消息是对单一的MIDI Channel起作用，其Channel是利用状态字节的低 4 位来表示，从0~F共有16个
 
 每个音轨最后肯定是以00 FF 2F 00结束，因为这是一个音轨结束事件

midi好像乐谱一样，记载的是乐器号，音符，力度
### 每个 Midi 文件的开头都有如下内容它们的十六进制代码为:“4d 54 68 64 00 00 00 06 ff ff nn nn dd dd”。
- 前四个是ASCII字符“MTrk” -- “4D 54 72 6B”，用来鉴别是否为Midi文件;

- 随后的四个字节是指明文件头描述部分的字节数，总是6，所以一定是“00 00 00 06”；

- ff ff 指定 Midi 的格式  
   00 00 单音轨  
   00 01 多音轨,且同步。这是最常见的  
   00 02 多音轨,但不同步

- nn nn 指定轨道数  
  实际音轨数加上一个全局的音轨 
- dd dd 指定基本时间  
  一般为 120(00 78),即一个四分音符的 tick 数,tick 是 MIDI 中的最小时间单位
   0为采用ticks计时，后面的数据为一个4分音符的ticks
   1为SMPTE格式计时，后面的数值则是定义每秒中SMTPE帧的数量及每个SMTPE帧的tick

  全局音轨包括歌曲的附加信息(比如标题和版权)、歌曲速度和系统码(Sysx)等内容。

音轨块的标志符串为"MTrk"，也是记录ASCII码，用十六进制表示就是4d 54 72 6b。音轨块数据区长度也为固定4字节，指定后面的数据区长度

#### 每一个数据都有相同的结构：时间差+事件
##### 时间差
- 指的是前一个事件到该事件的时间数,它的单位是 tick(MIDI 的最小时间单位) 
  一个字节有 8 位,如果仅使用 7 位,它可以表示 0~127 这 128 个数,而剩下的一位,则用来作为标志
  65535tick --> 65535=128^2*3+128^1*127+128^0*127  16进制表示 83 FF 7F
  只要标志位为 0,则表示结束读取时间差

  比如 82 C0 03 表示 1282*2+1281*64+1280*3=40963,如果基本时间为 120,则有 341:043 个四分音符
  341 * 120 + 043 = 40963

记录整数的字节称为动态字节

##### 事件
   分为音符、控制器和系统信息( 种类+参数)
  
  （通道消息）X为0~16.
  种类  参数(十六进制)
  //字节，含义     参数
- 8x 松开音符  音符(00~7F):松开的音符 力度:00~7F  
- 9x 按下音符 音符(00~7F):按下的音符  力度:00~7F
- Ax 触后音符  
- Bx 控制器
- Cx 改变乐器
- Dx 触后通道
- Ex 滑音 音高(Pitch)低位:Pitch mod 128
- F0 系统码 系统码字节数:动态字节，系统码:不含开头的 F0,但包括结尾的 F7
- FF 其他格式
- 00~7F 上次激活格式的参数(8x、9x、Ax、Bx、Cx、Dx、Ex)  
  特殊的状态字节FF,表示非MIDI事件(Non- MIDI events)，也叫meta-event（元事件）  
  FF + <种类字节>(1字节) + <数据字节长度> + <数据字节>


默认一个四分音符 等于 120tick
  可设置 48...(+24)

拍速BPM 拍/分   拍速100 ，每分钟100拍

拍号 多少音符一拍 3/8 中以8分音符为1拍

一个完全音符等于两个二分音符；等于四个四分音符，八个八分音符；十六个十六分音符，三十二个三十二分音符