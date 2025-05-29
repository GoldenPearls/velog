<blockquote>
<p>&quot;한빛미디어 서평단 &lt;나는리뷰어다&gt; 활동을 위해서 책을 협찬 받아 작성된 서평입니다.&quot;</p>
</blockquote>
<h1 id="들어가기-전">들어가기 전</h1>
<p>한빛 미디어에서 나온 주니어 백엔드 개발자가 반드시 알아야 할 실무 지식 이게 x에서도 핫해서.. 서평단에 되지 않는다면 따로 구매할 생각이 있을 정도로 궁금했던 책이었다..! </p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9862f0b5-864f-488b-bf15-c68bfc4ff504/image.png" /></p>
<p>이 책 말고도 비슷한 책이 있는데 &quot;개발자를 위한 최소한의 실무 지식&quot;이라는 책 또한 있었다. 전에 입사했을 때 앞부분 읽고 되게 잘 기억에 남았던 기억있다.
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2aaedcb1-0643-42b4-af38-95393f5d0915/image.png" /></p>
<p><strong>쿼리를 조회하기 전 explain이라던지, 인덱스가 어떤 구조로 타고 들어가는지</strong> 등 실무에 필요한 어느정도의 지식을 얻을 수 있던 책이었다.</p>
<p>이번에는 백엔드 전용으로 나왔다니 두근 두근한 마음이다..!</p>
<p>현재 교보문고 순위에서 출간한지 1달 밖에 안됐는데 <strong>컴퓨터/it 부문에서 17위</strong>를 할 정도로 사랑을 받고 있는 도서이다. 
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/01b059f2-e0f3-4438-a6c3-55d3d9e2edfb/image.png" /></p>
<h1 id="실무를-진짜로-알려주는-백엔드-책-이런-흐름으로-배운다">실무를 진짜로 알려주는 백엔드 책, 이런 흐름으로 배운다!</h1>
<p>실무를 진짜로 알려주는 백엔드 책, 이런 흐름으로 배운다!
백엔드 공부하다 보면 늘 이런 생각 들지 않아?</p>
<blockquote>
<p>“기능은 만들겠는데, 왜 자꾸 터지지?”
“서버는 잘 돌았는데 왜 느리지?”
“서비스가 커지니까 내가 만든 코드가 발목 잡네...?”</p>
</blockquote>
<p>그럴 때 딱 좋은 책이 있어.
이 책은 단순히 &quot;어떻게 만들까?&quot;가 아니라
<strong>&quot;만들었으면, 이제 어떻게 잘 굴러가게 하지?&quot;</strong>를 알려줘.
실제 서비스가 돌아가는 흐름을 기준으로 설명하기 때문에, 하나씩 따라가다 보면
성능, 구조, 장애 대응, 보안, 확장성까지 한 번에 잡을 수 있다.</p>
<h2 id="✅-이-책이-다루는-핵심-내용">✅ 이 책이 다루는 핵심 내용</h2>
<p>이 책은 빠르게 서비스를 만들고, 동시에 확장성과 안정성까지 고려한 시스템을 구축하는 방법을 실제 사례 중심으로 알려준다. 350p. 정도 안에 내용이 꽉꽉 들어 있다.</p>
<h3 id="1️⃣-빠르게-끊기지-않게">1️⃣ 빠르게! 끊기지 않게!</h3>
<blockquote>
<p>성능의 기초를 배워</p>
</blockquote>
<ul>
<li>느려진 서비스의 원인이 뭐고, 어디부터 봐야 할지 알려줘</li>
<li>처리량, 응답 시간, 병목 지점을 어떻게 찾는지 실제 예제로 설명해</li>
<li>커넥션 풀, 캐시, CDN 같은 실전 최적화 기법도 나와</li>
<li>진짜 서비스에서 튜닝하는 법을 처음으로 배우게 되는 챕터야</li>
</ul>
<p>책의 일부 파트로 </p>
<ul>
<li>커넥션 풀의 크기가 10이고 대기 시간이 30초</li>
</ul>
<p>이때 동시에 30개의 요청이 발생했는데 순간적으로 DB서버에 부하가 걸리면서 <strong>쿼리 실행시간이 10초으로 늘어났다.</strong></p>
<ul>
<li>요청 10개는 풀에서 커넥션을 확보하여 쿼리 실행을 시작함</li>
<li>요청 20개는 풀에서 커넥션을 확보하지 못해 대기 상태로 진입 </li>
</ul>
<p>대기 하는 사람들 중 절반이 기다리지 못하고 5초만에 요청을 취소하고 다시 요청했다고 가정하면 아래와 같이 된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f25be765-a6b3-42eb-8e43-41cc40be6430/image.png" /></p>
<p>10명의 클라이언트가 5초만에 요청을 취소하고 다시 요청을 보내면서 새로운 대기가 시작한다. 클라이언트가 요청을 취소하더라도 서버는 일정 시간 동안 하던 작업을 즉시 중단하지 않기에 대기 중인 요청 수는 30개가 된다. =&gt; 서버 부하가 커짐</p>
<p>그렇기에 대기 시간을 짧게 설정하는 것이 중요하다.</p>
<h3 id="2️⃣-연동과-데이터-흐름-진짜-설계란-이런-거다">2️⃣ 연동과 데이터 흐름, 진짜 설계란 이런 거다</h3>
<blockquote>
<p>단일 서비스가 아니라, 여러 시스템이 연결될 때 생기는 문제 해결법</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d26b6cac-4da5-4308-b37d-359814be6dc1/image.png" /></p>
<ul>
<li>DB 인덱스나 쿼리 성능뿐 아니라, API 연동 타임아웃/재시도/브레이커 패턴까지</li>
<li>메시지 큐, 아웃박스, CDC 등 비동기 설계 기법도 나온다</li>
<li>“그냥 연결하면 되잖아?” 했다가 겪는 장애들을 미리 방지하게 해줘</li>
</ul>
<h3 id="3️⃣-동시에-많은-요청이-올-때-어떻게-해야-할까">3️⃣ 동시에 많은 요청이 올 때 어떻게 해야 할까</h3>
<blockquote>
<p>동시성 제어와 리소스 관리 핵심</p>
</blockquote>
<ul>
<li>DB 락, 멀티스레드, 동시 요청 처리할 때 생기는 문제들을 짚어줘</li>
<li>자원 낭비 줄이고 효율 올리는 구조까지 실전에서 바로 써먹을 수 있어</li>
<li>논블로킹 IO, 가상 스레드 같은 최신 트렌드도 소개돼</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/dfe62a35-5c6e-4744-afdd-c53162343c62/image.png" /></p>
<h3 id="4️⃣-보안과-운영-진짜-실무-감각-생기는-파트">4️⃣ 보안과 운영, 진짜 실무 감각 생기는 파트</h3>
<blockquote>
<p>“이건 인프라팀 일이잖아”라고 넘기면 안 되는 내용들</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d2540948-a508-4180-8034-c52f4ceebe9b/image.png" /></p>
<ul>
<li>인증, 인가, 암호화, HMAC, 시큐어 코딩 등 진짜 보안의 기본</li>
<li>리눅스 디스크 확인, 크론 스케줄링, 네트워크 정보 확인 등
<strong>내가 만든 서비스가 운영 환경에서 어떻게 살아있는지</strong> 직접 체감하게 돼</li>
</ul>
<h3 id="5️⃣-마지막은-확장성과-구조-설계">5️⃣ 마지막은 확장성과 구조 설계</h3>
<blockquote>
<p>유지보수 가능한 설계는 실력의 차이를 만든다</p>
</blockquote>
<ul>
<li>MVC, 계층형, MSA, 이벤트 기반, CQRS까지 주요 아키텍처 패턴 정리</li>
<li>“왜 이렇게 나눴을까?” → “이래서 이렇게 나누는구나!”로 바뀌는 순간</li>
</ul>
<h2 id="이-책은-단순한-기능-구현-책이-아니야">이 책은 단순한 기능 구현 책이 아니야</h2>
<p>하나씩 따라가다 보면,
단순히 “잘 돌아가는 코드”를 넘어서
<strong>“서비스 전체가 잘 굴러가는 구조”를 이해하게 돼.</strong></p>
<blockquote>
<p>기능만 만들던 개발자에서
장애도 대응하고, 구조도 설계하는 개발자로 성장하고 싶다면
이 책, 한 번은 꼭 읽어봐야 해.</p>
</blockquote>
<p>뿐만 아니라 이해하기 쉽게 여러 그림들 또한 되어 있어 읽기가 편해!</p>
<h2 id="👀-이런-분들에게-추천해요">👀 이런 분들에게 추천해요!</h2>
<ul>
<li><p><strong>&quot;기능은 만들 수 있는데, 왜 불안정할까요?&quot;</strong>
→ 백엔드 개발의 ‘기초 체력’을 키우고 싶은 신입 개발자</p>
</li>
<li><p><strong>&quot;서비스는 돌아가는데, 구조가 복잡해요!&quot;</strong>
→ 프로젝트 구조, 데이터 설계, 운영 환경까지 고민하는 주니어~미들 개발자</p>
</li>
<li><p><strong>&quot;이제는 서비스 전체 흐름이 궁금해요!&quot;</strong>
→ 클라우드, 모니터링, 운영 환경까지 통합적으로 보고 싶은 개발자</p>
</li>
</ul>
<p>이 책은 단순한 기능 구현서가 아닙니다.
<strong>서비스 전체를 바라보는 개발자의 시야를 만들어주는 실전 가이드북</strong>입니다.
실무에서 ‘이건 왜 이렇게 하는 걸까?’라는 궁금증이 많은 개발자라면, 반드시 한 번은 읽어야 할 책이다.</p>
<h1 id="컴퓨터-구조-스터디--실전-백엔드-책으로-알아보는-진짜-보안">컴퓨터 구조 스터디 + 실전 백엔드 책으로 알아보는 진짜 보안</h1>
<blockquote>
<p>컴퓨터와 구조 책 스터디 또한 보안 파트를 공부해야 하기에 겸사겸사 두 개의 책을 합친 보안 알아보려 한다.</p>
</blockquote>
<p>보안의 핵심은 <strong>여러분과 여러분의 물건을 여러분이 정의한 안전함safe에 따라 유지하는 것이다.</strong> </p>
<blockquote>
<p>보안은 기술적인 문제만은 아니다. 보안은 사회적인 문제다. </p>
</blockquote>
<p>여러분과 여러분의 물건, 그리고 여러분의 안전에 대한 정의는 모두 다른 사람과 다른 사람의 물건, 그들의 안전에 대한 정의와 균형을 맞춰야 한다.</p>
<p>온라인 뱅킹을 생각해보라. 컴퓨터 하드웨어, 소프트웨어, 은행에서 개인에 이르는 통신 네트워크 등의 다양한 요소가 온라인 뱅킹을 이룬다. 하지만 우리가 <code>패스워드</code>를 <strong>포스트잇에 적어서 컴퓨터 모니터에 붙이면, 은행이 아무리 최고의 기술을 써도 전혀 도움이 되지 않는다!</strong></p>
<h2 id="1-중요한-보안">1) 중요한 보안</h2>
<p>고객정보가 유출된 K사의 보안 사고 사례를 보자. 해킹을 당한 기능은 요금 정보 페이지였다.</p>
<p>홈페이지에 로그인한 고객은 요금 정보 페이지에 접근해서 개인의 요금 관련 정보를 조회할 수 있었다. 요금 정보를 조회하기 위해 사용한 API는 다음과 유사하게 고객에 해당하는 코드값을 파라미터로 받았다.</p>
<pre><code>https://주소/..?cd=고객 코드</code></pre><p>웹 페이지는 고객 코드 값으로 로그인한 사용자의 코드를 사용하도록 구현되어 있었다. 여기서부터 문제가 시작되었다. 서버는 곡객코드가 로그인한 사용자의 고객코드인지 검증하지 않고, 고객코드에 해당하는 고객 정보를 응답했다.</p>
<blockquote>
<p>즉, 로그인만 하면 다른 고객의 정보를 조회할 수 있었던 것이다.</p>
</blockquote>
<h2 id="2-보안과-프라이버시">2) 보안과 프라이버시</h2>
<p>펜더의 블루투스 앰프 사례는 위협 모델 없이 제품을 설계했을 때 발생하는 전형적인 보안 실수이다. <strong>인증이 구현되지 않아 누구나 무대의 앰프에 연결해 소리를 낼 수 있었고, 이는 제품 기능을 완전히 무력화시켰다.</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e6da21e9-cd0c-4979-b2f5-8a96caa98148/image.png" /></p>
<p>또한 위협을 정확히 정의하지 않은 상태에서 보안을 설계하면, 사용자에게는 불편을 주면서도 실질적 보안은 얻지 못하는 결과를 초래할 수 있다.</p>
<p>예를 들어, 복잡한 패스워드 정책은 오히려 사용자가 종이에 메모를 하게 만들어 위험을 증가시킬 수 있다.</p>
<blockquote>
<p>따라서 시큐어 코딩, 인증·인가 체계, 비정상 접근 감지, 감사 로그 기록, 최소 권한 접근 제어 등은 <strong>정의된 위협 모델에 맞춰 설계되어야</strong> 하며, <strong>방화벽이나 데이터 노출 제한</strong> 또한 이러한 위협 분석을 기반으로 시행되어야 효과적이다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2243ede7-f168-450d-8d32-e6d23bb12f1d/image.png" />
출처 : <a href="https://brunch.co.kr/@23why/146">https://brunch.co.kr/@23why/146</a></p>
<p>컴퓨터를 사용한다면 수없이 많은 서드파티 하드웨어나 소프트웨어에 의존해야 한다. 이들 서드파티 소프트웨어나 하드웨어의 설계도나 소스 코드를 볼 수는 없지만 이들에 의존하는 수밖에 없다. 즉 <code>신뢰</code>할 수 밖에 없다.</p>
<h2 id="3-🔐-인증과-인가를-이해하기-위한-첫걸음-보안은-신뢰를-설계하는-일">3) 🔐 인증과 인가를 이해하기 위한 첫걸음: &quot;보안은 신뢰를 설계하는 일&quot;</h2>
<h2 id="1-왜-신뢰부터-시작해야-할까">1) 왜 ‘신뢰’부터 시작해야 할까?</h2>
<p>우리는 매일 수많은 시스템과 사람을 ‘신뢰’한다. 하지만 <strong>컴퓨터 보안에서 신뢰는 가장 취약한 고리</strong>가 되곤 한다.
예를 들어:</p>
<ul>
<li>펜더 앰프에 블루투스 페어링 없이 연결이 가능해, 관객이 앰프를 장악할 수 있었던 사례</li>
<li>소니와 레노버가 사용자의 동의 없이 루트킷, 광고 멀웨어를 심은 사례</li>
<li>지멘스, 시스코 등에서 <strong>하드코딩된 비밀번호</strong>가 보안에 심각한 허점을 만든 사례</li>
</ul>
<p>이 모든 사례는 다음의 질문을 던지게 한다:</p>
<blockquote>
<p>“도대체 무엇을, 누구를 믿을 것인가?”</p>
</blockquote>
<p>이 질문이 바로 <strong>위협 모델(Threat Model)</strong>의 시작점이다.</p>
<blockquote>
<p><strong>모든 보안은 ‘누구를 신뢰할 수 있는가?’에서 시작된다.</strong>
   보안 시스템은 신뢰를 기반으로 설계되며, 이 신뢰는 때로 의도적(루트킷, 백도어), 무능(기본 비밀번호, 암호화 누락), 부정직(NIST·NSA 암호 약화)의 형태로 배신당한다.</p>
