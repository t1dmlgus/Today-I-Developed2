
# 락(Lock)

락은 여러 프로세스가 하나의 데이터로 동시에 접근할 때, 제어하는 방법입니다. <br>
'락을 획득한다는 것' 은 자원을 사용해도 된다는 의미이며, 다른 프로세스는 현재 락을 획득한 프로세스가 
잠금을 건 자원에 대해 사용할 수 없음을 의미합니다.


### 스핀락
락을 걸지 못하면 무한 루프를 돌면서 계속 락을 시도하는 동기화 기법 <br>
만약, 락을 얻지 못할 경우 쉬지 않고 락을 얻기까지 계속 요청을 시도하기 때문에 서버에 많은 부하를 줍니다. <br>
따라서 부하를 낮추기 위해, 락을 요청하는 시간을 길게했을 때 락을 얻을 수 있는 시간임에도 불구하고 설정해놓은
시간만큼 더 기다려야 하는 상황이 발생할 수도 있습니다. <br>
이를 위해 *분산락* 을 사용합니다.



### 분산락

서버가 여러 대인 분산환경애서 동일한 데이터에 대한 동기화를 보장하기 위해 사용되는 동기화 기법

여러 독립된 프로세스에서 하나의 공유 자원에 접근할 때, 데이터 결함이 발생하지 않도록 원자성을 보장하기 위해 
사용하는 동기화 기법




- 공유락
    - 데이터를 읽을 때 사용되는 락으로, 공유락 간 읽는 건 가능하지만 데이터를 쓰는 걸 방지합니다.
      일반적으로 select 경우 사용됩니다.
- 베타락
    - 데이터를 변경할 때 사용되는 락으로, 트랜잭션이 완료될 때까지 데이터에 어떤 접근도 허용하지 않는 걸 말합니다.

- 사용경험

  주문서비스 내 상품재고를 계산하면데 데이터 정합성 이슈가 생기게 되었고,
  이때 JPA Pessimitic Lock + 베타 락을 사용하여 동시성 이슈를 해결한 경험이 있습니다.
  이때 transaction이 데이터를 점유하기때문에 일정시간이 넘게 되면 해당 트랜잭션을 롤백한 경우가 있으며