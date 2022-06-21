## MVC MODEL 비교

|  | MODEL1 | MODEL2 |
| --- | --- | --- |
| Model | Java | Java |
| View | JSP | JSP |
| Controller | JSP | Servlet |
|  |  |  |

## MVC Model 2

### View(뷰) (JSP)

- 화면에 내용을 표출하는 역할을 담당.
- 단지 정보를 보여주는 역할만을 담당.
- 데이터가 어떻게 생성되고, 어디서 왔는지에 전혀 관여하지 않는다.

### Model(모델) (javaBean)

- 어플리케이션의 수행에 필요한 데이터를 모델링하고 비즈니스 로직을 처리
- 데이터를 생성하고 저장하고 처리하는 역할만을 담당
1. 컨트롤러의 요청을 받는다.
2. 비즈니스 로직(데이터베이스와 사용자 인터페이스 사이의 정보 교환을 처리하는 알고리즘)을 처리한다.
3. 처리한 비즈니스 로직의 결과를 컨트롤러로 반환한다.

### Controller(컨트롤러) (servlet)

- 어플리케이션의 흐름을 제어하는 것으로 뷰와 모델 사이에서 이들의 흐름을 제어.
- 사용자의 요청을 받아서 모델에 넘겨주고 모델이 처리한 결과를 뷰에 보내준다.
1. 클라이언트의 요청을 받는다.
2. 클라이언트가 요구하는 작업을 분석한다.
    1. String type = request.getParameter(”type”);
3. 비즈니스 로직을 처리하는 모델(javaBean)을 사용
4. 처리결과를 request 또는 session의 속성에 저장
    1. request.setAttribute(”result”,result);
5. 적당한 뷰를 선택 후 뷰로 포워딩. 서블릿에서 dispatcher.forward(request, response)로 해당 JSP페이지와 request, response를 공유한 경우 해당 JSP페이지에서 request.getAttribute(”result”와 같이 사용해서 결과를 화면에 표출한다.
