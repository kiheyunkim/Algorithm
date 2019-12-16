# Merge Sort(병합 정렬)

**시간복잡도: 최악, 최선, 평균 O(n log n)**

**안정여부:  안정 정렬**



### 동작 원리

2개에서 1개까지 분할을 한다음 2개씩 묶어서 정렬을 한다.



### 코드

```c++
#include<iostream>
#define ARRAY_SIZE 11

//1개까지 분할한다음 2개씩 묶으면서 정렬한다.
int tempArray[ARRAY_SIZE];
void ReArrange(int* dataArray, int left, int mid, int right)
{
	int count = right - left + 1;
	int lPivot = left, rPivot = mid;
	int insert = left;
	while (--count)
	{
		int val1 = INT_MAX, val2 = INT_MAX;

		if (lPivot < mid)
			val1 = dataArray[lPivot];
		if (rPivot < right)
			val2 = dataArray[rPivot];

		if (val1 < val2)
		{
			tempArray[insert] = val1;
			++lPivot;
		}
		else
		{
			tempArray[insert] = val2;
			++rPivot;
		}

		++insert;
	}

	for (int i = left; i < right; ++i)
		dataArray[i] = tempArray[i];
}

void MergeSort(int* dataArray, int left, int right, int size)
{
	if (size <= 1)
		return;

	MergeSort(dataArray, left, left + size / 2, size / 2);
	MergeSort(dataArray, left + size / 2 , right, size - size / 2);
	ReArrange(dataArray, left, left + size / 2, right);
}

int data[ARRAY_SIZE] = { 103,72,6,3,334,100,5,23,19,8,611 };
int main(int argc, char* argv[])
{

	MergeSort(data,0, ARRAY_SIZE, ARRAY_SIZE);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서

103 72 6 3 334 100 5 23 19 8 611

**72 103** 6 3 334 100 5 23 19 8 611

72 103 **3 6 334** 100 5 23 19 8 611

**3 6 72 103 334** 100 5 23 19 8 611

3 6 72 103 334 **5 23 100** 19 8 611

3 6 72 103 334 5 23 100 **8 19 611**

3 6 72 103 334 **5 8 19 23 100 611**

**3 5 6 8 19 23 72 100 103 334 611**



### 출력

```
3 5 6 8 19 23 72 100 103 334 611
```

