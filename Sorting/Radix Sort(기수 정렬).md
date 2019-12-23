# Radix Sort(기수 정렬)

시간복잡도: O(최대 자리수 * n)

안정여부: 안정 정렬



### 동작 원리

일의 자리수 부터 비교하여 줄을 세우면서 정렬을 한다. 단, 각 자리수의 정렬을 할 때마다의 순서를 유지해야한다.



### 코드

```c++
#include<iostream>
#define ARRAY_SIZE 11

//Radix Sort
//각 자리를 비교한다.
int radixQueue[10][ARRAY_SIZE];	//자리수로 정렬하여 삽입
int tempRadixArray[ARRAY_SIZE];	//정렬된 숫자들을 임시로 저장
void RadixSort(int* dataArray, int size, int maxDigit)
{
	int factor = 1;	//자리수

	for (int i = 1; i <= maxDigit; ++i)
	{
		int radixQueueCount[10]{ 0, };

		for (int j = 0; j < size; ++j)	//각 자리수에 따라 정렬
		{
			radixQueue[dataArray[j] / factor % 10][radixQueueCount[dataArray[j] / factor % 10]] = dataArray[j];
			++radixQueueCount[dataArray[j] / factor % 10];
		}

		int insertIndex = 0;
		for (int j = 0; j < 10; ++j)
		{
			for (int k = 0; k < radixQueueCount[j]; ++k)
			{
				tempRadixArray[insertIndex] = radixQueue[j][k];	//정렬한 숫자들을 일렬로 나열
				++insertIndex;
			}
		}

		for (int j = 0; j < size; ++j)
			dataArray[j] = tempRadixArray[j];	//기존배열로 옮기고 반복

		factor *= 10;
	}
}

int data[ARRAY_SIZE] = { 103,72,6,3,334,100,5,23,19,8,611 };
int main(int argc, char* argv[])
{

	RadixSort(data, ARRAY_SIZE, 3);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서

100 611 72 103 3 23 334 5 6 8 19

100 103 3 5 6 8 611 19 23 334 72

3 5 6 8 19 23 72 100 103 334 611



### 출력

```
3 5 6 8 19 23 72 100 103 334 611
```



### 추가

정렬속도는 아주 빠르지만 공간을 아주 많이 쓴다.