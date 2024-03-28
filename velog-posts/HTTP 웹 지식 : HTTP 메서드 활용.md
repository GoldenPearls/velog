<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0914962d-e066-4645-ae6b-85ddf006ff3f/image.png" /></p>
<blockquote>
<p> 💡** 요약 :** <code>데이터 전송</code>은 주로 쿼리 파라미터와 메시지 바디를 통해 이루어져. 정적 데이터 조회는 주로 GET으로 처리되고, 동적 데이터 조회는 쿼리 파라미터를 활용해 검색과 필터링이 이뤄져. <code>HTML Form</code>을 사용한 데이터 전송은 회원 가입이나 상품 주문과 같은 경우에 POST로 처리돼, 주로 Content-Type은 application/x-www-form-urlencoded을 사용해.</p>
</blockquote>
<p><code>HTTP API 설계</code>에서는 컬렉션과 스토어 개념이 있어. <code>컬렉션</code>은 서버가 리소스 URI를 결정하고, <code>스토어</code>는 클라이언트가 리소스 URI를 결정해. URI 설계에서 문서는 단일 개념을 나타내고, <code>컬렉션</code>은 서버가 관리하는 리소스 디렉터리를 의미하며, <code>스토어</code>는 클라이언트가 관리하는 자원 저장소를 나타내. 컨트롤 URI는 추가 프로세스 실행을 위해 동사를 직접 사용해.</p>
<blockquote>
</blockquote>
<p>간단히 말하면, 데이터 전송 방식과 API 설계에서 각 상황에 맞게 메서드와 구조를 잘 활용하는 게 중요해!</p>
<h1 id="1-클라이언트에서-서버로-데이터-전송">1. 클라이언트에서 서버로 데이터 전송</h1>
<blockquote>
<p>사진 및 강의 출처 : <a href="https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC">모든 개발자를 위한 HTTP 웹 기본 지식</a></p>
</blockquote>
<h2 id="🖕데이터를-전달하는-방식은-크게-2가지">🖕데이터를 전달하는 방식은 크게 2가지</h2>
<h3 id="1-쿼리-파라미터를-통한-데이터-전송">1) 쿼리 파라미터를 통한 데이터 전송</h3>
<ul>
<li>GET</li>
<li>주로 정렬 필터(검색어)</li>
</ul>
<h3 id="2-메세지-바디를-통한-데이터-전송">2) 메세지 바디를 통한 데이터 전송</h3>
<ul>
<li>POST, PUT, PATCH</li>
<li>회원 가입, 상품 주문, 리소스 등록, 리소스 변경</li>
</ul>
<h2 id="👆-4가지-상황">👆 4가지 상황</h2>
<h3 id="1-정적-데이터-조회">1) <code>정적</code> 데이터 조회</h3>
<ul>
<li>이미지, 정적 텍스트 문서</li>
<li>쿼리 파라미터 미사용</li>
<li>조회는 GET 사용</li>
<li>정적 데이터는 일반적으로 쿼리 파라미터 없이 <strong>리소스 경로로 단순히 조회 가능</strong></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b8642375-9609-4530-ae35-e570a1c4cbe9/image.png" /></p>
<h3 id="2-동적-데이터-조회">2) <code>동적</code> 데이터 조회</h3>
<ul>
<li>주로 검색, 게시판 목록에서 정렬 필터(검색어)</li>
<li>쿼리 파라미터 사용</li>
<li>데이터 전송이 필요</li>
<li><strong>조회 조건을 줄여주는 필터</strong>, 조회 결과를 정렬하는 정렬 조건에 주로 사용</li>
<li>조회는 GET 사용</li>
<li>GET은 쿼리 파라미터 사용해서 데이터를 전달</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/97b40784-f8fa-41e0-9c62-d1404474c382/image.png" /></p>
<h3 id="3-html-form을-통한-데이터-전송">3) <code>HTML Form</code>을 통한 데이터 전송</h3>
<ul>
<li>회원 가입, 상품 주문, 데이터 변경</li>
</ul>
<ol>
<li>POST 전송 - 저장</li>
</ol>
<ul>
<li>쿼리 파라미터와 비슷한 형태로  HTTP 바디에 키 - Value로 넣고 서버에 전송</li>
<li>application/x-www-form-urlencoded : form으로 전송의 클라이언트와 서버와의 약속</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9efb636c-af2d-4f31-bb13-657cee1d92a8/image.png" /></p>
<ol start="2">
<li>GET 전송 - 저장</li>
</ol>
<ul>
<li>메세지 바디를 안쓰기 때문에</li>
<li>쿼리파라미터에 넣어버림</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4cbb4bcf-cb26-479e-8ea2-6dc5472acba4/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3bf7898a-c516-4c31-98e3-5b1120e2f26b/image.png" /></p>
<ol start="3">
<li>multipart/form-data</li>
</ol>
<ul>
<li>파일 전송을 위함</li>
<li>여러 컨텐츠에 타입을 보낼 수 있음</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d9bc3cff-790c-4fdf-9c04-20727630c245/image.png" /></p>
<h3 id="정리">정리</h3>
<ol>
<li>HTML Form submit시 <code>POST</code> 전송</li>
</ol>
<ul>
<li>예) 회원 가입, 상품 주문, 데이터 변경</li>
</ul>
<ol start="2">
<li>Content-Type: application/x-www-form-urlencoded 사용</li>
</ol>
<ul>
<li>form의 내용을 <strong>메시지 바디</strong>를 통해서 전송(key=value, 쿼리 파라미터 형식)</li>
<li>전송 데이터를 <strong>url encoding</strong> 처리<ul>
<li>예) abc김 -&gt; abc%EA%B9%80</li>
</ul>
</li>
</ul>
<ol start="3">
<li>HTML Form은 GET 전송도 가능</li>
<li>Content-Type: multipart/form-data</li>
</ol>
<ul>
<li><strong>파일 업로드</strong> 같은 바이너리 데이터 전송시 사용</li>
<li>다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 <strong>multipart</strong>)</li>
</ul>
<ol start="5">
<li>참고: HTML Form 전송은 GET, POST만 지원</li>
</ol>
<h3 id="4-html-api를-통한-데이터-전송">4) <code>HTML API</code>를 통한 데이터 전송</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/43d8d44a-c755-4e6d-b55c-8ebaf9b00450/image.png" /></p>
<ul>
<li>회원 가입, 상품 주문, 데이터 변경</li>
<li>서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)</li>
</ul>
<p><strong>ajax</strong>란?</p>
<ul>
<li>비동기식 자바스크립트</li>
<li>HTML 페이지 전체가 아닌 일부분만 갱신할 수 있도록 XMLHttpRequest객체를 통해 서버에 request</li>
</ul>
<h3 id="정리-1">정리</h3>
<ol>
<li>서버 to 서버</li>
</ol>
<ul>
<li>백엔드 시스템 통신</li>
</ul>
<ol start="2">
<li>앱 클라이언트</li>
</ol>
<ul>
<li>아이폰, 안드로이드</li>
</ul>
<ol start="3">
<li>웹 클라이언트</li>
</ol>
<ul>
<li>HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)</li>
<li>예) React, VueJs 같은 웹 클라이언트와 API 통신</li>
</ul>
<ol start="4">
<li>POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송</li>
<li>GET: 조회, 쿼리 파라미터로 데이터 전달</li>
<li>Content-Type: application/json을 주로 사용 (사실상 표준)</li>
</ol>
<ul>
<li>TEXT, XML, JSON 등등</li>
<li>지금은 데이터 전송의 JSON이 거의 표준이다.</li>
</ul>
<h1 id="2-http-api-설계-예시">2. HTTP API 설계 예시</h1>
<h2 id="🖕http-api---컬렉션">🖕HTTP API - 컬렉션</h2>
<ul>
<li><strong>POST 기반 등록</strong></li>
<li>예) 회원 관리 API 제공</li>
<li>PUT : 게시글 수정 같은 느낌</li>
</ul>
<h3 id="회원-관리-시스템-api-설계">회원 관리 시스템 API 설계</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/02aa1de6-f487-4ef4-bc53-9331dd384c5c/image.png" /></p>
<h3 id="post---신규-자원-등록-특징">POST - 신규 자원 등록 특징</h3>
<ol>
<li>클라이언트는 등록될 리소스의 URI를 모른다.</li>
</ol>
<ul>
<li>회원 등록 /members -&gt; POST</li>
<li>POST /members</li>
</ul>
<ol start="2">
<li>서버가 새로 등록된 리소스 URI를 생성해준다.</li>
</ol>
<ul>
<li>HTTP/1.1 201 Created
Location: /members/100</li>
<li>POST 등록시 <code>서버</code>가 <strong>새로운 URI를 만들어준다는 것이 가장 중요!!</strong></li>
</ul>
<ol start="3">
<li><strong>컬렉션(Collection)</strong></li>
</ol>
<ul>
<li><strong>서버가 관리</strong>하는 리소스 디렉토리</li>
<li>서버가 리소스의 URI를 생성하고 관리</li>
<li>여기서 컬렉션은 /members</li>
</ul>
<h2 id="👆-http-api---스토어">👆 HTTP API - 스토어</h2>
<ul>
<li><strong>PUT 기반 등록</strong></li>
<li>예) 정적 컨텐츠 관리, 원격 파일 관리</li>
</ul>
<h3 id="파일-관리-시스템-api-설계">파일 관리 시스템 API 설계</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5b55b5e6-0b46-4452-8c33-720e2bf02033/image.png" /></p>
<h3 id="put---신규-자원-등록-특징">PUT - 신규 자원 등록 특징</h3>
<ol>
<li>클라이언트가 <strong>리소스 URI를 알고 있어야 한다.</strong></li>
</ol>
<ul>
<li>파일 등록 /files/{filename} -&gt; PUT</li>
<li>PUT /files/star.jpg</li>
</ul>
<ol start="2">
<li>클라이언트가 직접 리소스의 URI를 지정한다.</li>
<li><code>스토어(Store)</code></li>
</ol>
<ul>
<li><strong>클라이언트가 관리</strong>하는 리소스 저장소</li>
<li>클라이언트가 리소스의 URI를 알고 관리</li>
<li>여기서 스토어는 /files</li>
</ul>
<h2 id="🤟-html-form-사용">🤟 HTML FORM 사용</h2>
<ul>
<li>웹 페이지 회원 관리</li>
<li><strong>GET, POST</strong>만 지원해서 제약이 있다.</li>
<li>AJAX 같은 기술을 사용해서 해결 가능 -&gt; 회원 API 참고</li>
<li>여기서는 순수 HTML, HTML FORM 이야기</li>
</ul>
<h3 id="api-설계">API 설계</h3>
<ol>
<li>등록의 경우 POST, GET를 같은 경로로 맞춰주지 않고 새로운 경로를 쓰면 서버에 문제가 생겨 POST의 최종 결과를 회원 등록 폼으로 보내야 할 때 못 돌아가기 때문에 <strong>같은 경로 맞추는 게 더 좋다.</strong></li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4198844e-6e81-4b48-a0bb-a74b35e4a30c/image.png" /></p>
<ol start="2">
<li><strong>컨트롤 URI</strong></li>
</ol>
<ul>
<li>GET, POST만 지원하므로 제약이 있음</li>
<li>이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용</li>
<li>POST의 /new, /edit, /delete가 컨트롤 URI</li>
<li>HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)</li>
<li>최대한 사용하지 말고 대체제로만 생각하자</li>
</ul>
<h3 id="정리-2">정리</h3>
<ol>
<li><strong>HTTP API - 컬렉션</strong></li>
</ol>
<ul>
<li>POST 기반 등록</li>
<li>서버가 리소스 URI 결정</li>
</ul>
<ol start="2">
<li><strong>HTTP API - 스토어</strong></li>
</ol>
<ul>
<li>PUT 기반 등록</li>
<li>클라이언트가 리소스 URI 결정</li>
</ul>
<ol start="3">
<li><strong>HTML FORM 사용</strong></li>
</ol>
<ul>
<li>순수 HTML + HTML form 사용</li>
<li>GET, POST만 지원</li>
</ul>
<h2 id="참고하면-좋은-uri-설계-개념">참고하면 좋은 URI 설계 개념</h2>
<ol>
<li><strong>문서(document)</strong></li>
</ol>
<ul>
<li>단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)</li>
<li>예) /members/100, /files/star.jpg</li>
</ul>
<ol start="2">
<li><strong>컬렉션(collection)</strong></li>
</ol>
<ul>
<li>서버가 관리하는 리소스 디렉터리</li>
<li>서버가 리소스의 URI를 생성하고 관리</li>
<li>예) /members</li>
</ul>
<ol start="3">
<li><strong>스토어(store)</strong></li>
</ol>
<ul>
<li>클라이언트가 관리하는 자원 저장소</li>
<li>클라이언트가 리소스의 URI를 알고 관리</li>
<li>예) /files</li>
</ul>
<ol start="4">
<li><strong>컨트롤러(controller), 컨트롤 URI</strong></li>
</ol>
<ul>
<li>문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행</li>
<li>동사를 직접 사용</li>
<li>예) /members/{id}/delete</li>
</ul>