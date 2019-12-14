# Selection Sort(선택 정렬)



**시간 복잡도: 최악, 최선, 평균 O(N^2)**

안정 여부: 불안정 정렬



### 동작 원리

정렬된 앞쪽을 제외하고 선택된 자리 뒤에 있는 값중에서 가장 작은 값을 선택된 자리와 바꾼다.



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

//현재 위치 보다 뒤에있는 것들중에 작은것을 골라
//현재 위치와 교체한다.
void SelectionSort(int* dataArray, int size)
{
	for (int i = 0; i < size; ++i)
	{
		int minIndex = i;
		for (int j = i+1; j < size; ++j)
		{
			if (dataArray[minIndex] > dataArray[j])
				minIndex = j;
		}

		Swap(dataArray[i], dataArray[minIndex]);
	}
}

int data[ARRAY_SIZE] = { 103,72,6,3,334,100,5,23,19,8,611 };
int main(int argc, char* argv[])
{

	SelectionSort(data, ARRAY_SIZE);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서

103 72 6 3 334 100 5 23 19 8 611

**3** 72 6 103 334 100 5 23 19 8 611 

**3 5** 6 103 334 100 72 23 19 8 611

**3 5 6** 103 334 100 72 23 19 8 611

**3 5 6 8** 334 100 72 23 19 103 611

**3 5 6 8 19** 100 72 23 334 103 611

**3 5 6 8 19 23** 72 100 334 103 611

**3 5 6 8 19 23 72** 100 334 103 611

**3 5 6 8 19 23 72 100** 334 103 611

**3 5 6 8 19 23 72 100 103** 334 611

**3 5 6 8 19 23 72 100 103 334** 611

**3 5 6 8 19 23 72 100 103 334 611**



### 출력

```
3 5 6 8 19 23 72 100 103 334 611
```





### 추가

전체를 정렬할때는 N^2의 속도가 걸리지만 선두 m개만 찾아낼때는 m*n 정도의 속도로 찾아낼 수 있다.  그렇기 때문에 어떤 정렬을 쓰더라도 이 부분에서는 더 빠를 수 있다.