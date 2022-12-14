
## SPA

Single Page Application, 사용자가 한 페이지에 머무르면서 필요한 데이터를 서버에서 받아와서
부분적으로 업데이트하는 방법


## CSR

Client Side Rendering, 
1. 웹 사이트 접속 시 프론트 서버로부터 index 파일을 받아옴
2. index 파일에서 웹 사이트에서 필요한 링크되어 있는 자바스크립트 요청
3. 클라이언트(브라우저) 측에서 어플리케이션에서 필요한 자바스크립트 링크로
4. 동적으로 HTML 생성할 수 있는 웹 어플리케이션이 담긴 자바스크립트 파일을 받아옴 <br>
   (어플리케이션에서 필요한 로직들, 어플리케이션을 구동하는 프레임워크, 리엑트 등 라이브러리 등, 소스코드 포함)

- 시간소요
- 추가로 필요한 경우 서버에 요청하여 데이터(JSON)를 받은 후, 클라이언트에서 동적으로 HTML 을 생성
- 리엑트, 뷰 ** 


#### 단점
- 사용자가 첫 화면을 보기까지 시간이 오래 걸린다는 점
- Low SEO(Search Engine Optimization)



## SSR

Server Side Rendering, 웹 사이트에 접속하면 서버 측에서 필요한 데이터를 다운받아 HTML 파일을 생성
후, 잘만들어진 HTML 파일을 동적으로 제어할 수 있는 소스코드롸 함께 클라이언트에게 전송
클라이언트는 HTML 파일을 렌더링하여 사용자에게 보여줌


- 첫번째 페이지 로딩이 빨라짐
- 효율적인 SEO


#### 단점

- 깜빡임 이슈 -> 클릭 시 전체적인 웹사이트를 다시 서버에서 받아오는 것과 동일
- 서버의 과부하 -> 사용자가 클릭할 수록 서버에서 요청해서 서버에서 필요한 데이터를 가져와서 HTML을 만듬으로 서버 과부하


### TTV(Time To View)

사용자에게 보여지는 시간

### TTI(Time To Interact)

사용자가 인터렉션이 가능한 시간



### Next.js





