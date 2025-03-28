
## 섹션 0. 시작하며

- 구 버전인 **페이지 라우터** 버전인 넥스트에 대해서 **4~5시간** 살펴보고, 신규 버전인 **앱 라우터** 버전의 넥스트에 대해서 **9~10시간** 정도 살펴볼 예정
- 페이지 & 앱 라우터 모두 넥스트에서 제공하는 기본적인 라우터
- 페이지 라우터: Next 초창기부터 제공되어 오던 구 버전의 라우터
- 앱 라우터: 2023년에 Next 13버전과 함께 처음으로 공개된 신규 라우터 (다양한 신규 기능을 제공한다)
- 앱 라우터는 페이지 라우터의 단점을 보완하기 위해 등장한 기술이고 아직은 과도기를 겪고 있는 기술

<br>

## 섹션 1.1 Next.js를 소개합니다

### Next.js 는...
- React.js 전용의 웹 개발 **"Framework"**
- React.js를 보다 더 강력하고 편하게 사용할 수 있는 기능들을 제공 함
- React.js **+ 페이지 라우팅, 빌트인 최적화 기능, 다이나믹 HTML 스트리밍**
- React.js의 **확장판**
- Vercel에서 개발
- 오픈소스로 운영되고 있음
- 카카오 웹툰, velog, inflearn, Rallit 등에서 이용하고 있음

### Next.js는 Library가 아닌 **FrameWork**
- 프레임워크와 라이브러리는 기능 구현에 있어서 주도권이 누구에게 있느냐에 따라 구분될 수 있음!
- **Framework:**
  - 예: Next.js, Remix
  - 주도권을 Framework가 가짐
  - 프레임워크가 제공하는 기능을 이용하거나, 허용하는 범위 내에서만 추가 도구 사용 가능
  - 방법이 다 정해져 있음!!
  - 자유도가 낮다 
  - 거의 모든 기능을 제공 (ex: Page Routing, Optimizations, Server Pre Rendering)
- **Library:**
  - 예: React.js, JQuery
  - 주도권을 개발자가 가짐
  - 기능 구현을 원하는 방향으로 진행한다
  - 쓰고 싶은 도구 및 기술을 쓴다
  - 자유도가 높다
  - 기본 기능 외 제공 X

<br> 

## 섹션 1.2 Next.js 사전렌더링 이해하기

### 사전 렌더링 (Pre Rendering)
- 브라우저의 요청에 사전에 렌더링이 완료된 HTML을 응답하는 렌더링 방식
- Client Side Rendering의 단점을 효율적으로 해결하는 기술

### Client Side Rendering(CSR)
- React.js 앱의 기본적인 렌더링 방식
- 클라이언트(브라우저)에서 직접 화면을 렌더링 하는 방식
- 페이지 이동이 매우 빠르고 쾌적하다는 장점이 있음 **But, FCP(초기 접속 속도)가 느리다**
  
**React의 렌더링 순서 및 원리:**
  1. 유저 to 서버: 유저가 브라우저를 통해 서버에게 접속 요청
  2. 서버 to 브라우저: index.html(빈껍데기) 전송
  3. 브라우저 to 유저: 서버에게 받은 html 파일을 화면에 렌더링 (빈 화면 렌더링)
  4. 화면에 아무것도 나오지 않음
  5. 서버 to 브라우저: 서버는 개발자가 작성한 리앱트 앱을 하나의 자바스크립트 파일로 묶어서 (JS Bundle) 후속으로 브라우저에게 보내줌
  6. 브라우저는 버들링된 자바스크립트를 직접 실행 (JS 실행) - 리앱트 앱 실행
  7. 컨텐츠 렌더링 - 리액트 컴포넌트들이 실제로 화면에 나타남
- **JS Bundle: 서비스에서 접근 가능한 모든 컴포넌트 코드 존재 -> 초기 접속 요청에 필요한 컴포넌트뿐만 아니라, 사이트 내부에서 접근할 수 있는 모든 페이지의 컴포넌트가 들어있음 -> 웹사이트에 필요한 전체 코드가 들어있음**
- **Hence, 유저가 페이지를 이동하게 되더라도 서버에게 새로운 페이를 요처할 필요 X => 브라우저가 이미 리액트 앱을 갖고있기 때문 (모든 페이지의 컴포넌트가 들어있음, 적절히 컴포넌트만 갈아끼우면 됨)**
- 대신 초기 접속 속도가 느림 (요청 시작 <-> 화면이 보임)
- **First Contentful Paint(FCP)**: 웹 페이지의 성능을 대표, 높아질수록 사용자의 이탈율이 가파른 속도로 증가

**Next.js의 SSR**
- Next.js를 대표하는 기능 중 하나
- JS 실행 (렌더링): 자바스크립트 코드(React 컴포넌트)를 HTML로 변환하는 과정
- 화면에 렌더링: HTML 코드를 브라우저가 화면에 그려내는 작업

1. 유저 to 서버: 유저가 브라우저를 통해 서버에게 초기 접속 요청을 보냄
2. 서버가 서버측에서 직접 자바스크립트 코드 (리액트 앱)을 실행을 시켜서, 우리가 만든 모든 리액트 컴포넌트들을 HTML로 변환, 즉 사전에 렌더링을 실행
3. 서버 to 브라우저: 렌더링된 HTML 파일을 그대로 브라우저에세 보내주게 됨
4. 브라우저 to 유저: HTML 파일을 그대로 화면에 렌더링 -> 사용자는 바로 완성된 화면을 보게됨
5. 현재 이 시점에서 인터렉션(상호 작용)은 동작하지 않음, HTML 파일 하나만 받은 상태이기 때문
6. 서버 to 브라우저가: 후속으로, 서버가 브라우저에게 작성한 모든 자바스크립트 코드 즉, 리앱트 앱을 번들링 해서 (= JS Bundle) 보내줌
7. 브라우저는 서버로부터 받은 리앱트 앱을 직접 실행해서 현재 화면에 렌더링 되어있는 HTML 요소들과 연결을 시켜줍니다.
8. 상호작용 가능
- TTI(Time to interact): 요청으로부터 hydration이 종료되는 시점까지의 시간
- 이후, 페이지 이동 요청은 CSR과 같은 방식으로 처리됨 (Hyradtion을 위해서 JS Bundle을 서버가 브라우저에게 전달했기 때문)

#### React App의 단점 해소 (빠른 FCP 달성) + React APP의 장점 승계 (빠른 페이지 이동)

  
