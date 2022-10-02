
## CORS

CORS는 Origin 간 리소스 공유 정책을 말합니다.

브라우저는 기본적으로 다른 출처에 대한 리소스를 공유하는 것을 제한합니다. 이와 같은 정책을 SOP라고 합니다. 출처 Origin은 url을 뜻합니다. 프로토콜 + host + 포트

출처에 대한 비교는 브라우저에서 일어납니다.

브라우저에는 쿠키, 로컬스토리지 등 사용자 정보를 저장할 수 있기에 다른 출처에 리소스를 공유하게 되면 보안상 취약해줄 수 있는 문제점 때문에 SOP가 생겼으며, 다른 출처에서 정보를 얻고자 한다면 CORS를 정의해야 한다.

기본적으로 브라우저는 **cross-origin 요청**을 전송하기 전에 **OPTIONS** 메소드로 **preflight**를 전송한다.

이때 **Response**로 **Access-Control-Allow-Origin**과 **Access-Control-Allow-Methods**가 넘어오는데 이는 서버에서 **어떤 origin**과 **어떤 method**를 허용하는지 브라우저에게 알려주는 역할을 한다.

브라우저가 결과를 성공적으로 확인하고 나면 **cross-origin** 요청을 보내서 그 이후 과정을 진행한다.

[https://dev-hyun.tistory.com/188](https://dev-hyun.tistory.com/188)

[https://hwanchang.tistory.com/3](https://hwanchang.tistory.com/3)