<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4feaeb00-5415-4418-939a-0e96d1f69314/image.png" /></p>
<blockquote>
<p>요약 : <code>상태 코드</code>는 클라이언트의 요청 처리 상태를 표시하며 <strong>주로 1xx(Informational), 2xx(Successful), 3xx(Redirection), 4xx(Client Error), 5xx(Server Error)로 분류</strong>된다. 모르는 상태 코드는 상위 카테고리로 처리되며, 클라이언트는 새로운 상태 코드 추가에도 변경 없이 대응할 수 있다. 이 구분은 요청 및 응답의 상태를 명확히 전달하고 이해하기 쉽게 도와준다.</p>
</blockquote>
<h1 id="1-http-상태코드">1. HTTP 상태코드</h1>
<blockquote>
<p>사진 및 강의 출처 : <a href="https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC">모든 개발자를 위한 HTTP 웹 기본 지식</a></p>
</blockquote>
<h2 id="🖕-상태-코드">🖕 상태 코드</h2>
<ul>
<li>클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능</li>
</ul>
<ol>
<li>1xx (Informational): 요청이 수신되어 처리중(거의 사용 X)</li>
<li>2xx (Successful): 요청 정상 처리</li>
<li>3xx (Redirection): 요청을 완료하려면 추가 행동이 필요</li>
<li>4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음</li>
<li>5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함</li>
</ol>
<h2 id="👆-만약-모르는-상태-코드가-나타나면">👆 만약 모르는 상태 코드가 나타나면?</h2>
<ol>
<li>클라이언트가 인식할 수 없는 상태코드를 서버가 반환하면?</li>
</ol>
<ul>
<li>클라이언트는 상위 상태코드로 해석해서 처리</li>
<li>미래에 새로운 상태 코드가 추가되어도 클라이언트를 변경하지 않아도 됨</li>
<li>예)<ul>
<li>299 ??? -&gt; 2xx (Successful)</li>
<li>451 ??? -&gt; 4xx (Client Error)</li>
<li>599 ??? -&gt; 5xx (Server Error)</li>
</ul>
</li>
</ul>
<h1 id="2-2xx--성공">2. 2XX -성공</h1>
<blockquote>
<p>클라이언트의 요청을 성공적으로 처리</p>
</blockquote>
<h2 id="1-200-ok">1) 200 OK</h2>
<ul>
<li>요청 성공</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a1ebd9a5-5a72-4100-8b42-1cf100b7d72f/image.png" /></p>
<h2 id="2-201-created">2) 201 Created</h2>
<ul>
<li>요청 성공해서 새로운 리소스 생성됨</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c7b200e7-e509-4eb5-85df-2ed56b88e90a/image.png" /></p>
<h2 id="3-202-accepted">3) 202 Accepted</h2>
<ul>
<li>요청이 접수되었으나 처리가 완료되지 않았음</li>
<li>배치 처리 같은 곳에서 사용</li>
<li>예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함</li>
<li>잘 사용 X</li>
</ul>
<h2 id="4-204-no-content">4) <strong>204 No Content</strong></h2>
<ul>
<li>서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음</li>
<li>예) 웹 문서 편집기에서 save 버튼</li>
<li>save 버튼의 결과로 아무 내용이 없어도 된다.</li>
<li>save 버튼을 눌러도 <strong>같은 화면을 유지해야 한다.</strong></li>
<li>결과 내용이 없어도 204 메시지(2xx)만으로 성공을 인식할 수 있다.</li>
</ul>
<h1 id="3-3xx---리다이렉션1">3. 3XX - 리다이렉션1</h1>
<ul>
<li>요청을 완료하기 위해 유저 에이전트(=웹 브라우저)의 추가 조치 필요</li>
</ul>
<h2 id="리다이렉션-이해">리다이렉션 이해</h2>
<ul>
<li>웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)</li>
</ul>
<h3 id="자동-리다이렉트-흐름">자동 리다이렉트 흐름</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d5621417-b4bd-4a32-aaf5-d10718292540/image.png" /></p>
<h3 id="종류">종류</h3>
<ol>
<li><strong>영구 리다이렉션</strong> : 특정 리소스의 URI가 영구적으로 이동</li>
</ol>
<ul>
<li>예) /members -&gt; /users</li>
<li>예) /event -&gt; /new-event</li>
</ul>
<ol start="2">
<li><strong>일시 리다이렉션</strong> : 일시적인 변경</li>
</ol>
<ul>
<li>주문 완료 후 주문 내역 화면으로 이동</li>
<li>PRG: Post/Redirect/Get</li>
</ul>
<ol start="3">
<li><strong>특수 리다이렉션</strong></li>
</ol>
<ul>
<li>결과 대신 캐시를 사용</li>
</ul>
<h2 id="1-영구-리다이렉션301-308">1) 영구 리다이렉션(301, 308)</h2>
<ul>
<li>리소스의 URI가 영구적으로 이동</li>
<li>원래의 URL를 사용X, 검색 엔진 등에서도 변경 인지</li>
</ul>
<h3 id="301-moved-permanently">301 Moved Permanently</h3>
<ul>
<li>리다이렉트시 요청 메서드가 <code>GET</code>으로 변하고, <strong>본문이 제거될 수 있음(MAY)</strong></li>
<li>완전 새로운 이벤트 페이지(메세지 제거로 인해)</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/53e96267-6420-45cc-ba9a-4a92ba342ab9/image.png" /></p>
<h3 id="308-permanent-redirect">308 Permanent Redirect</h3>
<ul>
<li>301과 기능은 같음</li>
<li>리다이렉트시 <strong>요청 메서드와 본문 유지</strong>(처음 POST를 보내면 리다이렉트도 POST 유지)</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f9fa46d2-c708-4314-8fd7-8e14fd07c062/image.png" /></p>
<h2 id="2-일시적인-리다이렉션302-307-303">2) 일시적인 리다이렉션(302, 307, 303)</h2>
<ul>
<li>가장 많이 사용</li>
<li>리소스의 URI가 일시적으로 변경</li>
<li>오던데로 들어와야 한다.</li>
<li>따라서 검색 엔진 등에서 URL을 변경하면 안됨</li>
</ul>
<h3 id="302-found">302 Found</h3>
<ul>
<li>리다이렉트시 요청 메서드가 <code>GET</code>으로 변하고, 본문이 제거될 수 있음(MAY) - 대부분 바뀌지만 아마라서 확실치는 않음</li>
</ul>
<h3 id="307-temporary-redirect">307 Temporary Redirect</h3>
<ul>
<li>302와 기능은 같음</li>
<li>리다이렉트시 요청 메서드와 <code>본문 유지</code>(<strong>요청 메서드를 변경하면 안된다.</strong> MUST NOT)</li>
</ul>
<h3 id="303-see-other">303 See Other</h3>
<ul>
<li>302와 기능은 같음</li>
<li>리다이렉트시 요청 메서드가 <strong>GET으로 변경</strong></li>
</ul>
<h2 id="3-prg-postredirectget일시적인-리다이렉션---예시">3) PRG: Post/Redirect/Get(일시적인 리다이렉션 - 예시)</h2>
<ul>
<li>POST로 주문후에 웹 브라우저를 새로고침하면?</li>
<li>새로고침은 다시 요청</li>
<li>중복 주문이 될 수 있다,</li>
</ul>
<h3 id="prg-사용-전">PRG 사용 전</h3>
<ul>
<li>새로고침을 하면 중복주문이 되어버림</li>
<li>새로고침 : 웹브라우저가 호스트의 마지막 요청을 다시 한 번 수행하기에 POST로 한 번 더 수행하며 중복주문이 되어버</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/090f6226-5270-476a-b5c9-b197a90dd004/image.png" /></p>
<h3 id="prg-사용-후">PRG 사용 후</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3495407c-6f30-4d35-8356-411797d779f5/image.png" /></p>
<ul>
<li>POST로 주문후에 새로 고침으로 인한 중복 주문 방지</li>
<li>URL이 POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트</li>
<li>새로고침해도 결과 화면을 <code>GET</code>으로 조회</li>
<li>중복 주문 대신에 결과 화면만 <code>GET</code>으로 다시 요청</li>
<li>서버의 부담도 줄어듦(물론 서버도 같은 주문번호 안되게 막아야 )</li>
</ul>
<h2 id="4-그래서-뭘-써야-하나요302-307-303">4) 그래서 뭘 써야 하나요?(302, 307, 303)</h2>
<h3 id="잠깐-정리">잠깐 정리</h3>
<ol>
<li>302 Found -&gt; GET으로 변할 수 있음</li>
<li>307 Temporary Redirect -&gt; 메서드가 변하면 안됨</li>
<li>303 See Other -&gt; 메서드가 GET으로 변경</li>
</ol>
<h3 id="역사">역사</h3>
<ul>
<li>처음 302 스펙의 의도는 HTTP 메서드를 유지하는 것</li>
<li>그런데 웹 브라우저들이 대부분 GET으로 바꾸어버림<strong>(일부는 다르게 동작)</strong></li>
<li>그래서 모호한 302를 대신하는 명확한 307, 303이 등장함(301 대응으로 308도 등장)</li>
</ul>
<h3 id="현실">현실</h3>
<ul>
<li>307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 <code>302</code>를 기본값으로 사용</li>
<li>자동 리다이렉션시에 GET으로 변해도 되면 그냥 302를 사용해도 큰 문제 없음</li>
</ul>
<h2 id="5-기타-리다이렉션300-304">5) 기타 리다이렉션(300 304)</h2>
<ol>
<li>300 Multiple Choices: 안쓴다.</li>
<li><strong>304 Not Modified</strong></li>
</ol>
<ul>
<li>캐시를 목적으로 사용</li>
<li><strong>클라이언트에게 리소스가 수정되지 않았음을 알려준다.</strong> 따라서 클라이언트는 로컬PC에
저장된 캐시를 재사용한다. <strong>(캐시로 리다이렉트 한다.)</strong></li>
<li>많이 사용한다.</li>
</ul>
<ol start="3">
<li>304 응답은 응답에 <strong>메시지 바디를 포함하면 안된다.</strong> (로컬 캐시를 사용해야 하므로)</li>
</ol>
<ul>
<li>조건부 GET, HEAD 요청시 사용</li>
</ul>
<h1 id="4-4xx---클라이언트-오류-5xx---서버-오류">4. 4XX - 클라이언트 오류, 5XX - 서버 오류</h1>
<h2 id="🖕-4xx-client-error--클라이언트-오류">🖕 4xx (Client Error) : 클라이언트 오류</h2>
<ul>
<li>클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음</li>
<li>오류의 원인이 <code>클라이언트</code>에 있음</li>
<li>중요! 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실
패함</li>
</ul>
<h3 id="1-400-bad-request">1) 400 Bad Request</h3>
<ul>
<li>클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음</li>
<li>요청 구문, 메시지 등등 오류</li>
<li>클라이언트는 요청 내용을 다시 검토하고, 보내야함</li>
<li>예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을 때(백엔드에서 막아줘야 클라이언트 개발자가 알 수 있게 됨)</li>
</ul>
<h3 id="2-401-unauthorized">2) 401 Unauthorized</h3>
<ol>
<li>클라이언트가 해당 리소스에 대한 <code>인증</code>이 필요함</li>
<li>인증(Authentication) 되지 않음</li>
</ol>
<ul>
<li>401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명</li>
</ul>
<ol start="3">
<li>참고</li>
</ol>
<ul>
<li><code>인증(Authentication)</code>: 본인이 누구인지 확인, (로그인)</li>
<li><code>인가(Authorization)</code>: 권한부여 (ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한,
인증이 있어야 인가가 있음)</li>
<li>오류 메시지가 <strong>Unauthorized 이지만 인증 되지 않음 (이름이 아쉬움)</strong></li>
</ul>
<h3 id="3-403-forbidden">3) 403 Forbidden</h3>
<ul>
<li>서버가 요청을 이해했지만 승인을 거부함</li>
<li>주로 인증 자격 증명은 있지만, <strong>접근 권한이 불충분한 경우</strong></li>
<li>예) 어드민 등급이 아닌 사용자가 로그인은 했지만, <strong>어드민 등급의 리소스에 접근하는 경우</strong></li>
</ul>
<h3 id="4-404-not-found">4) 404 Not Found</h3>
<ul>
<li>요청 리소스를 찾을 수 없음</li>
<li><strong>요청 리소스가 서버에 없음</strong></li>
<li>또는 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때</li>
</ul>
<h2 id="👆-5xx-server-error--서버-오류">👆 5xx (Server Error) : 서버 오류</h2>
<ul>
<li>서버 문제로 오류 발생</li>
<li>서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음(복구가 되거나 등등)</li>
</ul>
<h3 id="1-500-internal-server-error">1) 500 Internal Server Error</h3>
<ul>
<li>서버 문제로 오류 발생, 애매하면 500 오류</li>
<li>서버 내부 문제로 오류 발생</li>
<li>애매하면 500 오류</li>
<li>nullpointexception</li>
</ul>
<h3 id="2-503-service-unavailable--서비스-이용-불가">2) 503 Service Unavailable : 서비스 이용 불가</h3>
<ul>
<li>서버가 일시적인 <strong>과부하 또는 예정된 작업</strong>으로 잠시 요청을 처리할 수 없음</li>
<li>Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음</li>
</ul>