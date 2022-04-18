# Lombok
- Java라이브러리로 흔히 반복되는 getter, setter, toString등과 같이 다소 번거로울 수 있는 코드작성을 줄여주는 라이브러리다.
- Java 기반 애플리케이션에서 VO,DTO,Entity 등을 보다 쉽게 작성하기 위해 사용되는 라이브러리

### 장점
 - 어노테이션 기반의 코드 자동생성으로 생산성 향상
 - 반복코드 다이어트를 통해 가독성 및 유지보수성 향상
 - Getter/Setter 외 빌더 패턴이나 로그생성등 다양한 방면으로 활용 가능

### 단점
- 개발자에 따라 호불호가 갈리는 라이브러리이다. 
- API설명이나 내부동작등을 숙지하고 사용하지 않으면, StackOverflowError 와 같은 문제가 발생할 수 있다. 
- 그외에도 여러 예외문제가 발생할 수 있다.

### 프로젝트 롬복 홈페이지
- 롬복의 어노테이션은 크게 2가지로 나눌 수 있는데, 안정적인(stable) 것과 실험적인(exprimental) 것으로 나뉜다.
- 보다 자세히 알고 싶다면 아래 링크참조.   
[참고링크](https://projectlombok.org/features/all)

## annotation
자주사용하면서 안정적인(stable) 어노테이션만 정리해 보았다.
### @NonNull 
 - 변수에 선언을 해주면, 해당값은 반드시 값이 있어야 한다.
 - 만약 값이 없거나 null값이 들어오면 NullPointException예외를 일으킨다.

### @Getter/@Setter
- 특정 필드위에서 어노테이션을 붙여 주면, 자동으로 생성된 접근자와 설정자 메소드를 만들어준다.
- 그래서 다른곳에 생성자를 만들고 불러올때  get필드명, set필드명이 가능해진다.

### @RequiredArgsConstructor
 - 생성자를 만들어주는 어노테이션, final 또는 @NonNul인 필드 값만 파라미터로 받는 생성자
 - 아래 나오는 @AllArgsConstructor와 @NoArgsConstructor가 만드는 생성자를 제외한 나머지 생성자 생성이라고 볼 수 있다.
### @ToString
 - 필드를 기반으로 toString() 메소드를 자동생성하여, 
 - 속성으로 exclude를 사용하여 특정 필드를 toString() 결과에서 제외시킨다.
 - @ToString(exclude = "(필드명)") 으로 보통 개인정보와 같은 것을 방지하기위해 제외 시킨다.
 
 
### @EqualsAndHashCode
 - Equals와 HashCode 메소드를 자동으로 생성해준다.
    - equals : 두 객체의 내용이 같은지, 동등성을 비교하는 연산자
    - HashCode : 두 객체가 같은 객체인지, 동일성을 비교하는 연산자
- 속성 callSuper를 사용해서 메소드 자동 생성시 부모 클래스의 필드까지 고려할 것인지를 설정할 수 있다.
    - callSuper = false : 자신 클래스의 필드값만 적용
    - callSuper = true : 자신 클래스 뿐만아니라, 부모클래스 필드값도 체크

### @Data
 - @ToString, @EqualsAndHashCode,  @Getter/@Setter, @RequiredArgsConstructor 을 한번에 실행해준다.
 - 즉, 위에 어노테이션을 일일이 선언할 필요없이 @Data 하나 선언해주면 알아서 된다.
 - 알다시피 메소드를 자동으로 생성해준다는 것이지, 유효성검사한다던가, 예외처리를 해준다는 개념은 아님을 알고있자!  
  ---
  
### @Builder
 - 빌더 패턴을 사용할 때 사용한다. 
 - 다수의 필드(전역변수)를 가지는 복잡한 클래스의 경우 생성자를 사용할 때, 순서를 헷갈려서 에러가 날수도 있다. 
    - ex) init(String name, PhoneNum phoneNum, String id)
    - 만약 생성자가 위와 같이 이름, 전화번호, 아이디 순이라면, 생성시에도 3가지 순서를 올바르게 넣어야 오류가 나질않는다.
    - new init("이름",01012345678, "아이디") - 올바른 생성
    - 하지만 @Builder 어노테이션이 있다면, new init("아이디", "이름",01012345678) 이렇게 너도된다는 것!
### @AllArgsConstructor
 - 생성자를 자동으로 생성해주는 어노테이션
 - 필드 값을 모두 포함한 생성자를 생성해준다. 
### @NoArgsConstructor
- 생성자를 자동으로 생성해주는 어노테이션
- 파라미터(매개변수)가 없는 기본 생성자를 생성한다. 
