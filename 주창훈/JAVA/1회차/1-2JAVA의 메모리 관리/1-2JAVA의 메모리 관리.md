# JAVA의 메모리 관리

참고 - ([https://velog.io/@baek1008/JAVA-JAVA-메모리관리에-대해](https://velog.io/@baek1008/JAVA-JAVA-%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B4%80%EB%A6%AC%EC%97%90-%EB%8C%80%ED%95%B4))

## 1. Stack

- primitive 타입의 데이터가 할당 되는 영역, 지역변수들은 scope에 따라 visibility를 가진다.  (scope이 바뀌면 stack에 저장된 변수가 pop 된다)
    - 메소드가 종료되면 메소드 내의 지역변수는 stack에서 pop되어 사라진다.
- heap 영역에 할당된 Object 타입의 데이터들의 참조를 위한 값
- LIFO 의 직선형 구조 (stack)
- JVM의 각각의 스레드는 1개의 스택을 가지고 모든 메소드를 트래킹한다.

## 2. Heap

- 긴 생명주기의 데이터, 스레드의 갯수와 상관없이 heap은 하나
- Reference type의 객체, 배열등이 저장됨.
- 실제 데이터들을 가지고 있는 heap 영역의 데이터들의 주솟값을 stack에서 가짐
- new 연산자를 통한 동적할당된 객체 저장
- class를 선언할 때 class data는 heap에 저장, 주솟값을  stack에 저장
- 참조하는 변수가 없다면 heap에서 삭제 (JVM의 가비지 컬렉션 GC 가 삭제)

## 3. Static method area

- 필드 부분에서 선언된 변수(전역 변수), 정적 멤버 변수 (static 자료형)
- 프로그램 시작부터 종료까지 메모리에 남아있다.

tip) primitive type vs reference type

![Untitled](JAVA%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20e0f18cf18a1f4a52beb8319a825d6af1/Untitled.png)

## 4. 가비지 컬렉

![Untitled](JAVA%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20e0f18cf18a1f4a52beb8319a825d6af1/Untitled%201.png)

- method area, stack area에서 참조하고 있는 heap area의 객체들 중 어디서도 참조되고 있지 않은 객체 (Unreachable 한 객체)를 가비지 컬렉터가 제거

![Untitled](JAVA%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20e0f18cf18a1f4a52beb8319a825d6af1/Untitled%202.png)

- root로 부터 연결된 객체들을 그래프 순회로 찾고, 연결안된 객체를 제거, heap의 시작주소로 살아남은 객체들을 모아 압축

- heap 영역의 구조

![Untitled](JAVA%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20e0f18cf18a1f4a52beb8319a825d6af1/Untitled%203.png)

## 5. 가비지 컬렉션 동작 과정

1) 객체 생성 시 eden 영역에 age 0으로 저장됨

2) eden이 꽉차면 참조 정도에 따라 survivor0 영역으로 이동 or 제거, age 1증가

3) eden이 또 꽉차면 eden + survivor0이 survivor1로 이동 or 제거, age 1증가

반복

(위에서 제거하는 행위를 Minor GC라고 함)

4) 이 과정 반복시 age bit가 기준 이상이 되는 객체 등장, old generation으로 이동

5) old generation도 꽉차면 모든 객체들 검사해서 참조 안되는 객체 삭제, old generation영역의 메모리 회수 과정 (Major GC)

이 때 모든 스레드는 작업을 멈추어 “stop-the-world”라고 함, 이 작업이 너무 잦을 시 프로그램 성능에 문제가 생김