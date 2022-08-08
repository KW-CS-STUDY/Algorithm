# Algorithm
## Index

0. [알고리즘 분석](#알고리즘-분석)
   1. [시간 복잡도](#시간-복잡도(Time-Complexity))
   2. [공간 복잡도](#공간-복잡도(Space-Complexity))
   3. 알고리즘의 정당성 증명 
1. [정렬](#정렬-알고리즘)
   1. [Bubble sort](#Bubble-sort)
   2. [Insertion sort](#Insertion-sort)
   3. [Quick sort](#Quick-sort)
   4. [Merge sort](#Merge-sort)
   5. [Heap sort](#Heap-sort)
2. [References](#References)

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

## 정렬 알고리즘
정렬 알고리즘은 computer science에서 중요시되는 문제중 하나로 원소들을 번호나 사전 순서와 같이 일정한 순서대로 열거하는 알고리즘입니다. 

여러 가지의 정렬 알고리즘 중 대표적으로 사용되는 알고리즘 몇 가지를 정리해보면 다음과 같습니다.

### Bubble sort
bubble sort는 서로 인접한 두 개의 원소를 비교해가며 정렬해 나아가는 정렬 알고리즘입니다. n개의 원소가 배열에 속한다고 가정할 때, 0번에서 n-1번 인덱스의 원소까지 각각 최대 n번 인접한 원소를 비교하며 정렬을 수행하게 됩니다.

단순하게, 반복적으로 인접 원소를 비교하며 앞으로 보내기 때문에 구현 과정이 간단하지만, 정렬 알고리즘 중 가장 비효율적인 알고리즘으로 bubble sort의 시간 복잡도는 $O(n^2)$입니다. 

각각의 수행마다 최솟값을 맨 앞으로 보내주는 방식으로 정렬을 구현합니다. 

#### example souce code (C++)
```c
#include <iostream>

using namespace std;

int main(){
   int i, j, tmp;
   int arr[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};
   
   for(i = 0; i < 10; i++){
      // 9, 10까지만 비교가 가능하기 때문에 9 - i까지 비교한다.
      // arr[i]에는 매 시행에서의 최솟값이 배치된다.
      for(j = 0; j < 9 - i; j++){
         if(arr[j] > arr[j+1]){
            // change two adjacent elements
            tmp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = tmp;
         }
      }
   }
   return 0;
}
```

### Insertion sort
삽입 정렬(insertion sort)는 bubble sort와 같이 $O(n^2)$의 시간 복잡도를 갖는 정렬 알고리즘입니다.

삽입 정렬은 배열의 각 숫자를 적절한 위치에 삽입하는 방식으로 원소들을 정렬하고, 버블 정렬과는 다르게 필요할 때만 원소의 위치를 바꿔줍니다.


#### example source code (C++)
```c
#include <iostream>

using namespace std;

int main(){
   int i, j, tmp;
   int arr[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};
   
   for(i = 0; i < 10; i++){
      j = i;
      // i번째 원소까지는 이미 정렬되었다고 가정
      // i+1번째 원소를 알맞은 위치에 삽입한다.
      while(j > 0 && arr[j - 1] > arr[j]){
         // 오름 차순으로 정렬합니다. 
         tmp = arr[j];
         arr[j] = arr[j+1];
         arr[j+1] = tmp;
         j--;
      }
   }
   for(i = 0; i < 10; i++){
      cout << arr[i] << " ";
   }
   cout << endl;
   
   return 0;
}
```

위 예시 코드의 주석에 작성된 바와 같이 삽입 정렬은 각각의 원소를 이미 정렬된 왼편의 원소들 사이에 알맞은 위치에 끼워넣는 방식으로 정렬을 진행합니다. (그래서 삽입 정렬이라고 부릅니다.)

### Quick sort
퀵 정렬(quick sort)는 평균적으로 $O(nlogn)$의 시간 복잡도를 갖는 정렬 알고리즘입니다. 하지만, worst case에서는 $O(n^2)의 시간 복잡도를 갖기 때문에, 특정 경우에 사용하는 경우 문제 풀이시 시간 초과 문제를 발생시킬 수 있기 때문에, 주의해야 합니다.

퀵 정렬은 '분할 정복' 방식으로 데이터의 정렬을 진행하는 알고리즘으로 정렬 방식은 다음과 같습니다.

퀵 정렬은 특정한 값을 기준으로 큰 숫자는 오른편에 작은 숫자는 왼편에 배치하는 방식으로 문제를 더 작은 문제로 나누어서 해결하는 분할 정복 방식으로 문제를 해결하는데, 여기서 문제를 분할하는 특정한 값을 기준 값(pivot)이라고 부릅니다.

이 pivot을 기준으로 큰 값과 작은 값이 나누어지도록, 큰 값과 작은 값을 교환한 이후 배열을 pivot을 기준으로 반으로 쪼개서 다시 똑같은 작업을 모든 데이터가 정렬될 때가지 반복하는 과정을 통해 정렬 작업을 진행합니다.

(1) 10 5 8 7 6 4 3 2 9

위 배열을 예로 들어봅시다. 우선 가장 첫 번째 pivot은 첫 번째 원소인 1로 설정됩니다. 배열의 맨 오른쪽(end)에서 부터 pivot보다 작은 값을 찾고, 배열의 맨 왼쪽(start)에서 부터 pivot보다 큰 값을 찾으면 다음과 같게 찾을 수 있습니다.

(1)(i) 10(j) 5 8 7 6 4 3 2 9

이런 경우 i(작은 값)과 j(큰 값)의 위치가 올바르게 엇갈리므로 pivot을 기준으로 정렬이 되었다고 판단하여 작은 값과 pivot의 위치를 바꿔 pivot을 기준으로 왼편에는 작은 값, 오른편에는 큰 값이 위치한 결과 배열을 완성할 수 있습니다. (사실 이 단계에서는 변동 사항이 없어 그대로입니다.)

(1) 10 5 8 7 6 4 3 2 9

원래는 이 배열을 이제 두 개의 sub problem으로 나누는 방식으로 진행되는데, pivot을 기준으로 왼편은 배열의 끝이기 때문에 문제는 남은 오른편의 배열만을 다시 pivot을 기준으로 나누는 문제로 쪼개집니다.

1 / (10) 5 8 7 6 4 3 2 9

1 / (10)(j) 5 8 7 6 4 3 2 9(i)  
1 / (9) 5 8 7 6 4 3 2 10  
1 / (9) 5 8 7 6 4 3 2(i) 10(j)  
1 / 2 5 8 7 6 4 3 (9) 10  
=> 아래의 두 배열에 대한 퀵 정렬로 문제가 분할됩니다.  
{2 5 8 7 6 4 3}, {10}  
.  
.  
.  
1 2 3 4 5 6 7 8 9 10  

#### example code (C++)
```c
#include <iostream>

using namespace std;

int arr[] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};
int n = 10;

void quickSort(int start, int end){
   if(start >= end)
      return;
      
   int key = start;
   // i: index of bigger element, j: index of smaller element
   int i = start + 1, j = end, tmp;
   
   while(i <= j){
      while(i <= end && arr[i] <= arr[key])
         i++;
      while(j > start && arr[j] >= arr[key])
         j--;
         
      if(i <= j){ // 엇갈린 경우 큰 값과 작은 값을 교환
         tmp = arr[i];
         arr[i] = arr[j];
         arr[j] = tmp;
      }
      else{ // 엇갈리지 않은 경우 작은 값과 key(pivot)을 교환
         tmp = arr[i];
         arr[i] = arr[key];
         arr[key] = tmp;
         // 이 시점에서 pivot을 기준으로 왼편에는 작은 값들, 오른편에는 큰 값들이 위치하게 된다.
      }
   }
   // j가 기존의 pivot의 index
   quickSort(start, j - 1);
   quickSort(j + 1, end);
}

void print(){
   for(int i = 0; i < n; i++){
       cout << arr[i] << " ";
   }
   return;
}
int main(){
   quickSort(0, n - 1);
   print();
   return 0;
}
```

다시 간단하게 설명하면, 매 단계에서 pivot이 되는 값은 인자로 넘겨받은 부분 배열의 첫 번째 값이고, pivot보다 작은 값과 큰 값을 각각 배열의 오른쪽, 왼쪽부터 계속해서 바꿔주다 더 이상 큰 값과 작은 값의 인덱스가 (index 작은 값 > index 큰 값) 구조가 아닌 경우 마지막 작은 값과 pivot을 변경해서 현재 단계에서 pivot을 기준으로 왼편에는 기준 값보다 작은 값들이 오른편에는 기준 값보다 큰 값들이 위치하는 배열을 만들 수 있습니다.

이러한 퀵 정렬은 앞서 말했던 바와 같이 worst case에서 $O(n^2)$의 시간 복잡도를 갖는데 worst case는 이미 정렬된 배열을 퀵 정렬을 이용해 다시 정렬하는 경우에 해당합니다.

그 이유는 pivot 값을 첫 원소부터 설정해서 pivot보다 작은 값과 큰 값의 위치를 변경하기 위해 배열을 모두 탐색하지만, 이미 정렬된 경우이기 때문에 결국 pivot이 한 칸씩만 이동하면서 재귀적으로 퀵 정렬이 호출되며 결과적으로 $O(n^2)$의 시간 복잡도를 갖게 됩니다. (대략 n개의 pivot이 설정되고, 각 pivot마다 전체 배열을 탐색하기 때문이라고 생각하면 될 듯하다.)

### Merge sort
merge sort(병합 정렬) 또한 퀵 정렬과 동일하게 분할 정복 방법을 도입한 정렬 알고리즘입니다. 따라서 $O(n^2)$의 시간 복잡도를 갖고, 병합 정렬은 퀵 정렬과는 다르게 worst case에 대해서도 동일한 시간 복잡도를 갖는 것이 특징이라고 할 수 있습니다.

병합 정렬은 우선 문제(배열)을 가장 작은 단위(원소)로 나눈 후(분할한 후) 합치면서 정렬하는 과정을 통해 정렬을 진행합니다.   
![image](https://user-images.githubusercontent.com/68600592/183352471-9c66646e-f24a-4062-8de9-dcf56d32cfb5.png)
![image](https://user-images.githubusercontent.com/68600592/183352650-7d7b1c6f-e507-4c2c-ba9c-baa2ddf2cf3f.png)
![image](https://user-images.githubusercontent.com/68600592/183352670-a3014c69-0da8-4027-9413-0badcfecdceb.png)  
<사진 출처: 안경잡이개발자 네이버 블로그>
위 이미지를 예시로 들어 설명하면, 나뉘어진 두 개의 배열을 하나의 정렬된 배열로 합치는 과정은 i, j를 이용해 두 개의 배열에 속한 원소를 비교하며, 정렬하여 하나의 배열에 값을 복사하는 과정을 거칩니다.

![image](https://user-images.githubusercontent.com/68600592/183352868-f11b5d41-ad2c-4500-81a0-1873b9b37cad.png)

위 그림과 같이 대소 비교(primitive operation) 과정을 최대 이진 트리의 높이만큼(logN) 반복 수행하기 때문에 $O(nlogn)$의 시간 복잡도를 갖게 되는 것입니다.

#### example source code (C++)
```c
#include <iostream>

using namespace std;

int arr[] = {7, 6, 5, 8, 3, 5, 9, 1};
int n = 10;

// m: 왼쪽 부분 배열의 시작 index, mid: 가운데 지점, n: 오른쪽 부분 배열의 시작 index
void merge(int m, int mid, int n){
   int i = m;
   int j = mid + 1;
   
   int k = m;
   
   while(i <= mid && j <= n){
      // 두 개의 부분 배열을 정렬 순서에 맞게 sorted 배열에 저장한다.
      if(arr[i] <= arr[j]){
         sorted[k++] = arr[i++];
      }
      else{
         sorted[k++] = arr[j++];
      }
   }
   
   if(i > mid){
      for(int t = j; t <= n; t++){
         sorted[k++] = arr[t];
      }
   }
   else{
      for(int t = i; t <= mid; t++){
         sorted[k++] = arr[t];
      }
   }
   
   for(int t = m; t <= n; t++){
      // 정렬된 결과를 원래 배열에 복사한다. (다음 병합을 위해)
      arr[t] = sorted[t];
   }
}

void mergeSort(int m, int n){
   if(m < n){
      int mid = (m + n) / 2;
      // 재귀적으로 호출해서 문제를 최소 단위로 쪼개준다.
      mergeSort(m, mid);
      mergeSort(mid, n);
      // 분할된 문제를 병합하며 해결한다.
      merge(m, mid, n);
   }
}

int main(){
   mergeSort(0, n - 1);
   for(int i = 0; i < n; i++){
      cout << sorted[i] << " ";
   }
   return 0;
}

```

### Heap sort


## References
https://yoongrammer.tistory.com/79  
https://ko.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/asymptotic-notation  
https://blog.naver.com/PostView.naver?blogId=ndb796&logNo=221226813382&parentCategoryNo=&categoryNo=128&viewDate=&isShowPopularPosts=false&from=postList  

