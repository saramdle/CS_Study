# 동적 계획법

날짜: 2023년 4월 15일
주제: Algorithm

# 1. DP란?

**DP (Dynamic Programing) 또는 동적 계획법**은 기본적인 아이디어로 하나의 큰 문제를 여러 개의 작은 문제로 나누어서 그 결과를 저장하여 다시 큰 문제를 해결할 때 사용하는 것으로 특정한 알고리즘이 아닌 하나의 문제 해결 패러다임으로 볼 수 있습니다.

# 2. DP를 쓰는이유

사실 일반적인 재귀 방식또한 DP와 매우 유사합니다.

큰 차이점은 일반적인 재귀를 단순히 사용 시 동일한 작은 문제들이 여러 번 반복되어 비효율적인 계산이 될 수 도 있다는 것입니다.

에를 들어 피보나치 수열을 살펴보겠습니다.

일반적인 재귀로 구성하면 아래와 같습니다.

```
return f(n) = f(n-1) + f(n-2)
```

그런데 f(n-1), f(n-2)에서 각 함수를 1번씩 호출하면 동일한 값을 2번씩 구하게 되고 이로 인해 100번째 피보나치 수를 구하기 위해 호출되는 함수의 횟수는 기하급수 적으로 증가합니다.

![](https://file.notion.so/f/s/ed90cbd7-b4e7-47a7-8b9f-0b898dea29c7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-04-16_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.57.47.png?id=49c787d6-1e7f-476a-8b67-6e2f813a7d07&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1682319604532&signature=uloXNkzKjRAW3QQMWQpQWfJf9wYraqnTxIAzQ6shIUU&downloadName=%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2023-04-16+%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB+12.57.47.png)

그러나 한 번 구한 작은 문제의 결과 값을 저장해두고 재사용 한다면 어떨까요? 앞에서 계산된 값을 다시 반복할 필요가 없어져 효율적으로 값을 구할수 있습니다.

시간복잡도: O(n^2) → O(f(n))로 개선

# 3. DP의 사용조건

DP가 적용되기 위해서는 2가지 조건을 만족해야 합니다.

### 1. **Overlapping Subproblems(겹치는 부분문제)**

DP는 기본적으로 문제를 나누고 그 문제의 결과 값을 재활용해서 전체 답을 구합니다. 그래서 **동일한 작은 문제들이 반복하여 나타나는 경우에 사용이 가능합니다.**

즉, DP는 부분 문제의 결과를 저장하여 재 계산하지 않을 수 있어야 하는데, 해당 **부분 문제가 반복적으로 나타나지 않는다면 재사용이 불가능하니 부분 문제가 중복되지 않는 경우에는 사용할 수가 없습니다.**

### 2. **Optimal Substructure(최적 부분 구조)**

**부분 문제의 최적 결과 값을 사용해 전체 문제의 최적 결과를 낼 수 있는 경우**
를 의미한다. 그래서 특정 문제의 정답은 문제의 크기에 상관없이 항상 동일하다!

→ 길찾기에서 최단거리를 구할 때 최종단계 바로 전 단계의 최적값을 구하면 최종단계 값을 간단히 구할 수 있습니다.

# 4. 구현방법

1. Bottom-Up 방식 (Tablulation방식) - 반복문 사용

   아래에서부터 계산을 수행하고 누적시켜서 전체 큰 문제를 해결하는 방식입니다.

   왜 Tabulation?

    - 반복을 통해 dp[0]부터 하나 하나 씩 채우는 과정을 “table-filling”
    - 이 Table에 저장된 값에 직접 접근하여 재활용 하므로 Tabulation이라는 명칭이 붙었다고 합니다.
    - 사실상 근본적인 개념은 결과값을 기억하고 재활용한다는 측면에서 memoization과 크게 다르지 않습니다.
2. Top-Down 방식 (Memoization방식)- 재귀 사용

   dp[n]의 값을 찾기 위해 위에서부터 바로 호출을 시작하여 dp[0]의 상태까지 내려간 다음 해당 결과 값을 재귀를 통해 전이시켜 재활용하는 방식입니다.

   피보나치의 예시처럼, f(n) = f(n-2) + f(n-1)의 과정에서 함수 호출 트리의 과정에서 보이듯, n=5일 때, f(3), f(2)의 동일한 계산이 반복적으로 나오게 됩니다.

   이 때, 이미 이전에 계산을 완료한 경우에는 단순히 메모리에 저장되어 있던 내역을 꺼내서 활용하면 된다. 그래서 가장 최근의 상태 값을 메모해 두었다고 하여 **Memoization**
     이라고 부릅니다.

   30번째 피보나치수열을 Bottom-Up방식과 Top-Down방식으로 구현한 예시입니다.

    ```java
    public class Fibonacci{
        // DP 를 사용 시 작은 문제의 결과값을 저장하는 배열
        // Top-down, Bottom-up 별개로 생성하였음(큰 의미는 없음)
        static int[] topDown_memo; 
        static int[] bottomup_table;
        public static void main(String[] args){
            int n = 30;
            topDown_memo = new int[n+1];
            bottomup_table = new int[n+1];
            
            long startTime = System.currentTimeMillis();
            System.out.println(naiveRecursion(n));
            long endTime = System.currentTimeMillis();
            System.out.println("일반 재귀 소요 시간 : " + (endTime - startTime));
            
            System.out.println();
            
            startTime = System.currentTimeMillis();
            System.out.println(topDown(n));
            endTime = System.currentTimeMillis();
            System.out.println("Top-Down DP 소요 시간 : " + (endTime - startTime));
            
            System.out.println();
            
            startTime = System.currentTimeMillis();
            System.out.println(bottomUp(n));
            endTime = System.currentTimeMillis();
            System.out.println("Bottom-Up DP 소요 시간 : " + (endTime - startTime));
        }
        
        // 단순 재귀를 통해 Fibonacci를 구하는 경우
        // 동일한 계산을 반복하여 비효율적으로 처리가 수행됨
        public static int naiveRecursion(int n){
            if(n <= 1){
                return n;
            }
            return naiveRecursion(n-1) + naiveRecursion(n-2);
        }
        
        // DP Top-Down을 사용해 Fibonacci를 구하는 경우
        public static int topDown(int n){
            // 기저 상태 도달 시, 0, 1로 초기화
            if(n < 2) return topDown_memo[n] = n;
            
            // 메모에 계산된 값이 있으면 바로 반환!
            if(topDown_memo[n] > 0) return topDown_memo[n];
            
            // 재귀를 사용하고 있음!
            topDown_memo[n] = topDown(n-1) + topDown(n-2);
            
            return topDown_memo[n];
        }
        
        // DP Bottom-Up을 사용해 Fibonacci를 구하는 경우
        public static int bottomUp(int n){
            // 기저 상태의 경우 사전에 미리 저장
            bottomup_table[0] = 0; bottomup_table[1] = 1;
            
            // 반복문을 사용하고 있음!
            for(int i=2; i<=n; i++){
                // Table을 채워나감!
                bottomup_table[i] = bottomup_table[i-1] + bottomup_table[i-2];
            }
            return bottomup_table[n];
        }
    }
    
    /*
    결과
    832040
    일반 재귀 소요 시간 : 9
    
    832040
    Top-Down DP 소요 시간 : 0
    
    832040
    Bottom-Up DP 소요 시간 : 0
    */
    ```


# 5 Q&A

## Q. Top-Down vs Bottom-Up

Tod-Down 방식

- 점화식을 이해하기 쉽다는 장점이 있습니다.
- 재귀함수 기반이기 때문에 너무 많이 호출되면 아웃오브메모리

Bottom-Up 방식

- 재귀호출을 하지않기 때문에 시간과 메모리 사용량을 줄일 수 있다는 장점이 있습니다.
- 중복 계산을 하게되는 단점이 존재합니다.

결론

- 문제를 풀다 보면 두방식의 구현 난이도가 심하게 차이나는 상황을 만날수 있다.
- 편한걸로 구현하되 난이도 차이가 날 경우를 대비해 둘다 구현할수 있도록 연습해야한다.

## Q. 분할정복과 공통점과 차이점은?

공통점

- 문제를 잘게 쪼개서 가장 작은 단위로 분할

차이점

- 동적 계획법
    - 부분 문제는 중복되어, 상위 믄제 해결 시 재활용됨
    - Ex:) 피보나치 수열
- 분할 정복
    - 부분 문제는 서로 중복되지 않음
    - Memorization 기법 사용 안함
    - ex:) 병렬정합
