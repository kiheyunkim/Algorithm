# Floyd-Warshall 최단 경로 알고리즘

수학적 귀납법으로 시작해서 만들어진 알고리즘. 다음 2개의 식에 따라서 전체 정점을 순회한다. Vertex v1, v2, v3가 있을때  만약 v1- > v2의 사이에 완벽한 최단거리가 구해졌다고 가정한다. 만약 v3라는 새로운 Vertex가 주어졌다고 했을때 다음과 같은 가정 2가지를 할 수 있다. (단 v1,v2를 이은 edge는 e1, v1과 v3를 잇는 edge는 e2, v2와 v3를 잇는 edge는 e3라고 한다.)

1. 정점 v3를 거치지 않는 경우: v3를 거치지 않으므로 e1이 최단거리가 된다.
2. 정점 v3를 거치는 경우: v3를 거치므로 e2+e3 값이 최단거리가 될것이다. 

다시말해 경유하는것이 더 짧으면 경유하는것이 경유하지 않는 것이 더 빠르면 지나치는것이 최단거리가 될 것이다.



![PathFindTree](image/PathFindTree.png)



* 구현

  각각의 노드를 순회하면서 경유하는것과 경유하지 않는 경우의수 모두를 조회하여 작은값은 거리로 삼는다.

  ```c++
  #include <iostream>
  #include <cstring>
  
  #define INF 10000
  #define MAX_VERTEX 9
  int graph[9][9];
  void FloydInit(int n)
  {
  	for (int i = 0; i < n; ++i)
  		for (int j = 0; j < n; ++j)
  		{
  			if (i == j)
  				graph[j][i] = 0;
  			else
  				graph[j][i] = INF;
  		}
  }
  
  void Floyd(int n)
  {
  	for (int k = 0; k < n; ++k)
  		for (int i = 0; i < n; ++i)
  			for (int j = 0; j < n; ++j)
  			{
  				if (graph[i][j] > graph[i][k] + graph[k][j])
  					graph[i][j] = graph[i][k] + graph[k][j];
  			}
  	
  }
  
  
  int main(int argc, char* argv[])
  {
  	FloydInit(MAX_VERTEX);
  
  	int n;
  	std::cin >> n;
  
  	for (int i = 0; i < n; ++i)
  	{
  		int a, b, c;
  		std::cin >> a >> b >> c;
  		graph[a][b] = graph[b][a] = c;
  	}
  
  	Floyd(MAX_VERTEX);
  
  	for (int i = 0; i < MAX_VERTEX; ++i)
  	{
  		for (int j = 0; j < MAX_VERTEX; ++j)
  			std::cout << graph[j][i] << " ";
  		std::cout << "\n";
  	}
  
  	return 0;
  }
  ```
  
  
  
* 입력

  ```
  14
  0 1 4
  0 7 8
  1 7 11
  1 2 8
  7 8 7
  7 6 1
  2 8 2
  8 6 6
  2 3 7
  2 5 4
  6 5 2
  3 5 14
  3 4 9
  5 4 10
  ```

  

* 결과

  ```
  0 4 12 19 21 11 9 8 14
  4 0 8 15 22 12 12 11 10
  12 8 0 7 14 4 6 7 2
  19 15 7 0 9 11 13 14 9
  21 22 14 9 0 10 12 13 16
  11 12 4 11 10 0 2 3 6
  9 12 6 13 12 2 0 1 6
  8 11 7 14 13 3 1 0 7
  14 10 2 9 16 6 6 7 0
  ```

  

* 각 이동 거리
  * **0: 0** 거리:0
  * **1: 0 - 1** 거리:4
  * **2: 0 - 1 - 2** 거리:12
  * **3: 0 - 1 - 2 - 3** 거리:19
  * **4: 0 -1 - 2 - 3 - 4** 거리:21
  * **5: 0 - 7 - 6 - 5** 거리: 11
  * **6: 0 - 7 - 1** 거리: 8
  * **7: 0 - 1 - 2 - 8** 거리: 14
