```
//格式化字符串  
std::string FormatString( const char *str,... )  
{  
char msg[1024] = { 0 };  
va_list pArgList;   
va_start(pArgList, str);   
int nSize = vsprintf_s(msg, str, pArgList);   
va_end(pArgList);   
if (nSize==0){   
return "";   
}   
std::string strData = string(msg,nSize);   
//char *pData = new char[iSize];   
//memset(pData,0,sizeof(char)*iSize);   
//strcpy(pData,msg);   
//pData->pData[nSize]='\0';   
return strData;   
}   
```



[返回](https://zhoufashi.github.io/) 