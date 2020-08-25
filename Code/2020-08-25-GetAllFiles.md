```
//得到文件目录  
void GetAllFile( std::string root, list<string>& files,bool bFile ,std::string addpath,bool bFullPath,int iLevel )  
{ 
		_finddata_t FileInfo;  
		std::string fullpath = root;  
		if (!addpath.empty())  
		{  
			fullpath = root + "\\" + addpath;  
		}	  
		string strfind = fullpath;  
		strfind +="\\*";  
		long Handle = _findfirst(strfind.c_str(), &FileInfo);  
		  
		  
			if (Handle == -1L)  
			{  
			  cerr << "can not match the folder path" << endl;  
			  exit(-1);  
			}  
		 do{  
		//判断是否有子目录  
		if (FileInfo.attrib & _A_SUBDIR)      
		{  
			//这个语句很重要  
			if( (strcmp(FileInfo.name,".") != 0 ) &&(strcmp(FileInfo.name,"..") != 0))     
			{  
				bool bSkip = false;  
				string strName = FileInfo.name;  
				if (strName.find("aaaa")!=std::string::npos)  
				{  
					bSkip = true;  
				}  
				if ( 0 == iLevel)//第一级检测目录，后面不用在检测  
				{  
				}  
				if (!bSkip){  
					std::string adddir =  addpath;  
					if (!adddir.empty())  
					{  
						adddir +="\\" ;  
					}	  
					adddir += FileInfo.name;  
					if (!bFile)  
					{  
						if (bFullPath)  
						{  
							files.push_back(root + "\\" + adddir);  
						}  
						else{  
							files.push_back(adddir);  
						}  
					}  
	  
					GetAllFile(root,files,bFile,adddir,bFullPath,bCheckGame,iLevel+1);  
				}  
			}  
		}  
		else    
		{					  
			if (bFile)  
			{  
				std::string filename =  addpath;  
				if (!filename.empty())  
				{  
					filename +="\\" ;  
				}	  
				filename += FileInfo.name;  
	  
				if (bFullPath)  
				{  
					filename = root + "\\" + filename;  
				}  
				else{  
					filename = filename;  
				}  
				files.push_back(filename);  
			}  
		}  
	}while (_findnext(Handle, &FileInfo) == 0);  
	  
	_findclose(Handle);  
} 
```