# 객체 지향 프로그래밍 (Object Oriented Programming)
* 현실세계가 객체들 간의 상호작용에 의해 운영되듯, 프로그램도 객체라는 독립된 단위로 구성해 객체들 간 상호작용으로 프로그램이 실행되도록 프로그램 개발 방법

## 객체 지향 프로그래밍 vs 절차 지향 프로그래밍
* 절차 지향 프로그래밍
  * 데이터와 함수 분리
  * 함수 중심의 프로그래밍
  * 순차적 흐름 중시
  * 프로그래밍의 수정될 때 전체에 영향 미칠 가능성이 높음 

## 객체 지향 프로그래밍 vs 함수형 프로그래밍
* 함수형 프로그래밍
  * 순수 함수 
  * 공유 상태, 변경 가능한 데이터, 부작용 지양

## 구성 요소
* 현실 세계의 객체 (Object)
  * 실생활에 존재하는 명사형의 모든 실체
  * 사물, 개념 등
  * 식별 가능하며, **관련된 정보 (속성)와 행위 (기능)**을 외부에 제공 
  * e.g. 학생, 이름, 학과, 성적, 수강
* 클래스 (Class)
  * 객체 추상화
  * 현실 세계의 객체를 프로그램적으로 표현한 청사진
  * 정보 저장을 위한 **변수**와 기능을 정의한 **메소드**로 구성   
  * c.f. 메소드 (method) vs 함수 (function) ([출처](https://stackoverflow.com/questions/155609/whats-the-difference-between-a-method-and-a-function))
      * 메소드는 객체 관련
      * 함수는 객체와 독립적
  * e.g. 학생 클래스에 이름, 학과 속성과 출석하기, 시험 (중간고사/기말고사) 보기 기능 정의    
    ```
    class Student:
        # 생성자 : 인스턴스 변수 초기화
        # self (this) : 현재 실행 중인 인스턴스를 참조하는 데 사용
        def __init__(self, name, major):
            self.name = name
            self.major = major

        def attend(self, date, class_name):
            print("{0}일 {1} 수업에 {2}가 출석했습니다.", date, class_name, self.name)

        def take_exam(self, class_name, exam_type):
            print("{0}가/이 {1} 수업 {2}에 응시했습니다.", self.name, class_name, exam_type)
    ```    
* 인스턴스 (Instance)
    * 소프트웨어 객체
    * 클래스로부터 메모리에 생성된 실체
    * 고유 상태 정보를 가짐
    * 클래스에 정의한 기능 수행 가능
    ```
    student = Student('LEE SEUNGEUN', 'Philosophy')
    ```
* 메시지
    *  메시지 송수신을 통해 인스턴스 상호작용

## 객체지향 프로그래밍 절차
1. 객체 모델링
2. 클래스 정의
3. 인스턴스 생성 및 사용

## 객체 설계
* 객체지향 프로그래밍에서 클래스가 정의되면 클래스 동작 방식을 알 필요 없이 외부 인터페이스인 메소드를 사용하기만 하면 됨 (**객체지향 프로그래밍에서 클래스는 블랙박스에 해당**)
* 설계 절차
  1. 객체 후보 추출
      * 객체는 주로 명사형임
  2. 인스턴스 변수 식별
      * 해당 객체가 작업하기 위해 필요한 정보를 인스턴스 변수로 설정
  3. 인터페이스 설계
      * 객체에 관련된 동사형 (동작)을 검토해 인터페이스 설계
  4. 주요 메소드 재정비
      * 다른 객체와 상호작용하는 메소드 등은 하향식 설계 (top-down desing)과 단계별 개선 (stepwise refinement)를 통해 살을 붙임
  5. 설계 반복 검토
      * 새로운 클래스와 기존의 클래스를 왔다갔다 하며 검토
  6. 대안 탐색
  7. 단순화
      * 문제를 해결할 수 있는 가장 단순한 방법 고민

## 객체지향 관련 개념
* 캡슐화 (Encapsulation)
  * 객체가 어떻게 사용되는지와 객체의 상세사항에 대한 구현을 구분
  * 장점 
    * 모듈화 가능
    * **재사용성**을 높임
  * 캡슐화 vs 은닉화 (Data Hiding)
    * 데이터에 private 또는 protected 접근 제한자를 붙임으로써 데이터에 대한 직접적인 접근을 막고, 메소드로써 데이터에 접근하도록 함
    * 메소드로써 데이터 접근하도록 할 경우 변수에 값을 할당하기 전 입력 데이터를 검증할 수 있다는 장점이 있음
* 다형성 (Polymorphism)
  * 같은 선언부 (signature)를 가진 메소드를 여러 클래스가 구현함
  * 메소드의 선언부 (signature)
    ```
    # Python
    def attend(self, date, class_name):

    // Java
    public static final void main(String [] args) { ... }
    ```
  * 장점
    * 프로그램을 유연하게 만들어줌
  * 자바의 경우 오버라이딩 (상속 관련)과 관련
* 상속 (Inheritance)
  * 새로운 클래스 (하위 클래스 (subclass)가 됨)가 기존의 클래스로붕터 나옴
  * 장점
    * 기존 클래스의 코드를 재사용할 수 있음
  ```
  # Python
  class SuperClass:
    def __init__(self):
      self.super_instance_variable = 'I am super'

    def reusable_method(self):
      print('hi')

  class SubClass(SuperClass):
    def __init__(self, sub_instance_variable):
      super(self)
      self.sub_instance_variable = sub_instance_variable

  ```
  * 강한 결합 vs 느슨한 결합