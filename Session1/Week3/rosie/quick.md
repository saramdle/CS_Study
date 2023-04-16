# [퀵 정렬 (QuickSort)](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/QuickSort.md)
> 퀵 정렬에 대해 설명할 수 있어야 합니다.<br>
> 퀵 정렬 방식의 코드를 이해합니다.

## 퀵 정렬이란?
퀵 정렬(Quick Sort)은 가장 많이 사용되는 불안정 정렬 알고리즘 중 하나로, 분할 정복(Divide and Conquer) 방식을 사용하여 정렬하는 알고리즘입니다. pivot을 정한 뒤 pivot의 위치를 확정해가며 정렬합니다.
+ ```불안정 정렬``` 동일한 값에 기존 순서가 유지X
+ ```분할정복``` 커다란 문제를 나눠서 용이하게 문제단위로 풀기
+ ```pivot``` 리스트에서 분할을 위해 선택된 하나의 원소입니다. 일반적으로 리스트의 중앙값(median)을 선택하거나 무작위로 선택됩니다.

### 동작방식

![Quicksort.png](Quicksort.png)

#### Pivot(기준값) 선택
+ 리스트에서 임의의 pivot 값을 선택합니다.
#### Partition(분할)
+ pivot 값보다 작은 값은 pivot의 왼쪽으로, 큰 값은 pivot의 오른쪽으로 이동시킵니다. 이 때, pivot 값은 최종적으로 정렬된 위치에 놓습니다. 이 과정을 퀵 정렬의 가장 핵심적인 부분이라 할 수 있습니다.
#### Recursion(재귀호출)
+ 분할된 두 개의 리스트에 대해 위 과정을 재귀적으로 수행합니다. 즉, pivot의 왼쪽 리스트와 오른쪽 리스트에 대해 각각 pivot을 다시 선택하고 분할을 수행하는 과정을 반복합니다.
#### Conquer(정복)
+ 분할이 완료되면 정렬이 완료됩니다.

### 시간복잡도
+ 퀵 정렬의 시간 복잡도는 최악의 경우 ```O(n^2)```이지만, 평균적인 경우에는 ```O(n log n)```으로 매우 효율적인 알고리즘입니다.

### 특징
+ 같은 시간복잡도 ```O(n log n)```를 가진 정렬 알고리즘들보다 빠릅니다.
  + 분할정복방식
  + in-place 정렬 알고리즘으로 추가적 메모리 사용이 없음
  + 배열을 분할할 때, 해당 배열의 일부분만을 다루기 때문에 CPU 캐시(cache) hit rate가 높아져서 캐시 미스(cache miss)가 적게 발생
  + 좋은 피벗을 선택하면 분할이 균등하게 이루어지므로 불필요한 비교가 줄어들어서 빠르게 정렬

### 코드로 보는 퀵 정렬
```java
public class QuickSort {
  public static void main(String[] args) {
    int[] arr = {5, 3, 8, 4, 2, 7, 1, 10};
    quickSort(arr, 0, arr.length - 1);
    System.out.println(Arrays.toString(arr));
  }
  
  private static void quickSort(int[] arr, int left, int right) {
    if (left >= right) {
      return;
    }

    int pivot = partition(arr, left, right);
    quickSort(arr, left, pivot - 1);
    quickSort(arr, pivot + 1, right);
  }

  private static int partition(int[] arr, int left, int right) {
    int pivot = arr[right];
    int i = left - 1;

    for (int j = left; j < right; j++) {
      if (arr[j] <= pivot) {
        i++;
        swap(arr, i, j);
      }
    }

    swap(arr, i + 1, right);
    return i + 1;
  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
}
```
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left, right = [], []

    for num in arr:
        if num < pivot:
            left.append(num)
        elif num > pivot:
            right.append(num)

    return quick_sort(left) + [pivot] + quick_sort(right)
```
+ 파이썬의 ```list.sort()``` 함수나 자바의 ```Arrays.sort()```처럼 프로그래밍 언어 차원에서 기본적으로 지원되는 내장 정렬 함수는 대부분은 퀵 정렬을 기본으로 합니다.

<br><br><hr>

참고한 자료
https://www.techiedelight.com/quicksort/


