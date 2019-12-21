# Kruscal 최단 경로 알고리즘

Kruscal  최단 경로 알고리즘은 그래프에 존재하는 모든 정점 사이의 최단 경로를 한 번에 모두 찾아주는 알고리즘 



![WeightedTree](image/WeightedTree.jpg)

* #### 동작원리

  * 가장 작은 Edge부터 선택을 하며 만약 선택한 Edge가 Cycle이 생기면 그 Edge는 제외하고 다음 것을 검사한다. 
  * 사이클이 형성되었는지는 Union-find 자료구조를 이용하면된다. 선택된 두 원소의 최상위 Root를 찾았을 때, 그 값이 같다면 같은 집합에 있다는 것이고 같은 집합에 이미 들어가 있는 두원소를 합치면 사이클을 형성하게 된다는 것이다.
  * 속도는 약 O(elogn)를 가지게 된다.



* #### 구현

  ```c++
  #include <iostream>
  #include <cstring>
  #include <queue>
  #include <vector>
  
  int n;
  int parent[10 + 1];
  int rank[10 + 1];
  
  void UnionFindInit()
  {
  	for (int i = 1; i < 10 + 1; ++i)				//자신을 가르키도록 함
  	{
  		parent[i] = i;
  		rank[i] = 1;
  	}
  }
  
  int FindParent(int x)								//최상위 루트를 찾음 
  {
  	return parent[x] == x ? x : FindParent(parent[x]);
  }
  
  void Merge(int x, int y)							//x과 속한 집합과 y가 속한 집합을 합침
  {
  	int rootX = FindParent(x), rootY = FindParent(y);
  	int heightX = rank[rootX], heightY = rank[rootY];
  
  	if (heightX < heightY)
  		parent[rootX] = rootY;
  	else if (heightX == heightY)
  	{
  		parent[rootX] = rootY;
  		++rank[rootY];
  	}
  	else
  		parent[rootY] = rootX;
  }
  
  struct Edge
  {
  	int x;
  	int y;
  	int value;
  	Edge(int x, int y, int value) :
  		x(x), y(y), value(value) {}
  };
  
  struct Cmp
  {
  	bool operator()(const Edge& l, const Edge& r) 
  	{
  		return l.value > r.value;
  	}
  };
  
  int main(int argc, char* argv[])
  {
  	std::ios::sync_with_stdio(false);
  	std::cin.tie(nullptr);
  	std::cout.tie(nullptr);
  
  	std::priority_queue<Edge, std::vector<Edge>, Cmp> kruscalMST;
  	std::cin >> n;
  
  	UnionFindInit();
  
  	for (int i = 0; i < n; ++i)
  	{
  		int x, y, value;
  		std::cin >> x >> y >> value;
  		kruscalMST.push(Edge(x, y, value));
  	}
  
  	int length = 0;
  	while (!kruscalMST.empty())
  	{
  		Edge front = kruscalMST.top();
  
  		//부모가 같으면 합쳐져있는것.
  		//부모가 다르면 합쳐야 할것.
  		int rootX = FindParent(front.x), rootY = FindParent(front.y);
  		if (rootX != rootY)
  		{
  			Merge(rootX, rootY);
  			length += front.value;
  			std::cout << front.value << " ";
  		}
  
  
  		kruscalMST.pop();
  	}
  
  	std::cout <<"\n"<< length << "\n";
  
  
  	return 0;
  }
  ```

  

* #### 입력값

  ```
  19
  9 6 18
  9 7 2
  9 8 4
  6 7 14
  8 7 3
  6 4 16
  7 4 17
  7 5 11
  8 5 5
  4 5 19
  4 1 10
  5 1 15
  4 2 8
  1 2 7
  5 3 9
  1 3 6
  6 2 12
  8 3 1
  2 3 13
  ```

  

  

* #### 결과

  ```
  44
  ```

  
  
* #### 선택된 경로들

  ![WeightedTree(Selected)](image/WeightedTree(Selected).jpg)

#### Reference

Image1:[Link](//https://subscription.packtpub.com/book/application_development/9781788833738/6/ch06lvl1sec48/minimum-spanning-tree)