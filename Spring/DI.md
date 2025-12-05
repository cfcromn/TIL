## DI(Dependency Injection)

의존성 주입은 객체 간의 의존성을 외부에서 주입하여 결합도를 낮추고, 코드의 유연성과 테스트 용이성을 높이는 방법입니다.

## 의존성(Dependency)이란?

어떤 객체(또는 클래스)가 다른 객체(또는 클래스)를 필요로 하는 관계입니다.

즉, A라는 클래스가 B라는 클래스를 사용해야 제대로 동작한다면,

“A는 B에 의존한다”라고 말합니다.

## 의존성을 주입하는 방법

- 생성자 주입 (Constructor Injection)
- Setter 주입 (Setter Injection)
- 필드 주입 (Field Injection)

## 생성자 주입 (Constructor Injection)

의존성을 생성자를 통해 주입하는 방식

### 특징

- 가장 일반적이고 권장되는 방식
- 불변성 보장: 의존성이 변경되지 않음
- 객체가 생성될 때 필요한 의존성이 모두 준비되어야 함

```java
class Engine {
    void start() { System.out.println("엔진 시동"); }
}

class Car {
    private final Engine engine;

    // 생성자 주입
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
    }
}
```

### 장점

- 테스트 하기 쉽다.
- 명확한 의존성 요구 사항
- 불변성(imutability)

## Setter 주입 (Setter Injection)

의존성을 세터(setter) 메서드를 통해 주입하는 방식

### 특징

- 의존성을 선택적으로 주입 가능
- 객체 생성 후 의존성을 설정
- 변경 가능성이 있어 불변성 보장 X
    
    ```java
    class Car {
        private Engine engine;
    
        // 세터 메서드로 주입
        public void setEngine(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            if (engine != null) engine.start();
            else System.out.println("엔진 없음");
        }
    }
    ```
    

### 장점

- 유연함 (선택적 주입 가능)
- 순환 의존 해결에 유리할 수 있음

### 단점

- 객체가 완전하지 않은 상태로 생성 될 수 있음
- Null 체크를 꼭 해줘야 함

## 필드 주입 (Field Injection)

의존성을 필드에 바로 주입하는 방식

### 특징

- 주입 코드가 가장 간단함
- 테스트/유지보수에 약함

```java
class Car {

    @Autowired  // Spring이 자동으로 주입
    private Engine engine;

    public void drive() {
        engine.start();
    }
}
```

### 장점

- 코드가 깔끔하고 짧음

### 단점

- 테스트 시 주입이 어렵다 (필드에 바로 접근해야 함)
- 의존성을 숨기기 때문에, 코드 가독성이 낮아질 수 있음