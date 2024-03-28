<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f80b9452-0781-4f9a-8d65-2580b95c7c63/image.png" /></p>
<blockquote>
<p><strong>전문 요약 :</strong> 💡 API 설계는 리소스 중심의 URI 계층 구조를 활용한다. <code>HTTP 메서드</code>는 GET(조회), POST(데이터 처리 및 등록), PUT(리소스 대체 또는 생성), PATCH(리소스 일부 변경), DELETE(리소스 제거) 등이 있으며, 각 메서드는 안전, 멱등, 캐시 가능 속성을 가진다. 요약하면, 리소스 중심의 URI와 다양한 HTTP 메서드를 활용하여 안전하고 효율적인 API를 디자인할 수 있다.</p>
</blockquote>
<h1 id="1--http-api를-만들어보자">1.  HTTP API를 만들어보자</h1>
<blockquote>
<p>사진 및 강의 출처 : <a href="https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC">모든 개발자를 위한 HTTP 웹 기본 지식</a></p>
</blockquote>
<h2 id="1-api-uri-설계uniform-resource-identifier">1) API URI 설계(Uniform Resource Identifier)</h2>
<ul>
<li>회원 목록 조회 /read-member-list</li>
<li>회원 조회 /read-member-by-id</li>
<li>회원 등록 /create-member</li>
<li>회원 수정 /update-member</li>
<li>회원 삭제 /delete-member</li>
</ul>
<h3 id="가장-중요한-것은-리소스-식별">가장 중요한 것은 리소스 식별</h3>
<h2 id="2-api-uriuniform-resource-identifier-고민">2) API URI(Uniform Resource Identifier) 고민</h2>
<ol>
<li>리소스의 의미는 뭘까?</li>
</ol>
<ul>
<li>회원을 등록하고 수정하고 조회하는게 리소스가 아니다!<ul>
<li>예) 미네랄을 캐라 -&gt; 미네랄이 리소스</li>
<li><code>회원</code>이라는 개념 자체가 <strong>바로 리소스</strong>다.</li>
</ul>
</li>
</ul>
<ol start="2">
<li>리소스를 어떻게 식별하는게 좋을까?</li>
</ol>
<ul>
<li>회원을 등록하고 수정하고 조회하는 것을 모두 배제</li>
<li><strong>회원이라는 리소스만 식별하면 된다. -&gt; 회원 리소스를 URI에 매핑</strong></li>
</ul>
<h2 id="3-api-uri-설계">3) API URI 설계</h2>
<h3 id="리소스-식별-uri-계층-구조-활용">리소스 식별, URI 계층 구조 활용</h3>
<blockquote>
<p>참고: 계층 구조상 상위를 컬렉션으로 보고 <code>복수단어</code> 사용 권장(member -&gt; members)</p>
</blockquote>
<ul>
<li>회원 목록 조회 /members</li>
<li>회원 조회 /members/{id} -&gt; 어떻게 구분하지?</li>
<li>회원 등록 /members/{id} -&gt; 어떻게 구분하지?</li>
<li>회원 수정 /members/{id} -&gt; 어떻게 구분하지?</li>
<li>회원 삭제 /members/{id} -&gt; 어떻게 구분하지?</li>
</ul>
<h2 id="4-리소스와-행위을-분리">4) 리소스와 행위을 분리</h2>
<h3 id="가장-중요한-것은-리소스를-식별하는-것">가장 중요한 것은 리소스를 식별하는 것</h3>
<ol>
<li>URI는 리소스만 식별!</li>
<li>리소스와 해당 리소스를 대상으로 하는 행위을 분리</li>
</ol>
<ul>
<li><strong>리소스</strong> : 회원</li>
<li><strong>행위</strong> : 조회, 등록, 삭제, 변경</li>
</ul>
<ol start="3">
<li>리소스는 명사, 행위는 동사</li>
<li><code>행위(메서드)</code>는 어떻게 구분할까? 답변 2.</li>
</ol>
<h1 id="2-http-메서드---get-post">2. HTTP 메서드 - GET, POST</h1>
<h2 id="1-http-메서드-종류">1) HTTP 메서드 종류</h2>
<h3 id="주요-메서드">주요 메서드</h3>
<ol>
<li><code>GET</code>: 리소스 조회</li>
<li><code>POST</code>: 요청 데이터 처리, 주로 등록에 사용</li>
<li><code>PUT</code>: 리소스를 대체, 해당 리소스가 없으면 생성</li>
<li><code>PATCH</code>: 리소스 부분 변경</li>
<li><code>DELETE</code>: 리소스 삭제</li>
</ol>
<h3 id="기타-메서드">기타 메서드</h3>
<ol>
<li><strong>HEAD</strong>: GET과 동일하지만 <strong>메시지 부분을 제외하고, 상태 줄과 헤더만 반환</strong></li>
<li><strong>OPTIONS</strong>: 대상 리소스에 대한 <strong>통신 가능 옵션(메서드)</strong>을 설명(주로 <strong>CORS</strong>에서 사용)</li>
<li><strong>CONNECT</strong>: 대상 리소스로 식별되는 서<strong>버에 대한 터널을 설정</strong></li>
<li><strong>TRACE</strong>: 대상 리소스에 대한 경로를 따라 <strong>메시지 루프백 테스트를 수행</strong></li>
</ol>
<h2 id="2-get">2) GET</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ffdd6b1b-fcc4-4039-ba72-7559b7cba7da/image.png" /></p>
<h3 id="get-이란">GET 이란?</h3>
<ol>
<li><strong>리소스 조회</strong></li>
<li>서버에 전달하고 싶은 데이터는 Query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달</li>
<li>메세지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음</li>
</ol>
<h3 id="리소스-조회1--메세지-전달">리소스 조회1 : 메세지 전달</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2332b8c6-d90d-49ed-bddc-d79f35cc2d79/image.png" /></p>
<h3 id="리소스-조회2--서버-도착">리소스 조회2 : 서버 도착</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f01c1b4a-0d29-44f2-9104-c4a3f85cbdf0/image.png" /></p>
<h3 id="리소스-조회3--응답-데이터">리소스 조회3 : 응답 데이터</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/254565fd-478e-40e7-922a-5bb1c31cf16d/image.png" /></p>
<h2 id="3-post">3) POST</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3d34ffee-3776-4e6d-8cab-1c43100c4a5f/image.png" /></p>
<h3 id="post란">POST란?</h3>
<ol>
<li>요청 <code>데이터 처리</code>(데이터가 있)</li>
<li><strong>메시지 바디를 통해 서버로 요청 데이터 전달</strong></li>
<li>서버는 요청 데이터를 <strong>처리</strong></li>
</ol>
<ul>
<li>메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.</li>
</ul>
<ol start="4">
<li>주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용</li>
</ol>
<h3 id="리소스-등록1--메세지-전달">리소스 등록1 : 메세지 전달</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8077eabc-d7b3-46c4-aba1-c720944c7d48/image.png" /></p>
<h3 id="리소스-등록2--신규-리소스-생성">리소스 등록2 : 신규 리소스 생성</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/060a2255-55b6-4ef7-994c-069956fa8ce4/image.png" /></p>
<h3 id="리소스-등록3--응답-데이터">리소스 등록3 : 응답 데이터</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b79d96d6-46cb-42e2-8cdf-f94950ef8b11/image.png" /></p>
<h3 id="요청-데이터를-어떻게-처리한다는-뜻일까-예시">요청 데이터를 어떻게 처리한다는 뜻일까? 예시</h3>
<ol>
<li>스펙 : POST 메서드는 대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청</li>
<li>예시로 POST의 기능</li>
</ol>
<ul>
<li>HTML 양식에 입력 된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공<ul>
<li>예) HTML FORM에 입력한 정보로 회원 가입, 주문 등에서 사용</li>
</ul>
</li>
<li>게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시<ul>
<li>예) 게시판 글쓰기, 댓글 달기</li>
</ul>
</li>
<li>서버가 아직 식별하지 않은 새 리소스 생성<ul>
<li>예) 신규 주문 생성</li>
</ul>
</li>
<li>기존 자원에 데이터 추가<ul>
<li>예) 한 문서 끝에 내용 추가하기</li>
</ul>
</li>
<li>정리: 이 리소스 URI에 POST 요청이 오면 <strong>요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -&gt; 정해진 것이 없음</strong></li>
</ul>
<h2 id="4-post-정리">4) POST 정리</h2>
<ol>
<li><strong>새 리소스 생성(등록)</strong></li>
</ol>
<ul>
<li>서버가 아직 식별하지 않은 새 리소스 생성</li>
</ul>
<ol start="2">
<li><strong>요청 데이터 처리</strong></li>
</ol>
<ul>
<li>단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우</li>
<li>예) 주문에서 결제완료 -&gt; 배달시작 -&gt; 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우</li>
<li>POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음<ul>
<li>예) POST /orders/{orderId}/start-delivery <strong>(컨트롤 URI)</strong></li>
</ul>
</li>
</ul>
<ol start="3">
<li><strong>다른 메서드로 처리하기 애매한 경우</strong></li>
</ol>
<ul>
<li>예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우</li>
<li>애매하면 POST</li>
</ul>
<h1 id="3-http-메서드---put-patch-delete">3. HTTP 메서드 - PUT, PATCH, DELETE</h1>
<h2 id="1-put--리소스-수정보다는-갈아-치우는-느낌">1) PUT : 리소스 수정보다는 갈아 치우는 느낌</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/04d77ac8-de08-4334-a1bf-78aa57ab8adf/image.png" /></p>
<ol>
<li>리소스를 대체</li>
</ol>
<ul>
<li>리소스가 있으면 대체</li>
<li>리소스가 없으면 생성</li>
<li>쉽게 이야기해서 <strong>덮어버림</strong></li>
</ul>
<ol start="2">
<li>중요! <strong>클라이언트가 리소스를 식별</strong></li>
</ol>
<ul>
<li>클라이언트가 <code>리소스 위치</code><strong>를 알고 URI 지정</strong></li>
<li>POST와의 차이점</li>
</ul>
<h3 id="리소스가-있는-경우--대체">리소스가 있는 경우 : 대체</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ebbabe6a-a3c4-439b-9353-3d165adae804/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d4fa1052-d4c7-4757-9e91-c23446d013d8/image.png" /></p>
<h3 id="리소스가-없는-경우--생성">리소스가 없는 경우 : 생성</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/bb1940bc-fffd-43f4-8a47-a2fed63d2ddf/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4ae6c790-114d-4aec-bca1-d1461d908631/image.png" /></p>
<h3 id="주의---리소스를-완전히-대체한다">주의! - 리소스를 완전히 대체한다</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/50b6029d-91bf-4348-8cc2-082076165c99/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6ddc04ca-ff3e-49f1-87e8-3276e18c1be7/image.png" /></p>
<h2 id="2-patch">2) PATCH</h2>
<h3 id="patch란">PATCH란?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/798e9e44-df81-41d7-9d99-6d1c5e650d75/image.png" /></p>
<ul>
<li>리소스 부분 변경</li>
<li>PATCH가 안되는 서버에서는  POST를 사용하면 됨</li>
<li>요즘은 웬만하면 다</li>
</ul>
<h3 id="리소스-부분-변경">리소스 부분 변경</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d1a98aa3-b793-47db-9f42-abfca4db5351/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4cd92a63-73c5-4e59-b8dd-819835877a02/image.png" /></p>
<h2 id="3-delete">3) DELETE</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5daafa43-e27c-409e-8c27-e5cf5c4b5133/image.png" /></p>
<ul>
<li>리소스 제거</li>
</ul>
<h3 id="리소스-제거">리소스 제거</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a6ca4479-f73f-4169-9e61-4fc2fce56905/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f249def2-3028-451d-8329-69c58a839b59/image.png" /></p>
<h1 id="4-http-메서드의-속성">4. HTTP 메서드의 속성</h1>
<h2 id="1-http-메서드의-속성-종류">1) HTTP 메서드의 속성 종류</h2>
<ol>
<li>안전(Safe Methods)</li>
<li>멱등(Idempotent Methods)</li>
<li>캐시가능(Cacheable Methods)</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/945d113f-6616-4e94-bf6a-da1bb991f688/image.png" /></p>
<h2 id="2-안전safe">2) 안전(Safe)</h2>
<ol>
<li>호출해도 <strong>리소스를 변경하지 않는다.</strong></li>
</ol>
<ul>
<li>Q: 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?</li>
<li>A: 안전은 해당 <code>리소스만</code> <strong>고려한다.</strong> 그런 부분까지 고려하지 않는다.</li>
</ul>
<h2 id="3-멱등idempotent">3) 멱등(Idempotent)</h2>
<pre><code class="language-java">f(f(x)) = f(x)</code></pre>
<ol>
<li>한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다</li>
<li>멱등 메서드</li>
</ol>
<ul>
<li><code>GET</code>: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.</li>
<li><code>PUT</code>: 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다.</li>
<li><code>DELETE</code>: 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.</li>
<li><code>POST</code>: 멱등이 아니다! <strong><em>두 번 호출하면 같은 결제가 중복해서 발생할 수 있다</em></strong></li>
</ul>
<ol start="3">
<li>활용</li>
</ol>
<ul>
<li>자동 복구 메커니즘</li>
<li>서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, <strong>클라이언트가 같은 요청을 다시 해
도 되는가? 판단 근거</strong></li>
</ul>
<ol start="4">
<li>Q: 재요청 중간에 다른 곳에서 리소스를 변경해버리면?</li>
</ol>
<ul>
<li>사용자1: GET -&gt; username:A, age:20</li>
<li>사용자2: PUT -&gt; username:A, age:30</li>
<li>사용자1: GET -&gt; username:A, age:30 -&gt; 사용자2의 영향으로 바뀐 데이터 조회</li>
</ul>
<ol>
<li>A: 멱등은 <code>외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지는 않는다</code></li>
</ol>
<h2 id="4-캐시-가능cacheable">4) 캐시 가능(Cacheable)</h2>
<ol>
<li>응답 결과 리소스를 캐시해서 사용해도 되는가?</li>
<li>GET, HEAD, POST, PATCH 캐시가능</li>
<li>실제로는 <strong>GET, HEAD 정도만 캐시로 사용</strong></li>
</ol>
<ul>
<li>POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음💡 API 설계는 리소스 중심의 URI 계층 구조를 활용한다. <code>HTTP 메서드</code>는 GET(조회), POST(데이터 처리 및 등록), PUT(리소스 대체 또는 생성), PATCH(리소스 일부 변경), DELETE(리소스 제거) 등이 있으며, 각 메서드는 안전, 멱등, 캐시 가능 속성을 가진다. 요약하면, 리소스 중심의 URI와 다양한 HTTP 메서드를 활용하여 안전하고 효율적인 API를 디자인할 수 있다.</li>
</ul>