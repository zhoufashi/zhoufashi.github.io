```
//声明
//冒泡排序
void BubbleSort(int iNum[],int iLen);
//选择排序
void SelectionSort(int iNum[],int iLen);

//插入排序
void InsertionSort(int iNum[],int iLen);

//希尔排序
void ShellSort(int iNum[],int iLen);

//归并排序
void MergeSort(int iNum[],int iLen);

//快速排序
void QuickSort(int iNum[],int iLen);

//堆排序
void HeapSort(int iNum[],int iLen);




//实现
//冒泡排序
void BubbleSort(int iNum[],int iLen){
	for (int i = 0;i<(iLen-1);i++)
	{
		for (int j = 0;j<(iLen-1);j++)
		{
			if (iNum[j] > iNum[j+1])
			{
				int t = iNum[j+1];
				iNum[j+1] = iNum[j];
				iNum[j] = t;
			}
		}
	}
}
//选择排序
void SelectionSort(int iNum[],int iLen){
	for (int i = 0;i<(iLen-1);i++)
	{
		int imin = i;//减少数据交换
		for (int j = i+1;j<iLen;j++)
		{
			if (iNum[imin] > iNum[j])
			{
				imin = j;
			}
		}
		int t = iNum[i];
		iNum[i] = iNum[imin];
		iNum[imin] = t;
	}
}

void InsertionSort( int iNum[],int iLen )
{
	for (int i = 1;i<iLen;i++)
	{
		int iValue = iNum[i];
		int j = i - 1;
		for (;j>=0;j--)
		{
			if (iValue < iNum[j])
			{
				iNum[j+1] = iNum[j];
			}
			else{
				break;
			}
		}
		j++;
		iNum[j] = iValue;
	}
}

void ShellSort( int iNum[],int iLen )
{
	int increment = 1;
	while (increment < iLen / 3) {
		increment = 3 * increment + 1;
	}
	while (increment >= 1)
	{
		for (int i = 1;i<iLen;i++)
		{
			int iValue = iNum[i];
			int j = i - increment;
			for (;j >= 0;j -= increment)
			{
				if (iValue < iNum[j] )
				{
					iNum[j+increment] = iNum[j];
				}
				else{
					break;
				}
			}
			j+= increment;
			iNum[j] = iValue;
		}
		increment = increment/3;
	}
}

void MergeSortIter( int iNum[],int iStart,int iEnd,int iTemp[])
{
	if ((iEnd - iStart) == 1)
	{
		if (iNum[iEnd] < iNum[iStart])
		{
			int t = iNum[iEnd];
			iNum[iEnd] = iNum[iStart];
			iNum[iStart] = t;
		}
	}
	else if ((iEnd - iStart) == 0)
	{
		return;
	}
	else{
		int imid = (iEnd - iStart)/2 + iStart;
		MergeSortIter(iNum,iStart,imid ,iTemp);
		MergeSortIter(iNum,imid+1,iEnd ,iTemp);

		for (int i = iStart;i<=iEnd;i++)
		{
			iTemp[i] = iNum[i];
		}
		int iLen = iEnd - iStart+1;
		int i = iStart;
		imid++;
		for (;i<iEnd;i++)
		{
			if (imid > iEnd)
			{
				iNum[i] = iTemp[iStart];
				iStart++;
			}
			else if (iStart >= imid)
			{
				iNum[i] = iTemp[imid];
				imid++;
			}
			else{
				if (iTemp[iStart] > iTemp[imid])
				{
					iNum[i] = iTemp[imid];
					imid++;
				}
				else{
					iNum[i] = iTemp[iStart];
					iStart++;
				}
			}	
		}
	}
}
void MergeSort( int iNum[],int iLen )
{
	int *pNum = new int[iLen];
	MergeSortIter(iNum,0,iLen-1,pNum);
	delete []pNum;
}
void QuickSortIter( int iNum[],int iStart,int iEnd)
{
	if (iStart >= iEnd)
	{
		return;
	}
	//printData(iNum,iStart,iEnd,"QuickSortStart");
	int iValue = iNum[iStart];
	//int i = iStart + 1;
	int low = iStart;
	int high = iEnd;
	while(low < high)
	{
		while (high > low  && iNum[high] >= iValue)
		{
			high--;
		}
		if (high > low)
		{
			iNum[low] = iNum[high]; 
		}
		while (low < high && iNum[low] <= iValue)
		{
			low++;
		}
		if (high > low)
		{
			iNum[high] = iNum[low]; 
		}
	}
	iNum[high] = iValue;
	//printData(iNum,iStart,iEnd,"QuickSortEnd");
	if (iEnd - iStart > 1)
	{
		QuickSortIter(iNum,iStart,high);
		QuickSortIter(iNum,high+1,iEnd);
	}
}
void QuickSort( int iNum[],int iLen )
{
	QuickSortIter(iNum,0,iLen-1);
}

void HeapSort( int iNum[],int iLen )
{
	//int index = 0;
	
}

```
[返回2](../) 