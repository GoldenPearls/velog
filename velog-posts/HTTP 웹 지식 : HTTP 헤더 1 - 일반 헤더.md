<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/04318658-1435-4ba8-b7b6-045bc6b9de88/image.png" /></p>
<h1 id="1-http-헤더-개요">1. HTTP 헤더 개요</h1>
<h2 id="http-헤더">HTTP 헤더</h2>
<ol>
<li>header-field = field-name &quot;:&quot; OWS field-value OWS (OWS:띄어쓰기 허용)</li>
<li>field-name은 대소문자 구문 없음</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/82aeb62c-9732-4a30-adfa-c0b9488e6778/image.png" /></p>
<h3 id="1-용도">1) 용도</h3>
<ul>
<li>HTTP 전송에 필요한 모든 부가정보</li>
<li>예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐
시 관리 정보...</li>
<li>표준 헤더가 너무 많음</li>
<li>필요시 임의의 헤더 추가 가능</li>
</ul>
<h2 id="http-표준">HTTP 표준</h2>
<ul>
<li>1999년 RFC2616 폐기</li>
<li>2014년 RFC7230~7235 등장</li>
</ul>
<h3 id="1-rfc723x-변화">1) RFC723x 변화</h3>
<ol>
<li>엔티티(Entity) -&gt; <code>표현(Representation)</code></li>
<li>Representation = representation Metadata + Representation Data</li>
<li>표현 = 표현 메타데이터 + 표현 데이터</li>
</ol>
<h3 id="2-http-body--message-body---rfc7230최신">2) HTTP BODY : message body - RFC7230(최신)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/abccba84-a31e-466b-a461-ee6d8f39f608/image.png" /></p>
<ol>
<li>메시지 본문(message body)을 통해 표현 데이터 전달</li>
<li>메시지 본문 = <strong>페이로드(payload)</strong></li>
<li><code>표현</code>은 요청이나 응답에서 전달할 실제 데이터</li>
<li><strong>표현 헤더</strong>는 <strong>표현 데이터</strong>를 해석할 수 있는 정보 제공</li>
</ol>
<ul>
<li>데이터 유형(<strong>html, json</strong>), 데이터 길이, 압축 정보 등등</li>
</ul>
<ol start="5">
<li>참고: 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 하지만, 여기서는 생략</li>
</ol>
<h1 id="2-표현">2. 표현</h1>
<blockquote>
<p>회원이라는 리소스를 데이터 표현 : HTML, JSON 한다.</p>
</blockquote>
<ol>
<li>실제 리소스는 추상적인데 DB에 있을 수도 있고 바이트 코드로 저장 되어 있다 </li>
<li>클라이언트와 서버 간의 실제로 주고받을 때 이해할 수 있는 뭔가 변환해서 데이터 전달</li>
<li>바이너리데이터를 그대로 전달하는 게 아닌 그 상태로 HTML로 가기도 XML로 전송하기도 JSON으로 전송하기도 한다. </li>
<li>이 리소스를 JSON, HTML, XML으로 표현한다는 의미</li>
</ol>
<h2 id="표현의-언어">표현의 언어</h2>
<ul>
<li>Content-Type: 표현 데이터의 형식(어떤 형식으로 갔는지 알기 위해)</li>
<li>Content-Encoding: 표현 데이터의 압축 방식</li>
<li>Content-Language: 표현 데이터의 자연 언어(한국형인지, 영어인지) ⇒ 원래는 페이드로드 헤더지만</li>
<li>Content-Length: 표현 데이터의 길이</li>
<li>표현 헤더는 전송, 응답 둘다 사용</li>
</ul>
<h3 id="1-content-type">1) Content-Type</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/62930802-0ee5-4b12-8cdb-9ea9d702172a/image.png" /></p>
<ol>
<li>미디어 타입, 문자 인코딩</li>
<li>예)</li>
</ol>
<ul>
<li>text/html; charset=utf-8</li>
<li>application/json</li>
<li>image/png</li>
</ul>
<h3 id="2-content-encoding">2) Content-Encoding</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6f084d2a-f58a-4ae2-b5ec-b9c6d05a9645/image.png" /></p>
<ul>
<li>표현 데이터 인코딩</li>
<li>표현 데이터를 압축하기 위해 사용</li>
<li>데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가</li>
<li>데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제</li>
<li>예)gzip, deflate, identity</li>
</ul>
<h3 id="3-content-language">3) Content-Language</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/72c7801a-763d-4c58-8a12-c92505bf3288/image.png" /></p>
<ul>
<li>표현 데이터의 자연 언어</li>
<li>표현 데이터의 자연 언어를 표현</li>
<li>예) ko, en, en-US</li>
</ul>
<h3 id="4-content-length">4) Content-Length</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0ec90d10-a314-408a-b87a-a10dde911b53/image.png" /></p>
<ul>
<li>표현 데이터의 길이</li>
<li>바이트 단위</li>
<li>Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨</li>
</ul>
<h1 id="3-콘텐츠-협상콘텐츠-네고시에이션">3. 콘텐츠 협상(콘텐츠 네고시에이션)</h1>
<blockquote>
<p>모든 것을 맞출 수는 없지만 최대한 맞춰주기</p>
</blockquote>
<ul>
<li>클라이언트가 선호하는 표현 요청</li>
<li>서버가 그거에 맞춰서 만들어줌</li>
</ul>
<ol>
<li>Accept: 클라이언트가 선호하는 미디어 타입 전달</li>
<li>Accept-Charset: 클라이언트가 선호하는 문자 인코딩</li>
<li>Accept-Encoding: 클라이언트가 선호하는 압축 인코딩</li>
<li>Accept-Language: 클라이언트가 선호하는 자연 언어</li>
</ol>
<ul>
<li>협상 헤더는 요청시에만 사용</li>
</ul>
<h2 id="accept-language-적용-전">Accept-Language 적용 전</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/109d65d3-c93c-4b97-b0c9-e3948055ba57/image.png" /></p>
<h2 id="aceept-language-적용-후">Aceept-Language 적용 후</h2>
<ul>
<li>헤더로 처리</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/640ca8dd-3d86-456f-adbb-a3d57f97b20e/image.png" /></p>
<h2 id="accept-language-복잡한-예시">Accept-Language 복잡한 예시</h2>
<ul>
<li>한국어가 안 된다면 영어로라도…</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6007c344-405b-404e-a9b7-14c77d6badfa/image.png" /></p>
<h3 id="1-협상과-우선순위-1--quality-valuesq">1) 협상과 우선순위 1 : Quality Values(q)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0e336c5c-3237-44a0-a598-1dec5e5a7e57/image.png" /></p>
<ol>
<li>Quality Values(q) 값 사용</li>
<li>0~1, 클수록 높은 우선순위</li>
</ol>
<ul>
<li>생략하면 1</li>
</ul>
<ol start="3">
<li>Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7</li>
</ol>
<ul>
<li><ol>
<li>ko-KR;q=1 (q생략)</li>
</ol>
</li>
<li><ol start="2">
<li>ko;q=0.9</li>
</ol>
</li>
<li><ol start="3">
<li>en-US;q=0.8</li>
</ol>
</li>
<li><ol start="4">
<li>en;q=0.7</li>
</ol>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3b2ab2e3-1317-4e3b-9e34-176ca51470ee/image.png" /></p>
<h3 id="2-협상과-우선순위-2--quality-valuesq">2) 협상과 우선순위 2 : Quality Values(q)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/95198d45-7088-45a0-89d7-573a10fdf2dc/image.png" /></p>
<ul>
<li>구체적인 것이 우선한다.</li>
<li>Accept: text/<em>, text/plain, text/plain;format=flowed, */</em></li>
</ul>
<ol>
<li>text/plain;format=flowed</li>
<li>text/plain</li>
<li>text/*</li>
<li><em>/</em></li>
</ol>
<h3 id="3-협상과-우선순위-3">3) 협상과 우선순위 3</h3>
<ul>
<li>구체적인 것을 기준으로 미디어 타입을 맞춘다.</li>
<li>Accept: text/<em>;q=0.3, text/html;q=0.7, text/html;level=1,
text/html;level=2;q=0.4, */</em>;q=0.5</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ebb3e90c-8d7d-4f69-8d3e-93440c94e932/image.png" /></p>
<h1 id="4-전송방식">4. 전송방식</h1>
<ul>
<li>Transfer-Encoding</li>
<li>Range, Content-Range</li>
</ul>
<h2 id="전송-방식-설명">전송 방식 설명</h2>
<h3 id="1-단순-전송content-length">1) 단순 전송(Content-Length)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/82423ae4-b610-428b-81af-f905012ebd51/image.png" /></p>
<ul>
<li>컨텐츠 길이를 알 수 있을 때 사용</li>
</ul>
<h3 id="2-압축-전송content-encoding">2) 압축 전송(Content-Encoding)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7cf7d4ef-3d63-453e-9b99-24a024491590/image.png" /></p>
<ul>
<li>서버에서 압축하면 용량이 줄어든다.</li>
<li>뭘로 압축되어 있는지를 보내줘야 함</li>
</ul>
<h3 id="3-분할-전송transfer-encoding">3) 분할 전송(Transfer-Encoding)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9c63de5c-7b52-4d74-b1d9-f4097e72d5b1/image.png" /></p>
<ul>
<li>덩어리를 쪼개서 보낼거야</li>
<li>0이 끝을 의미</li>
<li>Content-Lanages를 보내면 안됨</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/650839ad-ae21-449f-a943-0e4aae0a19e3/image.png" /></p>
<h3 id="4-범위-전송range-content-range">4) 범위 전송(Range, Content-Range)</h3>
<ul>
<li>범위를 지정해서 전송</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/eb1a9c27-950c-49d5-acfb-9101f94a7650/image.png" /></p>
<h1 id="5-일반-정보">5. 일반 정보</h1>
<h2 id="1-from">1) From</h2>
<blockquote>
<p><strong>유저 에이전트의 이메일 정보</strong></p>
</blockquote>
<ul>
<li>일반적으로 잘 사용되지 않음</li>
<li>검색 엔진 같은 곳에서, 주로 사용</li>
<li>요청에서 사용</li>
</ul>
<h2 id="2-referer">2) Referer</h2>
<blockquote>
<p><strong>이전 웹 페이지 주소</strong></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/fa990754-c659-4029-a107-6ff9145b3964/image.png" /></p>
<ul>
<li>현재 요청된 페이지의 이전 웹 페이지 주소</li>
<li>A -&gt; B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청</li>
<li>Referer를 사용해서 유입 경로 분석 가능</li>
<li>요청에서 사용</li>
<li>참고: referer는 단어 referrer의 오타</li>
</ul>
<h2 id="3-user-agent">3) User-Agent</h2>
<blockquote>
<p><strong>유저 에이전트 애플리케이션 정보</strong></p>
</blockquote>
<ul>
<li>user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/</li>
</ul>
<p>537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36</p>
<ul>
<li>클라이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)</li>
<li>통계 정보</li>
<li>어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능</li>
<li>요청에서 사용</li>
</ul>
<h2 id="4-server">4) Server</h2>
<blockquote>
<p>요청을 처리하는 ORIGIN 서버의 소프트웨어 정보</p>
</blockquote>
<ul>
<li>Server: Apache/2.2.22 (Debian)</li>
<li>server: nginx</li>
<li>응답에서 사용</li>
</ul>
<h2 id="5-date">5) Date</h2>
<blockquote>
<p>메시지가 발생한 날짜와 시간</p>
</blockquote>
<ul>
<li>Date: Tue, 15 Nov 1994 08:12:31 GMT</li>
<li>응답에서 사용</li>
</ul>
<h1 id="6-특별한-정보">6. 특별한 정보</h1>
<h2 id="1-host">1) Host</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c5654755-79b0-496a-8438-71a9c6858c30/image.png" /></p>
<ul>
<li>요청한 호스트 정보(도메인)</li>
<li>요청에서 사용</li>
<li><strong>필수</strong></li>
<li>하나의 서버가 여러 도메인을 처리해야 할 때</li>
<li><strong>하나의 IP 주소에 여러 도메인이 적용되어 있을 때</strong></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6523b238-e17a-4ec9-af7e-ee8b9e3a45e2/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/053d6340-0431-4adb-bb49-f5337b87d449/image.png" /></p>
<h2 id="2-location페이지-리다이렉션">2) Location(페이지 리다이렉션)</h2>
<ul>
<li>웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
(리다이렉트)</li>
<li>응답코드 3xx에서 설명</li>
<li>201 (Created): Location 값은 요청에 의해 생성된 리소스 URI</li>
<li>3xx (Redirection): Location 값은 요청을 <strong>자동으로 리디렉션하기 위한 대상 리소스를
가리킴</strong></li>
</ul>
<h2 id="3-allow--허용-가능한-http-메서드">3) Allow : 허용 가능한 HTTP 메서드</h2>
<ul>
<li>405 (Method Not Allowed) 에서 응답에 포함해야함</li>
<li>클라이언트에서 지원하는 지 안하는지를 알수 있다.</li>
<li>서버에 많이 구현되어 있는 것은 아</li>
<li>Allow: GET, HEAD, PUT</li>
</ul>
<h2 id="4-retry-after">4) Retry-After</h2>
<ul>
<li><strong>유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간</strong></li>
<li>503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음</li>
<li>Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)</li>
<li>Retry-After: 120 (초단위 표기)</li>
</ul>
<h1 id="7-인증">7. 인증</h1>
<h2 id="1-authorization">1) Authorization</h2>
<ul>
<li>클라이언트 인증 정보를 서버에 전달</li>
<li>Authorization: Basic xxxxxxxxxxxxxxxx</li>
</ul>
<h2 id="2-www-authenticate">2) WWW-Authenticate</h2>
<ul>
<li>리소스 접근시 필요한 인증 방법 정의</li>
<li>401 Unauthorized 응답과 함께 사용</li>
<li>WWW-Authenticate: Newauth realm=&quot;apps&quot;, type=1,
title=&quot;Login to &quot;apps&quot;&quot;, Basic realm=&quot;simple&quot;</li>
</ul>
<h1 id="8-쿠키">8. 쿠키</h1>
<ul>
<li><code>Set-Cookie</code>: 서버에서 클라이언트로 쿠키 전달(응답)</li>
<li><code>Cookie</code>: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달</li>
</ul>
<h2 id="쿠키-미사용">쿠키 미사용</h2>
<h3 id="처음-welcome-페이지-접근">처음 welcome 페이지 접근</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9c090d62-c2e2-4dcf-be08-6844a8eacbef/image.png" /></p>
<h3 id="로그인">로그인</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/46d93828-70f5-4059-b326-59d024e4aa5f/image.png" /></p>
<h3 id="로그인-이후-welcome-페이지-접근">로그인 이후 welcome 페이지 접근</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/36bdab0d-c6bd-404a-8263-f00655647ea9/image.png" /></p>
<h3 id="대안--모든-요청에-사용자-정보-포함">대안 : 모든 요청에 사용자 정보 포함</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a7eff497-7a6c-4715-95c0-6b3710bd9934/image.png" /></p>
<h3 id="모든-요청에-정보를-넘기는-문제">모든 요청에 정보를 넘기는 문제</h3>
<ul>
<li>모든 요청에 사용자 정보가 포함되도록 개발 해야함</li>
<li>브라우저를 완전히 종료하고 다시 열면?</li>
</ul>
<h2 id="stateless">Stateless</h2>
<ul>
<li>HTTP는 <code>무상태(Stateless) 프로토콜</code>이다.</li>
<li>클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다.</li>
<li>클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못한다.</li>
<li>클라이언트와 서버는 서로 상태를 유지하지 않는다</li>
</ul>
<h2 id="쿠키">쿠키</h2>
<h3 id="로그인-1">로그인</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5c6ae06d-9c40-460f-96f1-485872fa7d25/image.png" /></p>
<h3 id="로그인-이후-welcome-페이지-접근-1">로그인 이후 welcome 페이지 접근</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8e34ef84-8d5b-4cc1-9ab7-75a3bb166ef4/image.png" /></p>
<h3 id="모든-요청에-쿠키-정보-자동-포함">모든 요청에 쿠키 정보 자동 포함</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/27e1bdbb-7a98-48a3-879f-870fac660929/image.png" /></p>
<h2 id="쿠키란">쿠키란?</h2>
<ol>
<li>예) set-cookie: <strong>sessionId=abcde1234; expires</strong>=Sat, 26-Dec-2020 00:00:00 GMT; <strong>path=/; [domain</strong>=.google.com](<a href="http://domain=.google.com/">http://domain=.google.com/</a>); <strong>Secure</strong></li>
<li><strong>사용처</strong></li>
</ol>
<ul>
<li>사용자 로그인 세션 관리</li>
<li>광고 정보 트래킹</li>
</ul>
<ol start="3">
<li><strong>쿠키 정보는 항상 서버에 전송됨</strong></li>
</ol>
<ul>
<li>네트워크 트래픽 추가 유발</li>
<li>최소한의 정보만 사용(세션 id, 인증 토큰)</li>
<li>서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 <code>웹 스토리지 (localStorage, sessionStorage)</code> 참고</li>
</ul>
<ol start="4">
<li>주의!</li>
</ol>
<ul>
<li>보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호 등등)</li>
</ul>
<h3 id="쿠키--생명주기">쿠키 : 생명주기</h3>
<ul>
<li>Expires, max-age</li>
</ul>
<ol>
<li>Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT</li>
</ol>
<ul>
<li>만료일이 되면 쿠키 삭제</li>
</ul>
<ol start="2">
<li>Set-Cookie: max-age=3600 (3600초)</li>
</ol>
<ul>
<li>0이나 음수를 지정하면 쿠키 삭제</li>
</ul>
<ol start="3">
<li><code>세션 쿠키</code>: 만료 날짜를 생략하면 <strong>브라우저 종료시 까지만 유지</strong></li>
<li><code>영속 쿠키</code>: 만료 날짜를 입력하면 <strong>해당 날짜</strong>까지 유지</li>
</ol>
<h3 id="쿠키--도메인">쿠키 : 도메인</h3>
<ol>
<li>예) <a href="http://domain=example.org/">domain=example.org</a></li>
<li><strong>명시: 명시한 문서 기준 도메인 + 서브 도메인 포함</strong></li>
</ol>
<ul>
<li>domain=example.org를 지정해서 쿠키 생성<ul>
<li>example.org는 물론이고</li>
<li>dev.example.org도 쿠키 접근</li>
</ul>
</li>
</ul>
<ol start="3">
<li>생략: 현재 문서 기준 도메인만 적용</li>
</ol>
<ul>
<li><a href="http://example.org/">example.org</a> 에서 쿠키를 생성하고 domain 지정을 생략<ul>
<li><a href="http://example.org/">example.org</a> 에서만 쿠키 접근</li>
<li>dev.example.org는 쿠키 미접근</li>
</ul>
</li>
</ul>
<h3 id="쿠키--경로">쿠키 : 경로</h3>
<ol>
<li>예) path=/home</li>
<li><strong>이 경로를 포함한 하위 경로 페이지만 쿠키 접근</strong></li>
<li>일반적으로 path=/ 루트로 지정</li>
</ol>
<ul>
<li>예)<ul>
<li>path=/home 지정</li>
<li>/home -&gt; 가능</li>
<li>/home/level1 -&gt; 가능</li>
<li>/home/level1/level2 -&gt; 가능</li>
<li>/hello -&gt; 불가능</li>
</ul>
</li>
</ul>
<h3 id="쿠키--보안">쿠키 : 보안</h3>
<ol>
<li><strong>Secure</strong></li>
</ol>
<ul>
<li>쿠키는 http, https를 구분하지 않고 전송</li>
<li><strong>Secure를 적용하면</strong> https인 경우에만 전송</li>
</ul>
<ol start="2">
<li><strong>HttpOnly</strong></li>
</ol>
<ul>
<li>XSS 공격 방지</li>
<li>자바스크립트에서 접근 불가(document.cookie)</li>
<li>HTTP 전송에만 사용</li>
</ul>
<ol start="3">
<li><strong>SameSite</strong></li>
</ol>
<ul>
<li>XSRF 공격 방지</li>
<li>요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송</li>
</ul>