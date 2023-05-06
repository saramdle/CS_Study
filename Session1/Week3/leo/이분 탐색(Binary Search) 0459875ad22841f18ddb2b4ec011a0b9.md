# 이분 탐색(Binary Search)

Created: May 2, 2023 6:33 PM

### 이분 탐색이란? (=이진검색)

![binary-and-linear-search-animations.gif](%E1%84%8B%E1%85%B5%E1%84%87%E1%85%AE%E1%86%AB%20%E1%84%90%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A2%E1%86%A8(Binary%20Search)%200459875ad22841f18ddb2b4ec011a0b9/binary-and-linear-search-animations.gif)

- 정렬된 배열에서 특정한 값을 찾는 알고리즘
- 탐색하고자 하는 배열의 중간 값과 비교해 탐색 범위를 반으로 줄여가면서 값을 찾아냄
- 배열을 반으로 나누어 검색 범위를 좁혀나가기 때문에 빠른 속도로 값을 찾을 수 있음
- 이 알고리즘을 수행하기 위해서는 반드시 정렬된 배열이어야함
- 이분 탐색 활용 예시
    - 특정 값의 존재 여부를 찾을 때
    - 최적화 문제에서 최솟값이나 최댓값을 찾을 때
    - 극단적인 값을 찾을 때 (e.g. 반복문이 돌 때마다 점점 증가하거나 감소하는 값)
    - 이외에도 문자열 탐색 등 다양한 분야에서 사용됨

### 시간 복잡도

- 전체 탐색 : O(N)
- 이분 탐색 : O(logN)
    - 탐색 범위를 반으로 줄여나가기 때문에 배열의 크기에 비례하지 않고, 탐색 범위의 로그에 비례하기 때문
    - 따라서 정렬이 된 큰 배열에서 값을 찾는 경우에 유용함

### 이분 탐색 과정

```jsx
function binarySearch(arr, target) {
  let start = 0;
  let end = arr.length - 1;

  while (start <= end) {
    let mid = Math.floor((start + end) / 2);

    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      start = mid + 1;
    } else {
      end = mid - 1;
    }
  }

  return -1;
}

const index = binarySearch([1, 3, 5, 7, 9], 5);
console.log(index); // 2
```

1. 배열의 시작 인덱스(0)와 끝 인덱스(n-1)를 정함
2. 배열의 중간 인덱스(mid)를 찾음. mid = (start + end) / 2
3. 중간 인덱스(mid)의 값과 찾고자 하는 값(target)을 비교함
    - mid === target : 값을 찾은 것
    - mid > target : 검색 범위를 배열의 왼쪽 반으로 좁히기 (end = mid-1)
    - mid < target : 검색 범위를 배열의 오른쪽 반으로 좁히기 (start = mid + 1)
4. 검색 범위를 좁혀나가면서 값을 찾을 때까지 2~3단계를 반복