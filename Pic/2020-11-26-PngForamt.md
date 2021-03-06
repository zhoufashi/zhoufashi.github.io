# png的格式解析

png的官网：<http://www.libpng.org/pub/png/>

文件头 (8字节): 89 50 4E 47  0D 0A 1A 0A
文件尾 (8字节)：AE 42 60 82  


## 数据组成  

###  关键数据块 : 关键数据块是必不可少的数据块 ;
- IHDR 数据块 : 文件头数据块 , 描述文件的相关信息
- IDATA 数据块 : 图像数据块 , 存储图像的具体的像素颜色数据
- IEND 数据块 : 图像结束数据块 , 是 PNG 文件的最后一个数据块 ;  
- 数据块类型有很多种此处不再详细说明名 ;
### 辅助数据块 : 该类型数据块是可选的 ;


## 数据块结构
    数据块结构 : 每个数据块由 4 部分组成 :

- 1.Length ( 长度 ) : 大小 4 字节 , 数据块的长度 , 取值范围 [ 0 , 2^31 − 1 ]
- 2.Chunk Type Code ( 数据块类型码 ) : 大小 4 字节 , 数据块的类型由 A~Z 和 a ~ z 等 4 个 ASCII 编码的字母组成 ;
- 3.Chunk Data ( 数据块数据 ) : 大小是在 Length 中设置的大小 , 存储对应类型的数据 ;
- 4.CRC ( 循环冗余监测信息 ) : 大小 4 字节 , 全称 cyclic redundancy check , 对 Chunk Type Code 和 Chunk Data 进行计算得到的 , 用来校验数据完整性 ;




## IHDR 数据块 简介



### IHDR 数据块简介 :

- 1.IHDR 数据块作用 : 文件头数据块 , 存储图像数据的基本信息 , 是 PNG 文件的第一个数据块 , 该类型数据块只能有一个 ;

- 2.数据块大小 : 该数据块由 13 字节组成 , 分为 7个部分 ;  

```
struct PNG_IHDR {
	int Width;
	int Height;
	char BitDepth;
	char ColorType;
	char Comethod;
	char Filthod;
	char Interthod;
	char CRC[4];
}IHDR;
```

## IHDR 数据块 结构 :

- 1.Width ( 宽度 ) : 4 Bytes , 图像的宽度 , 单位 : 像素 ;
- 2.Height ( 高度 ) : 4 Bytes , 图像的高度 , 单位 : 像素 ;
- 3.Bit depth ( 位深度 ) : 1 Byte , 图像深度 ; 下面是位深度的取值范围 :  
     ① 真彩色图像 : 8 位 , 16 位 ;  
     ② 灰度图像 : 1 位 , 2 位 , 4 位 , 8 位 , 16 位 ;  
     ③ 索引彩色图像 : 1 位 , 2 位 , 4 位 , 8 位 ;  
- 4.ColorType ( 颜色类型 ) : 1 Byte , 下面是可取值的范围和意义 :   
     ① 类型 0 : 灰度图像 ;  
     ② 类型 2 : 真彩色图像 ;  
     ③ 类型 3 : 索引彩色图像 ;  
     ④ 类型 4 : 带 α \alphaα 通道数据的灰度图像 ;  
     ⑤ 类型 6 : 带 α \alphaα 通道数据的真彩色图像 ;  
- 5.Compression method ( 压缩方法 ) : 1 Byte , 使用 LZ77 压缩算法 ;
- 6.Filter method ( 滤波器方法 ) : 1 Byte ;
- 7.Interlace method ( 扫描方法 ) : 1 Byte , 可取值的选择 :  
     ① 方法 0 : 非隔行扫描法 ;  
    ② 方法 1 : Adam7 扫描方法 ( 7遍隔行扫描方法 ) ; 