# 🎯 인덱스(Index)
- - -
데이터베이스 인덱스(Index)는 테이블 내의 데이터를 빠르게 검색할 수 있도록 지원하는 자료 구조입니다. 인덱스는 테이블의 특정 열(column)에 대해 생성됩니다. 이렇게 생성된 인덱스는 해당 열에 저장된 데이터의 값을 기준으로 정렬되어 있으며, 이를 이용하여 데이터를 빠르게 검색할 수 있습니다.

<br>

### **_인덱스의 원리_**
- - -
인덱스는 B-tree나 Hash Table과 같은 자료구조를 사용하여 구현됩니다. B-tree 인덱스는 데이터를 정렬하고 이진탐색(binary search) 알고리즘을 사용하여 검색합니다. 반면 Hash 인덱스는 해시 함수(hash function)을 사용하여 검색합니다.

<br>

### **_인덱스의 장단점_**
- - -

<span style="font-size: 20px">**⭐️ 인덱스의 장점**</span> <br>

1. **빠른 검색 속도**
   * 인덱스를 사용하면 데이터를 더 빠르게 검색할 수 있습니다.
2. **적은 리소스 사용**
   * 인덱스를 사용하면 데이터베이스 엔진이 데이터를 검색하는 데 필요한 리소스(시간, 메모리 등)가 줄어듭니다.
3. **데이터 정렬**
   * 인덱스를 생성할 때 정렬된 상태로 생성되기 때문에, 데이터를 정렬된 상태로 유지할 수 있습니다.


<span style="font-size: 20px">**💀️ 인덱스의 단점**</span> <br>

1. 인덱스를 생성할 때 추가적인 공간이 필요합니다.
2. 인덱스를 유지하기 위해 추가적인 리소스가 필요합니다.
3. 인덱스를 생성하면 데이터를 수정, 삭제, 삽입할 때 성능이 떨어질 수 있습니다.

<br>

### **_인덱스 사용시 고려사항_**
- - -
1. **인덱스 컬럼 선택**
   * 인덱스를 생성할 컬럼은 자주 검색되는 컬럼이어야 합니다. 불필요한 컬럼을 인덱스로 생성하면 인덱스 크기가 커지고 삽입, 수정, 삭제 작업의 성능이 저하될 수 있습니다.
2. **인덱스 타입 선택**
   * B-트리 인덱스는 범용적으로 사용되는 인덱스이며 대부분의 데이터베이스에서 기본 인덱스로 사용됩니다. 하지만 특정한 경우에는 해시 인덱스나 전문 검색 인덱스 등 다른 타입의 인덱스를 사용하는 것이 더 효율적일 수도 있습니다.
3. **인덱스 튜닝**
   * 인덱스를 생성해도 쿼리 성능이 향상되지 않을 경우, 인덱스의 튜닝 작업을 수행해야 합니다. 예를 들어 인덱스의 높이(height)가 너무 높은 경우(쿼리 실행 시 인덱스 블록을 계속해서 탐색해야 함), 인덱스 컬럼의 순서를 바꾸거나, 다중 컬럼 인덱스를 사용하거나, 인덱스 분할(partitioning) 등의 방법을 사용해서 인덱스를 튜닝할 수 있습니다.