</blockquote>
<h2 id="2-보안을-위협하는-세-가지-태도">2) 보안을 위협하는 세 가지 태도</h2>
<p><strong>위협 모델 수립</strong>은 기술만의 문제가 아니다. 아래 세 가지 태도가 시스템 보안에 큰 영향을 끼친다.</p>
<ol>
<li><p><strong>의도적(deliberate)</strong> 위협
사용자의 의도와 상관없이 설치되는 멀웨어, 백도어 등 (ex. 루트킷, NSA의 약화된 표준)</p>
</li>
<li><p><strong>무능(incompetent)</strong>에 의한 위협
암호화되지 않은 통신, 기본 비밀번호 방치, 잘못 설계된 장치 등</p>
</li>
<li><p><strong>부정직(disingenuous)</strong>한 표준이나 감시 체계
NSA와 NIST 사례처럼, 믿었던 보안 기관이 오히려 보안을 약화시킨 경우</p>
</li>
</ol>
<h2 id="3-사물함-비유로-보는-보안-개념---보안에서-중요한-개념-공격-표면attack-surface">3) 사물함 비유로 보는 보안 개념 - 보안에서 중요한 개념: 공격 표면(Attack Surface)</h2>
<p>학교 사물함은 좋은 보안 시스템의 모델이 될 수 있다.</p>
<ul>
<li><strong>문</strong>은 공격 표면 (Attack Surface)</li>
<li>번호 자물쇠는 <strong>인증 절차</strong></li>
<li>열쇠 구멍은 <strong>백도어</strong>, 즉 관리자가 접근할 수 있는 숨겨진 권한</li>
<li>‘누가 열 수 있는가’가 바로 <strong>인가(Authorization)</strong></li>
<li><strong>관리자의 마스터키</strong>는 높은 권한을 가진 존재</li>
</ul>
<p>이런 구조는 우리 시스템에서도 마찬가지다. 사용자에게는 제한된 권한만 부여하고, 관리자는 더 넓은 접근 권한을 갖는다.</p>
<p>하지만 너무 단순하거나 잘못된 조합을 쓰면 자물쇠가 쉽게 털리듯, <strong>약한 인증 수단</strong>이나 <strong>공용 비밀번호</strong>는 큰 위협이 된다.</p>
<h2 id="4-인터넷-시대의-새로운-공격들">4) 인터넷 시대의 새로운 공격들</h2>
<p><strong>좋은 보안은 ‘공격자에게는 비싸고, 방어자에게는 싸게’ 설계되어야 한다.</strong> 하지만 현실은 그 반대가 되기 쉽다. 예: 인터넷 시대엔 공격은 싸고, 방어는 어렵다. 현대 보안 위협은 눈에 보이지 않으며, 종종 자동화되어 있다.</p>
<ul>
<li><strong>MITM 공격(중간자 공격)</strong> : 누가 숙제를 가로채서 바꿔치기할 수도 있음</li>
<li><strong>DDoS 공격</strong> : 수많은 좀비 컴퓨터가 정당한 요청을 방해</li>
<li><strong>사회공학 공격</strong> : 사용자가 스스로 악성코드를 설치하게 유도</li>
</ul>
<blockquote>
<p><strong>‘모호성에 의한 보안’은 위험하다.</strong></p>
</blockquote>
<ul>
<li>숨겨두면 안전하다는 생각은 착각</li>
<li>오히려 <strong>투명성과 개방성</strong>이 보안의 강점을 만든다</li>
<li><strong>수천 개의 눈 원칙(Thousands of Eyeballs Principle)</strong>: 많은 이가 보는 시스템이 더 안전하다</li>
</ul>
<p>이러한 공격을 방지하기 위해선, <strong>누가 진짜인지 증명하고</strong>, <strong>누가 어디까지 접근 가능한지를 통제해야</strong> 한다.</p>
<blockquote>
<p>그렇다면, 우리는 ‘누가 무엇을 할 수 있게 허용할 것인가’를 어떻게 정할까?
바로 그걸 다루는 개념이 인증(Authentication)과 인가(Authorization)이다.</p>
</blockquote>
<ul>
<li>인증 : 사용자가 누구인지 확인하는 과정</li>
<li>인가 : 사용자에게 자원에 접근할 수 있는 권한을 부여하는 것이다. </li>
</ul>
<p>이 둘만 지켜도 기본적인 취약점은 막을 수 있다.</p>
<h3 id="인증과-토큰">인증과 토큰</h3>
<p>물론이지! 지금까지 내용들을 <strong>한 방에 쏙 이해할 수 있게</strong> 정리해줄게.
편하게 읽을 수 있도록 반말로 쓸게. 이건 ‘<strong>크립토그래피의 핵심 원리 + 실무 보안 적용</strong>’에 대한 내용이라, 앞으로 백엔드 개발할 때 진짜 많이 쓰일 거야.</p>
<h1 id="🔐-암호화-진짜-중요한-이유는">🔐 암호화, 진짜 중요한 이유는?</h1>
<h2 id="1-암호화가-필요한-이유">1) 암호화가 필요한 이유</h2>
<p>예를 들어 친구한테 숙제를 대신 내달라고 부탁한다고 해보자. 근데…</p>
<ul>
<li>그 친구가 진짜 친구인지 어떻게 알아?</li>
<li>숙제를 도중에 바꿔치기하지 않을까?</li>
<li>아예 잊어버리면 어쩌지?</li>
</ul>
<p>→ 이걸 <strong>인증(authentication)</strong>, <strong>무결성(integrity)</strong>, <strong>신뢰(trust)</strong> 문제라고 해.</p>
<p>이런 문제의 <strong>해결책이 바로 ‘암호화(cryptography)’</strong>야.
<strong>‘나와 상대만 아는 비밀 코드’</strong>를 이용해서 메시지를 주고받으면, 중간에 누가 훔쳐봐도 내용을 알 수 없고, 바꿔치기해도 티가 나게 돼.</p>
<h2 id="2-가장-위험한-데이터-비밀번호">2) 가장 위험한 데이터: 비밀번호</h2>
<p>비밀번호가 유출되면? 그냥 끝장이야.
왜냐면:</p>
<ul>
<li>로그인하면 <strong>모든 기능을 실행할 수 있으니까</strong></li>
<li>게다가 <strong>다른 사이트에서도 같은 비번</strong> 쓰는 경우가 많아서 한 번 뚫리면 줄줄이 터짐</li>
<li>내부자(예: DB 엔지니어)가 열람할 수 있어도 위험</li>
</ul>
<p>→ 그래서 <strong>비밀번호는 반드시 암호화해서 저장</strong>해야 돼.</p>
<p>암호화된 상태로 저장된 비밀번호는 설령 유출되더라도 원래 값을 알아내기 어렵고 알아내더라도 상당한 시간이 소요된다. </p>
<blockquote>
<p>이를 통해 실제 피해가 발생하기 전까지 비밀번호를 변경하는 등 <strong>사후 대응할 수 있는 시간을 벌 수 있다.</strong></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b26ba01d-9cb2-4c6e-a263-107888c56073/image.png" /></p>
<h2 id="3-단방향-암호화-복호화-불가능">3) 단방향 암호화 (복호화 불가능)</h2>
<h3 id="해시hash-함수란">해시(Hash) 함수란?</h3>
<p>비밀번호를 단방향으로 암호화할 땐 <strong>해시 함수</strong>를 써.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5e41fb85-3e9c-4181-97d0-1ef1726bb510/image.png" /></p>
<h4 id="암호화-메서드digest란">암호화 메서드(digest)란?</h4>
<p>자바에서 해시 함수(예: SHA-256)를 쓸 때 이렇게 써:</p>
<pre><code class="language-java">MessageDigest digest = MessageDigest.getInstance(&quot;SHA-256&quot;);
byte[] result = digest.digest(입력값);</code></pre>
<p>여기서 핵심은:</p>
<ul>
<li><code>digest(...)</code>라는 함수가 해시를 계산해 주는 함수야.</li>
<li>이 함수에 넣을 입력값도 <code>byte[]</code></li>
<li>결과값도 <code>byte[]</code>로 나와</li>
</ul>
<p>즉,</p>
<pre><code class="language-java">byte[] 입력값 → digest() → byte[] 결과값</code></pre>
<p>이라는 구조인 거지.</p>
<p> 왜 <code>byte[]</code>를 쓰는 걸까?</p>
<p>컴퓨터는 모든 걸 숫자(0과 1)로 처리해.
<strong>문자열(String)</strong>도 결국은 <strong>문자 인코딩 방식(UTF-8 등)</strong>에 따라 <strong><code>byte[]</code>로 변환해서 저장</strong>하거든.</p>
<p>그래서 해시 함수도 이렇게 동작해:</p>
<pre><code class="language-java">String input = &quot;password123&quot;;
byte[] origin = input.getBytes(&quot;UTF-8&quot;); // 문자열 → byte 배열
byte[] hash = digest.digest(origin);     // 해시 계산 → 결과도 byte[]</code></pre>
<h4 id="왜-결과도-byte로-줄까">왜 결과도 byte[]로 줄까?</h4>
<p>SHA-256 같은 해시 함수는 결과를 <strong>고정된 길이의 바이너리 데이터</strong>로 만들어.
예를 들어, SHA-256의 결과는 항상 <strong>32바이트(256비트)</strong>야.</p>
<p>이 결과를 그냥 byte[]로 주는 이유는:</p>
<blockquote>
<ul>
<li>결과는 사람이 읽을 수 있는 문자열이 아니라서</li>
</ul>
</blockquote>
<ul>
<li>원칙적으로는 네트워크나 파일에 쓸 때 그대로 쓸 수 있게 하려고 그래</li>
<li>암호화한 결과를 DB와 같은 저장소에 읽을 수 있는 형태로 저장하려면 바이트 배열을 문자열
로 표현해야 한다.</li>
</ul>
<p>보통은 <strong>16진수 문자열이나 Base64로 바꿔서</strong> 사람이 읽기 쉽게 표현하지.</p>
<pre><code class="language-java"> byte[] origin = input.getBytes(&quot;UTF-8&quot;);
 MessageDigest digestMessageDigest.getInstance(&quot;SHA-256&quot;);
 byte[] hash = digest.digest(origin); // byte 배열을 암호화</code></pre>
