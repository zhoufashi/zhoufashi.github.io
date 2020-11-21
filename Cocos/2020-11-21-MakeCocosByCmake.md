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

