# 기본세팅
- 설치에 앞서서, React를 사용하기 위해서는 Node.js를 먼저 설치를 해야하고
- React는 Visual Studio Code를 사용해서 실행할것이다.
- https://code.visualstudio.com/download 링크를 통해 Visual Studio Code 설치
- 설치가 완료되면 프로그램을 열어 본인이 원하는 폴더를 지정해서 설정해두자.


# Node.js 설치

### 설치파일 다운로드
- https://nodejs.org/ko/ 링크를 통해서 설치파일을 다운로드 한다.
- 기본적으로는 LTS파일로 다운받는게 좋다.
- 다운받은 파일을 실행하면 설치가 되는데, 다른 설정 없이 Next 버튼만 눌러서 설치하면 된다.
![](https://velog.velcdn.com/images/spwwy3437/post/ae7b1683-dc62-4098-8b8d-5f8a564f5f4b/image.png)


### 설치완료 확인
- 스튜디오 터미널을 열어 node --version을 입력해서 버전이 나오면 설치가 정상적으로 완료된것이다.
- 참고로 스튜디오 터미널은 상단의 터미널탭 -> 새 터미널을 클릭하여 띄울수 있다.
![](https://velog.velcdn.com/images/spwwy3437/post/36e60875-ff40-41ab-bd22-828dfb13b174/image.png)



# 리액트(React) 설치
- 스튜디오 터미널에 npx create-react-app my-app 명령어를 입력해주면 지정한 폴더에 설치가 시작된다.
![](https://velog.velcdn.com/images/spwwy3437/post/1e1b3c46-2174-45fe-b15c-f5f84c327237/image.png)

### 서버 실행
- 터미널에 cd my-app 을 입력해 디렉토리 이동해주고,
- npm start 를 입력해 서버를 실행해준다.
- 실행이 정상적으로 된다면, localhost:3000 주소로 아래 사진과 같은 창이 띄워진다.
![](https://velog.velcdn.com/images/spwwy3437/post/eb037f38-817d-4afd-95a9-b3625b59ef72/image.png)

![](https://velog.velcdn.com/images/spwwy3437/post/c2d7ac86-66f4-48cf-84a5-4f37114d77a0/image.png)


# 추가 확장 확장프로그램(필수아님)

### ESLint
- 자바스크립트는 인터프리터 언어이기 때문에 실행전까지 어디가 잘못됐는지 알 수 없는데
이 확장 프로그램을 사용하면 실행전에 문법을 검사해준다.
- 스튜디오 왼쪽에 큐브모양 클릭 후 ESLint 검색 후 설치

### Reactjs code snippets
- 리액트 자동완성 확장프로그램
- 스튜디오 왼쪽에 큐브모양 클릭 후 Reactjs code snippets 검색 후 설치

### Prettier - Code formatter
- 코드 정렬 프로그램
- 스튜디오 왼쪽에 큐브모양 클릭 후 Prettier 검색 후 설치

### 편의기능 설정
- FIle -> new File 해서 .prettierrc 파일 생성
- 아래 사진처럼 하나씩 코드 추가
- singleQuote : 따옴표 하나씩으로 자동 설정
- semi : 세미콜론 자동 추가
- tabWidth : 탭 2칸으로 설정
- trailingComma : 코드 작성하면 콤마 자동 생성





















