<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/10625551-8095-4d58-add6-100f3576ab65/image.png" /></p>
<blockquote>
<p>💡 간단 요약 : 인터넷 통신은 IP 프로토콜을 통해 이뤄지고, TCP는 연결 지향적이고 신뢰성이 높은 가상 회선 방식, UDP는 간단하고 빠른 데이터그램 방식이야. TCP는 연결 설정 후 안전하게 데이터 전송하고, UDP는 빠르게 전송하되 순서나 에러에 대한 보장은 없어. 포트는 프로세스 식별에 쓰이고, DNS는 도메인 명을 IP 주소로 변환해줘.</p>
</blockquote>
<h1 id="1-모든-것이-httphypertext-transfer-protocol">1. 모든 것이 HTTP(HyperText Transfer Protocol)</h1>
<h2 id="1-http-메세지에-모든-것을-전송">1) HTTP 메세지에 모든 것을 전송</h2>
<ol>
<li>전송종류</li>
</ol>
<ul>
<li>HTML, TEXT</li>
<li>IMAGE, 음성, 영상, 파일</li>
<li>JSON, XML (API)</li>
</ul>
<ol start="2">
<li>거의 모든 형태의 데이터 전송 가능</li>
<li>서버간에 데이터를 주고 받을 때도 <strong>대부분 HTTP 사용</strong></li>
<li>1997년에 나온 <code>HTTP/1.1</code> 버전이 가장 많이 사용됨</li>
</ol>
<h2 id="2-기반-프로토콜">2) 기반 프로토콜</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0364c56a-a259-4b88-8f0f-bcb368105d6b/image.png" /></p>
<ol>
<li>TCP : HTTP/1.1, HTTP</li>
<li>UDP : HTTP/3</li>
</ol>
<h2 id="3-http-특징">3) HTTP 특징</h2>
<ol>
<li>클라이언트 서버 구조</li>
<li>무상태 프로토콜(스테이스리스), 비연결성</li>
<li>HTTP 메세지</li>
<li>단순함, 확장 기능</li>
</ol>
<h1 id="2-클라이언트-서버-구조">2. 클라이언트 서버 구조</h1>
<ol>
<li>Request, Response 구조</li>
<li>클라이언트는 서버에 요청을 보내고, 응답을 대기</li>
<li>서버가 요청에 대한 결과를 만들어서 응답</li>
</ol>
<h2 id="서버와-클라이언트-분리가-중요">서버와 클라이언트 분리가 중요</h2>
<ol>
<li>서버 </li>
</ol>
<ul>
<li>데이터</li>
<li>비즈니스 로직</li>
</ul>
<ol start="2">
<li>클라이언트</li>
</ol>
<ul>
<li>UI</li>
<li>사용성</li>
</ul>
<h1 id="3-무상태-프로토콜">3. 무상태 프로토콜</h1>
<h2 id="1-스테이스리스stateless">1) 스테이스리스(Stateless)</h2>
<ol>
<li>서버가 클라이언트의 상태를 보존 x</li>
<li>장점 : 서버 확장성 높음(스케일 아웃)</li>
<li>단점 : 클라이언트가 추가 데이터 전</li>
</ol>
<h2 id="2-stateful-stateless-차이">2) Stateful, Stateless 차이</h2>
<h3 id="stateful상태-유지">Stateful(상태 유지)</h3>
<ol>
<li>고객: 이 노트북 얼마인가요?</li>
<li>점원: 100만원 입니다. . (노트북 상태 유지)</li>
<li>고객: 2개 구매하겠습니다.</li>
<li>점원: 200만원 입니다. 신용카드, 현금중에 어떤 걸로 구매 하시겠어요?<strong>(노트북, 2개 상태 유지)</strong></li>
<li>고객: 신용카드로 구매하겠습니다.</li>
<li>점원: 200만원 결제 완료되었습니다. <strong>(노트북, 2개, 신용카드 상태 유지)</strong></li>
</ol>
<h3 id="stateless-중간에-점원이-바뀌면무상">Stateless 중간에 점원이 바뀌면?(무상)</h3>
<ol>
<li>고객: 이 노트북 얼마인가요?</li>
<li>점원A: 100만원 입니다.</li>
<li>고객: 2개 구매하겠습니다.</li>
<li>점원B: ? 무엇을 2개 구매하시겠어요?</li>
<li>고객: 신용카드로 구매하겠습니다.</li>
<li>점원C: ? 무슨 제품을 몇 개 신용카드로 구매하시겠어요?</li>
</ol>
<h2 id="3-stateful">3) Stateful</h2>
<ol>
<li><code>상태 유지</code>: 중간에 다른 점원으로 바뀌면 안된다.<strong>(중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다.)</strong></li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/14eeabc6-769b-44f3-bf7a-f3007cc2709c/image.png" /></p>
<h2 id="4-stateless">4) Stateless</h2>
<ul>
<li>아무 서버나 호출해도 된다.</li>
</ul>
<ol>
<li><code>무상태</code>: 중간에 다른 점원으로 바뀌어도 된다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4eb000d5-40ec-4659-8c06-528c54f0a6fc/image.png" /></p>
<ul>
<li>갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.</li>
<li>갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.</li>
<li>무상태에서는 고객이 필요한 정보를 그때 그때 넘겨줌 마지막말로만 구매할 수 있듯이</li>
<li>중간에 서버가 장애가 나면?</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1216568c-0486-40f9-bcb3-ef7cb387bbeb/image.png" /></p>
<ol start="2">
<li>무상태는 응답 서버를 쉽게 바꿀 수 있다. <strong>-&gt; 무한한 서버 증설 가능(스케일 아웃)</strong></li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0de15d34-0ad1-4bb8-a7f2-585b1a74a324/image.png" /></p>
<h2 id="5-stateless-실무-한계">5) Stateless 실무 한계</h2>
<ol>
<li>모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있다.</li>
<li>무상태<ul>
<li>예) 로그인이 필요 없는 단순한 서비스 소개 화면</li>
</ul>
</li>
<li>상태 유지 <ul>
<li>예) 로그인</li>
<li>로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지</li>
<li>일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지</li>
<li>상태 유지는 최소한만 사용</li>
</ul>
</li>
</ol>
<h1 id="4-비연결성connectionless">4. 비연결성(connectionless)</h1>
<h2 id="1-연결을-유지하는-모델">1) 연결을 유지하는 모델</h2>
<ul>
<li>서버는 연결을 계속 유지, 서버 자원 소모</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3e4ee9a9-e725-4857-a24a-a1e334bbc0a7/image.png" /></p>
<h2 id="2-연결을-유지하지-않는-모델">2) 연결을 유지하지 않는 모델</h2>
<ul>
<li>서버는 연결 유지X, 최소한의 자원 사용</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/14398cc4-ed8e-4c96-a25d-0862f6885ae9/image.png" /></p>
<h2 id="3-비-연결성">3) 비 연결성</h2>
<ol>
<li><code>HTTP</code>는 <strong>기본이 연결을 유지하지 않는 모델</strong></li>
<li>일반적으로 초 단위의 이하의 <strong>빠른 속도로 응답</strong></li>
<li>1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이
하로 매우 작음</li>
</ol>
<ul>
<li>예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않는다.</li>
<li>서버 자원을 매우 효율적으로 사용할 수 있음</li>
</ul>
<h2 id="4-비-연결성-한계와-극복">4) 비 연결성 한계와 극복</h2>
<ul>
<li>TCP/IP 연결을 새로 맺어야 함 - <code>3 way handshake 시간 추가</code></li>
<li>웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등
등 수 많은 자원이 함께 다운로드</li>
<li>지금은 <code>HTTP 지속 연결(Persistent Connections)</code>로 문제 해결</li>
<li>HTTP/2, HTTP/3에서 더 많은 최적화</li>
</ul>
<h2 id="5-http-초기--연결-종료-낭비">5) HTTP 초기 : 연결, 종료 낭비</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e2733a5e-70cf-438c-b585-2806cc35065e/image.png" /></p>
<h2 id="6-http-지속-연결persistent-connections">6) HTTP 지속 연결(Persistent Connections)</h2>
<ul>
<li>다 받을 때까지 연결을 유지해둠</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/023ec0f7-b901-4771-90e7-221cdb1c1a00/image.png" /></p>
<h2 id="7-스테이스리스를-기억하자서버-개발자들이-어려워하는-업무">7) 스테이스리스를 기억하자(서버 개발자들이 어려워하는 업무)</h2>
<ul>
<li>정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽</li>
<li>예) 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록</li>
<li>예) 저녁 6:00 선착순 1000명 치킨 할인 이벤트 -&gt; 수만명 동시 요청</li>
<li>보통 첫 페이지는 정적 페이지인 html(상태 없음) ⇒ 그 후 이벤트 버튼 누르게</li>
</ul>
<h1 id="5-http-메세지">5. HTTP 메세지</h1>
<h2 id="1-요청-메세지와-응답-메세지-구조">1) 요청 메세지와 응답 메세지 구조</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/74008ab2-b147-4859-9546-eaf7dffba786/image.png" /></p>
<h2 id="2-요청-메세지-공식-스펙">2) 요청 메세지 공식 스펙</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ff8425af-8ff5-4c6e-8cf4-0de00184edb1/image.png" /></p>
<h3 id="시작라인요청-메세지">시작라인(요청 메세지)</h3>
<ul>
<li>start-line = <strong>request-line</strong> / status-line</li>
<li><strong>request-line</strong> = method SP(공백) request-target SP HTTP-version CRLF(엔터)</li>
<li>HTTP 메서드 (GET: 조회)</li>
<li>요청 대상 (/search?q=hello&amp;hl=ko)</li>
<li>HTTP Version</li>
</ul>
<h3 id="시작라인요청메세지-http-메서드">시작라인(요청메세지-HTTP 메서드)</h3>
<ul>
<li>종류: GET, POST, PUT, DELETE...</li>
<li>서버가 수행해야 할 동작 지정<ul>
<li><code>GET</code>: 리소스 조회</li>
<li><code>POST</code>: 요청 내역 처리</li>
</ul>
</li>
</ul>
<h3 id="시작라인요청-메세지-요청-대상">시작라인(요청 메세지-요청 대상)</h3>
<ul>
<li>absolute-path[?query] (절대경로[?쿼리])<ul>
<li>절대경로= <code>&quot;/&quot;</code> 로 시작하는 경로</li>
<li>참고: *, http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.</li>
</ul>
</li>
</ul>
<h3 id="시작-라인요청메세지---http-버전">시작 라인(요청메세지 - HTTP 버전)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b0ed4622-d791-4e02-8bc8-d30d1661978c/image.png" /></p>
<ul>
<li>HTTP 버전</li>
</ul>
<h2 id="3-시작라인응답-메세지">3) 시작라인(응답 메세지)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d23d9a6c-5564-47f0-86ce-35ac8ef0f22b/image.png" /></p>
<ul>
<li>start-line = request-line / <strong>status-line</strong></li>
<li><strong>status-line</strong> = HTTP-version SP status-code SP reason-phrase CRLF</li>
<li>HTTP 버전</li>
<li><code>HTTP 상태 코드</code>: 요청 성공, 실패를 나타냄<ul>
<li>200: 성공</li>
<li>400: 클라이언트 요청 오류</li>
<li>500: 서버 내부 오류</li>
</ul>
</li>
<li>이유 문구: 사람이 이해할 수 있는 짧은 상태 코드 설명 글</li>
</ul>
<h2 id="4-http-헤더">4) HTTP 헤더</h2>
<ul>
<li>header-field = field-name &quot;:&quot; OWS field-value OWS <strong>(OWS:띄어쓰기 허용)</strong></li>
<li><strong>field-name</strong>은 대소문자 구문 없음</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6359f7c8-fdf3-4ee5-a098-8b22eb937143/image.png" /></p>
<h3 id="용도">용도</h3>
<ol>
<li>HTTP 전송에 필요한 <strong>모든 부가정보</strong></li>
</ol>
<ul>
<li>예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...</li>
</ul>
<ol start="2">
<li>표준 헤더가 너무 많음</li>
</ol>
<ul>
<li><a href="https://en.wikipedia.org/wiki/List_of_HTTP_header_fields">https://en.wikipedia.org/wiki/List_of_HTTP_header_fields</a></li>
</ul>
<ol start="3">
<li>필요시 임의의 헤더 추가 가능</li>
</ol>
<ul>
<li>helloworld: hihi</li>
</ul>
<h2 id="5-http-메세지-바디">5) HTTP 메세지 바디</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/97807144-52e6-458c-a6e4-fc47df226bee/image.png" /></p>
<h3 id="용도-1">용도</h3>
<ul>
<li>실제 전송할 데이터</li>
<li>HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능</li>
</ul>
<h2 id="6-단순함의-확장-가능">6) 단순함의 확장 가능</h2>
<ul>
<li>HTTP는 단순하다. 스펙도 읽어볼만...</li>
<li>HTTP 메시지도 매우 단순</li>
<li>크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술</li>
</ul>
<h2 id="7-http-정리">7) HTTP 정리</h2>
<ol>
<li>HTTP <code>메시지</code>에 <strong>모든 것을 전송</strong></li>
<li>HTTP 역사 <strong>HTTP/1.1</strong>을 기준으로 학습</li>
<li>클라이언트 서버 구조</li>
<li>무상태 프로토콜(스테이스리스)</li>
<li>HTTP 메시지</li>
<li>단순함, 확장 가능</li>
<li>지금은 HTTP 시대</li>
</ol>