//CString转string  
CString toCString( std::string str )  
{  
#ifdef _UNICODE  
//如果是unicode工程  
USES_CONVERSION;  
CString s(str.c_str());  
CString ans(str.c_str());  
return ans;  
#else  
//如果是多字节工程  
CString ans;  
ans.Format("%s", str.c_str());  
return ans;  
#endif  
}  
  
//string转CString  
std::string toString( CString cs )  
{  
#ifdef _UNICODE  
//如果是unicode工程  
USES_CONVERSION;  
std::string str(W2A(cs));  
return str;  
#else  
//如果是多字节工程   
std::string str(cs.GetBuffer());  
cs.ReleaseBuffer();  
return str;  
#endif  
}  