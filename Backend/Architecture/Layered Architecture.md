## Layered Architecture란?

Layered Architecture는 각 구성 요소들이 **관심사의 분리(Separation Concerns)**를 달성하기 위해 **‘책임’**을 가진 계층으로 분리한 아키텍처이다

## 관심사를 분리하는 이유

- 하나의 계층에 여러 관심사가 존재하면 해당 계층의 응집도가 떨어지고 결합도가 높아진다
- 각 계층의 관심사를 분리하면 계층의 응집도가 높아지고 결합도를 낮추어 재사용성과 유지보수성을 높일 수 있다

## 4-Tier Layered Architecture  **(N-tier)**

일반적인 계층형 아키텍처의 경우 4개의 레이어로 구분한다.

### 1. Presentation Layer

사용자와의 요청 및 응답 등 상호작용 처리에 관심사를 둔 계층으로 대표적인 구성요소로는 view와 controller가 있다

### 2. Business Layer (Domain Layer)

비즈니스 로직을 수행하는 것을 주 관심사로 가진다.

Presentation Layer에서 데이터를 가져와서 비즈니스 로직을 수행하고 결과를 Presentation Layer로 전달한다 대표적인 구성요소로는 Service와 Domain Model이 있

### 3. Persistence Layer (Data Access Layer)

데이터베이스에 직접적으로 접근하는데 관심사를 둔 계층으로 데이터베이스와 매핑되는 객체로서 엔티티를 영구히 관리하는 계층이다. 대표적인 구성요소로는 Repository, ORM, DAO가 있다.

### 4. Database Layer

실제 데이터베이스 서버가 운영되는 계층이다. 서비스에서 사용하고 있는 DB가 이 계층에 속할 수 있다.

## Layered Architecture의 의존성

한 계층에서 자신의 책임 외의 행위는 하위 계층에 의존하는 구조이다.

그러나 하위 계층은 상위 계층에 대한 어떠한 지식이나 정보가 없어야 한다.