<ul>
<li>입력이 조금만 달라도 <strong>완전히 다른 결과</strong>가 나와</li>
<li>복호화는 불가능 (즉, 원래 비밀번호를 복원할 수 없어)</li>
</ul>
<blockquote>
<p>📌 대표 해시 알고리즘
SHA-256, SHA-512, MD5, BCrypt 등</p>
</blockquote>
<h3 id="값의-비교">값의 비교</h3>
<blockquote>
<p><code>단방향 암호화</code>는 해시 함수로 생성한 해시 값이 같다면 두 데이터가 같다고 간주한다. </p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/34960d04-61bd-4bd6-93bb-6eead91ae3f8/image.png" /></p>
<p><strong>로그인할 때 비밀번호가 일치하는지 여부도 해시 값을 이용해서 비교한다.</strong> 회원 가입할 때 입력한 비밀번호를 암호화한 해시 값을 DB에 저장하고, 로그인 시에는 입력한 비밀번호를 암호화해서 DB에 저장된 값과 비교한다. 두 값이 일치하면 비밀번호를 올바르게 입력한 것으로 판단한다.</p>
<blockquote>
<p>단방향 암호화는 원본 데이터로 복호화할 수 없기 때문에, 사용자가 비밀번호를 잊었을 때 기
존 비밀번호를 알려주는 기능은 구현할 수 없다. </p>
</blockquote>
<h3 id="해시-충돌collision을-막는-법-salt">해시 충돌(Collision)을 막는 법: Salt</h3>
<p>문제: 같은 비밀번호는 항상 같은 해시 결과가 나와
→ 이걸 이용하면 ‘레인보우 테이블’로 역추적할 수 있음</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/85dd8abb-1218-4996-a7ba-2ed47dc88323/image.png" /></p>
<p>참고 : 해커가 다양한 문자열과 해시 값을 미리 계산해서 만든 표를 <code>레인보우 테이블</code>이라고 한다.</p>
<p>해결책: <strong>Salt(소금)를 추가</strong>해서 해시 결과를 다르게 만들어. <code>솔트</code>는 임의의 값이며 암호화할
때 솔트를 함께 사용하면 솔트값에 따라 결과 해시 값이 달라진다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/aef1005a-6120-4484-b9ee-e6d6e9463050/image.png" /></p>
<pre><code class="language-plaintext">password + salt1 → 해시A  
password + salt2 → 해시B</code></pre>
<p>→ 해시 충돌을 막고, 같은 비번이어도 결과가 달라져</p>
<h3 id="단방향-암호화의-특징">단방향 암호화의 특징</h3>
<ul>
<li>복호화 불가능</li>
<li>로그인할 땐, 사용자가 입력한 값을 해시해서 DB의 해시값과 비교</li>
<li>비밀번호 찾기는 불가 → 대신 임시 비밀번호 발급</li>
</ul>
<h2 id="4-양방향-암호화-복호화-가능">4) 양방향 암호화 (복호화 가능)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8b82b8ed-6856-45e9-a784-ee7e47efff2d/image.png" /></p>
<p><strong>양방향 암호화는 암호화와 복호화가 모두 가능한 방식이다.</strong> 서버에 접속할 때 사용하는 SSH 프로토콜이나 API 호출 시 사용하는 HTTPS처럼 보안이 중요한 <strong>데이터 송수신 과정에서 주로 사용</strong>된다.</p>
<blockquote>
<p>양방향 암호화는 암호화와 복호화할 때 키를 사용한다 같은 알고리즘, 같은 원본 데이터라도 <strong>어떤 키를 사용하느냐에 따라 결과는 달라진다.</strong></p>
</blockquote>
<h3 id="대칭키-방식-aes-등">대칭키 방식 (AES 등)</h3>
<ul>
<li><strong>암호화/복호화에 같은 키</strong>를 사용</li>
<li>키가 유출되면 모든 데이터가 위험함</li>
<li>그래서 키 관리가 엄청 중요해</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/66516f31-b134-40e4-a996-b7e5f8d0b78d/image.png" /></p>
<pre><code class="language-java">// 1. 키 생성
KeyGenerator keyGen = KeyGenerator.getInstance(&quot;AES&quot;);
keyGen.init(256); // 256비트 키 생성
SecretKey key = keyGen.generateKey();

