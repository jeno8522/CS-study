# OOP, 메모리, JAVA특징

자료: https://minchoi0912.tistory.com/93
다중 선택: JAVA
주차: 1

# [OOP(객체지향프로그래밍)](https://universitytomorrow.com/15)

- OOP란?
    - 클래스 기반으로 인스턴스를 생성하여 서로 다른 행동을 시행, C++, JAVA가 OOP
    - C언어의 절차지향과 반대개념
- OOP의 특징
    - 재사용 가능
    - 유지보수 용이
    - 객체간 유기적 상호작용
- **가장 중요한 OOP 특징**
    - 캡슐화(Encapsulation)
        - 속성과 함수를 하나로 묶는것. 정보은닉 효과
        - ex) 여기서 '클래스'라는 개념은 객체를 만드는 틀(붕어빵 틀), '객체'라는 개념은 틀을 통해 만들어진 실체(붕어빵)를 의미합니다.
    - 추상화(Abstraction)
        - 공통특징(속성과 기능) 도출
        - ex) 아이패드와 갤럭시탭 두가지의 객체가 있다고 하면, 두 객체의 공통점(디스플레이가 있다, 스피커가있다, 카메라가 있다 전원을 켤 수있다 등)을 찾아내여 하나로 정의하는 것.
    - 상속성(Inheritance)
        - 부모(상위)클래스 특성을 하위(자식) 클래스가 물려받는것.
        - ex) 동물(호흡함 + 걸어다님) -> 포유류(호흡함 + 걸어다님 + 새끼에게 젖을 먹여 영양분을 공급함)
    - 다형성(Polymorphism)
        - 하나의 변수나 함수가 상황에 따라 다른 의미로 응답하는것.
        - ex) 동물소리를 내는 클래스가 있다면, 고양이를 입력 했을때 결과 값은 '야옹', 닭을 입력했을 때 결과값은 '꼬꼬댁' 으로 출력됨.
- 장점
    - 재사용 및 유지보수 용이
    - 생산성 향상 → 기존의 잘 설계된 클래스 재활용
    - 자연적 모델링 → 일상생활에 개념 그대로 갖다 붙히면됨
- 단점
    - 실행속도 느림 → 하드웨어 성능 발전으로 [JVM](https://doozi0316.tistory.com/entry/1%EC%A3%BC%EC%B0%A8-JVM%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B8%EA%B0%80) 기능이 향상되어 속도의 격차는 많이 줄었다.
    - 프로그램 용량이 큼
    - 설계에 많은시간 소요

# [JVM](https://doozi0316.tistory.com/entry/1%EC%A3%BC%EC%B0%A8-JVM%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B8%EA%B0%80)(Java Virtual Machine)

- 자바를 실행하기 위한 가상 기계
- OS에 종속받지 않고 CPU가 Java를 인식, 실행할 수 있게 해주는 가상 컴퓨터

# 메모리

- 저장 영역
    - 메소드 영역 : static변수, 전역변수, class 정보들 저장.
    - stack : 지역변수, 함수(메소드) 등이 할당
    - heap : new 연산자를 통해 동적 할당 된 객체 저장. 가비지 컬렉션에 의해 관리
- 기본형 vs 참조형
    - 기본형(Primitive Type)
        - stack메모리 영역에 실제값을 저장하는 데이터 타입
        - byte, short, int, long, float, double, char, boolean
        - Call By Value 호출방식
    - 참조형(Reference Type)
        - 메모리상 객체의 위치를 저장
        - String, Class, Interface….
        - new 연산자로 정의하며 실제값은 heap에 저장되고 stack에 메모리 주소만 저장
        - Call By Reference

# [가비지 컬렉션(GC)](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%EC%85%98GC-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC#heap_%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%9D%98_%EA%B5%AC%EC%A1%B0)

- 가비지 컬렉션(Garbage Collection)이란?
    - 유효하지 않은 메모리(Garbage)를 JVM의 가비지 컬렉터가 알아서 정리
- GC 동작 과정
    - Young Generation(영역)
        - 새로 생성된 객체가 할당되는 영역
        - 대부분 객체가 금방 Unreachable 상태가 되기에 많은 객체가 여기서 생성되었다가 사라진다.(큰공간 필요없음)
        - Minor GC이 발생
    - Old Generation(영역)
        - Young 영역에서 Reachable 상태를 유지해서 살아남은 객체가 복사되는 영역
        - Young 영역보다 크고 그만큼 Garbage는 적게 발생
        - Major GC(Full GC)이 발생
    
    ![Untitled](OOP,%20%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5,%20JAVA%E1%84%90%E1%85%B3%E1%86%A8%E1%84%8C%E1%85%B5%E1%86%BC%20e6e17f3cf31749c48b98b1f5b21c30d0/Untitled.png)
    

![Untitled](OOP,%20%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5,%20JAVA%E1%84%90%E1%85%B3%E1%86%A8%E1%84%8C%E1%85%B5%E1%86%BC%20e6e17f3cf31749c48b98b1f5b21c30d0/Untitled%201.png)

# 전역변수 vs 지역변수

- 전역변수
    - 함수 바깥에 선언하여 클래스 전체에서 사용가능한 변수
- 지역변수
    - 함수 안쪽에 선언하여 해당 함수 속에서만 사용 가능한 변수

# [객체 vs 인스턴스](https://velog.io/@dongvelop/Java-%ED%81%B4%EB%9E%98%EC%8A%A4-%EA%B0%9D%EC%B2%B4-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4)

- 객체(Object)란?
    - 자신 고유의 속성을 가지는 물리적, 추상적인 모든 대상을 일컫는다.
- 인스턴스(Instance)란?
    - 현실의 객체를 소프트웨어 내에서 구현한 실체라고 볼 수 있다.
    - 클래스를 사용하여 **힙 영역(Heap Area)에 새로운 인스턴스(객체)를 생성**할 수 있다.
- 대체로 객체와 인스턴스는 혼용해서 표현한다.

# [Static](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=heartflow89&logNo=220959033435)

- Static 의미
    - 객체를 생성하지도 않고도 사용할 수 있는 필드와 메소드
    - 객체를 마다 가지고 있을 필요가 없는 공용 데이터라면 static으로 선언
- Static 호환
    - 객체 생성을 하지 않고 사용 가능하기 때문에 인스턴스 필드, 메소드를 내부에서 사용 할 수 없음 → static끼리 놀아라
