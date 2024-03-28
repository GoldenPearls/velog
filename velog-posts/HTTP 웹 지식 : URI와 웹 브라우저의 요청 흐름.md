<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e1fcad90-9d05-433c-a9c8-040d46db17a3/image.png" /></p>
<blockquote>
<p>💡 간단 요약 : <code>URI</code>는 자원을 식별하는 방법으로, <code>URL</code>은 자원의 위치를, <code>URN</code>은 이름을 나타냐고 생각해. URL은 scheme, host, port, path, query, fragment 등으로 이뤄져 있어. <strong>웹 브라우저가 서버에 요청할 때는</strong> DNS 조회, HTTP 요청 생성, TCP/IP 연결 등이 순서대로 이루어져. 그리고 서버가 응답하면 데이터가 브라우저에 렌더링돼. URI는 자원을 유일하게 식별하는 데 쓰여.</p>
</blockquote>
<blockquote>
<p>🔗 사진과 강의 출처 : <a href="https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC">김영한님의 HTTP 웹 기본 지식</a></p>
</blockquote>
<h1 id="1-uriuniform-resource-identifier">1. URI(Uniform Resource Identifier)</h1>
<blockquote>
<p>URI는 로케이터(<strong>l</strong>ocator), 이름(<strong>n</strong>ame) 또는 둘 다 추가로 분류될 수 있다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/267e6e41-226e-4309-9221-de23897fa6e7/image.png" /></p>
<p>URI 안에 URL과 URN으로 구성되어 있다.</p>
<h2 id="1-url과-urn의-예시">1) URL과 URN의 예시</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/30baf40c-50cf-4e4b-b261-2a9658c8192d/image.png" /></p>
<h2 id="2-uri의-단어의-뜻">2) URI의 단어의 뜻</h2>
<ol>
<li><strong>Uniform</strong> : 리소스 식별하는 통일된 방식</li>
<li><strong>Resource</strong> : 자원, URI로 식별할 수 있는 모든 것(제한 없음)</li>
</ol>
<ul>
<li>실시간 교통 정보, 파일 등</li>
</ul>
<ol start="3">
<li><strong>Identifier</strong> : 다른 항목과 구분하는데 필요한 정보</li>
</ol>
<h2 id="3-url-urn-단어의-뜻">3) URL, URN 단어의 뜻</h2>
<ol>
<li>URL - Locator: 리소스가 있는 <code>위치</code>를 지정</li>
<li>URN - Name: 리소스에 <code>이름</code>을 부여</li>
</ol>
<ul>
<li>위치는 변할 수 있지만, 이름은 변하지 않는다.</li>
</ul>
<ol start="3">
<li>urn:isbn:8960777331 (어떤 책의 isbn URN)</li>
<li>URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음</li>
</ol>
<ul>
<li>앞으로 URI를 URL과 같은 의미로 이야기하겠음</li>
</ul>
<h2 id="4-url-전체-문법">4) URL 전체 문법</h2>
<ol>
<li>scheme://[userinfo@]host[:port][/path][?query][#fragment]</li>
</ol>
<ul>
<li><a href="https://www.google.com/search?q=hello&amp;hl=ko">https://www.google.com:443/search?q=hello&amp;hl=ko</a></li>
</ul>
<ol start="2">
<li>구성</li>
</ol>
<ul>
<li>프로토콜(https)</li>
<li>호스트명(<a href="http://www.google.com/">www.google.com</a>)</li>
<li>포트 번호(443)</li>
<li>패스(/search)</li>
<li>쿼리 파라미터(q=hello&amp;hl=ko)</li>
</ul>
<h2 id="5-url-scheme">5) URL scheme</h2>
<ol>
<li><strong>scheme:</strong>//[userinfo@]host[:port][/path][?query][#fragment]</li>
</ol>
<ul>
<li><strong>https:</strong>//<a href="http://www.google.com:443/search?q=hello&amp;hl=ko">www.google.com:443/search?q=hello&amp;hl=ko</a><ul>
<li>q : 검색 쿼리 검색어 hello</li>
</ul>
</li>
</ul>
<ol>
<li>주로 프로토콜 사용</li>
</ol>
<ul>
<li>프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙</li>
<li>예) http, https, ftp 등등</li>
<li>http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능</li>
<li><code>https</code>는 http에 보안 추가 (HTTP Secure)</li>
</ul>
<h2 id="6-usluserinfo">6) USL(userinfo)</h2>
<ol>
<li>scheme://<strong>[userinfo@]</strong>host[:port][/path][?query][#fragment]</li>
</ol>
<ul>
<li>URL에 사용자 정보를 포함해서 인증</li>
<li>거의 사용하지 않음</li>
</ul>
<h2 id="7-uslhost">7) USL(host)</h2>
<ul>
<li>scheme://[userinfo@]<strong>host</strong>[:port][/path][?query][#fragment]</li>
<li>https://<strong><a href="http://www.google.com">www.google.com</a></strong>:443/search?q=hello&amp;hl=ko</li>
<li>호스트명</li>
<li>도메인명 또는 IP 주소를 직접 사용가능</li>
</ul>
<h2 id="8-uslport">8) USL(PORT)</h2>
<ul>
<li>scheme://[userinfo@]host<strong>[:port]</strong>[/path][?query][#fragment]</li>
<li><a href="https://www.google.com:**443**/search?q=hello&amp;hl=ko">https://www.google.com:**443**/search?q=hello&amp;hl=ko</a></li>
<li>포트(PORT)</li>
<li>접속 포트</li>
<li>일반적으로 생략, 생략시 http는 80, https는 443</li>
</ul>
<h2 id="9-urlpath">9) URL(PATH)</h2>
<ul>
<li>scheme://[userinfo@]host[:port]<strong>[/path]</strong>[?query][#fragment]</li>
<li><a href="https://www.google.com:443/**search**?q=hello&amp;hl=ko">https://www.google.com:443/**search**?q=hello&amp;hl=ko</a></li>
<li>리소스 경로(path), <strong>계층적 구조</strong></li>
<li>예)<ul>
<li>/home/file1.jpg</li>
<li>/members</li>
<li>/members/100, /items/iphone12</li>
</ul>
</li>
</ul>
<h2 id="10-urlquery">10) URL(Query)</h2>
<ul>
<li>scheme://[userinfo@]host[:port][/path]<strong>[?query]</strong>[#fragment]</li>
<li><a href="https://www.google.com:443/search**?q=hello&amp;hl=ko">https://www.google.com:443/search**?q=hello&amp;hl=ko</a>**</li>
<li>key=value 형태</li>
<li><strong>?로 시작, &amp;로 추가 가능</strong> ?keyA=valueA&amp;keyB=valueB</li>
<li>query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태</li>
</ul>
<h2 id="11-urlfragment">11) URL(Fragment)</h2>
<ul>
<li>scheme://[userinfo@]host[:port][/path][?query]<strong>[#fragment]</strong></li>
<li><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/gettingstarted.html**#getting-started-introducing-spring-boot">https://docs.spring.io/spring-boot/docs/current/reference/html/gettingstarted.html**#getting-started-introducing-spring-boot</a>**</li>
<li>fragment</li>
<li>html <code>내부 북마크</code> 등에 사용</li>
<li>서버에 전송하는 정보 아님</li>
</ul>
<h1 id="2-웹-브라우저-요청-흐름">2. 웹 브라우저 요청 흐름</h1>
<h2 id="http-메세지-정보">HTTP 메세지 정보</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e5c23f20-a6a3-4552-b6ea-f777d5835ce9/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b6f2afb0-1222-4ed8-8b0c-b9072106aa1b/image.png" /></p>
<ol>
<li>DNS 조회(IP 매칭)</li>
<li>HTTPS PORT 생략</li>
<li>HTTP 요청 메세지 생성</li>
</ol>
<ul>
<li>HTTP 버전 정보</li>
<li>Host 정보</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/52e175f3-fc80-42af-bcdd-db5c508dcbc2/image.png" /></p>
<ol start="4">
<li>SOCKET 라이브러리를 통해 전달</li>
</ol>
<ul>
<li>A : TCP/IP 연결(IP, PORT)</li>
<li>B : 데이터 전달</li>
</ul>
<ol start="5">
<li>TCP/IP 패킷 생성, HTTP 메세지 포함</li>
</ol>
<ul>
<li>웹브라우저가 만든 전송 데이터</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8450d75b-df1d-477f-80f6-507738cf37c9/image.png" /></p>
<ol start="6">
<li>웹 브라우저가 구글 서버에게 <code>요청</code> 패킷 전달</li>
<li>요청 패킷 도착</li>
<li>구글 서버가 웹 브라우저에게 <code>응답</code> 패킷 전달</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6ae7f1b5-3d17-4308-a41e-d7027d0c1f9e/image.png" /></p>
<ul>
<li>응답하는 데이터 타입은 HTML에 UTF-8</li>
</ul>
<ol start="9">
<li>응답 패킷 도착</li>
<li>웹 브라우저 HTML 렌더링</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3619a388-7dc3-458a-8e64-adf3ad169995/image.png" /></p>