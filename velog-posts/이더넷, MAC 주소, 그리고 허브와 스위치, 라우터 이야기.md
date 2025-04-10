<blockquote>
<p>이더넷이란? → NIC(랜카드)와 MAC 주소 → 허브와 스위치의 차이와 동작 방식  </p>
</blockquote>
<h2 id="🧠-핵심-메시지">🧠 핵심 메시지</h2>
<blockquote>
<p>&quot;우리가 사용하는 와이파이와 인터넷, 그 근간에는 조용히 일하는 이더넷과 스위치가 있다.&quot;</p>
</blockquote>
<h1 id="🛠-1-이더넷이란-무엇일까">🛠 1. 이더넷이란 무엇일까?</h1>
<h2 id="🧭-1-인터넷은-마법이-아니다">🧭 1) 인터넷은 마법이 아니다</h2>
<p>우리는 인터넷을 너무나 당연하게 여깁니다.<br />주소창에 <code>www.google.com</code>을 치면 바로 구글이 뜨고, 고양이 영상도 척척 재생되죠. 하지만 이 모든 건 수많은 기술과 장비가 눈에 보이지 않는 곳에서 일사불란하게 움직이기 때문입니다.</p>
<p>그 중심에 있는 것이 바로 <strong>이더넷, MAC 주소, 허브, 스위치, 라우터</strong>입니다.</p>
<p>인터넷과 이름이 비슷해서 헷갈리지만,<br /><strong>이더넷(Ethernet)</strong>은 ‘인터넷’의 일부가 아니라,<br /><strong>하나의 네트워크(LAN)를 구성하는 기술 방식</strong>입니다.</p>
<h2 id="2-이더넷이란">2) 이더넷이란?</h2>
<blockquote>
<p>즉, 인터넷이 ‘전 세계 네트워크의 연결’이라면,<br />이더넷은 ‘하나의 지역 네트워크(LAN)를 만드는 설계도’입니다!</p>
</blockquote>
<p>이더넷은 케이블, 전기 신호, 신호 처리 규칙, MAC 주소 등<br /><strong>LAN을 구축하는 모든 요소와 방식</strong>을 하나로 정리한 네트워크 만들기 키트예요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a6622ee7-d0c0-43df-bbb3-c53e13eec2be/image.png" /></p>
<p>📝 <strong>표준 이름: IEEE 802.3</strong><br />이 표준은 IEEE라는 국제 기술 기관에서 정리한 공식 문서로,<br /><strong>케이블 방식, 신호 처리, 충돌 대응 방식 등</strong>이 포함되어 있습니다.</p>
<h1 id="🌶-2-이더넷도-떡볶이처럼-종류가-다양하다">🌶 2. 이더넷도 떡볶이처럼 종류가 다양하다?</h1>
<p>이더넷은 하나의 기술이지만,<br /><strong>속도, 케이블 종류, 신호 방식</strong>에 따라 여러 가지 버전이 있어요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/51f2e521-1540-4084-8d1b-b529d456614a/image.png" /></p>
<table>
<thead>
<tr>
<th>규격 이름</th>
<th>전송 속도</th>
<th>특징</th>
</tr>
</thead>
<tbody><tr>
<td>10BASE-T</td>
<td>10Mbps</td>
<td>구리선 사용, 초기 이더넷</td>
</tr>
<tr>
<td>100BASE-T</td>
<td>100Mbps</td>
<td>Fast Ethernet</td>
</tr>
<tr>
<td>1000BASE-T</td>
<td>1Gbps</td>
<td>현재 가장 일반적인 형태</td>
</tr>
<tr>
<td>10GBASE-T</td>
<td>10Gbps 이상</td>
<td>데이터센터, 기업용 등</td>
</tr>
</tbody></table>
<blockquote>
<p>마치 <strong>밀떡, 쌀떡, 치즈떡볶이</strong>처럼 속도와 환경에 따라 골라 쓰는 네트워크 떡볶이입니다!</p>
</blockquote>
<p>10Mbps 앞에 적힌 단위는 1초 사이에 주고받을 수 있는 데이터의 크기를 말하며 <code>1Gbps</code>는 1초에 1기가바이트를 전송할 수 있다는 뜻입니다. 오늘날 일반 가정 및 사무실에서는 주로 <code>1Gbps</code>가 사용되며, <code>10Gbps 이상</code>의 이더넷은 데이터 센터나 인터넷 제공 업체처럼 많은 양의 데이터를 처리해야 하는 곳에서 사용합니다.</p>
<h1 id="👨💼-3-통역사처럼-일하는-nic랜카드의-역할">👨‍💼 3. 통역사처럼 일하는 ‘NIC(랜카드)’의 역할</h1>
<p><code>이더넷</code>에는 유선으로 네트워크를 연결하기 위해 꼭 필요한 케이블에 대한 설명이 
담겨 있습니다. </p>
<p>이더넷에서 사용하는 <strong>케이블의 종류</strong>는 구리로 되어 있는 케이블부터 유리나 플라스틱으로 되어 있는 케이블까지 다양한데, 이더넷은 이러한 케이블 종류와 더불어 연결 단자의 규격에 관한 내용까지 정의하고 있습니다. </p>
<p>또 이후에 설명할 허브와 스위치처럼 <strong>자신에게 연결된 컴퓨터들이 보내는 데이터를 받아 또 다른 컴퓨터에 전송 하는 중간 장치에 대한 내용도 담겨 있습니다.</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e9cb090c-9e30-4b79-983b-eadbacde7f8e/image.png" /></p>
<p>이외에도 네트워크 계층에서 사용하는 IP 주소처럼 각 기기를 구분하는 역할을 하는 MAC 주소와 이러한 MAC 주소가 붙어 있는 장치인 <code>네트워크 인터페이스 카드</code>에 관한 내용도 들어 있습니다</p>
<blockquote>
<p>NIC(Network Interface Card), 흔히 ‘랜카드’라고 부르는 이 부품은<br /><strong>컴퓨터를 네트워크와 연결하는 통역사</strong> 역할을 합니다.</p>
</blockquote>
<p>예전에는 PC 본체에 별도로 장착된 네트워크 인터페이스 카드가 있었는데, </p>
<blockquote>
<p>요즘에는 <code>메인보드</code>에 LAN 포트가 통합되어 있어 따로 신경 쓰지 않아도 간편하게 네트워크에 연결할 수 있습니다. </p>
</blockquote>
<h2 id="nic의-주요-역할">NIC의 주요 역할</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/052156d5-cb0f-4e22-88da-00e012281a89/image.png" /></p>
<p>1) <strong>직렬화(serialization)</strong><br />   → 데이터를 전기 신호로 변환하거나, 반대로 신호를 데이터로 되돌림<br />2) <strong>MAC 주소 관리</strong><br />   → 고유 식별 번호로, 네트워크 상에서 자신을 식별함</p>
<p>📦 데이터를 NIC에 전달하면 → ⚡ 전기 신호로 변환되어 케이블을 통해 전송됩니다.<br />반대로, 들어온 신호도 NIC가 읽어서 다시 데이터로 바꿔주죠.</p>
<h1 id="🆔-4-진짜-주소-mac-주소란">🆔 4. 진짜 주소, MAC 주소란?</h1>
<p>NIC에는 고유한 ‘<strong>MAC 주소 (Media Access Control)</strong>’가 들어 있습니다.<br />이 주소는 마치 <strong>기기의 주민등록번호</strong> 같아요.</p>
<p>MAC 주소는 <strong>PC나 스마트폰처럼 네트워크를 사용하는 기기라면 모두가 가진 주소</strong>로, IP 주소처럼 장치들을 서로 인식하고 식별하기 위해 사용합니다.</p>
<table>
<thead>
<tr>
<th>비교 항목</th>
<th>MAC 주소</th>
<th>IP 주소</th>
</tr>
</thead>
<tbody><tr>
<td>고정 여부</td>
<td>고정 (제조 시 부여)</td>
<td>변경 가능</td>
</tr>
<tr>
<td>용도</td>
<td>물리적인 기기 식별</td>
<td>논리적인 네트워크 식별</td>
</tr>
<tr>
<td>예시</td>
<td><code>ab:cd:ef:01:23:45</code></td>
<td><code>192.168.0.1</code></td>
</tr>
</tbody></table>
<p>MAC 주소는 <strong>48비트(6바이트)</strong>로 구성되며,<br />앞 3바이트는 제조사 식별, 뒤 3바이트는 기기 고유 번호입니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7540c7ed-f562-47af-b027-de7ae5bc4972/image.png" /></p>
<blockquote>
<p>이 MAC 주소를 가지고 어떤 일을 할 수 있을까요? </p>
</blockquote>
<ol>
<li>기기 내부에서 자신에게 들어온 데이터가 맞는지 판별하는 데 사용할 수 있습니다.</li>
</ol>
<p>데이터가 들어왔을 때 헤더에 적힌 도착지 MAC 주소를 확인하고, 자기 주소가 맞으면 IP, TCI〕처럼 상위 레벨에서 처리할 수 있게 데이터를 전송하고, 아니라면 폐기하는 식입니다.</p>
<ol start="2">
<li><strong>스위치</strong>에서도 이 MAC 주소를 활용해 자신에게 연결된 컴퓨터로 데이터를 전달합니다.</li>
</ol>
<h1 id="🔌-5-네트워크는-선만-연결하면-끝일까">🔌 5. 네트워크는 선만 연결하면 끝일까?</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c2db51ac-8748-4286-8d5d-170975bdb641/image.png" /></p>
<p>처음 컴퓨터를 연결할 땐 단순히 선만 연결하면 됐습니다.<br />하지만 컴퓨터가 5대 이상이 되면?</p>
<blockquote>
<p>케이블이 복잡해지고, 충돌과 전송 문제가 발생해요.</p>
</blockquote>
<p>그래서 등장한 것이 <strong>허브(Hub)</strong>와 <strong>스위치(Switch)</strong>입니다.<br />두 장치는 모두 <strong>여러 컴퓨터를 하나의 네트워크로 묶어주는 중심 장치</strong>이지만,<br />그 작동 방식에는 <strong>큰 차이</strong>가 있습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2bef2fde-8b5b-40d6-86ea-c8adbd75d561/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1f22ca78-5da2-4dbc-83c9-63c12e213fb3/image.png" /></p>
<p>‘이더넷이란?’에서는 공유기가 라우터의 역할도 수행하고 있다고 이야기했습니다. </p>
<p>그럼 공유기는 라우터일까요, 아니면 스위치나 허브일까요? 정답은 둘 다입니다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d6e7afde-cb29-4f47-99de-143316ba80f6/image.png" /></p>
<p>우리가 생각하는 것 이상으로 가정용 공유기는 하는 일이 많은데요, <code>라우터</code>처럼 <strong>외부 네트워크에서 내부 네트워크로 데이터를 연결하는 일도 수행</strong>하고, <code>스위치나 허브</code>처럼 <strong>내부적으로 데이터를 주고받는 역할도 수행</strong>합니다</p>
<h1 id="🚦-5-라우터-길을-안내하는-네트워크의-내비게이션">🚦 5. 라우터, 길을 안내하는 네트워크의 내비게이션</h1>
<blockquote>
<p>라우터（router)는 길을 뜻하는 route에서 따온 용어로. 이름처럼 데이터가 원하는 목적지로 원활하게 도착할 수 있도록 적절한 통신 경로를 안내하는 장치입니다.</p>
</blockquote>
<p>물론입니다! 위 내용을 기반으로 라우터와 라우팅 테이블, TTL까지 <strong>이야기 중심 발표 스크립트 스타일</strong>로 정리해드릴게요. 비유와 흐름을 활용해 쉽게 이해될 수 있도록 구성했습니다.</p>
<hr />
<h1 id="🚦-라우터-길을-안내하는-네트워크의-내비게이션">🚦 <strong>라우터, 길을 안내하는 네트워크의 내비게이션</strong></h1>
<blockquote>
<p>라우터（router)는 길을 뜻하는 route에서 따온 용어로. 이름처럼 데이터가 원하는 목적 지로 원활하게 도착할 수 있도록 적절한 통신 경로를 안내하는 장치입니다</p>
</blockquote>
<h2 id="🧭-1-네트워크에도-길잡이가-필요해요">🧭 1) 네트워크에도 길잡이가 필요해요</h2>
<p>생각해봅시다.<br />우리가 <strong>지도 앱</strong>을 켜고 목적지를 입력하면 앱은 <strong>최적의 경로</strong>를 찾아주죠.<br />“이 길은 막혔어요, 우회하세요!”<br />“3분 더 빨리 가려면 이쪽으로 가세요!”</p>
<blockquote>
<p>마치 안내 데스크입
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/bf2c1d2d-a29e-49d8-ba2c-d9a0bf492d30/image.png" /></p>
</blockquote>
<p>이런 기능은 인터넷 세계에도 필요합니다.<br />수많은 데이터가 네트워크망 속을 이리저리 오가는 가운데, 데이터도 목적지까지 <strong>최적의 길</strong>로 가야 합니다.</p>
<p>이 역할을 해주는 장치가 바로 <strong>라우터(Router)</strong>입니다.</p>
<h2 id="🧱-2-라우터는-뭐-하는-기계일까">🧱 2) 라우터는 뭐 하는 기계일까?</h2>
<p><strong>라우터는 '길을 안내해주는 장비'</strong>입니다.<br /><code>Route</code>라는 단어에서 왔듯, 데이터가 목적지까지 <strong>가장 빠르고 정확하게</strong> 갈 수 있도록 중간에서 경로를 안내해줍니다.</p>
<blockquote>
<p>📦 라우터 = 네트워크의 안내데스크<br />&quot;이쪽으로 가세요!&quot;<br />&quot;아, 그 목적지라면 이 라우터를 거쳐 가세요.&quot;</p>
</blockquote>
<h2 id="🏡-3-공유기도-사실-라우터예요">🏡 3) 공유기도 사실 라우터예요</h2>
<p>우리 집에 있는 <strong>공유기(Wi-Fi 라우터)</strong>도 라우터의 역할을 합니다.<br />공유기 뒷면을 보면 ‘WAN’ 단자가 있죠? 여기에 외부 인터넷 선을 꽂으면 <strong>외부 네트워크(WAN)</strong>와 <strong>집 안 네트워크(LAN)</strong>를 연결하는 <strong>게이트웨이</strong> 역할을 하게 됩니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f445b99b-0552-46f5-bcea-6a4cf6bdcc69/image.png" /></p>
<p>하지만 라우터는 집 안에만 있는 게 아닙니다.<br />KT, SK브로드밴드 같은 통신사, 대기업 데이터 센터, 글로벌 네트워크 중심지에도 수많은 라우터가 복잡한 통신망을 관리하고 있습니다.</p>
<h2 id="🗺️-4-라우팅-테이블-라우터-속의-지도">🗺️ 4) 라우팅 테이블: 라우터 속의 지도</h2>
<p>자, 질문이 생깁니다.</p>
<blockquote>
<p>“라우터는 어떻게 수많은 경로 중에서 최적의 길을 찾을까?”</p>
</blockquote>
<p>그 비밀은 바로 <strong>라우팅 테이블(Routing Table)</strong>에 있습니다.<br />라우터는 이 테이블에 다음과 같은 정보를 기록해두고 있어요.</p>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>목적지 주소</td>
<td>데이터가 가야 할 IP 주소</td>
</tr>
<tr>
<td>다음 홉(Next hop)</td>
<td>그 목적지로 가기 위한 다음 라우터의 주소</td>
</tr>
<tr>
<td>거리/우선순위</td>
<td>가장 빠른 경로에 우선순위를 둠</td>
</tr>
</tbody></table>
<p>📌 <strong>이 정보는 직접 사람이 설정할 수도 있고</strong>, 주변 라우터들과 자동으로 정보 교환을 통해 갱신될 수도 있어요.</p>
<h2 id="🧪-5-실제-데이터의-여정은">🧪 5) 실제 데이터의 여정은?</h2>
<p>예를 들어, <strong>김네트</strong>의 집에서 <strong>박워크</strong>의 집으로 데이터를 보내고 싶다고 해봅시다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/75defa27-fcbd-46cc-a917-55816f18158a/image.png" /></p>
<ol>
<li>김네트의 컴퓨터는 데이터를 만들어 근처 라우터에 보냅니다.</li>
<li>라우터는 <strong>라우팅 테이블</strong>을 보고 목적지와 유사한 주소를 찾습니다.</li>
<li>“가장 가까운 건 저쪽 라우터네!” 하고 다음 라우터로 데이터를 넘깁니다.</li>
<li>이렇게 중간 라우터를 계속 거치면서 목적지인 박워크의 집까지 도착하게 됩니다.</li>
</ol>
<h2 id="🔁-6-무한-루프를-막는-ttl">🔁 6) 무한 루프를 막는 TTL</h2>
<p>문제는, 라우터가 잘못된 경로를 갖고 있다면 어떻게 될까요?</p>
<blockquote>
<p>❗ A → B → A → B → A…<br />데이터가 같은 자리만 계속 돌 수도 있어요. 이걸 <strong>라우팅 루프</strong>라고 해요.</p>
</blockquote>
<p>이런 상황을 막기 위해 <strong>TTL(Time To Live)</strong>이라는 제도가 있습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/33e8b8bc-b2b0-4b0a-9ffe-94a04d1ab032/image.png" /></p>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>TTL의 역할</td>
<td>데이터가 네트워크를 무한히 떠도는 걸 방지</td>
</tr>
<tr>
<td>기본 구조</td>
<td>데이터가 라우터를 하나 지날 때마다 TTL 값이 1씩 감소</td>
</tr>
<tr>
<td>종료 조건</td>
<td>TTL = 0이 되면 데이터는 폐기됨</td>
</tr>
</tbody></table>
<blockquote>
<p>TTL은 마치 음식에 붙은 ‘유통기한’ 같아요.<br />너무 오래 지나면 버리는 거죠!</p>
</blockquote>
<h2 id="💡-정리해봅시다">💡 정리해봅시다</h2>
<table>
<thead>
<tr>
<th>개념</th>
<th>요약 설명</th>
</tr>
</thead>
<tbody><tr>
<td>라우터</td>
<td>데이터를 목적지로 보내는 네트워크의 길 안내자</td>
</tr>
<tr>
<td>라우팅 테이블</td>
<td>라우터 속의 지도 (어디로 보낼지 정보 저장)</td>
</tr>
<tr>
<td>TTL</td>
<td>데이터가 네트워크 속을 무한히 맴도는 걸 막는 유효기간</td>
</tr>
</tbody></table>
<h2 id="✨-한-문장-요약">✨ 한 문장 요약</h2>
<blockquote>
<p><strong>라우터는 데이터의 내비게이션이다.<br />그 안에는 라우팅 테이블이라는 지도와, TTL이라는 유효기간이 있다.<br />덕분에 데이터는 빠르고 안전하게 목적지까지 도달한다.</strong></p>
</blockquote>
<h1 id="📣-7-허브-모두에게-공평하지만-비효율적">📣 7. 허브: 모두에게 공평하지만, 비효율적</h1>
<blockquote>
<p>📢 허브는 확성기다</p>
</blockquote>
<p>허브는 <strong>모든 컴퓨터에 데이터를 똑같이 전달</strong>합니다.<br />이를 ‘브로드캐스트 통신’이라고 해요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/579c32c7-cf6d-4400-9602-4a1ad3b800d1/image.png" /></p>
<p>그래서 하나가 말할 땐, 나머지는 조용해야 합니다. 동시에 두 명이 말하면? 충돌(Collision)이 발생하죠.</p>
<p>📢 예시: 카페 공지사항처럼 모든 사람에게 보내는 방식</p>
<h3 id="허브의-단점">허브의 단점</h3>
<ul>
<li>한 번에 <strong>하나의 통신만 가능</strong></li>
<li>데이터를 많이 보낼수록 <strong>충돌 가능성 증가</strong></li>
<li><strong>충돌이 나면 재전송</strong>, 비효율 발생</li>
</ul>
<blockquote>
<p>그래서 허브는 <strong>간단하지만 성능이 떨어지는 방식</strong>이에요.</p>
</blockquote>
<h1 id="🎯-8-스위치-목적지를-알고-보내는-똑똑한-장치">🎯 8. 스위치: 목적지를 알고 보내는 똑똑한 장치</h1>
<blockquote>
<p>스위치는 편지지</p>
</blockquote>
<p>스위치는 <strong>데이터의 목적지를 파악해 해당 컴퓨터에게만 전달</strong>합니다.<br />이걸 ‘<strong>유니캐스트 통신</strong>’이라고 합니다.</p>
<p>📦 예시: 택배처럼 ‘받는 사람’에게만 정확히 전달하는 방식</p>
<blockquote>
<p>그럼 스위치는 어떻게 정확히 목적지를 찾을 수 있는 걸까요?</p>
</blockquote>
<h3 id="스위치의-동작-방식">스위치의 동작 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a92e3067-0598-4e2b-96c9-d1122ab65b0e/image.png" /></p>
<p>1) 컴퓨터의 MAC 주소를 보고
2) 어떤 포트에 어떤 기기가 연결됐는지 학습 (MAC 주소 테이블)
3) 목적지 주소에 따라 정확히 데이터 전송</p>
<table>
<thead>
<tr>
<th>장치</th>
<th>통신 방식</th>
<th>충돌 방지</th>
<th>효율성</th>
</tr>
</thead>
<tbody><tr>
<td>허브</td>
<td>브로드캐스트</td>
<td>없음</td>
<td>낮음</td>
</tr>
<tr>
<td>스위치</td>
<td>유니캐스트</td>
<td>있음</td>
<td>높음</td>
</tr>
</tbody></table>
<blockquote>
<p>이 덕분에 <strong>여러 컴퓨터가 동시에 통신 가능</strong>하고,<br />네트워크 성능도 대폭 향상됩니다!</p>
</blockquote>
<p>보통 스위치에 연결된 컴퓨터들은 <strong>각자 고유한 포트 번호</strong>를 갖고 있습니다. 가령 거실에 
있는 컴퓨터는 포트 번호 1234번, 동생 방에 있는 노트북은 포트 번호 5678번과 같은 식 
입니다. </p>
<p>그리고 처음 데이터 통신이 시작되면 스위치는 자신에게 들어온 데이터의 헤더를 보고 목적지의 MAC 주소는 어디이며 포트 번호는 몇 번인지를 확인해 MAC 주소 테이블이라는 공간에 저장합니다. </p>
<p>이렇게 한 번 테이블에 정보가 저장되고 나면 다시 데이터를 주고받을 때 스위치에서 데이터의 MAC 주소를 확인한 뒤 <strong>MAC 주소 테이블을 확인해 주소가 일치하는 기기의 포트로만 데이터를 전송하게 됩니다.</strong></p>
<p>이렇게 <code>스위치</code>는 정해진 목적지로만 데이터를 보내기 때문에 여러 기기가 충돌 없이 동 
시에 데이터를 주고받을 수 있게 되었고, 그 결과 허브에 비해 더 효율적인 네트워크 통 
신이 가능해졌습니다</p>
<blockquote>
<p>“스위치와 MAC 주소는, 인터넷 통신의 골목길을 막힘 없이 연결해주는 도로와 표지판이다.”</p>
</blockquote>
<pre><code>[ 컴퓨터 ]
   │    ↑
[ NIC (MAC 주소) ]
   │
[ 스위치 ↔ MAC 주소 기반으로 분배 ]
   │
[ 라우터 ↔ 외부 네트워크와 연결 ]
   │
[ 인터넷 ↔ 수많은 라우터, DNS, 서버 ]</code></pre><h1 id="출처">출처</h1>
<ul>
<li>그림으로 쉽게 이해하는 웹, HTTP, 네트워크 (강추)</li>
</ul>