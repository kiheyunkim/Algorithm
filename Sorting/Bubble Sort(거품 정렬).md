# Bubble Sort(거품 정렬)

**시간복잡도: 최악, 최선, 평균 O(N^2)**

**안정여부: 안정 정렬**



### 동작 원리

바로 옆에 있는 값과 비교하여 옆이 더 작다면 교환하는것을 반복한다.



### 코드

```c++
#include<iostream>
#define ARRAY_SIZE 5

void Swap(int& target1, int& target2)
{
	int temp = target1;
	target1 = target2;
	target2 = temp;
}

//바로 뒤에 있는 데이터와 비교하여 교체한다.
//이를 N번 반복하면 정렬이 된다.
//한번의 PASS동안 교체가 없으면 정렬이 이미 되었다고 본다.
void BubbleSort(int* dataArray, int size)
{
	for (int i = 0; i < size; ++i)
	{
		bool isChanged = false;

		for (int j = 0; j < size - i - 1; ++j)
			if (dataArray[j] > dataArray[j + 1])
			{
				Swap(dataArray[j], dataArray[j + 1]);
				isChanged = true;
			}

		if (!isChanged)
			break;
	}
}

int data[ARRAY_SIZE] = { 103,72,6,3,334};
int main(int argc, char* argv[])
{

	BubbleSort(data, ARRAY_SIZE);

	for (int i = 0; i < ARRAY_SIZE; ++i)
		std::cout << data[i] << " ";
	std::cout << "\n";

	return 0;
}
```



### 동작 순서

103 72 6 3 334

**72 103** 6 3 334

72 **6 103** 3 334

72 6 **3 103** 334

72 6 3 **103 334**  //1 Pass

**6 72** 3 103 334

6 **3 72** 103 334

6 3 **72 103** 334 // 2Pass

**3 6** 72 103 334

3 **6 72** 103 334 //3 Pass

**3 6** 72 103 334 //4 Pass



### 출력

```
3 6 72 103 334
```

