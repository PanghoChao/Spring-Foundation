# Lombok
- Java라이브러리로 흔히 반복되는 getter, setter, toString등과 같이 다소 번거로울 수 있는 코드작성을 줄여주는 라이브러리다.
- 기본적으로 웹 애플리케이션에서 사용하는 VO객체

### 장점
 - 어노테이션 기반의 코드 자동생성으로 생산성 향상
 - 반복코드 다이어트를 통해 가독성 및 유지보수성 향상
 - Getter/Setter 외 빌더 패턴이나 로그생성등 다양한 방면으로 활용 가능

### 단점
- 개발자에 따라 호불호가 갈리는 라이브러리이다. 
- API설명이나 내부동작등을 숙지하고 사용하지 않으면, StackOverflowError 와 같은 문제가 발생할 수 있다. 
- 그외에도 여러 예외문제가 발생할 수 있다.

### 프로젝트 롬복 홈페이지
- 보다 자세히 알고 싶다면 아래 링크참조.
[참고링크](https://projectlombok.org/features/all)

## annotation
### @Getter/@Setter
- 특정 필드위에서 어노테이션을 붙여 주면, 자동으로 생성된 접근자와 설정자 메소드를 만들어준다.
- 그래서 다른곳에 생성자를 만들고 불러올때  get필드명, set필드명이 가능해진다.

### @RequiredArgsConstructor

### @ToString
### @EqualsAndHashCode

### @Data
 - @ToString, @EqualsAndHashCode,  @Getter/@Setter, @RequiredArgsConstructor 을 한번에 실행해준다.
 - 즉, 위에 어노테이션을 일일이 선언할 필요없이 @Data 하나 선언해주면 알아서 된다.
### @Builder
 - 빌더 패턴을 사용할 때 사용한다. 
 - 다수의 필드(전역변수)를 가지는 복잡한 클래스의 경우 생성자를 사용할 때, 순서를 헷갈려서 에러가 날수도 있다. 
    - ex) init(String name, PhoneNum phoneNum, String id)
    - 만약 생성자가 위와 같이 이름, 전화번호, 아이디 순이라면, 생성시에도 3가지 순서를 올바르게 넣어야 오류가 나질않는다.
    - new init("이름",01012345678, "아이디") - 올바른 생성
    - 하지만 @Builder 어노테이션이 있다면, new init("아이디", "이름",01012345678) 이렇게 너도된다는 것!
### @AllArgsConstructor


### @NoArgsConstructor
