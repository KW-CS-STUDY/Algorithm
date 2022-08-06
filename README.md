# Algorithm
## Index

0. [알고리즘 분석](#알고리즘-분석)
   1. [시간 복잡도](#시간-복잡도(Time-Complexity))
   2. [공간 복잡도](#공간-복잡도(Space-Complexity))
   3. 알고리즘의 정당성 증명 
1. [References](#References)

## 알고리즘 분석
동일한 작업을 수행하는 알고리즘이라 할지라도, 다른 성능을 갖게될 수 있습니다. 따라서 알고리즘마다 평가를 하기 위한 기준이 필요한데, 그 기준으로 시간 복잡도(time complexity)와 공간 복잡도(space complexity)를 사용합니다.

이 복잡도가 낮을수록 좋은 알고리즘이라고 평가할 수 있습니다.

### 시간 복잡도(Time Complexity)
시간 복잡도는 알고리즘의 수행 시간을 평가하며, 점근적 표기법 중에서도 big O 표기법을 이용해 시간 복잡도를 표기합니다. 이 점근적 표기법은 연산의 횟수를 계산할 때, 불필요한 상수 계수및 상수 항을 제거해서 표현하는 방법을 의미합니다.

$e.g.$ $O(3n^2)$ => $O(n^2)$, $O(3n + 5)$ => $O(n)$

알고리즘의 수행 시간은 실행 환경에 따라 천차만별이기 때문에, 기본 연산(primitive operations)의 실행 횟수를 기준으로 평가하며, 기본 연산은 다음과 같습니다.

1. 데이터 입출력
2. 산술 연산
3. 제어 연산

위의 3가지 연산을 수행한 횟수를 센 것을 기준으로 수행 시간을 평가하게 됩니다.

시간 복잡도는 또한 아래의 3가지 경우로 나타낼 수 있습니다.
1. Best case: big omega 표기법 사용, 최선의 방식으로 이 정도의 시간이 소모된다.
2. Worst case: big o 표기법 사용, 최악의 방식으로 이 정도의 시간이 소모된다.
3. Average case: 전체 경우의 수에 대한 평균 소모 시간, big theta 표기법 사용.

일반적으로 시간 복잡도는 big O 표기법을 이용해 평가합니다. (그렇기 때문에 알고리즘은 worst case로 성능이 평가된다고 생각할 수 있습니다.)

```c
int sum(int arr[]){
   int res = 0;
   for(int i = 0; i < length of arr; i++){
      res += arr[i];
   }
   return res;
}
```
위 코드는 인자로 입력 받은 배열의 총 합을 구해서 반환하는 간단한 함수입니다. 위 예시 코드를 big O notation으로 표현하면 다음과 같습니다. (입력 배열의 크기가 n일때)
$T(n) = n + 1 = O(n)$

### 공간 복잡도(Space Complexity)
공간 복잡도 또한 시간 복잡도와 같이 big O 표기법을 이용해 표기하며, 알고리즘이 사용하는 메모리 공간을 기준으로 알고리즘의 성능을 평가하는 방법입니다.

공간 복잡도 (요구되는 총 공간) = 고정 공간 요구 + 가변 공간 요구
- 고정 공간: 입력과 출력의 횟수나 크기와 관계없이 요구되는 공간 (코드가 저장되는 공간, 단순 변수, 고정 크기의 구조 변수, 상수 등..)
- 가변 공간: 해결하려는 문제의 특정 instance에 의존하는 크기를 갖는 구조화 변수들을 위해 필요한 공간, 함수가 순환 호출을 할 경우 요구되는 추가 공간이다. 즉, 동적으로 필요한 공간.

```c
int sum(int arr[]){
   int res = 0;
   for(int i = 0; i < length of arr; i++){
      res += arr[i];
   }
   return res;
}
```
위 예시 코드를 이용해 공간 복잡도를 표기하면 다음과 같습니다.
$O(n)$
인자로 전달되는 배열의 크기 n + res 변수 1

## References
https://yoongrammer.tistory.com/79
https://ko.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/asymptotic-notation
