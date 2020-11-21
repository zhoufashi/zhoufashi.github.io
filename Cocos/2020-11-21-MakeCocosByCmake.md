#cmake创建cocos工程  

cmake -G"Visual Studio 14 2015" -Tv140 -A win32  -S "源目录" -B "目标目录"  
  
源目录 ：cocos2dx库所在的目录  

目标目录：生成项目所在目录，（但是我发现只是工程创建在这个目录，实际库文件还在源目录，并没有拷贝库过去,或许只能手动拷贝，然后当前目录创建工程了）  


1):  

cmake -G"Visual Studio 14 2015" -Tv140 -A win32 -B "目标目录"   

也可以cd到源目录，即cocos2dx所在目录，camke文件所在目录  


2):  

也可以cd到源目录工程目录，cocos2dx库所在目录创建的工程目录  

cmake .. -G"Visual Studio 14 2015" -Tv140 -A win32  


"Visual Studio 14 2015" -Tv140 这是vs版本相关的  

#python + cmake创建cocos工程  

只用cmake创建，会导致有很多其余多余的代码，而且没有其他平台的工程，所以更好的办法是先用python创建一个，然后再去用cmake创建平台工程

pyhton应用  

在cocos库的对应的 \tools\cocos2d-console\bin 目录下，打开命令行工具输入：  
cocos new programname -p com.proj.package -l cpp -d G:\CocosProject\Cocos2dX\Test22   
programname:  项目名  
com.proj.package   包名  
G:\CocosProject\Cocos2dX\Test22 生成的路径名  

然后再用cmake创建  
cmake -G"Visual Studio 14 2015" -Tv140 -A win32

目录就很简洁了

4.0以下可以只用python去创建