# (sieve of Eratosthenes) 에라토스테네스의 체

소수를 구하는 방법 중 하나로 배수들을 제외시킴으로서 소수를 제외하고 지운다.



![Sieve_of_Eratosthenes_animation](image/Sieve_of_Eratosthenes_animation.gif)



* 기존의 소수 획득방법

  ```c++
  #include <iostream>
  #include <cstring>
  #define MAXSIZE 10000000+1
  bool isPrime[MAXSIZE];
  
  int main(int argc, char* argv[])
  {
  	std::ios::sync_with_stdio(false);
  	std::cin.tie(nullptr);
  	std::cout.tie(nullptr);
  
  	memset(isPrime, 0, sizeof(isPrime));
  	for (int i = 2; i < MAXSIZE; ++i)
  	{
  		int count = 0;
  		for (int j = 1; j <= i; ++j)
  		{
  			if (i % j == 0)		//1부터 n까지 모두 나눠서 약수인지를 판단한다.
  				++count;
  		}
  
  		if (count == 2)			//자신과 1로만 나누어 진다면 소수이다.
  			isPrime[i] = true;
  	}
  
  
  
  	for (int i = 2; i < MAXSIZE; ++i)
  		if (isPrime[i])
  			std::cout << i << " ";
  	std::cout << "\n";
  
  	return 0;
  }
  ```

  * 단점: 1부터 n까지의 모든 수의 나누기를 1부터 n까지 해야하므로 너무 느리다

    

* 기존 소수 조금더 개선(약수 구하는 부분에 대한 개선)

  ```c++
  #include <iostream>
  #include <cstring>
  #include <cmath>
  #define MAXSIZE 100+1
  bool isPrime[MAXSIZE];
  
  int main(int argc, char* argv[])
  {
  	std::ios::sync_with_stdio(false);
  	std::cin.tie(nullptr);
  	std::cout.tie(nullptr);
  
  	memset(isPrime, 0, sizeof(isPrime));
  	for (int i = 2; i < MAXSIZE; ++i)
  	{
  		int count = 0;
  		int sqr = sqrt(i);
  		for (int j = 1; j <= sqr; ++j)
  		{
  			if (i % j == 0)
  			{
  				if (i / j == j)
  					++count;
  				else
  					count += 2;
  			}
  		}
  
  		if (count == 2)
  			isPrime[i] = true;
  	}
  
  	for (int i = 2; i < MAXSIZE; ++i)
  		if (isPrime[i])
  			std::cout << i << " ";
  	std::cout << "\n";
  
  	return 0;
  }
  ```

  * 단점: 1부터 n까지 조사하는 것은 여전하지만 1부터 sqrt(n)까지만 약수 조사를 하므로 n*(n^1/2)까지 줄였지만 여전히 느리다.





* 에라토스테네스의 체 구현

  * 구현법
  * 2부터 시작한다.
    * 반복문을 돌리되 다음 조건을 충족시킨다.
    * 아직 소수로 선택되지 않았으나 처음으로 선택된 숫자는 소수이다.(i 반복문)
    * 소수로 선택된 숫자에 소수 자신을 더해 만들어지는 최대 숫자 N까지의 모든 숫자는 소수가 아니다. (j 반복문)
    * 이를 반복한다.
  
  ```c++
  #include <iostream>
  #include <cstring>
  #define MAXSIZE 10000000+1
  bool eratosSieve[MAXSIZE];
  
  int main(int argc, char* argv[])
  {
  	std::ios::sync_with_stdio(false);
  	std::cin.tie(nullptr);
  	std::cout.tie(nullptr);
  
  	memset(eratosSieve, 1, sizeof(eratosSieve));
  	for (int i = 2; i * i < MAXSIZE; ++i)
  		if(eratosSieve[i])
  			for (int j = i * i; j < MAXSIZE; j += i)
  				eratosSieve[j] = false;
  	
  	for (int i = 2; i < MAXSIZE; ++i)
		if (eratosSieve[i])
  			std::cout << i << " ";
  	std::cout << "\n";
  
  	return 0;
  }
  ```
  
  * 에라토스테네스의 체를 이용한다면 O(nlogn)거나 O(nloglogn) 정도 까지 줄어든다 [LINK](https://medium.com/@chenfelix/time-complexity-sieve-of-eratosthenes-fb0184da81dc)



## Reference

Image1: [LINK](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)