// 2. IV 생성
byte[] iv = new byte[16];
new SecureRandom().nextBytes(iv);

// 3. 암호화
Cipher cipher = Cipher.getInstance(&quot;AES/CBC/PKCS5Padding&quot;);
cipher.init(Cipher.ENCRYPT_MODE, key, new IvParameterSpec(iv));
byte[] encrypted = cipher.doFinal(&quot;HELLO&quot;.getBytes(&quot;UTF-8&quot;));

// 4. 복호화
cipher.init(Cipher.DECRYPT_MODE, key, new IvParameterSpec(iv));
byte[] decrypted = cipher.doFinal(encrypted);</code></pre>
<blockquote>
<p>📌 키 + IV를 조합해서 암호화 → 결과가 매번 달라짐 (패턴 방지)</p>
</blockquote>
<h3 id="비대칭키-방식-rsa-등">비대칭키 방식 (RSA 등)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4a21e7f9-f25b-4505-9da2-89695f073eef/image.png" /></p>
<ul>
<li>**공개키(Public Key)**로 암호화</li>
<li>**개인키(Private Key)**로 복호화</li>
</ul>
<pre><code class="language-java">// 1. 키 쌍 생성
KeyPairGenerator keyGen = KeyPairGenerator.getInstance(&quot;RSA&quot;);
keyGen.initialize(2048);
KeyPair pair = keyGen.generateKeyPair();
PublicKey pubKey = pair.getPublic();
PrivateKey priKey = pair.getPrivate();

