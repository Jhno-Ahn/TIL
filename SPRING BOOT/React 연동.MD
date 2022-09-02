## Axios(엑시오스) 설치
- 벡엔드와의 통신을 위해 Axios를 설치해야한다.
- VS Code를 실행하여 터미널을 켜고 npm i axios 를 입력하여 설치한다.
- 설치가 완려되면 pakage.json 파일을 열어보면 axios가 추가된 것을 확인 할 수 있다.
![](https://velog.velcdn.com/images/spwwy3437/post/8befa466-f9fe-49f4-99a5-2d08cab82cf7/image.png)


## 프론트엔드 파일 수정
- VS Code의 my-app 폴더의 srt\App.js 파일을 수정한다.
```java
import React, { useState, useEffect } from 'react';
import './App.css';
import customAxios from './customAxios';

function App() {
  // IP주소 변수 선언
  const [ip, setIp] = useState('');

  // IP주소 값을 설정합니다.
  function callback(data) {
    setIp(data);
  }

  // 첫번째 렌더링을 다 마친 후 실행합니다.
  useEffect(
    () => {
      // 클라이언트의 IP주소를 알아내는 백엔드의 함수를 호출합니다.
      customAxios('/ip', callback);
    }, []
  );

  return (
    <div className="App">
      <header className="App-header">
        이 기기의 IP주소는 {ip}입니다.
      </header>
    </div>
  );
}

export default App;
```

- my-app 폴더에 src 아래에 customAxios.js 파일을 생성해 아래 코드를 추가해준다.
```java
import axios from 'axios'; // 액시오스

export default function customAxios(url, callback) {
  axios(
    {
      url: '/api' + url,
      method: 'post',

      /**
       * 개발 환경에서의 크로스 도메인 이슈를 해결하기 위한 코드로
       * 운영 환경에 배포할 경우에는 15~16행을 주석 처리합니다.
       * 
       * ※크로스 도메인 이슈: 브라우저에서 다른 도메인으로 URL 요청을 하는 경우 나타나는 보안문제
       */
      baseURL: 'http://localhost:8080',
      withCredentials: true,
    }
  ).then(function (response) {
    callback(response.data);
  });
}
```

## 벡엔드 파일 수정
- 벡엔드는 클라이언트가 IP주소를 알아내는 함수를 호출하면 그 함수를 실행하고 IP주소 값을 반환하는 역할을 한다.


- SPRING BOOT에서 src\main\java\com\myapp\TestController.java 파일을 추가하여 코드를 작성해준다.

```java
package com.myapp;

import javax.servlet.http.HttpServletRequest;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class TestController {
	
	@PostMapping("/ip")
	public ResponseEntity<String> ip (HttpServletRequest request) {
		// 요청을 보낸 클라이언트의 IP주소를 반환합니다.
		return ResponseEntity.ok(request.getRemoteAddr());
	}
}
```

- src\main\java\com\myapp\WebConfig.java 파일을 추가하여 코드를 작성해준다.
```java
package com.myapp;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebConfig implements WebMvcConfigurer {
	/**
	 * 개발 환경에서의 크로스 도메인 이슈를 해결하기 위한 코드로
	 * 운영 환경에 배포할 경우에는 15~18행을 주석 처리합니다.
	 * 
	 * ※크로스 도메인 이슈: 브라우저에서 다른 도메인으로 URL 요청을 하는 경우 나타나는 보안문제
	 */
	@Override
	public void addCorsMappings(CorsRegistry registry) {
		registry.addMapping("/api/**").allowCredentials(true).allowedOrigins("http://localhost:3000");
	}
}
```

## 개발단계에서 프론트엔드(React) 코딩하며 벡엔드와 연동하기

### 1. jar파일 만들기
- Spring Boot에서 프로젝트 우클릭 Run As -> Maven Clean 클릭 후 실행이 종료되면
- 다시 프로젝트 우클릭 Run As -> Maven install 클릭해서 jar 파일생성
- 프로젝트 경로 폴더\target으로 가면 jar파일이 생성된 것을 확인할 수 있다.
![](https://velog.velcdn.com/images/spwwy3437/post/c5bc5232-6479-489d-b74f-952c525030f9/image.png)

### 2. 벡엔드 실행하기
- cmd창을 열고 프로젝트 경로 폴더>java -jar ./target/my-app-backend-1.0.0.jar 를 쳐서 실행
- jdk버전이 맞지 않는 경우에는 실행이 안될 수도 있으니 버전을 미리 확인한다.
- 아래 사진과 같이 나오면 VS Code를 열고 프론트엔드 코딩하면 된다.
![](https://velog.velcdn.com/images/spwwy3437/post/61a9d9e5-a6a1-4f8a-9fac-388c46970b74/image.png)


## 개발단계에서 벡엔드(Spring Boot) 코딩하며 프론트엔드와 연동하기
- VS Code 터미널 창을 열고 프로젝트 경로 > npm start를 입력한다.
![](https://velog.velcdn.com/images/spwwy3437/post/0dec68a4-b9dc-438e-b6da-7ea19a6316ad/image.png)

- 아래 사진과 같이 위에서 준비했던 IP주소가 나오면 성공이다.
![](https://velog.velcdn.com/images/spwwy3437/post/91e1f9c3-26aa-4327-a709-109513e5b94b/image.png)
- Spring Boot 환경에서 벡엔드를 코딩하고 실행한다.

## 출처
- https://joshua-dev-story.blogspot.com/2020/01/react-spring.html


