# Upload
servlet과 spring을 이용하여 file upload를 구현해본다<br/>
<br/>
HTML 폼 전송 방식<br/>
 -application/x-www-form-urlencoded<br/>
 -multipart/form-data<br/>
 <br/>
 ![image](https://user-images.githubusercontent.com/69129562/207521802-962efc54-ca8b-41b4-a8b5-00ff74e48135.png)
<br/>
application/x-www-form-urlencoded 방식은 HTML 폼 데이터를 서버로 전송하는 가장 기본적인
방법이다. Form 태그에 별도의 enctype 옵션이 없으면 웹 브라우저는 요청 HTTP 메시지의 헤더에 다음
내용을 추가한다.<br/>
Content-Type: application/x-www-form-urlencoded<br/>
그리고 폼에 입력한 전송할 항목을 HTTP Body에 문자로 username=kim&age=20 와 같이 & 로 구분해서
전송한다.<br/>
파일을 업로드 하려면 파일은 문자가 아니라 바이너리 데이터를 전송해야 한다. 문자를 전송하는 이
방식으로 파일을 전송하기는 어렵다. 그리고 또 한가지 문제가 더 있는데, 보통 폼을 전송할 때 파일만
전송하는 것이 아니라는 점이다.<br/>
이 문제를 해결하기 위해 HTTP는 multipart/form-data 라는 전송 방식을 제공한다<br/>
<br/>
![image](https://user-images.githubusercontent.com/69129562/207523569-b2809d0a-890e-43a7-acae-c3530662666b.png)
<br/>
multipart/form-data 방식은 다른 종류의 여러 파일과 폼의 내용 함께 전송할 수 있다. (그래서 이름이
multipart 이다.)<br/>
폼의 입력 결과로 생성된 HTTP 메시지를 보면 각각의 전송 항목이 구분이 되어있다. ContentDisposition 이라는 항목별 헤더가 추가되어 있고 여기에 부가 정보가 있다.<br/> 예제에서는 username ,
age , file1 이 각각 분리되어 있고, 폼의 일반 데이터는 각 항목별로 문자가 전송되고, 파일의 경우 파일
이름과 Content-Type이 추가되고 바이너리 데이터가 전송된다.
multipart/form-data 는 이렇게 각각의 항목을 구분해서, 한번에 전송하는 것이다.
<br/>
스프링은 MultipartFile 이라는 인터페이스로 멀티파트 파일을 매우 편리하게 지원한다.
<br/>
고객이 업로드한 파일명으로 서버 내부에 파일을 저장하면 안된다. 왜냐하면 서로 다른 고객이 같은
파일이름을 업로드 하는 경우 기존 파일 이름과 충돌이 날 수 있다. 서버에서는 저장할 파일명이 겹치지
않도록 내부에서 관리하는 별도의 파일명이 필요하다.



