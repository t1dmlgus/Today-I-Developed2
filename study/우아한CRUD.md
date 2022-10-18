
# 우하한 CRUD [우아한 테크 세미나]


## 클래스

속성 값을 담을 클래스가 필요하다.

- 만능 클래스
  - 명확하지 않은 역할 구분
    - 뷰 관점, 요청/응답 관점, 모든 속성의 집합
  - 무분별한 객체간 연관관계(의존성 이슈)
    - 성능 저하
      - 항상 연관된 객체를 다 조회하면 불필요한 쿼리가 날라감(eager)
      - N+1 문제
    - eager, lazy Loading 어떤 걸 써야할지 애매함
    - 객체 간 협력을 구성할 수 없음


## 패턴과 이름

- Java Beans
- VO(Value Object)
  - 식별성(ID)없이 속성만으로 동일성을 판단하는 객체 <br>
    (ex. Money.class, Color.class)
  - DTO 와 동일시 되기도 함
  
- DTO(Data Transfer Object)
  - 원격호출(요청, 응답)을 효율화하기 위해 나온 패턴
  - 레이어 간 경계를 넘어서 데이터를 전달하는 역할, 다만 다양한 객체의 역할을 'DTO'로 칭하는 건 고려해봐야 한다.
    - HTTP 요청으로 오는 파라미터를 담는 객체
    - QueryDSL에서 DB조회 결과를 담을 객체
  - 불변성(final)으로 구현하면 좋다 -> 왜?
  
- Entity
 - DB 테이블과 대응되는 객체(JPA), 연속성과 식별성의 맥락에서 정의되는 객체(DDD)


### Entity 감추기

- 캡슐화를 지키기 어려워진다.
  - @getter, @setter 등 꼭 필요하지 않는 속성이 외부로 노출됨 -> 
- JSP, 등 객체 참조
  - Entity에 의존적이기 때문에 수정시 뷰에서 에러발생 -> 컴파일 시점이 좁다
- JSON 응답
  - @JsonIgnore 등 클래스만 보고 런타임 시 예측해야 하는 난이도가 올라감

### 외부 노출용 DTO 따로 만들기

- Entity -> DTO 변환 로직은 컴파일 타임에 체크된다.
- DTO는 비교적 구조를 단순하게 가져갈 수 있다.
  - 단순한 JSON 응답, 
- 외부 인터페이스로 의식해서 관리가능
  - Swagger 활용
- 여러 Entity 조합 가능

### DTO 이름 고민

- 역할 별로 구분된 DTO 정의
  - 이슈 생성 요청(JSON): IssueCreationRequest, IssueCreationCommand
  - 이슈 조회 응답(JSON): IssueResponse, IssueDto, IssueDetail
  - 이슈 조회 조건: IssueQuery, IssueCriteria
  - 이슈 DB 통계 조회 결과: IssueStatRaw
  - 복합 조회 결과(이슈 + 코맨트): IssueCommentRow


## AGGREGATE 로 Entity 간 선긋기

### AGGREGATE 

하나의 단위로 취급되는 연관된 객체군, 객체망

- Entity + Value Object
- 엄격한 데이터 일관성, 제약사항으로 유지
- Transaction, Lock 범위(필수)
- 불변식, 데이터가 변결될 때마다 유지되어야 하는 규칙 <br>
  (ex. 주문 요청시 일정 금액 이상은 주문할 수 없다.)
- Document DB와 어울림

<br>

- AGGREGATE 1개 당, Repository 1개
  - 외부에서 AGGREGATE ROOT 를 통해서 접근가능 

### AGGREGATE 간 경계가 있는 시스템
  - 별도의 저장소, 또는 API 서버를 분리할 때 유리
    - eventual consistency
    - AGGREGATE 간 이벤트, SAGA, TCC 패턴 활용
  - AGGREGATE 별 캐시(Cache) 적용 수월 
  - 코드 간 영향성 파악 가능

### AGGREGATE 간 참조

- 다른 AGGREGATE 간 객체참조(ROOT) 가 아닌, ID 참조
  - 의존성 분리
  - ex. 대체키, 제네릭 타입, Spring Data JDBC.AggregateReference

```java
public class Issue {
  private Association<Repo> repoId;
}


public class Association<T>{
  private final long id;
  
  public Association(long id){
    this.id = id;
  }
}
```

### 여러 AGGREGATE 에 걸친 조회

- Service 레이어에서 조합
- JOIN이 필수인 경우
  - WHERE 절에 다른 AGGREGATE 속성이 필요한 경우
  - SELECT 결과까지 다른 AGGREGATE 속성을 포함할 경우



## Repository VS DAO



## JPA vs JDBC

### O/R Mapping

@Value : 값 객체 -> 불변객체

jpa : 프록시를 만들어야하는데

final 은 프록시를 만들 수 없다.
JPA 
Spring data jdbc 프록시를 만들지 않느다. -> final 가능

