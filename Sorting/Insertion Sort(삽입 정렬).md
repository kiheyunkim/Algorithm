# Insertion Sort(삽입 정렬)



**시간복잡도: 최악 O(N^2), 최선 O(N), 평균 O(N^2)**

안정 여부 : 안정 정렬



### 동작 원리

정렬된 앞쪽에서 현재 선택된 값이 삽입될 위치를 찾고 그 자리에 값을 삽입하는 것을 반복한다.



### 코드

```c++
#include<iostream>
#define ARRAY_SIZE 11

void Swap(int& target1, int& target2)
{
	int temp = target1;
	target1 = target2;
	target2 = temp;
}

//이미 정렬된 부분들에 대하여 현재 선택한것이 들어갈 위치를 찾고
//그 위치에 삽입한다.
void InsertSort(int* dataArray, int size)
{
	for (int i = 1; i < size; ++i)
	{
		int insertPos = i;
		int insertData = dataArray[i];

		for (int j = i; j >= 0; --j)
			if (dataArray[j - 1] < dataArray[i])
			{
				insertPos = j;
				break;
			}

		for (int j = i; j > insertPos; --j)
			Swap(dataArray[j - 1], dataArray[j]);

		dataArray[insertPos] = insertData;
	}
}

int data[ARRAY_SIZE] = { 103,72,6,3,334,100,5,23,19,8,611 };
int main(int argc, char* argv[])
{

	InsertSort(data, ARRAY_SIZE);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서

103 72 6 3 334 100 5 23 19 8 611

**72** 103  6 3 334 100 5 23 19 8 611

**72 103** 6 3 334 100 5 23 19 8 611

**6 72 103** 3 334 100 5 23 19 8 611

**3 6 72 103** 334 100 5 23 19 8 611

**3 6 72 100 103** 334 5 23 19 8 611

**3 6 72 100 103 334** 5 23 19 8 611

**3 5 6 72 100 103 334** 23 19 8 611

**3 5 6 23 72 100 103 334** 19 8 611

**3 5 6 19 23 72 100 103 334** 8 611

**3 5 6 8 19 23 72 100 103 334** 611

**3 5 6 8 19 23 72 100 103 334 611**



### 출력

```
3 5 6 8 19 23 72 100 103 334 611
```

























