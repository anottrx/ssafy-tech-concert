<div align="center">
  <br />
  <h1>REST API 가이드?</h1>
  <br />
</div>

## 목차

1. [**REST API URI 가이드**](#1)
2. [**HTTP 응답 상태 코드**](#2)

<br />


<div id="1"></div>

##  ✅ REST API URI 가이드



### 1. 복수형 명사와 소문자를 사용한다.

 Bad
```
  http://ssafe.com/user
```
Good
```
  http://ssafe.com/users
```

### 2. 소문자를 사용한다.
주소에서 대소문자를 구분하므로, 카멜방식이 아닌 소문자를 사용하여 작성한다.

 Bad
```
  http://ssafe.com/users/postComment
```
Good
```
  http://ssafe.com/users/post-comments
```

### 3. 언더바를 대신 하이픈을 사용한다.
가급적 하이픈의 사용도 최소화하며, 정확한 의미나 표현을 위해 단어의 결합이 불가피한 경우에 사용한다.

Bad
```
  http://ssafe.com/users/post_comments
```
Good
```
  http://ssafe.com/users/post-comments
```
### 4. 마지막에 슬래시를 포함하지 않는다.
슬래시는 계층을 구분하는 것으로, 마지막에는 사용하지 않는다.

Bad
```
  http://ssafe.com/users/
```
Good
```
  http://ssafe.com/users
```
### 5. 행위는 포함하지 않는다.
행위는 URL대신 Method를 사용하여 전달한다.(GET, POST, PUT, DELETE 등)

Bad
```
  POST http://ssafe.com/users/1/create-posts
  DELETE http://ssafe.com/users/1/delete-post/1
  PUT http://ssafe.com/users/1/update-post/1
```
Good
```
  POST http://ssafe.com/users/1/posts
  DELETE http://ssafe.com/users/1/posts/1
  PUT http://ssafe.com/users/1/posts/1
```
### 6.파일 확장자는 URI에 포함시키지 않는다.
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 말고 Accept header를 사용하도록 한다.

Bad
```
  http://ssafe.com/users/moram.jpg
```
Good
```
  GET http://ssafe.com/users/moram
  HTTP/1.1 Host: ssafe.com Accept: image/jpg
```
### 7. 가급적 전달하고자하는 자원의 명사를 사용하되, 컨트롤 자원을 의미하는 경우 예외적으로 동사를 허용한다.

Bad
```
  http://ssafe.com/posts/registering
```
Good
```
  http://ssafe.com/posts/register
```


### 8. 검색, 정렬, 필터링 그리고 페이징을 위한 규칙 사용

| **상태 코드** | **설명** |
| --- | --- |
| _**Sorting**_ |  예를들어 클라이언트가 정렬된 회사 목록을 가져오려는 경우 다음의 예처럼 처리 <br/> ex) GET /companies?sort=date_desc |
| _**Filtering**_  | 데이터셋의 데이터를 필터링 할 때, 다양한 쿼리 파라미터를 통해 필터링 처리 가능   <br/> ex) GET /companies?name=삼성&job=back-end    |
| _**Searching**_ | 검색은 다음의 예제와 같이 표현  <br/> ex) GET /companies?search=companies |
| _**Pagination**_ |페이징 처리 예제   <br/> ex) _GET_ /companies?page=3 |


<div id="2"></div>

##  ✅ HTTP 응답 상태 코드 

 ### 200번대 : 성공

-   200: Ok, 클라이언트의 요청을 정상적으로 수행함.
-   201: Created, 클라이언트에게 생성 작업을 요청받았고, 생성 작업을 성공함.
-   204: No Content, 요청은 성공했으나 응답할 콘텐츠가 없음.
-   205: Reset Content, 요청은 성공했으나 클라이언트의 화면을 새로 고침하도록 권고
-   206: Partial Content, 요청은 성공했으나 일부 범위의 데이터만 반환함.
    
 ### 300번대 : 리다이렉션

 - 301: Moved Permantly, 클라이언트가 요청한 리소스에 대한 URI가 영구적으로 변경되었음을 의미.
 - 302: Found, 요청한 URI가 일시적으로 주소가 바뀌었을 경우를 의미.
 - 303: See Other, 요청한 자원이 임시 주소에 존재함.
 - 304: Not Modified, 이전에 방문했을 때의 요청 결과와 다르지 않을 경우(캐시 된 페이지를 그대로 사용)
 - 307: Temporary Redirect, 임시 페이지로 리다이렉트.
### 400번대 : 클라이언트 오류

- 400: Bad Request, 클라이언트가 올바르지 못한 요청을 보냄.
- 401: Unauthorized, 인증 혹은 승인되지 않은 접근(로그인을 하지 않아 페이지를 열 권한이 없음)
- 403: Forbidden, 금지된 페이지, 로그인을 하든 안하든 접근할 수 없음. (관리자 페이지)
- 404: Not found, 찾을 수 없는 페이지, 주소를 잘 못 입력했을 때 사용함.인증받지 않은 클라이언트로 부터 리소스를 숨기기 위해 403 대신에 사용할 수도 있음.(해커들의 공격을 방지하고자 페이지가 없는 것처럼 위장하는 경우)
- 405: Method Not Allowed, 허용되지 않은 요청 메소드를 받았을 경우.
- 408: Request Timeout, 요청 시간이 초과됨.
- 409: Conflict, 서버가 요청을 처리하는 과정에서 충돌이 발생한 경우. (회원가입 중 중복된 아이디인 경우)
- 410: Gone, 영구적으로 사용할 수 없는 페이지.

### 500번대 : 서버 오류

- 501: Not Implemented, 해당 요청을 처리하는 기능이 만들어지지 않음.
- 502: Bad Gateway, 서버로 가능 요청이 중간에서 유실된 경우.
- 503: Service Unavailable, 서버가 터졌거나 유지 보수 중(유지 보수 중일때는 유지 보수 중이라는 것을 알려주는 페이지로 전송해주는 것이 좋음)
- 504: Gateway Timeout, 서버 게이트웨이에 문제가 생겨 시간 초과가 된 경우.
- 505: HTTP Version Not Surpported, HTTP 버전이 달라 요청이 처리할 수 없음.

#### 🤣 그동안에 REST API 만들었다고 했었는데 이러한 세세한 부분까지는 신경써서 못했었던 것 같습니다. 프로젝트를 진행하면서 Rest api 작성 규칙을 엄청 많이 검색했었는데 이렇게 한번 정리하고 나서 URI 작성 법과 status code(일부분)은 안보고도 대답 할 수 있을 것 같습니다. 


## 참고 자료

> http://domoticx.com/http-status-codes/

> [REST? REST API? REST ful?](https://github.com/ssafy-tech-concert/ssafy-tech-concert/blob/master/web/REST.md) 

> [블로그](https://codingjhj.tistory.com/27)

> 새 창 열기 방법 : CTRL+click (on Windows and Linux) | CMD+click (on MacOS)
