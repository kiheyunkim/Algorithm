# Selection Sort(선택 정렬)



**시간 복잡도: 최악, 최선, 평균 O(N)**

안정 여부: 불안정 정렬



### 동작 원리

순서가 있는 각 원소들의 개수를 세고 그 원소들을 개수만큼 나열하여 정렬한다.

### 코드

```c++
#include <iostream>
#include <ctime>

#define DATA_SIZE 25
char dataArray[DATA_SIZE];

void CountingSort(char* data, int n)
{
	int counter[26]{ 0, };
	for (int i = 0; i < n; ++i)
		++counter[data[i] - 'a'];

	int inputIndex = 0;
	for (int i = 0; i < 26; ++i)
		for (int j = 0; j < counter[i]; ++j)
		{
			data[inputIndex] = 'a' + i;
			++inputIndex;
		}
		
}

int main(int argc, char* argv[])
{
	srand(time(nullptr));
	for (int i = 0; i < DATA_SIZE; ++i)
		dataArray[i] = rand() % 26 + 'a';

	CountingSort(dataArray, DATA_SIZE);

	for (int i = 0; i < DATA_SIZE; ++i)
		std::cout << dataArray[i];
	std::cout << "\n";

	return 0;
}
```



### 입력(랜덤 생성)

```
fwtbdlhfuevchgsbsomjaovlc
```





### 동작 순서

counter = {1, 2, 2, 1, 1, 2, 1, 2, 0, 1, 0, 2, 1, 0, 2, 0, 0, 0, 2, 1, 1, 2, 1, 0, 0, 0}



### 출력

```
abbccdeffghhjllmoosstuvvw
```





### 추가

개수를 셀 수 있는 정도의 데이터로 한정되어 있을 때만 사용할 수 있다.