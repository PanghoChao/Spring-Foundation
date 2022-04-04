# Ioc 와 DI

## DI(Dependency Injection)
외부로부터 메모리에 올라가있는 인스턴스의 레퍼런스를 인터페이스 타입의 파라미터로 의존관계를 설정하는것을 말한다.
 - 쉽게 말해 IoC가 저장해본 객체들을 가져와 사용할 때 쓰이는 용어이다.

### 의존관계(Dependency)?
그럼 여기서 의존관계란 무엇일까?

#### 장난감 예시
장난감을 예시로 들어보자 
<p align =center><img src ="/images/1.WhatIsSpring/2-1.dependency.png" width=80%></p>
- 위와 같이 배터리가 필요한 장난감이 있다. 
- 하나는 배터리를 분리할 수 없는 일체형이고 다른 하나는 배터리를 분리할 수 있는 분리형 이다. 
- 둘다 배터리가 없으면 움직이지 않는다. 이것은 장난감이 배터리에 의존하고 있다고 한다.

 
 
 #### 자바 코드 예시
 그럼이제 코드를 예시로 봐보자
 - 먼저 배터리 일체형의 경우
 ```
 public class ElectronicCarToy{
 
  private Battery battery;
  
  public ElectronicCarToy(){
     battery = new EnergyBattery();
  }
 
 ```
 
 > 생성자에서만 의존성을 주입해주는 상황이라, 배터리가 떨어지게 되면 새로운것으로 바꿔야 하기에 유연하지 못한 방식이다.
 
 ---
  - 배터리 분리형의 경우

 ```
  public class ElectronicCarToy{
 
  private Battery battery;
  
  public ElectronicCarToy(){
  
  }
  public void setBattery(Battery battery){
     this.battery = battery;
  }
  
 ```
 > setter, 생성자를 이용해서 외부에서 주입해주는 상황은 외부에서 배터리를 교채해줄 수 있기 때문에 일체형보다 유연한 방식이다.

- - -
 <br></br>
 
 ### 의존성 예시와 정리 
 ```
 import org.springframework.stereotype.Service;

@Service
public class BookService {

    private BookRepository bookRepository;

    public BookService(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }
}
```
```
@Service
public class BookRepository {
      // DI Test
}
```
위 코드와 같이 BookService 클래스가 만들어 지기 위해서는 BookRepository 클래스를 필요로 한다.
- 이것을 **BookService 클래스는 BookRepository 클래스의 의존성을 가진다**
- 하지만 BookRepository 클래스가 수정되었을때, BookService클래스도 함께 수정해야하는 문제가 발생한다.
  - 즉 결합도가 높아지게된다. 
- 위의 코드에서, BookRepository라는 클래스를 직접 new를 사용하여 객체를 주입하는 것이 아니라 **생성자를 사용하여 주입받는 것을 Inversion of Control** 이라고 한다.
  - 굳이 스프링이 아니더라고 IoC가 가능하다는 것이다.(생성자와 setter조합으로)
-  BookService와 BookRepository가 둘다 Bean으로 등록되어 있을 때,   
BookService의 생성자만 만들어주면 스프링 IoC 컨테이너가 BookRepository에 의존성 주입을 알아서 해준다.
    -(스프링 4.3 이후부터는 생성자가 하나인 경우는 @Autowired를 사용하지 않아도 된다)


그러면 굳이 IoC컨테이너를 사용하는 이유는 무엇일까?


 <br></br>

## IoC(Inversion of Controll)
오브젝트 생성, 관계설정, 사용, 제거 등 오브젝트 전반에 걸친 모든 제어권을 애플리케이션이 갖는게 아니라 프레임워크의 컨테이너에게 넘기는 개념을 말한다. 
- 가장 중요한 인터페이스는 BeanFactory, ApplicatonContext이다.
- 참고로 스프링 프레임워크만의 개념이 아니다.
- 스프링에서 오브젝트(Object)는 빈(Bean)이라고 칭한다.  [추후에 더 자세히 다루고자한다.]
- IoC를 이해하기전에 Class, Object, Instance의 개념을 알고오자 

### 기존의 자바 
 - Star라는 객체가 존재한다고 가정해보자
 - 그리고 make()라는 쓰레드에서 star객체를 사용하고자 한다면 아래와 같이 인스턴스를 만들어야 한다.
```
public void make(){
  star s = new star();
}
```
 - 이렇게 사용자(개발자)가 직접 서로 다른 객체간에 참조를 시켜줘야한다. 
---
 - 이번엔 user()라는 쓰레드에서도 star 객체를 사용하려고 한다. 
 ```
public void use(){
  star s = new star();
}
```
 - 위 상태도 아무런 이상이 없다.


> 허나, make()와 use()가 서로 독립적으로 관계가 없으면 상관이 없지만, 서로 데이터를 공유한다고 하면, 각자 인스턴스를 만들었기 때문에 
공유하기가 힘들어진다. 

그렇기 때문에 스프링에서는 직접 객체를 메모리에 등록해준다. 


### 클래스 호출 방식
클래스내에 선언과 구현이 같이 있기 때문에 다양한 형태로 변화가 불가능하다.

### 인터페이스 호출 방식
클래스를 **인터페이스**와 **인터페이스를 상속받아 구현하는 클래스**로 분리했다.    
구현클래스 교체가 용이하여 다양한 변화가 가능하다.   
그러나 구현클래스 교체시 호출클래스의 코드에서 수정이 필요합니다. (부분적으로 종속적)   

### 팩토리 호출 방식
팩토리 방식은 팩토리가 구현클래스를 생성하기 때문에 호출클래스는 팩토리를 호출 하는 코드로 충분하다.   
구현클래스 변경시 팩토리만 수정하면 되기 때문에 호출클래스에는 영향을 미치지 않는다.   
그러나 호출클래스에서 팩토리를 호출하는 코드가 들어가야 하는 것 또한 팩토리에 의존함을 의미한다.   

### IoC
팩토리 패턴의 장점을 더해 **어떠한 것에도 의존하지 않는 형태가 되었다.**    
실행시점에 클래스간의 관계가 형성이 된다. 즉, 의존성이 삽입된다는 의미로 IoC를 DI라는 표현으로 사용한다.

### IoC를 쓰는 이유 
 - 객체지향 원칙을 잘 지키기위해
 - 역할과 관심을 분리해 응집도를 높이고 결합도를 낮추며, 이에 따라 변경에 유연한 코드를 작성 할 수 있는 구조가 될 수 있기 때문


## 빈(Bean)이란?

### 주입방법

  - Autowired 어노테이션을 활용한다.
 ```
   @Autowired
    private CourseService courseService;

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }
 ```
