# 添加文件右键快捷方式  

## 新建一个文件，把扩展名改为.reg，然后添加如下内容后保存，双击此文件即可  
```

Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Apps\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\*\shell\VSCode\command]
@="\"D:\\Apps\\Microsoft VS Code\\Code.exe\" \"%1\""

```

## 添加目录右键快捷方式
```

Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Apps\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\Directory\shell\VSCode\command]
@="\"D:\\Apps\\Microsoft VS Code\\Code.exe\" \"%V\""

```

[返回](../) 