// 2. 암호화
Cipher cipher = Cipher.getInstance(&quot;RSA&quot;);
cipher.init(Cipher.ENCRYPT_MODE, pubKey);
byte[] encrypted = cipher.doFinal(&quot;HELLO&quot;.getBytes(&quot;UTF-8&quot;));

// 3. 복호화
cipher.init(Cipher.DECRYPT_MODE, priKey);
byte[] decrypted = cipher.doFinal(encrypted);</code></pre>
<ul>
<li>공개키는 누구나 공유 가능</li>
<li>개인키만 있으면 복호화 가능 → 보안에 유리함</li>
<li><strong>SSH, HTTPS, 전자서명</strong>에 주로 사용돼</li>
</ul>
<blockquote>
<p>공개키로 암호화한 데이터는 개인 키로만 복호화할 수 있기 때문에, 공개 키가 유출되더라도 암호
화한 데이터를 복호화할 수 없다. <strong>따라서 같은 키를 공유해야 하는 대칭 키 방식과 비교하면 비대칭키 방식이 보안에 좀 더 안전하다</strong></p>
</blockquote>
<h3 id="ssh의-키쌍-인증-과정-공개키-인증-원리">SSH의 키쌍 인증 과정 (공개키 인증 원리)</h3>
<ol>
<li>클라이언트 → 서버에 <strong>공개키 등록</strong></li>
<li>로그인 요청 시, 서버가 임의 숫자를 <strong>공개키로 암호화</strong>해서 보냄</li>
<li>클라이언트는 <strong>개인키로 복호화</strong>함</li>
<li>클라이언트는 복호화한 숫자를 해시해서 서버에 보냄</li>
<li>서버가 값 비교 → <strong>일치하면 인증 완료!</strong></li>
</ol>
<blockquote>
<p>공개키는 누구나 가질 수 있고, 개인키만이 진짜 사용자임을 증명함.</p>
</blockquote>
<h2 id="📌-단방향-vs-양방향-암호화-비교">📌 단방향 vs 양방향 암호화 비교</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>단방향 암호화 (해시)</th>
<th>양방향 암호화 (AES, RSA 등)</th>
</tr>
</thead>
<tbody><tr>
<td>복호화 가능 여부</td>
<td>❌ 불가능</td>
<td>✅ 가능</td>
</tr>
<tr>
<td>사용 예시</td>
<td>로그인 비밀번호 저장</td>
<td>HTTPS, SSH, 민감한 데이터 전송</td>
</tr>
<tr>
<td>키 필요 여부</td>
<td>❌ 없음 (알고리즘만 있음)</td>
<td>✅ 키 필요 (대칭/비대칭 키)</td>
</tr>
<tr>
<td>보안 수준</td>
<td>해시 알고리즘 + Salt 필요</td>
<td>키 관리가 보안의 핵심</td>
</tr>
</tbody></table>
<ul>
<li><strong>AES</strong>: 빠르고 효율적인 <strong>대칭키 암호화</strong>. 키 유출 주의!</li>
<li><strong>RSA</strong>: 안전한 <strong>비대칭키 암호화</strong>, 키 쌍 이용. 인증/서명에 강함!</li>
<li><strong>SSH/HTTPS/전자서명</strong>에는 RSA, <strong>파일/DB 암호화</strong>에는 AES!</li>
</ul>
<blockquote>
<p>🔐 실무에서는 보통 <strong>RSA로 AES 키를 안전하게 전달</strong>하고, <strong>AES로 데이터 자체를 암호화</strong>하는 방식이 쓰여.</p>
</blockquote>
<h2 id="🔐-실제-로그인-인증-흐름-예시">🔐 실제 로그인 인증 흐름 예시</h2>
<ol>
<li><p>회원가입할 때:</p>
<ul>
<li>입력한 비밀번호를 <code>SHA-256 + Salt</code>로 해시</li>
<li>그 결과를 DB에 저장</li>
</ul>
</li>
<li><p>로그인할 때:</p>
<ul>
<li>사용자가 입력한 비밀번호 → 똑같이 해시해서</li>
<li>DB 값과 비교 → 같으면 인증 성공!</li>
</ul>
</li>
</ol>
<p>이제 로그인 비밀번호는 반드시 해시 + 솔트 조합으로 암호화해야 한다는 거 알았지?
그리고 중요한 데이터는 양방향 암호화로 안전하게 주고받는 게 기본 중의 기본이야.</p>
<blockquote>
<p>&quot;암호화는 보안의 끝판왕이 아니라, <strong>신뢰를 위한 최소한의 시작점</strong>이다.&quot;</p>
</blockquote>
<h1 id="📽️-딥페이크-기술의-동작-원리-완전-정복">📽️ 딥페이크 기술의 동작 원리 완전 정복</h1>
<p>현대 기술로 인해 어떤 것이 진본인지를 결정하기가 점점 어려워지고 있다.</p>
<h2 id="1-서론--딥페이크-기술의-등장">1) 서론 – 딥페이크 기술의 등장</h2>
<p>인공지능 기술의 급속한 발전으로 등장한 딥페이크(Deepfake)는 실제 존재하지 않는 가짜 영상이나 음성을 매우 사실적으로 만들어내는 기술이다. '딥러닝(Deep Learning)'과 '페이크(Fake)'의 합성어로, 고도의 딥러닝 기법을 이용해 사람의 얼굴, 표정, 음성 등을 조작함으로써 진짜처럼 보이는 가짜 콘텐츠를 생성한다.</p>
<p>이 기술은 긍정적인 활용 가능성과 동시에 심각한 사회적 위협 요소로 주목받고 있다. </p>
<h2 id="2-딥페이크-기술의-개념-및-동작-원리">2) 딥페이크 기술의 개념 및 동작 원리</h2>
<h3 id="🧠-데이터-수집-및-학습-얼굴을-학습하는-ai">🧠 데이터 수집 및 학습: 얼굴을 학습하는 AI</h3>
<p>딥페이크 기술은 기본적으로 <strong>딥러닝</strong> 기반이다. 특히 <strong>Autoencoder(오토인코더)</strong> 구조를 사용하는 경우가 많다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/40433c24-1ac6-404b-86ce-4e1c9519c05f/image.png" /></p>
<h4 id="오토인코더란">오토인코더란?</h4>
<blockquote>
<p>입력 데이터를 스스로 <strong>압축했다가 다시 복원하는</strong> 딥러닝 모델</p>
</blockquote>
<p><strong>🔷 인코더 (Encoder)</strong></p>
<ul>
<li>아래쪽 파란 부분.</li>
<li><strong>입력 데이터를 압축</strong>해서 중요한 정보만 담은 **&quot;표현 벡터&quot;**를 만들어.</li>
<li>예: 얼굴 사진 → 핵심 특징만 담은 벡터로 축소.</li>
</ul>
<p><strong>🟠 디코더 (Decoder)</strong></p>
<ul>
<li>위쪽 주황 부분.</li>
<li>표현 벡터를 다시 <strong>원래 데이터처럼 복원</strong>하려고 해.</li>
<li>예: 벡터 → 다시 얼굴 사진처럼 보이도록 출력.</li>
</ul>
<ol>
<li>입력 데이터 → 인코더 → 압축</li>
<li>표현 벡터 → 디코더 → 압축 해제</li>
<li>출력 ≈ 입력 (완벽하진 않아도 최대한 비슷하게)</li>
</ol>
<p><strong>✨ 어디에 쓰일까?</strong></p>
<ul>
<li><strong>딥페이크</strong>: 사람 얼굴 특징을 벡터로 바꾸고 다시 재구성할 때</li>
<li><strong>노이즈 제거</strong>, <strong>이상 탐지</strong>, <strong>데이터 압축</strong> 등에도 쓰여</li>
</ul>
<h4 id="11-학습-데이터-준비">1.1 학습 데이터 준비</h4>
<ul>
<li>얼굴이 잘 나온 <strong>대량의 이미지나 영상 데이터</strong>를 수집해. 예: 연예인, 정치인의 인터뷰 영상 등.</li>
<li>데이터는 다양한 표정, 조명, 각도에서의 얼굴이어야 한다. 이게 많을수록 더 자연스러운 결과가 나와.</li>
</ul>
<h4 id="12-오토인코더autoencoder-기반-학습">1.2 오토인코더(Autoencoder) 기반 학습</h4>
<ul>
<li>오토인코더는 입력 이미지(예: A의 얼굴)를 인코딩해서 **특징 벡터(latent vector)**로 만들고,</li>
<li>다시 디코더가 이 벡터를 바탕으로 원래 얼굴을 재구성해.</li>
</ul>
<pre><code class="language-plaintext">입력 이미지 (A) → Encoder → 잠재 벡터 → Decoder → 재구성된 A</code></pre>
<h3 id="13-얼굴-바꾸기용-딥페이크-구조">1.3 얼굴 바꾸기용 딥페이크 구조</h3>
<ul>
<li>A의 얼굴을 <strong>B의 얼굴 표정/움직임에 맞춰</strong> 재구성하는 식으로 작동해.</li>
<li>결국, **B의 얼굴 정보 + A의 스타일(표정 등)**을 혼합하여, A의 얼굴이 마치 B처럼 말하거나 행동하게 만드는 것이죠.</li>
</ul>
<h3 id="🎭-얼굴-합성-및-생성-단계">🎭 얼굴 합성 및 생성 단계</h3>
<p>학습이 끝나면 실제로 딥페이크 영상이 만들어진다.</p>
<h4 id="21-얼굴-탐지--정렬-alignment">2.1 얼굴 탐지 &amp; 정렬 (Alignment)</h4>
<ul>
<li>입력된 영상에서 <strong>얼굴 영역을 인식하고 정렬</strong>해.</li>
<li>눈, 코, 입의 위치를 맞추기 위해 **얼굴 랜드마크(facial landmarks)**를 잡는다.</li>
</ul>
<h3 id="22-교체할-얼굴-적용-face-swapping">2.2 교체할 얼굴 적용 (Face Swapping)</h3>
<ul>
<li><strong>소스 얼굴 A</strong>를 <strong>타겟 얼굴 B</strong>의 움직임에 맞춰 합성해.</li>
<li>표정, 입 모양, 머리 기울기 등을 반영하여, 얼굴이 매끄럽게 이어지게 한다.</li>
</ul>
<h3 id="23-포스트-프로세싱-후처리">2.3 포스트 프로세싱 (후처리)</h3>
<ul>
<li>경계선이 부자연스러워 보이지 않도록 <strong>블렌딩</strong> 작업을 한다.</li>
<li>피부 톤, 조명 효과 등을 맞추고 영상의 흐름이 자연스럽도록 조정한다.</li>
</ul>
<h3 id="🔍-딥페이크-탐지-기술-검출">🔍 딥페이크 탐지 기술 (검출)</h3>
<p>딥페이크 영상은 점점 정교해지고 있어서, <strong>탐지 기술</strong>도 점점 중요해지고 있어.</p>
<h3 id="31-미세한-신호-포착">3.1 미세한 신호 포착</h3>
<ul>
<li><p>AI는 딥페이크 영상의 <strong>이상한 점</strong>을 찾아낸다:</p>
<ul>
<li>눈 깜빡임이 <strong>비정상적으로 적거나 많음</strong></li>
<li><strong>얼굴 피부의 흔들림</strong>, <strong>광원 반사</strong>가 실제와 안 맞음</li>
<li><strong>입 모양과 발화 내용</strong>이 싱크가 안 맞음</li>
</ul>
</li>
</ul>
<h4 id="32-주로-사용되는-검출-기술">3.2 주로 사용되는 검출 기술</h4>
<table>
<thead>
<tr>
<th>기술명</th>
<th>원리</th>
</tr>
</thead>
<tbody><tr>
<td>CNN 기반 모델</td>
<td>얼굴의 픽셀 단위 차이 분석</td>
</tr>
<tr>
<td>눈 깜빡임 탐지</td>
<td>딥페이크는 눈 깜빡임이 없거나 일정함</td>
</tr>
<tr>
<td>혈류 분석</td>
<td>실제 얼굴은 <strong>피부색의 미세 변화</strong> 있음</td>
</tr>
<tr>
<td>오디오-비디오 싱크 분석</td>
<td>말하는 입 모양과 소리 일치 여부 검사</td>
</tr>
</tbody></table>
<h4 id="33-최근엔-딥러닝-vs-딥러닝-전쟁">3.3 최근엔 ‘딥러닝 vs 딥러닝’ 전쟁</h4>
<ul>
<li>딥페이크 생성도 AI, 탐지도 AI</li>
<li>GAN(생성적 적대 신경망) 구조처럼,
<strong>생성 AI와 탐지 AI가 서로 진화하면서 싸우는 구조</strong>로 발전 중</li>
</ul>
<h2 id="🤔-일반인은-어떻게-딥페이크-사기의-대상이-될까">🤔 일반인은 어떻게 딥페이크 사기의 대상이 될까?</h2>
<h3 id="1-소셜미디어에-공개한-사진·영상">1) <strong>소셜미디어에 공개한 사진·영상</strong></h3>
<ul>
<li>인스타그램, 페이스북, 틱톡, 유튜브 등에 <strong>올린 셀카, 영상</strong>들로 충분히 학습 가능해.</li>
<li>특히 <strong>웃거나 말하는 모습</strong>이 담긴 영상이 있으면 딥페이크 학습 데이터로 쓰기 좋아.</li>
<li>몇 초짜리 짧은 영상 몇 개만 있어도 요즘 모델은 그걸로 얼굴을 합성해.</li>
</ul>
<blockquote>
<p>예: &quot;셀카 영상 3~5개 + 공개된 인터뷰나 브이로그&quot; → 음성까지 덧붙여 사기 영상 생성 가능</p>
</blockquote>
<h3 id="2-ai-음성-합성까지-결합">2) <strong>AI 음성 합성까지 결합</strong></h3>
<ul>
<li><strong>전화 통화 한 번</strong>, <strong>보이스톡</strong>, <strong>유튜브 음성</strong>만 있어도 음성 딥페이크가 가능해.</li>
<li>실제로 부모나 자식의 목소리를 복제해서 **&quot;납치됐어요, 엄마&quot;**라고 울먹이는 보이스피싱 사례가 있음.</li>
</ul>
<blockquote>
<p>2023년에는 미국·한국 모두 <strong>음성 딥페이크 보이스피싱 피해 사례</strong> 뉴스로 보도됐어.</p>
</blockquote>
<h2 id="💸-딥페이크-사기-수법-예시">💸 딥페이크 사기 수법 예시</h2>
<table>
<thead>
<tr>
<th>사기 방식</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>보이스피싱</strong></td>
<td>가족·지인 목소리로 전화해서 금전 요구 (송금, 긴급 상황 연기)</td>
</tr>
<tr>
<td><strong>지인 사칭 영상</strong></td>
<td>&quot;친구가 투자 얘기하길래 봤더니 영상도 있어!&quot; → 딥페이크 영상</td>
</tr>
<tr>
<td><strong>인터뷰 영상 위조</strong></td>
<td>회사를 사칭하거나, 본인 영상 위조해서 신뢰 조작</td>
</tr>
<tr>
<td><strong>이력서·면접 사기</strong></td>
<td>AI로 만든 외국인 딥페이크가 실제 화상 면접 응시하기도 함</td>
</tr>
</tbody></table>
<p>딥페이크 기술은 분명히 흥미롭고 유용한 가능성을 지니고 있지만, 동시에 심각한 윤리적, 법적, 사회적 문제를 동반한다. 기술의 발전에만 초점을 맞추기보다는 그 사용 범위와 방식에 대한 사회적 합의와 법적 제도 정비가 병행되어야 한다. 우리는 지금 '진짜 같은 가짜'가 현실을 위협하는 시대에 살고 있으며, 진짜를 지켜내기 위한 대응이 절실하다.</p>
<h1 id="🔐-마무리하며">🔐 <strong>마무리하며</strong></h1>
<p>이번 주는 스터디 주제와 딱 맞게, 『한 권으로 읽는 컴퓨터 구조와 프로그래밍』의 <strong>보안 개념</strong>과 『주니어 백엔드 개발자가 반드시 알아야 할 실무 지식』의 <strong>암호화 실습 중심 내용</strong>을 함께 정리해보았다.</p>
<p>이론으로는 <strong>암호화의 필요성과 구조(대칭/비대칭 키), 인증 흐름, 해시와 솔트 개념</strong>을, 실무에서는 <strong>AES/RSA 암호화 방식, SHA-256 해시 구현, SSH 인증 흐름</strong> 등 실제 코드 기반으로 다뤄보며 실전 감각을 키울 수 있었다.</p>
<p>보안은 단순히 ‘막는 기술’이 아니라, <strong>사용자와 시스템 사이의 신뢰를 만들어가는 과정</strong>이다. 코드 한 줄에도 보안적인 사고를 담을 수 있다면, 이미 한 단계 성장한 개발자가 된 것이겠지.</p>
<blockquote>
<p><strong>&quot;보안은 끝이 아니라, 개발의 시작이다.&quot;</strong>
당장의 프로젝트에 꼭 쓰이지 않더라도, <strong>개발자로 오래 일하고 싶다면 꼭 한 번은 정리해봐야 할 영역</strong>이 바로 보안이다.</p>
</blockquote>
<p>📘 <strong>실무 관점에서 보안을 차근차근 다뤄보고 싶다면</strong>, 『주니어 백엔드 개발자가 반드시 알아야 할 실무 지식』을 꼭 추천드리고 싶다.
단순한 설명을 넘어서 <strong>직접 써볼 수 있는 코드 예제와 실제로 마주할 수 있는 보안 상황들까지 잘 담겨 있어</strong>, 실무에 바로 연결되는 인사이트를 얻을 수 있다.</p>
<p>다음에도 이렇게 이론과 실무를 함께 엮은 공부를 해보며, 더욱 탄탄한 개발자로 함께 성장해가자 :)</p>