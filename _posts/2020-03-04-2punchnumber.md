---
title:  "백준 2193번 이친수"
#excerpt: "ROT13 풀어보기"

categories:
  - 알고리즘
  
tags:
  - altorithm
  - study
last_modified_at: 2020-03-04T21:30:00-00:00
--- 
# ** 이친수 문제 풀어보기 **  
  
문제 링크 : https://www.acmicpc.net/problem/2193  

오늘 풀어볼 `이친수` 라는 문제입니다.  
이 문제는 길이를 입력받아 그 길이만큼의 자릿수 일 때 이친수가  
몇가지 나오는지 찾아보는 문제입니다.  
  
먼저 문제를 먼저 보겠습니다.  
  
![문제](https://user-images.githubusercontent.com/59772554/75879696-28f0df80-5e5f-11ea-86a8-b2983621010f.PNG)   
  
### * 문제 분석  
  
맨 앞에 0이 올 수 없고, 1이 연속으로 위치할 수 없으니까  
맨 앞에 두자리는 10으로 고정입니다. 이 상태에서 알아봅시다.  

한 자릿수 이친수 = 1 (1개)  
두 자릿수 이친수 = 10 (1개)  
세 자릿수 이친수 = 100, 101 (2개)  
네 자릿수 이친수 = 1000, 1001, 1010 (3개)  
  
▶ 네 자릿수의 고정된 앞의 두자리를 빼고보면 뒤의 두자리는  
   세 자릿수의 마지막 뒤에 2자리 + 두 자릿수의 마지막 2자리와 같습니다.  

이걸 생각하면서 다섯 자릿수의 이친수를 찾아봅시다.  
다섯자리 이친수 = 10000, 10001, 10010, 10100, 10101 (5개)  
  
위 규칙이 성립하는 것을 볼 수 있습니다.  
  
▶ 즉, N자리의 수의 이친수의 개수는 N-1자리의 이친수 개수와 N-2의 이친수 개수의  
 합과 같습니다. 이걸로 점화식을 만들어보면 d[N] = d[N-1] + d[N-2] 가 됩니다.  
  
![IOPE](https://user-images.githubusercontent.com/59772554/75950361-4cae3700-5eec-11ea-8e01-9be797ab1ea4.PNG)  
 

### * 알고있어야 할 것  
이친수란 0 으로 시작하지 않으며, 1이 두번 연속으로 나타나지 않는 수 입니다.  
ex) 1, 100, 10101 등등  
  
      
### * 해결 과정  

  1. 길이 변수 N을 입력 받는다.  
  2. 자릿수에 따라 몇가지 경우가 오는지 기록하는 배열을 선언한다.      
  3. 배열에 0번째와 1번째에 몇가지가 오는지 미리 기록해준다.        
  4. 2번째 부터는 점화식에 따라 계산해 기록해준다.      
  5. 입력받은 N까지 경우를 구하면 출력한다.      
  
  
### * C++ 코드  
  
```c++
#include <iostream>
using namespace std;

int main()
{
	//숫자의 자릿수
	int n=0;
	cin >> n;

	//인덱스 자릿수에 몇가지 경우가 오는지 기록
	long long int d[91];

	// 자릿 수가 0일 때는 0가지
	d[0] = 0;
	//자릿 수가 1일 때는 1가지
	d[1] = 1;

	//두자리 부터는 앞의 0,1 자리의 
	//경우를 통해 구해나갈 수 있다.
	for (int i = 2; i <= n; i++)
	{
		d[i] = d[i - 1] + d[i - 2];
	}

	cout << d[n];

	return 0;
}
```  
  
  
### * 결과   
  
![콘솔결과](https://user-images.githubusercontent.com/59772554/75880842-63f41280-5e61-11ea-8a32-58f7f233eaab.PNG)  
![제출결과](https://user-images.githubusercontent.com/59772554/75880869-6fdfd480-5e61-11ea-887a-df4fd182be00.PNG)  
  
   
  
감사합니다!😀  