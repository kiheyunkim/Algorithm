# Quick Sort(퀵 정렬)

##### 시간복잡도: 최악 O(N^2), 최선, 평균 O(n log n)

##### 안정여부: 불안정 정렬



### 동작 원리

pivot을 정하고 그 pivot을 기준으로 값을 나눈다. pivot을 가운데 옮기고 양쪽으로 나누어 분할 정복으로 진행한다.



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

//Pivot을 잡고 그 피벗을 기준으로 좌우로 나누어 가며 분할정복을 한다.
int Partitioning(int* dataArray, int left, int right)
{
	int lPivot = left, rPivot = right, pivot = right;

	while (true)
	{
		while (dataArray[lPivot] < dataArray[pivot] && lPivot <right)
			++lPivot;
		while (dataArray[rPivot] >= dataArray[pivot] && rPivot > left)
			--rPivot;

		if (lPivot >= rPivot)
			break;

		Swap(dataArray[lPivot], dataArray[rPivot]);
	}

	Swap(dataArray[lPivot], dataArray[pivot]);

	return lPivot;
}

void QuickSort(int* dataArray, int left, int right)
{
	if (right - left <= 0) return;

	int pivot = Partitioning(dataArray, left, right);
	QuickSort(dataArray, left, pivot - 1);
	QuickSort(dataArray, pivot + 1, right);
}

int data[ARRAY_SIZE] = { 103,72,6,3,611,100,5,23,19,8,334 };
int main(int argc, char* argv[])
{

	QuickSort(data, 0, ARRAY_SIZE-1);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서 ( 괄호안은 피벗이거나 교환한 자리)

103 72 6 3 334 100 5 23 19 8 (611)

**(103) 72 6 3 334 100 (5) 23 19 8 611**

**5 3 6 (8) 334 100 103 23 19 (72)** 611

**5 3 (6)** 8 334 100 103 23 19 72 611

**3 (5)** 6 8 334 100 103 23 19 72 611

**(3)** 5 6 8 334 100 103 23 19 72 611

3 5 6 8 **334 100 103 23 19 (72)** 611

3 5 6 8 **19 23 (72) 100 334 (103)** 611

3 5 6 8 **19 (23)** 72 100 334 103 611

3 5 6 8 **(19)** 23 72 100 334 103 611

3 5 6 8 19 23 72 **100 334 (103)** 611

3 5 6 8 19 23 72 **100 (103) (334)** 611

3 5 6 8 19 23 72 100 103 334 611



### 출력

```
3 5 6 8 19 23 72 100 103 334 611
```





### 추가

데이터가 일부분으로 정렬되어 있을 경우 피벗의 위치가 한쪽으로 쏠리게 되고 삽입정렬과 비슷하게 작동한다. 이를 방지하기 위해서 피벗을 한방향이 아니라 가장 앞, 가장 뒤, 중간 등으로 다양하게 잡아 이를 방지한다. 만약 정렬된 경우에는 의미 없는 정렬을 시행하기 때문에 미리 정렬상태를 검색하는 것도 방법이다.









