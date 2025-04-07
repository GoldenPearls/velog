<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/106010f6-884f-4c7c-bbdf-f2f1505387c7/image.png" /></p>
<blockquote>
<p><strong>MMU(Memory Management Unit)</strong>는 컴퓨터 메모리를 훨씬 더 유연하게 만들어주는 마법 같은 장치입니다. 주기억장치관리의 핵심은 '메인 메모리를 어떻게 잘 관리할 수 있을까'에 있습니다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2d5c9153-4792-4b17-a28e-6427d13b02f0/image.png" /></p>
<blockquote>
<p><a href="https://cho-light.tistory.com/53">메모리를 좀 더 자세히</a></p>
</blockquote>
<h2 id="1-🚨-멀티태스킹의-시대-안전은-필수다">1) 🚨 멀티태스킹의 시대, 안전은 필수다!</h2>
<p>과거에는 컴퓨터가 한 번에 하나의 프로그램만 실행해도 충분했지만,
요즘은 백그라운드에서 여러 프로그램이 동시에 실행되는 <strong>멀티태스킹</strong>이 당연한 시대예요.</p>
<p>하지만 문제가 있습니다.</p>
<ul>
<li>여러 프로그램이 한 메모리를 공유할 경우</li>
<li><strong>버그가 난 프로그램이 다른 프로그램의 메모리를 침범할 수 있음</strong></li>
<li>심하면 운영체제(OS) 자체의 메모리를 덮어쓸 수도 있음</li>
</ul>
<blockquote>
<p>🧨 보안 위협뿐만 아니라, 시스템 전체가 뻗을 수 있어요!</p>
</blockquote>
<p>그래서 필요한 것이 바로 <strong>MMU (Memory Management Unit)</strong>입니다.</p>
<h2 id="2-🧰-mmu란-무엇인가요">2) 🧰 MMU란 무엇인가요?</h2>
<p>MMU는 컴퓨터에 들어 있는 <strong>하드웨어 장치</strong>로,</p>
<blockquote>
<p>✅ 프로그램이 사용하는 &quot;가상 주소&quot;를 실제 &quot;물리 주소&quot;로 변환해주는 장치입니다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0a142379-b4e7-4ab6-97b9-454899474ebb/image.png" />
출처 : <a href="https://velog.io/@tycode4/%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC">https://velog.io/@tycode4/%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC</a></p>
<p>우리가 보통 알고 있는 가상 메모리는:</p>
<blockquote>
<p>&quot;MMU가 프로그램이 사용하는 가상 주소를 물리 주소로 바꿔주는 시스템&quot;</p>
</blockquote>
<p>...이 정도로 알고 있지만, 사실 그 기능은 시작일 뿐이고, 진짜 강력한 기능은 <strong>훨씬 더 대담한 착각(!)</strong>을 만들어내요.</p>
<p><strong>🧠 프로그램은 &quot;메모리 부족&quot;을 모른다?</strong>
운영체제는 이렇게 속입니다:</p>
<p>“그래, 네가 필요한 만큼 메모리가 있는 것처럼 써도 돼~ 내가 뒤에서 알아서 해줄게!”</p>
<p>실제로는 메모리가 부족해도 프로그램이 느끼지 않도록, <strong>페이지 폴트(page fault)</strong>와 함께 요구불 페이징(demand paging) 기법이 작동합니다.</p>
<p>즉, 프로그램은 자신이 마치 독립적인 메모리를 갖고 있는 것처럼 느끼게 만들어 주는 장치죠.</p>
<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>가상 주소</strong></td>
<td>프로그램이 사용하는 주소. 겉보기용</td>
</tr>
<tr>
<td><strong>물리 주소</strong></td>
<td>실제 메모리(RAM) 상의 위치</td>
</tr>
<tr>
<td><strong>MMU</strong></td>
<td>가상 주소 → 물리 주소로 바꿔주는 장치</td>
</tr>
</tbody></table>
<blockquote>
<p>📌 이 과정 덕분에 여러 프로그램이 서로 독립된 공간에서 실행되는 것처럼 동작할 수 있어요!</p>
</blockquote>
<h2 id="3-🧭-가상-주소의-동작-원리-페이지와-페이지-테이블">3) 🧭 가상 주소의 동작 원리: 페이지와 페이지 테이블</h2>
<p>MMU는 가상 주소를 물리 주소로 단순히 1:1 매핑하지 않습니다.
대신, <strong>페이지(Page)</strong>라는 단위로 메모리를 관리하죠.</p>
<h3 id="📦-demand-paging요구불-페이징이란">📦 Demand Paging(요구불 페이징)이란?</h3>
<p>프로그램이 진짜로 필요한 페이지만 물리 메모리에 올려요.</p>
<p>나머지는 아직 메모리에 없어요. 필요할 때 그때그때 불러옵니다.</p>
<p>마치 넷플릭스에서 보고 싶은 장면만 스트리밍하는 것과 같아요.</p>
<h3 id="📦-페이지란">📦 페이지란?</h3>
<ul>
<li>메모리를 일정한 크기로 쪼갠 단위 (예: 256B, 4KB 등)</li>
<li>프로그램은 페이지 단위로 메모리를 할당받고 사용</li>
</ul>
<h3 id="🧠-가상-메모리의-동작-방식">🧠 가상 메모리의 동작 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/710bf947-6720-4326-be60-a7c2d71fa582/image.png" /></p>
<blockquote>
<p>출처 ： <a href="https://velog.io/@hyun0310woo/11-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC">https://velog.io/@hyun0310woo/11-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC</a></p>
</blockquote>
<p>가상 메모리는 &quot;가상 주소(Virtual Address)&quot;를 사용해서, <strong>물리 주소(Physical Address)</strong>로 간접 접근하게 만드는 기술입니다.</p>
<ul>
<li>프로세스는 오직 가상 주소만 사용합니다.</li>
<li>가상 주소는 실제 메모리 주소가 아니라, 중간에서 <strong>커널이 번역</strong>해주는 주소예요.</li>
<li>번역 작업은 <strong>페이지 테이블(Page Table)</strong>을 통해 이루어집니다.</li>
</ul>
<h3 id="📑-페이지-테이블page-table">📑 페이지 테이블(Page Table)</h3>
<ul>
<li>각 프로그램마다 <strong>자신의 가상 페이지</strong>가 <strong>어느 물리 페이지에 매핑되는지 저장</strong>하는 테이블</li>
<li>. 페이지 테이블에는 각 페이지가 물리 메모리상에서 차지하는 실제 위치 정보가 들어 있어 있습니다.</li>
<li>프로그램마다 다르고, 운영체제가 관리함</li>
</ul>
<h3 id="🔁-mmu-주소-변환-흐름">🔁 MMU 주소 변환 흐름</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4db0650b-4b47-4dbe-ad78-9c9dbe1acecd/image.png" /></p>
<blockquote>
<p>CPU는 무조건 가상메모리만을 참조해달라고 요청하고, 그 가상메모리 주소가 실제 어느 물리 주소에 있는지 MMU가 변환 시켜주고, 그 해당 물리 메모리에 접근을 하여 그 해당 데이터를 CPU에 전달합니다.</p>
</blockquote>
<ol>
<li>프로그램은 가상 주소를 사용해 메모리에 접근</li>
<li>MMU가 가상 주소의 페이지 번호를 읽고</li>
<li><strong>해당 페이지 번호를 페이지 테이블에서 검색</strong>하여</li>
<li>매핑된 물리 페이지의 주소로 접근!</li>
</ol>
<blockquote>
<p>가상 주소는 연속적이지만, 물리 주소는 불연속일 수 있음 → <strong>메모리 조각 문제 방지!</strong></p>
</blockquote>
<blockquote>
<p><a href="https://velog.io/@tycode4/%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC">이로 인해 페이징 기법이 생겨남 더 읽어보기</a></p>
</blockquote>
<h3 id="페이지-테이블은-그냥-메모리의-일부분">페이지 테이블은 그냥 메모리의 일부분</h3>
<p>프로그램 입장에서는 가상 메모리가 연속적인 것처럼 보이지만, 실제 물리 메모리상의 위치는 굳이 연속적일 필요가 없습니다. </p>
<blockquote>
<p>심지어 프로그램이 실행되는 도중에 프로그램이 위치한 물리적 메모리 주소가 바뀔 수도 있어요. </p>
</blockquote>
<p>그리고 프로그램들이 서로 협력하는 경우에는 여러 프로그램의 가상 메모리 중 *<em>일부가 같은 물리 메모리를 함께 사용하는 공유 메모리 기능을 제공할 수도 있어요. *</em></p>
<p>이제 페이지 테이블의 내용이 프로그램 문맥의 일부분이 된다는 사실에 유의하고 보면, 페이지 테이블은 그냥 메모리의 일부분이 됩니다.</p>
<h2 id="4-💡-예시-16비트-주소와-페이지-테이블">4) 💡 예시: 16비트 주소와 페이지 테이블</h2>
<p>가상 주소: <code>A15~A0</code> (총 16비트)</p>
<ul>
<li>상위 비트(<code>A15~A8</code>) → 페이지 번호 (256개 페이지)</li>
<li>하위 비트(<code>A7~A0</code>) → 페이지 안의 오프셋</li>
</ul>
<p>페이지 테이블:</p>
<table>
<thead>
<tr>
<th>가상 페이지 번호</th>
<th>매핑된 물리 페이지 번호</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>8</td>
</tr>
<tr>
<td>1</td>
<td>5</td>
</tr>
<tr>
<td>...</td>
<td>...</td>
</tr>
</tbody></table>
<p>→ 예를 들어, 가상 주소 <code>0x01A2</code>는:</p>
<ul>
<li>페이지 번호: 0x01</li>
<li>오프셋: 0xA2</li>
<li>페이지 테이블을 통해 → 물리 페이지 5번 → <code>0x05A2</code>로 변환됨</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/fd5a0dcd-e8bb-4520-8e29-3064555f317e/image.png" /></p>
<h2 id="5-🧷-프로그램-분리를-통한-보안성-강화">5) 🧷 프로그램 분리를 통한 보안성 강화</h2>
<p>MMU가 없다면?</p>
<ul>
<li>프로그램 1이 프로그램 2의 메모리를 침범할 수 있음</li>
<li>악성 코드가 운영체제를 덮어쓸 수 있음</li>
</ul>
<p>MMU가 있다면?</p>
<ul>
<li>각 프로그램은 <strong>자기만의 가상 메모리 공간</strong>을 가짐</li>
<li>서로의 메모리에 접근할 수 없음</li>
<li>운영체제의 메모리 영역도 보호됨 (커널 모드 전용)</li>
</ul>
<h2 id="6-📛-예외-처리와-페이지-폴트와-스왑">6) 📛 예외 처리와 페이지 폴트와 스왑</h2>
<h3 id="📍-페이지-폴트page-fault">📍 페이지 폴트(Page Fault)</h3>
<ul>
<li>프로그램이 <strong>존재하지 않는 가상 주소</strong>에 접근하면 발생하는 예외</li>
<li>OS는 이 예외를 받아 새 메모리 페이지를 할당하거나, 프로그램을 중단함</li>
</ul>
<h3 id="📌-활용-예시-스택-오버플로">📌 활용 예시: 스택 오버플로</h3>
<ul>
<li>스택이 범위를 초과하면 → 페이지 폴트 발생</li>
<li>OS가 <strong>스택을 위한 메모리를 확장</strong>해줄 수 있음 (동적 증가)</li>
</ul>
<h3 id="💿-스왑-아웃swap-out--스왑-인swap-in">💿 스왑 아웃(Swap Out) / 스왑 인(Swap In)</h3>
<p>운영체제는 물리 메모리가 꽉 찼을 때 이렇게 처리해요:</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a11cf4a4-ec05-45ae-83f7-e2a1f1e9ab3d/image.png" /></p>
<table>
<thead>
<tr>
<th>동작</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>💤 <strong>스왑 아웃</strong></td>
<td>사용하지 않는 페이지를 디스크로 옮김 (속도 느림)</td>
</tr>
<tr>
<td>⚡ <strong>스왑 인</strong></td>
<td>프로그램이 그 페이지를 다시 필요로 할 때, 디스크에서 다시 불러옴</td>
</tr>
</tbody></table>
<p>이 과정을 통해 <strong>물리 메모리가 실제보다 더 커 보이게</strong> 만들 수 있어요. 이것이 바로 <strong>가상 메모리의 핵심 마법</strong>입니다.</p>
<h3 id="🔁-동작-흐름-예시">🔁 동작 흐름 예시</h3>
<ol>
<li>프로그램이 <code>0x2000</code> 주소에 접근하려 함</li>
<li>해당 페이지가 물리 메모리에 없음 → <strong>페이지 폴트 발생</strong></li>
<li>OS는 필요 없는 다른 페이지를 <strong>스왑 아웃</strong>해서 공간 확보</li>
<li>디스크에서 <code>0x2000</code>이 포함된 페이지를 <strong>스왑 인</strong></li>
<li>MMU가 가상 주소 → 물리 주소 매핑 다시 설정</li>
<li>프로그램은 아무 일도 없었던 것처럼 실행 계속</li>
</ol>
<blockquote>
<p>요구불 페이징은 “필요한 메모리만 즉시 가져오고, 안 쓰는 메모리는 디스크로 보내는” 스마트한 가상 메모리 운영 방식입니다.</p>
</blockquote>
<p>이 과정을 '요구 페이징(Demand Paging)'이라고 합니다. OS는 페이지 접근 패턴을 추적해 어떤 페이지를 스왑할지 결정합니다. 대표적으로 LRU(Least Recently Used) 알고리즘이 사용됩니다.</p>
<blockquote>
<p>&quot;자주 쓰는 건 냉장고에, 덜 쓰는 건 창고에. 그런데 창고에서 꺼낼 땐 시간이 걸린다!&quot;</p>
</blockquote>
<h2 id="9-🔄-mmu-vs-인덱스-레지스터">9) 🔄 MMU vs 인덱스 레지스터</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>MMU</th>
<th>인덱스 레지스터</th>
</tr>
</thead>
<tbody><tr>
<td>기능</td>
<td>가상 → 물리 주소 변환</td>
<td>동적 주소 계산 (오프셋 계산용)</td>
</tr>
<tr>
<td>범위</td>
<td>모든 메모리</td>
<td>제한적 (일부 주소에만 적용)</td>
</tr>
<tr>
<td>보호 기능</td>
<td>있음 (보안, 권한 등)</td>
<td>없음</td>
</tr>
<tr>
<td>프로그램 분리</td>
<td>가능</td>
<td>불가능</td>
</tr>
</tbody></table>
<blockquote>
<p>MMU는 단순한 주소 계산기가 아니라, <strong>보안·안정성·다중 프로그램 실행의 핵심 장치</strong>입니다.</p>
</blockquote>
<h2 id="10-스와핑에-두-가지-의미">10) 스와핑에 두 가지 의미</h2>
<h3 id="1-교과서에서는-이렇게-말해요">1. 교과서에서는 이렇게 말해요</h3>
<blockquote>
<p><strong>&quot;메모리가 부족한 상황에서는 스와핑을 통해서라도 프로그램을 실행시키는 게 낫다.&quot;</strong></p>
</blockquote>
<ul>
<li>운영체제는 가상 메모리를 통해 <strong>메모리보다 많은 프로그램</strong>을 실행하게 도와줘요.</li>
<li>이때 <strong>물리 메모리가 부족하면 디스크에 데이터를 잠시 옮겨두는 스와핑</strong>을 사용합니다.</li>
<li>성능은 좀 떨어져도 <strong>시스템이 멈추지 않고 돌아가는 것</strong>이 더 중요하다고 보는 거예요.</li>
<li>그래서 OS는 LRU(Least Recently Used) 같은 <strong>페이지 교체 알고리즘</strong>을 써서 덜 쓰는 페이지부터 스왑 아웃해요.</li>
</ul>
<blockquote>
<p>요약: 성능보다 <strong>가용성(Availability)</strong>이 중요한 상황에서는 스와핑이 합리적이에요.</p>
</blockquote>
<h3 id="2-실무에서는-왜-다르게-말할까요">2. 실무에서는 왜 다르게 말할까요?</h3>
<blockquote>
<p><strong>&quot;Kafka 같은 고처리량 시스템에서는 (거의) 무조건 스와핑을 막아야 한다.&quot;</strong><br />– 카프카 핵심 가이드 p.40</p>
</blockquote>
<p>고성능 시스템에서는 상황이 완전히 달라요. 성능이 떨어지면 <strong>비즈니스 자체가 타격</strong>을 입을 수 있기 때문이에요.</p>
<h4 id="실무에서-스와핑이-문제-되는-이유">실무에서 스와핑이 문제 되는 이유</h4>
<table>
<thead>
<tr>
<th>이유</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>💥 성능 저하</td>
<td>스왑은 디스크 I/O를 유발해요. RAM보다 수천 배 느려요.</td>
</tr>
<tr>
<td>🌀 레이턴시 증가</td>
<td>Kafka, DB, 게임 서버처럼 실시간성이 중요한 시스템에선 치명적이에요.</td>
</tr>
<tr>
<td>🧠 예측 불가</td>
<td>커널이 어떤 페이지를 스왑할지 결정하기 때문에, 예측이 어려워요.</td>
</tr>
<tr>
<td>📉 처리량 감소</td>
<td>CPU는 한가한데 메모리 I/O 때문에 전체 속도가 늦춰져요.</td>
</tr>
</tbody></table>
<h3 id="3-✋-예를-들면-이런-상황이-생겨요">3. ✋ 예를 들면 이런 상황이 생겨요</h3>
<ul>
<li>Kafka의 <strong>Page Cache</strong>가 스왑되면 디스크 접근 속도가 심각하게 느려져요.</li>
<li>JVM 기반 시스템은 <strong>GC 타이밍</strong>이 중요한데, 스왑이 끼면 GC가 <strong>언제 작동할지 예측 불가</strong>해져요.</li>
</ul>
<h3 id="4-📌-그래서-실무에서는-이렇게-막아요">4. 📌 그래서 실무에서는 이렇게 막아요</h3>
<ul>
<li><p><code>vm.swappiness</code> 값을 <strong>10 이하</strong>로 줄이거나 아예 <strong>0으로 설정</strong></p>
<pre><code class="language-bash">sudo sysctl -w vm.swappiness=10</code></pre>
</li>
<li><p>Kafka, Elasticsearch, Redis 등은 <strong>스왑 비활성화가 권장</strong></p>
</li>
<li><p>컨테이너에서는 <code>--memory-swappiness=0</code> 옵션 사용</p>
</li>
</ul>
<h3 id="🧩-쉽게-비교하면">🧩 쉽게 비교하면?</h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>일반 PC (교과서 관점)</th>
<th>Kafka 같은 고성능 서버 (실무 관점)</th>
</tr>
</thead>
<tbody><tr>
<td>목표</td>
<td>실행 가능한 시스템 유지</td>
<td>지연 최소화, 처리량 극대화</td>
</tr>
<tr>
<td>스와핑 허용</td>
<td>허용 (필요악)</td>
<td>❌ 최대한 방지</td>
</tr>
<tr>
<td>페이지 교체</td>
<td>LRU 등 사용</td>
<td>스와핑 자체를 안 하도록 세팅</td>
</tr>
<tr>
<td>리소스 부족 시</td>
<td>느려져도 동작 유지</td>
<td>성능 저하는 SLA 위반으로 치명적</td>
</tr>
</tbody></table>
<h3 id="💡-한-줄-정리">💡 한 줄 정리</h3>
<blockquote>
<p><strong>교과서에서 말하는 스와핑은 ‘최후의 안전장치’지만, 실무에서는 ‘절대 피해야 할 성능 지옥’입니다.</strong></p>
</blockquote>
<h2 id="✅-마무리-요약">✅ 마무리 요약</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3f8fe5f7-af64-4830-bc37-c3beb84dab14/image.png" /></p>
<table>
<thead>
<tr>
<th>키워드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>MMU</td>
<td>가상 주소 ↔ 물리 주소 변환 하드웨어</td>
</tr>
<tr>
<td>페이지</td>
<td>일정 단위로 쪼갠 메모리 블록</td>
</tr>
<tr>
<td>페이지 테이블</td>
<td>가상 → 물리 주소 매핑 정보 저장 테이블</td>
</tr>
<tr>
<td>페이지 폴트</td>
<td>없는 가상 주소 접근 시 발생하는 예외</td>
</tr>
<tr>
<td>제어 비트</td>
<td>실행불가, 읽기전용 등 접근 권한 제어</td>
</tr>
<tr>
<td>프로그램 분리</td>
<td>가상 메모리 공간으로 서로 격리</td>
</tr>
</tbody></table>
<blockquote>
<p>&quot;현대 컴퓨터에서 MMU 없는 시스템은 상상할 수 없습니다.<br />프로그램이 안전하게, 그리고 서로 간섭 없이 실행될 수 있도록 돕는 조력자.<br />그게 바로 MMU입니다!&quot;</p>
</blockquote>
<blockquote>
<p>&quot;가상 메모리는 마치 각 가정이 자기 집 주소 체계를 쓰는 것처럼, 다른 집 주소와 겹치지 않게 만들어주는 장치입니다.&quot;</p>
</blockquote>