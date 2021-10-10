> 나동빈님의 서적 ['이것이 취업을 위한 코딩테스트다'](https://play.google.com/store/books/details/%EB%82%98%EB%8F%99%EB%B9%88_%EC%9D%B4%EA%B2%83%EC%9D%B4_%EC%B7%A8%EC%97%85%EC%9D%84_%EC%9C%84%ED%95%9C_%EC%BD%94%EB%94%A9_%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%8B%A4_with_%ED%8C%8C%EC%9D%B4%EC%8D%AC?id=vBz-DwAAQBAJ)를 읽고 정리하였습니다.



## 순차 탐색

순차 탐색은 가장 기본적인 탐색 방법이다. 대부분 자연스레 순차 탐색의 원리를 이해하고 있을 것이다. 

**순차 탐색(Sequential Search)**이란 리스트 안에 있는 특정한 **데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례대로 확인**하는 방법이다.

보통 **정렬되지 않은 리스트에서 데이터를 찾아야 할 때** 사용한다. 데이터 개수가 N개일 때 최대 N번의 비교 연산이 필요하므로 순차 탐색의 최악의 경우 **시간 복잡도**는 **O(N)**이다.



## 이진 탐색

**이진 탐색(Binary Search)**은 **탐색 범위를 절반씩 좁혀가며 데이터를 탐색**하는 알고리즘이다. 



### 탐색 과정

탐색하는 범위의 시작점, 끝점, 그리고 중간점을 두고 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는다.



### 제한 및 특징

**배열 내부의 데이터가 정렬되어 있어야만 사용**할 수 있는 알고리즘이다. 데이터가 무작위일 때는 사용할 수 없지만, 이미 정렬되어 있다면 **매우 빠르게 데이터를 찾을 수** 있다는 특징이 있다.



### 시간 복잡도

이진 탐색은 한 번 확인할 때마다 확인하는 원소의 개수가 절반씩 줄어든다는 점에서 시간 복잡도가 O(logN)이다.



### 코드

#### < 재귀 함수로 구현 >

```python
def binary_search(array, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    # 찾은 경우 중간점 인덱스 반환
    if array[mid] == target:
        return mid
    # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    elif array[mid] > target:
        return binary_search(array, target, start, mid - 1)
    # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    else:
        return binary_search(array, target, mid + 1, end)
```

#### < 반복문으로 구현 >

```python
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        # 찾은 경우 중간점 인덱스 반환
        if array[mid] == target:
            return mid
        # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        elif array[mid] > target:
            end = mid - 1
        # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else:
            start = mid + 1
    return None
```



## 트리 자료구조

트리 자료구조는 노드와 노드의 연결로 표현한다.

노드는 정보의 단위로서 어떠한 정보를 가지고 있는 개체다.

트리 자료구조는 그래프 자료구조의 일종으로 데이터베이스 시스템이나 파일 시스템과 같은 곳에서 많은 양의 데이터를 관리하기 위한 목적으로 사용한다.



### 특징

- 트리는 부모와 자식 노드의 관계로 표현된다.
- 트리의 최상단 노드를 루트 노드라고 한다.
- 트리의 최하단 노드를 단말 노드라고 한다.
- 트리에서 일부를 떼어내도 트리 구조이며 이를 서브 트리라 한다.
- 트리는 파일 시스템과 같이 계층적이고 정렬된 데이터를 다루기에 적합하다.



큰 데이터를 처리하는 소프트웨어는 대부분 데이터를 트리 자료구조로 저장해서 이진 탐색과 같은 탐색 기법을 이용해 빠르게 탐색이 가능하다.



### 이진 탐색 트리

이진 탐색 트리란 이진 탐색이 동작할 수 있도록 고안된, 효율적인 탐색이 가능한 자료구조이다.
