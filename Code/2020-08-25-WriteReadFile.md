`
//写
FILE* pf = fopen(strFile.c_str(), strMode.c_str());
if (!pf)
{
	return false;
}

fwrite(strData.c_str(), strData.size(), 1, pf);
fflush(pf);
fclose(pf);
return true;



//读
FILE* pf= fopen(filePath.c_str(),"rb");
if (!pf){
	return;
}
fseek(pf, 0, SEEK_END);
int iSize = ftell(pf);

fseek(pf, 0, SEEK_SET);
char* pData = (char*)malloc(iSize);
memset(pData,0,iSize);
fread(pData, 1, iSize, pf);
fclose(pf);
strData=string(pData,iSize);
free(pData);
`