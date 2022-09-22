# 예외(Exception)


## CheckedException
- CheckedException은 RumtimeException을 상속하지 않은 클래스이며,
- **컴파일 시점에서 반드시 예외처리를 해야**


## UnCheckedException

- RuntimeException을 상속하여 런타임 시 발생하는 예외로, 애플리케이션 동작에 이상이 없음으로 
  예외처리하지 않아도 됨





### 예외처리

예외 처리 전략으로는 크케

- 예외복구
- 예외회피
- 예외전환

- 저는 DB Connectoin 과 같은 CheckedException 예외 복구 전략을 통해
  일정 시도 후에 실패하면 RuntimeException을 상속받는 커스텀예외를 사용해서 핸들링하는 방법을 사용하고 있으며,

- 비즈니스 로직의 경우 단순히 커스텀예외를 상속받은 예외를 던저셔 핸들링하는 방법을 사용하고 있습니다.