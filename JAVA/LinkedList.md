## LinkedList란?
* LinkedList?
  - 연속적인 메모리 공간에 저장되지 않으며, element들이 포인터(주소값)로 연결되어있는 자료구조
  - java의 Collection 프레임워크의 일부
* 자료 구조
  - Node
    + data
    + next
  - Head
  - 맨 마지막 Node의 next는 null
  - ref) https://www.geeksforgeeks.org/what-is-linked-list/?ref=lbp

* 시간 복잡도
  - 탐색
    + Head 노드부터 내가 원하는 데이터가 나올 때 까지 전부 탐색
    + O(n)
  - 추가/삭제
    + 추가, 삭제할 노드 주변 노드의 Link만 수정해주면 된다.
    + O(1)
    + 다만 삽입, 삭제할 노드를 탐색하는 과정이 필요한 경우 최악의 경우 O(n)의 시간복잡도를 갖는다.
      + ArrayList는 무조건 O(n)
* ArrayList vs LinkedList
  - LinkedList와 ArrayList의 가장 큰 차이점은 '메모리의 연속성'
    + ArrayList는 연속된 메모리 공간에 저장되어있는 배열, LinkedList는 주소값으로 서로 연결되어있는 구조
    + ref) https://www.nextree.co.kr/p6506/
    + ref) https://opentutorials.org/module/1335/8821
    + ref) https://webprogramcustom.tistory.com/47
  - LinkedList의 장점
    + 추가/삭제 연산의 최악의 경우 시간 복잡도 O(1)
    + 크기의 제약이 없음
      + 물론, 일반 배열과 달리 ArrayList는 크기를 가변적으로 늘릴 수 있지만, 내부적으로 capacity(default 10) 이상의 데이터가 들어오면 재조정하는 연산을 수행해야 하고, 이 연산의 비용이 비싸다.
  - LinkedList의 단점
    + 탐색 연산의 시간복잡도 O(n)
      + ArrayList는 O(1), i번째 index에 바로 접근 가능
* 언제, 어떤걸 사용?
  - LinkedList : 추가, 삭제가 많이 발생하는 경우
  - ArrayList : 탐색, 정렬이 많이 발생하는 경우
