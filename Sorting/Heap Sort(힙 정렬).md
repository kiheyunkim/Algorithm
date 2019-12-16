# Heap Sort(힙 정렬)

**시간복잡도: 최악, 최선, 평균 O(n log n)**

**안정여부: 불안정 정렬**



### 동작 원리

heap이라는 자료구조는 항상 root에 가장 작거나 가장 큰 값이 오게 만든다. 그렇기에 모든 수를 heap에 넣은다음 pop을 시켜 정렬시킨다.



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

//힙의 정렬 됨을 이용해서 정렬을 함.
int heapArray[ARRAY_SIZE + 1];
int heapIndex = 1;
void HeapPush(int data)
{
	int cur = heapIndex;
	heapArray[heapIndex++] = data;
	
	while (cur != 1)
	{
		if (heapArray[cur] < heapArray[cur / 2])
			Swap(heapArray[cur], heapArray[cur / 2]);
		else
			break;

		cur /= 2;
	}
}

int HeapPop()
{
	int retval = heapArray[1];
	heapArray[1] = heapArray[--heapIndex];

	int cur = 1;
	while (true)
	{
		if (heapArray[cur] > heapArray[cur * 2] && cur * 2 < heapIndex && heapArray[cur * 2] < heapArray[cur * 2 + 1])
		{
			Swap(heapArray[cur], heapArray[cur * 2]);
			cur = cur * 2;
		}
		else if (heapArray[cur] > heapArray[cur * 2 + 1] && cur * 2 + 1 < heapIndex && heapArray[cur * 2] > heapArray[cur * 2 + 1])
		{
			Swap(heapArray[cur], heapArray[cur * 2 + 1]);
			cur = cur * 2 + 1;
		}
		else
			break;
	}

	return retval;
}

void HeapSort(int* dataArray, int size)
{
	for (int i = 0; i < size; ++i)
		HeapPush(dataArray[i]);
	for (int i = 0; i < size; ++i)
		dataArray[i] = HeapPop();
}

int data[ARRAY_SIZE] = { 103,72,6,3,334,100,5,23,19,8,611 };
int main(int argc, char* argv[])
{

	HeapSort(data, ARRAY_SIZE);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서

3 5 6 8 19 23 72 100 103 334 611



### 출력

```
3 5 6 8 19 23 72 100 103 334 611
```

