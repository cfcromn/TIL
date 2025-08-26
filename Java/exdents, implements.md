# extends, implements

## 상속(Inheritance)

자바에서 상속이란 기존 클래스를 재활용하여 **새로운 클래스**를 작성하는 자바의 문법 요소이다.

상속은 상위 클래스와 하위 클래스로 나누어 상위 클래스의 멤버를 공유하는 것을 의미한다

## Extends

- 상속의 대표적인 형태
- 부모 메소드를 그대로 사용할 수 있으며 오버라이딩 할 필요 없이 부모에 구현된 것을 직접 사용 가능하다.

```java
// 부모 클래스
class Animal {
    String name;

    void eat() {
        System.out.println(name + " is eating.");
    }
}

// 자식 클래스
class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog(); // dog 객체 생성
        dog.name = "Buddy";
        dog.eat();   
        dog.bark(); 
    }
}
```

## 오버라이딩(Overriding)이란?

오버라이딩은 부모클래스에서 상속 받은 메소드의 자식 클래스를 ****재정의** 하는 것이다.

## Implements

```java
// 인터페이스
interface Animal {
    void eat();
}

// 클래스가 인터페이스를 구현할 때 implements 사용
class Dog implements Animal {
    @Override
    public void eat() {
        System.out.println("Dog is eating.");
    }

    void bark() {
        System.out.println("Dog is barking.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();   
        dog.bark();  
    }
}
```

- implements는 부모의 메소드를 반드시 오버라이딩(재정의) 해야 한다.
- implemenis는 ****다중상속**을 대신해준다.

## extends와 implements의 차이점

### extends

- 부모에서 선언
- 정의를 모두하며 자식은 메소드 변수를 그대로 사용할 수 있다

### implemenis

- 부모 객체는 선언만 한다.
- 정의는 자식에서 오버라이딩해서 사용해야 한다.

### abstract

- extends와 interface의 혼합
- extends하되 몇 개는 추상 메소드로 구현 되어 있다.