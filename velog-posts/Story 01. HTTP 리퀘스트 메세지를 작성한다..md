<blockquote>
<p>이 글은 성공과 실패를 결정하는 1% 네트워크 원리 책을 읽고 정리한 글입니다!</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5b25d976-8025-4c4d-8e1c-bbd5c679e240/image.png" /></p>
<blockquote>
<p>그림 출처 : <a href="https://sangbeomkim.tistory.com/117">https://sangbeomkim.tistory.com/117</a></p>
</blockquote>
<ol>
<li><p>URL을 브라우저에 입력하면 </p>
</li>
<li><p>브라우저는 결정된 규칙에 따라 URL의 의미를 조사한 후 </p>
</li>
<li><p>그 의미에 따라 리퀘스트 메시지를 만든다. </p>
</li>
<li><p>이 예의 경우 samplel, hum이라는 파일에 저장된 페이지의 데이터를 주십시오.&quot;라는 의미의 리퀘스트 메시지를 안들고, 이것을 웹 서버에 보낸다. </p>
</li>
</ol>
<ul>
<li>하지만 브라우저 자체가 메시지를 보내는 것은 아님</li>
</ul>
<ol start="2">
<li>메시지를 보내는 것은 디지털 데이터를 운반하는 구조의 역할이므로 이러한 구조에 의뢰하여 데이터를 넘긴다. 구체적으로는 OS에 내장된 네트워크 제어용 소프트웨어에 의뢰하여 메시지를 서버측까지 도착하게 하는데, 1장에서는 이렇게 '의뢰하는 동작까지 추적한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b200c0ff-e62f-4ccc-91e6-c2f2d22fdc54/image.png" /></p>
<ul>
<li>URL는 해독하는 곳부터 브라우저의 동작이 시작된다.</li>
</ul>
<h1 id="1-탐험-여행은-url-입력부터-시작">1. 탐험 여행은 URL 입력부터 시작</h1>
<p>브라우저는 웹 서버에 액세스하는 클라이언트로 사용하는 경우가 많지만, 브라우저의 기능을 그뿐만 아니라, 파일을 다운로드/업로드 하는 FTP의 클라이언트 기능이나 메일의 클라이언트 기능도 가지고 있다. </p>
<p>즉, 몇 개가 있는 기능 중의 어느 것을 사용하여 데이터에 액세스하면 좋을 것인지 판단하는 재료가 필요하므로, <strong>웹 서버에 액세스할 때 여러 종류의 URL이 준비</strong>되어 있는 것</p>
<h2 id="쓰는-방법">쓰는 방법</h2>
<blockquote>
<p><code>액세스의 대상</code>에 따라 다르다.</p>
</blockquote>
<ul>
<li>웹 서버, FTP 서버에 액세스 하는 경우, 서버의 도메인명이나 액세스하는 파일의 경로명 등을 URL에 포함시킴</li>
<li>필요에 따라 사용자명이나 패스워드, 서버 측 포트번호 등을 쓸 수 도 있음</li>
</ul>
<h2 id="url의-하나의-공통점">URL의 하나의 공통점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c9b27809-2097-47d9-b9a9-ecbc76920a54/image.png" /></p>
<p>URL의 맨 앞에 있는 문자열, 즉 http; ftp; file; mailto;라는 부분에서 <code>액세스하는 방법</code>을 나타낸다는 점</p>
<p>즉, 액세스할 때의 프로토콜 종류가 쓰여져 있다고 생각하면 </p>
<h1 id="2-브라우저는-먼저-url-해독">2. 브라우저는 먼저 URL 해독</h1>
<blockquote>
<p>브라우저가 가장 먼저 하는 일은 <strong>URL을 해독하는 것</strong>이다.</p>
</blockquote>
<p>브라우저가 처음에 하는 일을 웹 서버에 보내는 리퀘스트의 메세지를 작성하기 위해 이 <strong>URL을 해독하는 것</strong></p>
<ol>
<li>요소를 분해</li>
<li>분해한 요소를 나열하는 방법을 살표보면 URL의 의미를 알 수 있음</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/dd76998b-0e8d-4adb-baea-84b3e3ed06bf/image.png" /></p>
<h1 id="3-파일명을-생략한-경우">3. 파일명을 생략한 경우</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/beb9cc03-9d13-4740-9b06-5d6d41a67698/image.png" /></p>
<pre><code class="language-jsx">http://www.lab.cyber.co.kr/dir/</code></pre>
<p>끝이 /로 끝난 것은 /dir/의 다음에 써야 할 파일명을 쓰지 않고 생략한다는 것</p>
<h2 id="파일명의-생략">파일명의 생략</h2>
<p>다만, 파일명을 쓰지 않으면, 어느 파일에 액세스해야 할지 모르니, <strong>파일명을 생략할 때 대비하여 파일명을 미리 서버측에 설정</strong>해 둔다.</p>
<ul>
<li>index.html</li>
<li>default.html</li>
</ul>
<pre><code class="language-jsx">http://www.lab.cyber.co.kr</code></pre>
<p>끝의 /까지 생략되기도 하는데, 경로명이 아무 것도 없는 경우에는 루트 디렉토리의 아래에 있는 미리 설정된 파일명의 파일을 액세스하면 혼란이 없다.</p>
<h2 id="무조건-파일명은-아니다">무조건 파일명은 아니다.</h2>
<p>다만, 아래와 같은 예는 미묘하다.</p>
<pre><code class="language-jsx">http://www.lab.cyber.co.kr/whatisthis</code></pre>
<p><strong>whatisthis를 파일명과 결부시키지 않는 쪽이 좋을 수도 있다.</strong> 그래서 이 경우는 웹 서버에 'whatisthis'라는 파일이 있으면 whatisthis를 파일명으로 보고, 'whatisthis' 라는 디렉토리가 있으면 whatisthis를 디렉토리명으로 본다는 것</p>
<h1 id="4-http의-기본-개념">4. HTTP의 기본 개념</h1>
<blockquote>
<p>URL을 해독하면 <strong>어디에 액세스해야 하는지</strong>가 판명</p>
</blockquote>
<p>브라우저는 HTTP 프로토콜을 사용하여 웹 서버에 액세스하는데, HTTP 프로토콜의 의미</p>
<ul>
<li>HTTP의 개념 따로 정리한 게 있음</li>
</ul>
<h2 id="http-프로토콜">HTTP 프로토콜</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9417a5ce-26d2-4e50-8ec8-b74906664304/image.png" /></p>
<ul>
<li>클라이언트와 서버가 주고받는 메세지의 내용이나 순서를 정한 것</li>
</ul>
<ol>
<li>클라이언트에서 서버를 향해 <code>리퀘스트 메세지</code>를 보냄</li>
<li>리퀘스트 메세지가 웹 서버에 도착하면 웹 서버는 그 속에 쓰여있는 내용을 해독</li>
<li>URI와 메세지를 조사하여 무엇을, 어떻게 하는지 판단 후 요구에 따라 동작하고, 결과 데이터를 <strong>응답 메세지에 저장</strong></li>
</ol>
<ul>
<li>응답 메세지 맨 앞 부분에는 실행 결과가 정상 종료되었는지 이상이 발생했는지 나타내는 <strong>스테이터스 코드</strong></li>
</ul>
<ol start="4">
<li>헤더 파일과 페이지의 데이터가 이어지고, 이 응답 메세지를 클라이언트에 반송</li>
<li>클라이언트에 도착하여 브라우저가 메세지의 안에서 데이터를 추출하여 화면에 표시하면서 HTTP 동작은 끝</li>
</ol>
<h2 id="리퀘스트-메세지">리퀘스트 메세지</h2>
<h3 id="무엇을---uriuniform-resource-identfier">무엇을  : URI(Uniform Resource Identfier)</h3>
<blockquote>
<p>다양항 액세스 대상을 쓸 수 있으며, <strong>액세스 대상을 통칭</strong>하는 말</p>
</blockquote>
<ul>
<li>보통 페이지 데이터를 저장한 파일의 이름이나 CGI 프로그램의 파일명을 URI로 씀</li>
</ul>
<h3 id="어떻게-해서--메소드">어떻게 해서 : 메소드</h3>
<ul>
<li>메소드에 의해 웹 서버에 어떤 동작을 하고 싶은 지를 전달</li>
<li>EX. 데이터를 읽고 싶다 OR 클라이언트에서 입력한 데이터를  URI로 나타낸 프로그램에 전달</li>
<li>GET, POST : <a href="https://www.notion.so/HTTP-887dfbe97acf4dca8ad3ccc9a35df680?pvs=21">http 정리 velog 글</a></li>
</ul>
<h2 id="5-http-리퀘스트-메세지를-만든다">5) HTTP 리퀘스트 메세지를 만든다.</h2>
<blockquote>
<p>HTTP 메세지 쓰는 방법 = <code>포맷</code> 에 맞게 브라우저는 리퀘스트 메세지를 만듦</p>
</blockquote>
<p>URL을 해독하고 웹 서버와 파일명을 판단하면 <strong>브라우저는 이것을 바탕으로 HTTP의 리퀘스트 메세지를 만든다.</strong></p>
<h2 id="제너럴-헤더">제너럴 헤더</h2>
<ul>
<li>리퀘스트와 응답 양쪽 모두 사용하는 헤더 필드</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1f7fd59d-b542-46e0-aee0-cb9e00248fa2/image.png" /></p>
<h2 id="리퀘스트-메세지의-구조http-메세지의-포맷">리퀘스트 메세지의 구조(HTTP 메세지의 포맷)</h2>
<ul>
<li>브라우저나 웹 서버는 이 포맷에 맞게 메세지를 만든다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/241e0432-3cf3-484a-86bf-6a118c53ca51/image.png" /></p>
<h3 id="리퀘스트-라인">리퀘스트 라인</h3>
<ul>
<li>첫 번째 행</li>
<li>맨 앞에 있는 <code>메서드</code>가 가장 중요한 것으로 이것을 통해 웹 브라우저는 <strong>웹 서버에 어떻게 할 것인지를 전달</strong></li>
<li>이 한 행으로 리퀘스트의 내용을 대략 알 수 있음</li>
</ul>
<pre><code class="language-jsx">&lt;메소드&gt;&lt;공백&gt;&lt;URI&gt;&lt;공백&gt;&lt;HTTP 버전&gt;</code></pre>
<ul>
<li>경로명은 보통 URL에 포함되어 있으므로 URL에서 경로명을 추출하여 복사</li>
</ul>
<h3 id="메세지-헤더">메세지 헤더</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b8edc1c8-196a-4f52-bb07-e5f3329ca11e/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/374a0297-9277-45ed-bbcd-bf3923086c85/image.png" /></p>
<ul>
<li>한 행에 한 개의 헤더 필드를 씀</li>
<li>이를 통해 리<strong>퀘스트의 부가적인 정보</strong>를 나타낸다.</li>
<li>행 수는 상황에 따라 달라지며, 공백 행까지가 메세지 헤더가 됨</li>
</ul>
<pre><code class="language-jsx">&lt;필드명&gt;:&lt;필드값&gt;
.
.
.
&lt;공백 행&gt;</code></pre>
<h3 id="메세지-본문">메세지 본문</h3>
<ul>
<li>클라이언트에서 서버에 송신하는 데이터, 폼 페이지에 입력한 데이터를 <code>POST 메서드</code>로 웹 서버에 보낼 때 등의 데이터가 들어감</li>
</ul>
<pre><code class="language-jsx">&lt;메세지 본문&gt;</code></pre>
<h2 id="응답-메세지http-메세지의-포맷">응답 메세지(HTTP 메세지의 포맷)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/cc216a15-b553-4de3-90b4-ee453dfb6f0b/image.png" /></p>
<ul>
<li>브라우저나 웹 서버는 이 포맷에 맞게 메세지를 만든다.</li>
</ul>
<h3 id="스테이터스-라인">스테이터스 라인</h3>
<pre><code class="language-jsx">&lt;HTTP 버전&gt; &lt;공백&gt; &lt;스테이터스 코드&gt; &lt;공백&gt; &lt;응답 문구&gt;</code></pre>
<ul>
<li>스테이터스 코드의 내용을 나타내는 짧은 설명 문</li>
</ul>
<h3 id="메세지-본문-1">메세지 본문</h3>
<ul>
<li>서버에서 클라이언트에 송신하는 데이터, 파일에서 읽은 <strong>데이터나 CGI 애플리케이션이 출력한 데이터</strong>가 들어간다.</li>
<li>메세지 본문은 바이너리 데이터 취급한다.</li>
</ul>
<h3 id="응답-헤더">응답 헤더</h3>
<ul>
<li>응답의 부가 정보로 사용하는 헤더 필드</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8e8a1e8d-bbaf-496c-ab3d-e08956dece0e/image.png" /></p>
<h2 id="엔터티-헤더">엔터티 헤더</h2>
<ul>
<li>엔터티(메세지 본문)의 부가 정보로 사용하는 헤더 필드</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5d53712f-512d-4208-a5d8-d8b5059f0375/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1f55a0d1-698f-41f8-bded-5cf67a86249e/image.png" /></p>
<h2 id="폼에서-메소드를-구분하여-사용하기">폼에서 메소드를 구분하여 사용하기</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2bb6b9d3-1cbe-440e-a58c-2970c2b7a657/image.png" /></p>
<h3 id="get-메소드">GET 메소드</h3>
<ul>
<li>단, 메소드가 <code>GET인 경우</code>에는 메소드와 URI만으로 웹 서버가 무엇을 할 지 판단할 수 있으므로 <strong>메세지 본문에 쓰는 송신 데이터는 아무것도 없다.</strong></li>
<li>메세지 헤더가 끝난 곳에서 메세지는 끝난다.</li>
</ul>
<h3 id="post-메소드">POST 메소드</h3>
<ul>
<li>폼에 입력한 <code>데이터</code> 등을 <strong>메세지 본문 부분</strong>에 씀</li>
</ul>
<h2 id="6-리퀘스트-메세지를-보내면-응답이-되돌아온다">6) 리퀘스트 메세지를 보내면 응답이 되돌아온다.</h2>
<h2 id="첫-번째-행">첫 번째 행</h2>
<ul>
<li>응답의 경우는 정상 종료했는지, 아니면 오류가 발생했는지, 즉 <code>리퀘스트의 실행 결과</code>를 나타내는 <strong>스테이터스 코드와 응답 문구</strong>를 첫 번째 행에 써야 함</li>
</ul>
<h3 id="스테이터스-코드">스테이터스 코드</h3>
<ul>
<li>숫자로 쓴 것으로, 주로 프로그램 등에 <code>실행 결과</code>를 알려주는 것이 목적</li>
<li>1xx : 처리 경과 상황 통지, 2xx : 정상 종료, 3xx : 무언가 다른 조치가 필요함, 4xx : 클라이언트측 오류, 5xx : 서버측 오류</li>
<li>스테이터스 코드는 첫 번째 행의 개요를 나타내고, 두 번째와 세 번째 행에 상세한 상황을 나타냄</li>
</ul>
<h3 id="응답-문구">응답 문구</h3>
<ul>
<li>문장으로 쓰여 있으며, 사람에게 실행 결과를 알리는 것이 목적</li>
</ul>
<p>응답 메시지가 되돌아오면, 그때부터 데이터를 추출한 후 화면에 표시하여 웹 페이지를 눈으로 볼 수 있다. 하지만, 페이지가 문장으로만 되어 있으면 이것으로 끝이지만, <strong>영상 등이 포함되어 있는 경우에는 계속 내용이 있다.</strong></p>
<h2 id="영상이-포함되어-있다면">영상이 포함되어 있다면?</h2>
<p>문장 안에 영상 파일을 나타내는 <strong>html의 제어 정보,</strong> <code>태그</code>가 포함되어 있으며, 브라우저는 화면에 문장을 표시할 때 태그를 탐색한다.</p>
<ol>
<li>영상을 포함하고 있는 의미의 태그를 만나면 그곳에 <strong>영상용 공백을 비워두고</strong> 문장을 표시</li>
<li>다시 한 번 <strong>웹 서버에 액세스</strong>하여 태그에 쓰여있는 영상 파일을 웹 서버에서 읽어와서 비워둔 공백에 표시</li>
</ol>
<ul>
<li>이 때도 URI 부분에 영상 파일의 이름을 쓴 리퀘스트 메세지를 만들어 보냄</li>
</ul>
<h3 id="리퀘스트-메세지에-쓰는-uri는-파일-1번에-1개씩만-읽을-수-있다">리퀘스트 메세지에 쓰는 URI는 파일 1번에 1개씩만 읽을 수 있다.</h3>
<p>리퀘스트 메세지에 쓰는 <strong>URI는 한 개만으로 결정</strong>되어 있으므로 파일을 <strong>한 번에 한 개씩만 읽을 수 있기 때문에 파일을 따로 읽어야 한다.</strong></p>
<p>즉, 한 문장에 3개의 영상이 포함되어 있다면 총 4회의 리퀘스트 메세지를 웹 서버에 보낸다.</p>
<p><code>웹 서버</code>는 4회의 리퀘스트가 한 개의 페이지인지, 아니면 각각 별도의 페이지인지는 신경쓰지 않고, <strong>단순히 한 개의 리퀘스트에 대해 한 개의 응답을 돌려보낼 뿐이다!</strong></p>
<h2 id="http-메세지의-예">HTTP 메세지의 예</h2>
<ul>
<li>브라우저와 웹 서버의 대화의 전체 모습
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6efa2f86-6b8a-4848-a369-ff5cfaa8ac3f/image.png" /><blockquote>
<p>그림 출처 : <a href="https://velog.io/@wlwl99/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-%EA%B5%AC%EC%A1%B0">https://velog.io/@wlwl99/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-%EA%B5%AC%EC%A1%B0</a></p>
</blockquote>
</li>
</ul>