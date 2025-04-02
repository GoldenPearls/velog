<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/899e2654-fd0e-4590-8e23-049f47737362/image.png" /></p>
<h1 id="1-💡-컴퓨터-어떻게-똑똑해졌을까--계산기에서-멀티태스커로">1. 💡 컴퓨터, 어떻게 똑똑해졌을까? – 계산기에서 멀티태스커로</h1>
<h2 id="1-🧠-단순했던-컴퓨터-점점-복잡해진-설계">1) 🧠 단순했던 컴퓨터, 점점 복잡해진 설계</h2>
<p>4장까지는 CPU가 메모리와 I/O 장치와 어떻게 소통하는지 간단한 구조를 살펴봤어요.<br />하지만 현실 속 컴퓨터는 그렇게 단순하지 않아요. 빠르고, 효율적이며, 전력도 덜 먹고, 동시에 여러 프로그램을 실행해야 하죠.  </p>
<p>그래서 컴퓨터 설계는 점점 더 <strong>복잡한 기술과 구조</strong>를 요구하게 됐습니다.</p>
<p>컴퓨터가 단순히 계산만 하던 시절은 오래전에 지나갔습니다. 이제 컴퓨터는 우리가 사용하는 수많은 프로그램을 동시에 실행하고, 그 과정에서 메모리도 효율적으로 잘 배분합니다. </p>
<blockquote>
<p>그렇다면 이런 복잡한 기능들이 어떻게 가능한 걸까요?</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d97f6d2c-3003-4a83-8006-f230f72d8026/image.png" /></p>
<p>그 핵심에는 '컴퓨터 아키텍처'와 '운영체제'라는 두 주인공이 있습니다. 아키텍처는 하드웨어의 설계 철학, 운영체제는 그것을 효율적으로 사용하는 소프트웨어의 관리자입니다. 이 둘은 마치 <strong>대규모 주방의 설비(아키텍처)와 요리사장(운영체제)처럼 협력</strong>합니다.</p>
<h2 id="2-🏛️-컴퓨터-아키텍처는-설계도이지-양식이-아니다">2) 🏛️ 컴퓨터 아키텍처는 설계도이지 양식이 아니다</h2>
<p>'컴퓨터 아키텍처'는 마치 고대 건축 양식처럼 들릴 수 있지만, 실제로는 <strong>CPU, 메모리, I/O 등의 구성요소를 어떻게 배치할지</strong>에 대한 설계 철학입니다.  </p>
<blockquote>
<p>“도리스식이나 이오니아식 말고, 진짜 속 내용물 이야기!”</p>
</blockquote>
<p>성공적인 아키텍처도 있었고, 실험적으로 끝난 구조도 있었어요. 다양한 시도가 있었기에 지금의 컴퓨터가 존재하는 거죠.</p>
<h2 id="3-🧩-이번-장의-초점-메모리와-프로그램-실행">3) 🧩 이번 장의 초점: 메모리와 프로그램 실행</h2>
<p>5장은 <strong>메모리 구조와 실행 장치의 설계</strong>, 그리고 여러 프로그램을 동시에 실행하기 위한 <strong>멀티태스킹</strong>을 집중적으로 다룹니다.</p>
<ul>
<li>최신 CPU 안에서 가장 큰 영역은 ‘메모리 처리 회로’예요.</li>
<li>멀티코어, 전력 관리, 실행 최적화 장치 등도 함께 등장합니다.</li>
<li>동시에 여러 프로그램을 돌리려면 ‘운영체제’라는 관리자가 꼭 필요합니다.</li>
</ul>
<h3 id="✍️-한-줄-요약">✍️ 한 줄 요약!</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/34237671-bf70-4cc5-891b-9e24443ed2f5/image.png" /></p>
<blockquote>
<p>컴퓨터 아키텍처는 뼈대, 운영체제는 감독, 메모리는 전략의 핵심!  
우리가 프로그램을 ‘똑똑하게’ 실행할 수 있는 비결은 여기에 있어요.</p>
</blockquote>
<h1 id="2-🛣️-폰-노이만-vs-하버드-메모리-고속도로-전쟁">2. 🛣️ 폰 노이만 vs 하버드: 메모리 고속도로 전쟁</h1>
<h2 id="💡-두-개의-뇌-컴퓨터-구조의-선택지와-진화">💡 두 개의 뇌: 컴퓨터 구조의 선택지와 진화</h2>
<h3 id="1-📚-폰-노이만-vs-하버드-구조--한길을-갈-것인가-두-갈래로-나눌-것인가">1) 📚 폰 노이만 vs 하버드 구조 – &quot;한길을 갈 것인가, 두 갈래로 나눌 것인가&quot;</h3>
<p>컴퓨터 설계에는 두 가지 대표적인 길이 있어요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/dc66d2eb-2ac7-43c3-a302-980c2c998bd6/image.png" /></p>
<ul>
<li><strong>폰 노이만 구조</strong>는 명령어와 데이터를 <strong>같은 메모리</strong>에서 읽는 구조예요. 도로가 하나라서 데이터를 실어 나르거나 명령을 받을 때 <strong>줄을 서야 하는</strong> 상황이 발생하죠. 그래서 약간 느릴 수 있어요.</li>
<li><strong>하버드 구조</strong>는 명령어와 데이터가 <strong>각기 다른 메모리</strong>에 있어요. 명령도 가져오고, 데이터도 동시에 받을 수 있어서 더 <strong>빠르고 효율적</strong>이지만, 하드웨어 설계가 복잡해집니다. 두 번째 메모리를 처리하기 위한 버스가 더 필요해요</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/cdca263d-bd02-4386-a8dc-3d77d8715fc8/image.png" /></p>
<blockquote>
<p>📌 정리:  </p>
<ul>
<li><strong>폰 노이만</strong>: 단순하지만 느릴 수 있음  </li>
<li><strong>하버드</strong>: 복잡하지만 병렬성이 좋음  </li>
</ul>
</blockquote>
<p>이 두 구조의 유일한 차이는 메모리 배열뿐입니다.</p>
<h3 id="2-🧠-코어-이야기--하나의-뇌보다-여럿이-낫다">2) 🧠 코어 이야기 – 하나의 뇌보다 여럿이 낫다?</h3>
<p>처음엔 CPU 하나면 충분하다고 생각했어요. 위 사진의 두 구조 모두 cpu가 하나뿐이었죠. 하지만 성능의 한계에 부딪혔습니다. </p>
<p><strong>🔌 회로는 작아지는데, 발열은 커진다? 전력 장벽 이야기</strong></p>
<p>기술 발전으로 CPU 회로는 점점 더 작아지고 빨라졌습니다. 하지만 작아지면서 생긴 문제도 있죠. </p>
<blockquote>
<p>바로 <strong>전력 장벽(Power Wall)</strong> 때문이에요.</p>
</blockquote>
<ul>
<li>CPU 속도는 빨라졌지만, <strong>전력 소비와 발열</strong>도 같이 증가했어요.</li>
<li>회로를 작게 만들수록 열은 더 많이 나고, 결국 회로가 <strong>녹는 수준</strong>에 이를 수도 있었죠.</li>
</ul>
<p>속도는 빨라졌지만 그만큼 전력 소모와 발열이 커졌습니다. </p>
<blockquote>
<p>이를 해결하기 위해 우리는 하나의 CPU에 여러 개의 코어를 넣는 '멀티코어 프로세서'를 만들었습니다. </p>
</blockquote>
<p>이 코어들은 각자 다른 작업을 병렬로 처리할 수 있어서 효율이 훨씬 높아졌습니다.</p>
<ul>
<li>하나의 CPU 안에 여러 개의 <strong>코어(뇌)</strong>를 넣어, 병렬로 작업을 나눠 처리합니다.</li>
<li>이제 CPU는 &quot;단일한 두뇌&quot;가 아니라 &quot;작은 팀&quot;으로 움직여요!</li>
</ul>
<blockquote>
<p>그래서 요즘 CPU를 보면 'i5-1235U (10코어)' 같은 표현을 자주 보게 되죠.</p>
</blockquote>
<h3 id="3-멀티-코어-프로세스-멀티-코어가-뭘까">3) 멀티 코어 프로세스, 멀티 코어가 뭘까</h3>
<blockquote>
<p>출처 : <a href="https://imjeongwoo.tistory.com/152?category=943671">https://imjeongwoo.tistory.com/152?category=943671</a></p>
</blockquote>
<p><strong>멀티코어(Multi-core)</strong>
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/cbf43ef4-2dbe-483b-8e97-6171e3fdc5ae/image.png" /></p>
<ul>
<li>하나의 CPU 내부에 두 개 이상의 독립적인 core가 있는 기술.</li>
<li>하나의 core 처리하는 작업을 여러 개의  core가 분담하여 처리 가능.</li>
</ul>
<p><strong>멀티 프로세서</strong>
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9cbbd92c-80a5-4d93-89c5-554d7d31f903/image.png" /></p>
<ul>
<li>여러 개의 Processor(=CPU)를 사용하는 것.</li>
<li>여러 개의 CPU가 각각 독립적으로 작업을 처리.</li>
</ul>
<p><strong>멀티 코어 프로세서란?</strong>
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/230a7dfd-5100-4758-8910-5687d857fccd/image.png" /></p>
<p>멀티 코어 또는 멀티 코어 프로세서(multi-core processor) CPU는 두 개 이상의 독립 코어를 단일 집적 회로로 이루어진 하나의 패키지로 통합한 것을 말합니다.</p>
<ul>
<li>멀티코어 + 멀티프로세스 </li>
<li>하나의 CPU 내부에 두개 이상의 core가 있고, 이러한 멀티코어 CPU가 여러 개 존재.</li>
</ul>
<h3 id="4-🖥️-칩-하나에-우주가-마이크로컴퓨터와-soc">4) 🖥️ 칩 하나에 우주가! 마이크로컴퓨터와 SoC</h3>
<p>하드웨어의 구성 방식도 다양합니다. 여기서 혼동하기 쉬운 세 가지를 구분해볼게요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f77a4717-809b-42b3-b163-a928a1c9beb3/image.png" /></p>
<table>
<thead>
<tr>
<th>구분</th>
<th>구성 요소</th>
<th>특징</th>
</tr>
</thead>
<tbody><tr>
<td><strong>마이크로프로세서</strong></td>
<td>CPU만 있음</td>
<td>메모리, I/O는 외부에 따로</td>
</tr>
<tr>
<td><strong>마이크로컴퓨터</strong></td>
<td>CPU + 메모리 + I/O</td>
<td>하나의 칩에 통합, 아두이노 등이 예</td>
</tr>
<tr>
<td><strong>SoC (System on a Chip)</strong></td>
<td>마이크로컴퓨터 + WiFi, GPU 등</td>
<td>스마트폰에 들어가는 복잡한 컴퓨터 시스템</td>
</tr>
</tbody></table>
<ul>
<li>아두이노는 <strong>하버드 구조</strong>를 따르는 <strong>마이크로컴퓨터</strong>예요. 센서나 간단한 제어에 아주 유용하죠. 번쩍이는 장난감부터 센서 제어까지 다양하게 사용됩니다.</li>
<li>SoC는 말 그대로 <strong>칩 하나에 모든 걸 담은 작은 도시</strong>예요. 스마트폰, IoT 기기 등에 탑재됩니다.</li>
</ul>
<blockquote>
<p>🎯 요약하면,  </p>
<ul>
<li><strong>마이크로프로세서</strong>는 큰 시스템의 부품  </li>
<li><strong>마이크로컴퓨터</strong>는 작지만 독립적인 시스템  </li>
<li><strong>SoC</strong>는 고기능, 고집적, 멀티기능 칩!</li>
</ul>
</blockquote>
<h2 id="5-실제-사용-cpu">5) 실제 사용 cpu</h2>
<h3 id="✅-멀티코어-multi-core-cpu-예시">✅ <strong>멀티코어 (Multi-core) CPU 예시</strong></h3>
<blockquote>
<p>하나의 CPU(하나의 패키지) 내부에 여러 개의 <strong>코어</strong>가 있는 구조</p>
</blockquote>
<table>
<thead>
<tr>
<th>CPU 이름</th>
<th>코어 수</th>
<th>주요 용도</th>
<th>비고</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Intel Core i5-12400</strong></td>
<td>6코어 12스레드</td>
<td>일반 PC, 게임</td>
<td>P코어 6개</td>
</tr>
<tr>
<td><strong>AMD Ryzen 5 5600G</strong></td>
<td>6코어 12스레드</td>
<td>사무용, 내장그래픽 포함</td>
<td>멀티코어 설계</td>
</tr>
<tr>
<td><strong>Apple M1</strong></td>
<td>8코어 (4P+4E)</td>
<td>맥북, 맥미니</td>
<td>ARM 기반 SoC</td>
</tr>
<tr>
<td><strong>Snapdragon 8 Gen 2</strong></td>
<td>8코어 (1+4+3)</td>
<td>플래그십 스마트폰</td>
<td>고성능 모바일 칩</td>
</tr>
</tbody></table>
<blockquote>
<p>💡 대부분의 노트북, 데스크탑, 스마트폰에 들어있는 CPU들은 <strong>멀티코어</strong>입니다.</p>
</blockquote>
<h3 id="✅-멀티코어-프로세서-multi-core-processor-예시">✅ <strong>멀티코어 프로세서 (Multi-core Processor) 예시</strong></h3>
<blockquote>
<p><strong>여러 개의 코어</strong>를 가진 CPU가 <strong>여러 개</strong> 있는 구성<br />즉, <strong>멀티코어 + 멀티프로세서</strong> 조합입니다.</p>
</blockquote>
<table>
<thead>
<tr>
<th>시스템 구성 예시</th>
<th>사용 CPU</th>
<th>총 코어 수</th>
<th>사용 예</th>
</tr>
</thead>
<tbody><tr>
<td><strong>듀얼 Intel Xeon Silver 4310</strong></td>
<td>12코어 × 2</td>
<td>24코어</td>
<td>서버, 클러스터</td>
</tr>
<tr>
<td><strong>듀얼 AMD EPYC 7313</strong></td>
<td>16코어 × 2</td>
<td>32코어</td>
<td>가상화 서버</td>
</tr>
<tr>
<td><strong>Apple M2 Ultra</strong></td>
<td>24코어 단일 패키지</td>
<td>24코어 (16P+8E)</td>
<td>워크스테이션용 SoC</td>
</tr>
<tr>
<td><strong>GPU 병렬 처리 연산</strong></td>
<td>CUDA Core 수천 개</td>
<td>수천 스레드</td>
<td>병렬 과학 연산 (비유적 멀티코어)</td>
</tr>
</tbody></table>
<blockquote>
<p>💡 고성능 서버나 워크스테이션에서는 <strong>2개 이상의 멀티코어 CPU</strong>를 장착해 처리 능력을 높입니다.</p>
</blockquote>
<h3 id="멀티프로세서-시스템-multi-processor-system-예시"><strong>멀티프로세서 시스템 (Multi-processor System) 예시</strong></h3>
<blockquote>
<p>완전히 <strong>독립된 CPU(=Processor)</strong> 들이 하나의 시스템에 연결되어 있는 구조</p>
</blockquote>
<table>
<thead>
<tr>
<th>시스템 유형</th>
<th>사용 프로세서</th>
<th>특징</th>
</tr>
</thead>
<tbody><tr>
<td><strong>대형 서버 시스템 (예: IBM Power System)</strong></td>
<td>여러 개의 Power9 CPU</td>
<td>SMP 또는 NUMA 구조</td>
</tr>
<tr>
<td><strong>HPC(고성능 컴퓨팅) 클러스터</strong></td>
<td>각 노드에 별도 CPU</td>
<td>병렬 컴퓨팅, 분산 처리</td>
</tr>
<tr>
<td><strong>이중화 시스템 (Failover Server)</strong></td>
<td>두 CPU가 각각 실행</td>
<td>안정성, 백업 목적</td>
</tr>
<tr>
<td><strong>엔터프라이즈 메인프레임</strong></td>
<td>수십 개의 프로세서</td>
<td>금융, 통신 대형 시스템</td>
</tr>
</tbody></table>
<blockquote>
<p>💡 멀티프로세서는 <strong>하드웨어적으로 완전히 분리된 CPU</strong>를 여러 개 연결하는 구조예요. 성능보다 안정성과 병렬처리에 강점이 있죠.</p>
</blockquote>
<h3 id="🔍-정리-비교">🔍 정리 비교</h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>정의</th>
<th>예시</th>
</tr>
</thead>
<tbody><tr>
<td><strong>멀티코어</strong></td>
<td>하나의 CPU 안에 여러 코어</td>
<td>Intel i7, M1, Ryzen 등</td>
</tr>
<tr>
<td><strong>멀티코어 프로세서</strong></td>
<td>멀티코어 CPU 여러 개</td>
<td>듀얼 Xeon 서버 등</td>
</tr>
<tr>
<td><strong>멀티프로세서</strong></td>
<td>독립된 CPU 여러 개</td>
<td>HPC, 메인프레임</td>
</tr>
</tbody></table>
<h1 id="3-📦-프로그래머의-게으름이-낳은-발명-함수-프로시저-서브루틴-이야기">3. 📦 프로그래머의 게으름이 낳은 발명: 함수, 프로시저, 서브루틴 이야기</h1>
<h2 id="1-왜-함수가-생겼을까">1) 왜 함수가 생겼을까?</h2>
<p>프로그래머들은 종종 &quot;게으르다&quot;는 소리를 들어요. 근데 이건 사실 비하가 아니라 <strong>창의력의 원천</strong>이기도 해요.<br />똑같은 코드를 두 번 이상 쓰는 걸 진심으로 싫어하거든요.</p>
<blockquote>
<p>“왜 같은 코드를 또 쓰지? 한 번만 써놓고 다시 부르면 되잖아?”</p>
</blockquote>
<p>이런 생각에서 <strong>함수(function)</strong>라는 개념이 등장했어요.<br />어떤 작업을 미리 정해놓고, 필요할 때마다 그걸 &quot;호출&quot;해서 쓰는 방식이죠.</p>
<p>함수는 실제로 <strong>프로시저(procedure)</strong>, <strong>서브루틴(subroutine)</strong> 같은 이름으로도 불려요.<br />쓰는 언어나 맥락에 따라 다르지만, 우리가 생각하는 기능은 거의 같아요.</p>
<h3 id="함수를-프로시저나-서브루틴으로-부르는-이유는">함수를 프로시저나 서브루틴으로 부르는 이유는?</h3>
<h4 id="📌-함수-프로시저-서브루틴-왜-이름이-다를까">📌 함수, 프로시저, 서브루틴… 왜 이름이 다를까?</h4>
<table>
<thead>
<tr>
<th>용어</th>
<th>의미</th>
<th>왜 그렇게 불렸을까?</th>
</tr>
</thead>
<tbody><tr>
<td><strong>함수 (Function)</strong></td>
<td>어떤 값을 입력받아, 계산하고, 결과를 반환하는 코드 묶음</td>
<td>수학적 함수 개념에서 유래. 수학처럼 <strong>입력 → 출력</strong>이 있는 계산 단위</td>
</tr>
<tr>
<td><strong>프로시저 (Procedure)</strong></td>
<td>일련의 명령을 순서대로 실행하는 코드 묶음. 반환값이 <strong>없을 수도 있음</strong></td>
<td>&quot;절차적 절차(procedure)&quot;라는 뜻에서, 결과를 만들기보단 <strong>작업 흐름</strong> 자체에 초점</td>
</tr>
<tr>
<td><strong>서브루틴 (Subroutine)</strong></td>
<td>메인 루틴(메인 프로그램)에서 호출되는 작은 코드 블록</td>
<td>옛날 어셈블리 언어나 초기 언어에서 <strong>&quot;루틴의 하위 개념&quot;</strong>으로 사용. 기능적 분할을 위한 용어</td>
</tr>
</tbody></table>
<h4 id="💡-한마디로-요약하면">💡 한마디로 요약하면?</h4>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/02fad4fa-5f37-4f08-93d3-df06870aa938/image.png" /></p>
<ul>
<li><strong>Function</strong>은 <strong>&quot;값을 계산해서 돌려주는 느낌&quot;</strong></li>
<li><strong>Procedure</strong>는 <strong>&quot;작업을 순서대로 처리하는 절차&quot;</strong></li>
<li><strong>Subroutine</strong>은 <strong>&quot;메인 작업을 도와주는 작은 기능&quot;</strong></li>
</ul>
<p>서로 미묘하게 다른 느낌이 있지만, 현대의 많은 언어에서는 거의 <strong>동의어처럼 쓰이기도 해요</strong>.</p>
<p>예를 들어:</p>
<ul>
<li><strong>C 언어</strong>에서는 <code>void printHello()</code> 같은 반환값 없는 것도 함수라고 부르고</li>
<li><strong>Pascal</strong>에서는 반환값이 있으면 <strong>Function</strong>, 없으면 <strong>Procedure</strong></li>
<li><strong>어셈블리</strong>나 옛 언어에서는 서브루틴이란 말을 더 자주 썼죠</li>
</ul>
<h4 id="🎯-지금은-그냥-함수function라고-부르면-거의-다-통합니다">🎯 지금은 그냥 &quot;함수(Function)&quot;라고 부르면 거의 다 통합니다.</h4>
<p>하지만 이런 다양한 이름을 알고 있으면, <strong>옛 문서나 다른 언어</strong>를 읽을 때 도움이 돼요!</p>
<blockquote>
<p>&quot;다른 이름을 가졌지만, 결국 다 같은 '게으른 프로그래머의 친구'예요.&quot; 😄</p>
</blockquote>
<h2 id="2-함수의-모습--자바스크립트-예제로-보자">2) 함수의 모습 – 자바스크립트 예제로 보자</h2>
<p>예를 들어, 아래처럼 자바스크립트에서는 <code>cube(x)</code>라는 함수를 만들 수 있어요:</p>
<pre><code class="language-javascript">function cube(x) {
  return (x * x * x);
}</code></pre>
<p>이 함수는 간단하게 말해서, <strong>어떤 숫자를 받아서 세제곱한 값을 반환</strong>합니다.</p>
<p>그럼 실제로 함수를 호출해서 써볼까요?</p>
<pre><code class="language-javascript">y = cube(3);      // y에는 27이 저장됨
z = cube(4) + cube(6);  // z는 64 + 216 = 280</code></pre>
<p>함수 하나만 잘 정의해두면, 복붙 없이도 어디서든 쓸 수 있게 되는 거예요.</p>
<h2 id="3-근데-이게-어떻게-작동하는-걸까">3) 근데 이게 어떻게 작동하는 걸까?</h2>
<p>우리가 함수 <code>cube()</code>를 호출하면, 컴퓨터는 이런 식으로 생각합니다:
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f02b0253-6da0-4d8f-aa97-d675dcbc4f08/image.png" /></p>
<ol>
<li>&quot;좋아, 지금 작업은 잠깐 멈추고 cube 함수로 가자!&quot;</li>
<li>&quot;근데 나중에 어디서 돌아와야 하지? … 아, 현재 명령어 다음 주소를 기억하자!&quot;</li>
<li>&quot;cube 함수 실행 완료!&quot;</li>
<li>&quot;이제 저장해둔 그 주소로 돌아가서 다음 명령 실행하자!&quot;</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ac6b3c76-8dfb-4ba5-8ee9-519b7e2f8230/image.png" /></p>
<blockquote>
<p>즉, <strong>&quot;함수 호출 지점의 주소&quot;</strong>를 저장하고, 함수 실행이 끝나면 그 주소로 <strong>점프</strong>해서 돌아오는 거예요.</p>
</blockquote>
<h2 id="4-진짜-컴퓨터는-어떻게-기억하고-이동할까">4) 진짜 컴퓨터는 어떻게 기억하고 이동할까?</h2>
<p>이건 컴퓨터 내부 구조와 관련된 일이에요. 예전 기계에서는 이렇게 처리했어요:</p>
<h3 id="🧠-가상의-메모리-주소-예시-표-5-1-방식">🧠 가상의 메모리 주소 예시 (표 5-1 방식)</h3>
<table>
<thead>
<tr>
<th>주소</th>
<th>명령어</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>100</td>
<td>pca</td>
<td>프로그램 카운터를 누산기로 옮김</td>
</tr>
<tr>
<td>101</td>
<td>add 5</td>
<td>5를 더해서 반환 주소 계산 (105)</td>
</tr>
<tr>
<td>102</td>
<td>store 200</td>
<td>반환 주소를 메모리 200번지에 저장</td>
</tr>
<tr>
<td>103</td>
<td>load 3</td>
<td>세제곱할 값(x)을 누산기에</td>
</tr>
<tr>
<td>104</td>
<td>bra 300</td>
<td>cube 함수로 분기 (jump)</td>
</tr>
<tr>
<td>105</td>
<td>함수 끝나고 여기부터 계속 실행</td>
<td></td>
</tr>
</tbody></table>
<p>함수의 시작 주소는 300이고, 함수가 끝난 후엔 <code>bra 200 (간접)</code> 명령을 통해<br /><strong>200번지에 저장된 값(=105)</strong>으로 다시 분기하는 거예요.</p>
<p>즉,</p>
<ul>
<li>함수 <strong>호출 전에는 ‘돌아갈 주소’를 따로 저장</strong>해둬야 하고,</li>
<li><strong>함수 끝에는 ‘그 주소로 점프’</strong>해야 합니다.</li>
</ul>
<p>이런 점프 방식은 ‘간접 분기(indirect branch)’라고도 불러요.</p>
<h2 id="5-흐름을-도식으로-보면-이렇게">5) 흐름을 도식으로 보면 이렇게!</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6160531b-333c-492d-80fe-99a819141721/image.png" /></p>
<p>이게 바로 우리가 <code>cube(3)</code>을 호출했을 때 <strong>백그라운드에서 일어나는 일</strong>이에요.</p>
<h2 id="6-복잡하니까-명령어도-진화했어요">6) 복잡하니까, 명령어도 진화했어요!</h2>
<p>이렇게 함수 호출을 구현하려면 생각보다 <strong>명령어가 많이 필요</strong>해요.<br />그래서 CPU 설계자들은 &quot;이거 좀 자동으로 처리해주는 명령 없을까?&quot; 하고 고민했죠.</p>
<p>그 결과 나온 명령어가 바로:</p>
<blockquote>
<p>✅ <strong>ARM의 <code>BL (Branch with Link)</code></strong> 명령어</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2f603c56-055c-4d71-9170-768a6692fa75/image.png" /></p>
<ul>
<li><code>BL</code>은 함수로 점프하는 동시에 <strong>“돌아올 주소”를 링크 레지스터에 자동 저장</strong>해줘요.</li>
<li>함수에서 돌아올 땐, 링크 레지스터 값을 다시 프로그램 카운터에 넣으면 OK!</li>
</ul>
<p>이런 식으로 프로세서들은 점점 더 똑똑하게 진화해왔어요.</p>
<h2 id="📌-한눈에-요약하면">📌 한눈에 요약하면?</h2>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>함수 (Function)</td>
<td>코드 재사용 단위, 호출하고 반환</td>
</tr>
<tr>
<td>반환 주소 저장</td>
<td>함수 호출 직전에 현재 위치 저장</td>
</tr>
<tr>
<td>간접 분기</td>
<td>저장된 주소로 다시 이동</td>
</tr>
<tr>
<td>ARM의 <code>BL</code></td>
<td>분기 + 반환 주소 저장을 한 번에 처리하는 명령</td>
</tr>
<tr>
<td>장점</td>
<td>코드 재사용, 메모리 절약, 유지보수 용이</td>
</tr>
</tbody></table>
<h1 id="4-부가적인-이야기--🚀-arm-어떻게-세계를-정복했을까---m1">4. 부가적인 이야기 : 🚀 ARM, 어떻게 세계를 정복했을까? - M1</h1>
<blockquote>
<p>앞에 나온 것 같은데 기억이 안나... 이번주에 다시 정리해야겠다.</p>
</blockquote>
<h3 id="1-arm은-cpu를-직접-만들지-않는-cpu-회사">1) <strong>ARM은 CPU를 직접 만들지 않는 CPU 회사</strong></h3>
<p>ARM은 CPU를 직접 만들지 않아요. 대신, <strong>가볍고 효율적인 CPU 설계도</strong>를 만들어서 다른 반도체 회사들에게 <strong>라이선스(설계 사용권)</strong> 형태로 팔죠.</p>
<ul>
<li>회사 이름은 <strong>ARM (Advanced RISC Machine)</strong>  </li>
<li><strong>RISC란?</strong> Reduced Instruction Set Computer<br />→ 적은 수의 단순한 명령어로 효율을 높이는 구조!</li>
</ul>
<p>이런 단순하고 가벼운 설계는 <strong>전력 소모를 줄이면서도 빠른 연산</strong>이 가능하게 만들어줘요. 그래서 스마트폰, IoT 기기, 디지털카메라 등 <strong>저전력이 중요한 기기들</strong>에 딱이에요!</p>
<h3 id="2-arm의-탄생은-bbc-교육-방송에서부터">2) <strong>ARM의 탄생은 BBC 교육 방송에서부터</strong></h3>
<p>1980년대, 영국은 '국민에게 컴퓨터를 알리자!'라는 <strong>BBC 컴퓨터 리터러시 프로젝트</strong>를 시작해요.<br />BBC는 교육 방송에 쓸 컴퓨터를 만들어달라고 <strong>에이콘(Acorn) 컴퓨터사</strong>에 요청했죠.</p>
<p>그 결과 만들어진 게 바로 <strong>BBC 마이크로(BBC Micro)</strong>.  
당시로선 고성능이었고, 영국 교육 시장을 평정했어요!</p>
<p>하지만 에이콘은 더 강력한 CPU가 필요하다고 판단, 인텔에 협조를 요청했지만 거절당하고…</p>
<blockquote>
<p>결국 “그럼 우리가 만들자!” 하고 자체 CPU 개발에 뛰어듭니다.</p>
</blockquote>
<p>이렇게 탄생한 게 바로 <strong>ARM = Acorn RISC Machine</strong>이에요!</p>
<h3 id="3-arm의-첫-작품-arm2-→-인텔을-압도하다">3) <strong>ARM의 첫 작품: ARM2 → 인텔을 압도하다</strong></h3>
<ul>
<li><p>첫 ARM CPU인 <strong>ARM2 (1987)</strong> 는 단 2만 7천 개의 트랜지스터로 구성됐지만,<br />인텔의 80286보다 빠른 성능을 보여줘요!</p>
</li>
<li><p>이 기술력 덕분에 애플도 주목하게 되고,<br />에이콘은 ARM 부서를 분사시켜 지금의 <strong>ARM Holdings</strong>가 됩니다.</p>
</li>
</ul>
<h3 id="4-애플-닌텐도-스마트폰까지--arm의-확장">4) <strong>애플, 닌텐도, 스마트폰까지 – ARM의 확장</strong></h3>
<ul>
<li><strong>애플 뉴튼</strong>에 ARM CPU를 사용했고,  </li>
<li>이후 <strong>아이팟</strong>, <strong>닌텐도 DS</strong>, <strong>초대 아이폰</strong>까지 ARM이 들어가게 돼요!</li>
</ul>
<p>전력 소모가 적고, 발열도 낮으면서도 충분히 빠르기 때문에<br />모바일 기기에서는 ARM을 따라올 수 있는 아키텍처가 없었죠.</p>
<h3 id="5-arm-아키텍처-이제는-노트북mac도-접수">5) <strong>ARM 아키텍처, 이제는 노트북(Mac)도 접수!</strong></h3>
<blockquote>
<p>2020년, 애플이 발표한 <strong>M1 칩</strong>은 ARM 기반 CPU에요.</p>
</blockquote>
<ul>
<li><p>이전까지는 맥북에 인텔 CPU를 썼지만,<br />M1부터는 애플이 직접 설계한 <strong>ARM 기반 SoC</strong>를 사용!</p>
</li>
<li><p>저전력임에도 불구하고 성능이 엄청나서,<br />데스크탑 분야에서도 ARM이 경쟁력을 입증했어요.</p>
</li>
</ul>
<h3 id="🧠-요약-정리">🧠 요약 정리</h3>
<table>
<thead>
<tr>
<th>구분</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td>ARM이란?</td>
<td>저전력 RISC 기반 CPU 설계 회사 (직접 생산 X)</td>
</tr>
<tr>
<td>설계 철학</td>
<td>단순한 명령어 세트 → 빠르고 전력 효율 높음</td>
</tr>
<tr>
<td>시작은?</td>
<td>1980년대 영국, BBC 교육용 컴퓨터에서 탄생</td>
</tr>
<tr>
<td>유명 제품</td>
<td>애플 M1, 아이폰, 닌텐도 DS, 스마트폰 대부분</td>
</tr>
<tr>
<td>장점</td>
<td>전력 효율, 저발열, 모바일/IoT에 최적화</td>
</tr>
<tr>
<td>현재</td>
<td>노트북(Mac), 서버, 슈퍼컴퓨터까지 확장 중!</td>
</tr>
</tbody></table>
<hr />
<blockquote>
<p>“단순한 설계로, 세상을 바꾼 CPU”<br />이게 바로 ARM의 이야기입니다 😎</p>
</blockquote>
<h2 id="🎯-스택의-등장은-다음-이야기">🎯 스택의 등장은 다음 이야기!</h2>
<p>지금까지는 반환 주소를 ‘200번지’ 같은 고정된 곳에 저장했어요.<br />그런데 <strong>재귀 함수</strong>나 <strong>여러 개의 함수가 연달아 호출</strong>될 땐 어떻게 될까요?</p>
<p>이때 필요한 게 바로 <strong>&quot;스택(Stack)&quot;</strong>입니다.<br />다음 장에서는, 함수를 안전하게 반복 호출할 수 있게 해주는 스택과 LIFO 구조의 등장을 이야기해볼게요.</p>
<blockquote>
<p>함수 호출은 단순히 코드 분할이 아니라, <strong>주소 기억과 점프의 미학</strong>이었습니다.</p>
</blockquote>
<h1 id="5-🍜-스택과-재귀-함수의-마법--함수-호출의-진짜-원리">5. 🍜 스택과 재귀 함수의 마법 – 함수 호출의 진짜 원리</h1>
<h2 id="1-🧠-함수는-단순하지-않다-재귀의-세계">1) 🧠 함수는 단순하지 않다! (재귀의 세계)</h2>
<p>프로그래밍에서 함수는 단순히 계산만 하는 도구가 아니에요.<br />함수가 <strong>다른 함수를 호출</strong>하거나, 심지어 <strong>자기 자신을 다시 호출</strong>할 수도 있죠!  
이걸 <strong>재귀(recursion)</strong>라고 부릅니다.</p>
<blockquote>
<p>예: 이미지를 재귀적으로 쪼개는 <code>subdivide()</code> 함수</p>
</blockquote>
<pre><code class="language-pseudo">function subdivide(x, y, size):
  if size ≠ 1 and 색이 모두 같지 않다면:
    half = size / 2
    subdivide(x, y, half)         // 왼쪽 아래
    subdivide(x, y+half, half)    // 왼쪽 위
    subdivide(x+half, y+half, half) // 오른쪽 위
    subdivide(x+half, y, half)    // 오른쪽 아래
  else:
    색 정보 저장</code></pre>
<h2 id="2-🌳-재귀-함수와-쿼드트리--함수가-자기-자신을-부른다고">2) 🌳 재귀 함수와 쿼드트리 – 함수가 자기 자신을 부른다고?</h2>
<p>“함수가 자기 자신을 부르는 건 너무 위험한 거 아냐?”<br />아니요! 오히려 <strong>재귀(recursion)</strong>는 많은 분야에서 아주 유용하게 사용됩니다.</p>
<h4 id="예시-이미지를-압축하는-subdivide-함수">예시: 이미지를 압축하는 subdivide 함수</h4>
<pre><code class="language-pseudo">function subdivide(x, y, size):
  if size ≠ 1 and 색이 모두 같지 않다면:
    half = size / 2
    subdivide(x, y, half)         // 왼쪽 아래
    subdivide(x, y+half, half)    // 왼쪽 위
    subdivide(x+half, y+half, half) // 오른쪽 위
    subdivide(x+half, y, half)    // 오른쪽 아래
  else:
    색 정보 저장</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/41a66e24-37f6-4b95-b117-9a387d2f1a6e/image.png" /></p>
<p>subdivide 함수는 이미지를 네 등분하며 <strong>재귀적으로 분할</strong>해요.<br />모든 픽셀이 같은 색이 아니면 계속 쪼갭니다. </p>
<blockquote>
<p><strong>모든 색이 같을 때까지 나누는 방식</strong>이에요.</p>
</blockquote>
<p>이 구조는 <strong>쿼드트리(Quad Tree)</strong>라고 부르며, 트리 구조로 데이터를 표현해요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a7370a9d-e056-46c6-a664-851b9d78323d/image.png" /></p>
<p>각각의 블록이 나눌 필요가 없다면, 잎 노드(leaf node)로 남아요.</p>
<ul>
<li><p>나뭇가지처럼 뻗어나가는 구조</p>
</li>
<li><p>최종 결과는 <strong>40개의 조각</strong>만 저장하면 됨 </p>
</li>
<li><p>모든 색이 같지 않으면 → 4개의 하위 정사각형으로 분할</p>
</li>
<li><p>같은 색이면 더 이상 분할 X → 저장 공간 절약!</p>
</li>
</ul>
<blockquote>
<p>✅ 이 구조는 ‘압축’에도 유리해요. 64개의 픽셀을 40개만 저장해도 되니까요!</p>
</blockquote>
<h2 id="3-🔁-재귀는-어떻게-돌아올-위치를-기억할까">3) 🔁 재귀는 어떻게 돌아올 위치를 기억할까?</h2>
<p>함수를 호출하는 순간, 컴퓨터는 두 가지 일을 해야 해요:</p>
<ol>
<li><strong>함수로 점프</strong>해서 새로운 작업을 처리</li>
<li><strong>작업이 끝나면 원래 자리로 정확히 복귀</strong></li>
</ol>
<p>함수를 호출하면, 그 자리에서 <strong>어디로 다시 돌아와야 할지</strong>를 기억해야 해요.<br />이걸 <strong>“반환 주소”</strong>라고 해요.</p>
<p>그래서 <strong>프로그램 카운터(PC)</strong> 값, 즉 현재 위치를 어딘가에 저장해둡니다.<br />이게 바로 <strong>“반환 주소(Return Address)”</strong>예요.</p>
<p>예전에는 이 주소를 특정 메모리 위치(예: 200번지)에 저장했는데요,<br />만약 함수 안에서 또 다른 함수를 호출한다면…?</p>
<blockquote>
<p>😨 <strong>반환 주소가 덮어쓰기 되어버리겠죠!</strong></p>
</blockquote>
<p>이 반환 주소와 함수의 지역 변수들을 저장해 두는 공간이 '스택'입니다.</p>
<h2 id="4-🍽️-접시를-쌓는-방식--스택stack">4) 🍽️ 접시를 쌓는 방식 – <strong>스택(Stack)!</strong></h2>
<blockquote>
<p>✅ “접시처럼 위에 쌓고, 위에서부터 꺼낸다!”</p>
</blockquote>
<p>컴퓨터는 <strong>함수를 호출할 때마다 ‘스택’에 정보</strong>를 쌓습니다.<br />그리고 함수가 끝나면 <strong>가장 마지막에 쌓은 정보부터 꺼내서</strong> 실행을 이어가죠.</p>
<blockquote>
<p>이 방식은 <strong>LIFO 구조 (Last In, First Out)</strong><br />즉, &quot;나중에 넣은 게 먼저 나간다&quot;는 규칙을 따릅니다.</p>
</blockquote>
<h3 id="🔧-함수-호출-시-스택에는-어떤-정보가-쌓일까">🔧 함수 호출 시, 스택에는 어떤 정보가 쌓일까?</h3>
<p>함수를 호출할 때, 컴퓨터는 다음 정보를 <strong>스택 프레임(stack frame)</strong>이라는 단위로 저장해요:</p>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>반환 주소</strong></td>
<td>함수 실행이 끝난 뒤 돌아가야 할 코드 위치</td>
</tr>
<tr>
<td><strong>매개변수</strong></td>
<td>함수가 처리해야 할 입력 값들</td>
</tr>
<tr>
<td><strong>지역 변수</strong></td>
<td>함수 안에서만 사용되는 변수들</td>
</tr>
<tr>
<td><strong>상태 정보</strong></td>
<td>레지스터, 조건 코드 등 특정 하드웨어 상태</td>
</tr>
</tbody></table>
<p>이렇게 스택 프레임 하나가 <strong>함수 호출의 모든 맥락(Context)</strong>을 담고 있습니다.</p>
<h3 id="🔄-호출될-때마다-쌓이고-끝나면-빠진다">🔄 호출될 때마다 쌓이고, 끝나면 빠진다</h3>
<p>함수가 다른 함수를 호출하면?</p>
<ul>
<li>새로운 <strong>스택 프레임이 위에 또 쌓이고</strong></li>
<li>그 함수가 끝나면 <strong>스택에서 해당 프레임만 pop!</strong></li>
</ul>
<p>이렇게 하면 <strong>각 함수의 실행 상태가 서로 완전히 독립</strong>적으로 유지됩니다.<br />그래서 함수가 자기 자신을 호출하는 <strong>재귀(Recursion)</strong>도 가능한 거죠!</p>
<h3 id="🎯-왜-하필-스택-구조일까">🎯 왜 하필 ‘스택’ 구조일까?</h3>
<p>스택은 다음과 같은 이유로 함수 호출에 딱 맞아요:</p>
<ol>
<li><strong>복잡한 함수 호출 구조</strong>에서도 실행 흐름을 정확하게 복원할 수 있음  </li>
<li><strong>재귀 호출</strong>도 문제없이 처리 가능 (반환 주소가 계속 분리되어 저장되니까요)</li>
<li><strong>중첩된 함수 실행</strong>이 가능 (예: A → B → C 호출 후, C → B → A 복귀)</li>
</ol>
<blockquote>
<p>❗ 만약 반환 주소를 한 군데에만 저장하면?<br />→ A가 B를 호출하고 B가 C를 호출할 때,<br />마지막 C만 기억되고 A나 B로 <strong>돌아갈 수 없게 됩니다!</strong></p>
</blockquote>
<h3 id="🧠-하드웨어도-스택을-특별히-지원한다">🧠 하드웨어도 스택을 특별히 지원한다!</h3>
<p>스택이 너무 중요해서, 컴퓨터 아키텍처에는 다음과 같은 <strong>하드웨어 지원</strong>도 있어요:</p>
<ul>
<li><strong>스택 포인터(Stack Pointer) 레지스터</strong>:  
현재 스택의 꼭대기(Top)를 가리킴</li>
<li><strong>프레임 포인터(Frame Pointer)</strong>:  
현재 스택 프레임의 시작 위치</li>
<li><strong>스택 한계(limit) 레지스터</strong>:  
스택이 넘치는 걸 방지하는 안전장치</li>
</ul>
<p>이 덕분에 함수 호출과 반환은 <strong>빠르고 안정적으로 처리</strong>될 수 있어요.</p>
<h3 id="📦-스택을-사용하는-또-다른-예들">📦 스택을 사용하는 또 다른 예들</h3>
<ul>
<li><strong>인터럽트 처리</strong>: 외부 이벤트가 발생했을 때, 현재 작업을 스택에 저장</li>
<li><strong>예외 처리 (try/catch)</strong>: 예외 발생 시 호출 스택을 추적해 오류 위치를 찾아냄</li>
<li><strong>멀티스레딩</strong>: 각 스레드는 자신만의 스택 공간을 가짐 (독립적인 함수 실행을 위해)</li>
</ul>
<blockquote>
<p>“스택은 함수 호출의 은밀한 조력자입니다.<br />프로그램이 복잡해질수록, 스택은 더 바쁘게 움직이고 있어요!” 😎</p>
</blockquote>
<h2 id="5-🧠-함수-호출의-숨은-비밀--스택이-없다면-아무-것도-돌아가지-않는다">5) 🧠 함수 호출의 숨은 비밀 – 스택이 없다면 아무 것도 돌아가지 않는다!</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9dd841d3-091d-4f7d-b2d0-ab41acc98710/image.png" /></p>
<h3 id="✅-왜-스택이-필요할까">✅ 왜 스택이 필요할까?</h3>
<p>함수를 호출하면 컴퓨터는 그 함수 안에서 무엇을 해야 할지 여러 정보를 기억해야 합니다:</p>
<ol>
<li><strong>어디서 왔는지?</strong> → <strong>반환 주소</strong></li>
<li><strong>무엇을 처리해야 하는지?</strong> → <strong>인자(argument)</strong></li>
<li><strong>처리 중 필요한 변수는?</strong> → <strong>지역 변수(local variable)</strong></li>
</ol>
<p>이 모든 정보를 한 곳에 담아두지 않으면,<br />함수가 끝났을 때 <strong>원래 자리로 돌아갈 수 없고</strong>, <strong>처리 흐름도 엉망</strong>이 돼버립니다.</p>
<h3 id="🧱-각-호출마다-스택-프레임stack-frame이-생성된다">🧱 각 호출마다 ‘스택 프레임(Stack Frame)’이 생성된다</h3>
<blockquote>
<p>함수를 호출할 때마다 생기는 작은 저장 공간이 바로 <strong>스택 프레임</strong>입니다!</p>
</blockquote>
<p>스택 프레임에는 다음과 같은 정보들이 들어 있어요:</p>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>반환 주소</strong></td>
<td>함수 실행이 끝난 뒤 돌아갈 위치</td>
</tr>
<tr>
<td><strong>매개변수 (인자)</strong></td>
<td>호출 시 전달된 입력 값</td>
</tr>
<tr>
<td><strong>지역 변수</strong></td>
<td>함수 내에서만 사용하는 임시 값</td>
</tr>
<tr>
<td><strong>이전 스택 포인터</strong></td>
<td>함수 종료 후 스택 복구를 위한 포인터 저장</td>
</tr>
</tbody></table>
<p>이 프레임은 <strong>스택(Stack)</strong>이라는 자료구조에 <strong>위에서부터 쌓이고</strong>,  
함수가 끝나면 해당 프레임이 <strong>제거(pop)</strong>되며 실행이 이어져요.</p>
<h3 id="📌-스택이-없다면-이런-문제가-생겨요">📌 스택이 없다면 이런 문제가 생겨요!</h3>
<pre><code class="language-c">int add(int a, int b) {
    return a + b;
}

int doubleAdd(int x) {
    return add(x, x) + add(x, x);
}</code></pre>
<p>위 코드는 <code>add(x, x)</code>를 <strong>두 번 호출</strong>하죠.<br />스택이 없으면 <strong>두 번째 <code>add()</code> 호출 시 첫 번째 호출의 반환 주소와 변수들이 덮어쓰기</strong>되기 때문에<br />정상적인 결과를 기대할 수 없습니다.</p>
<blockquote>
<p>🧠 스택이 있기 때문에 두 호출의 정보가 <strong>서로 분리</strong>되어 안전하게 처리됩니다!</p>
</blockquote>
<h3 id="🔁-재귀-호출의-대표-사례-팩토리얼">🔁 재귀 호출의 대표 사례: 팩토리얼</h3>
<pre><code class="language-c">int factorial(int n) {
    if (n &lt;= 1) return 1;
    return n * factorial(n - 1);
}</code></pre>
<p>이 함수가 <code>factorial(5)</code>를 호출하면, 내부적으로 이런 호출이 연쇄적으로 일어나요:</p>
<pre><code>factorial(5)
 ↳ factorial(4)
   ↳ factorial(3)
     ↳ factorial(2)
       ↳ factorial(1)</code></pre><p>각 호출마다:</p>
<ul>
<li><code>n</code>의 값이 달라야 하고</li>
<li>각각 <strong>다른 반환 주소</strong>로 돌아가야 해요</li>
</ul>
<p>이 모든 걸 기억하는 공간이 <strong>스택</strong>이며,<br /><code>factorial(1)</code>이 종료되면 스택 프레임이 하나씩 <strong>pop</strong>되며<br /><code>n * factorial(n-1)</code>이 계산됩니다.</p>
<h3 id="🌟-요약하면">🌟 요약하면!</h3>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>스택(Stack)</strong></td>
<td>함수 호출 시 컨텍스트 정보를 저장하는 공간</td>
</tr>
<tr>
<td><strong>스택 프레임</strong></td>
<td>하나의 함수 호출에 대한 정보 묶음</td>
</tr>
<tr>
<td><strong>반환 주소</strong></td>
<td>어디로 돌아가야 할지 저장</td>
</tr>
<tr>
<td><strong>함수 인자, 지역 변수</strong></td>
<td>호출 시 필요한 데이터 저장</td>
</tr>
<tr>
<td><strong>재귀 호출</strong></td>
<td>스택이 있어야만 가능</td>
</tr>
<tr>
<td><strong>스택 오버플로</strong></td>
<td>너무 많은 호출 → 메모리 초과</td>
</tr>
</tbody></table>
<p>함수가 함수 안에서 또 다른 함수를 호출하는 구조(또는 자기 자신을 재귀 호출)는<br /><strong>각 호출마다 ‘고유한 반환 주소와 변수’를 기억해야</strong> 합니다.</p>
<blockquote>
<p>✅ 이 모든 것을 담는 저장소가 바로 <strong>스택(Stack)</strong>이에요!</p>
</blockquote>
<ul>
<li>반환 주소도</li>
<li>지역 변수도</li>
<li>함수 인자도</li>
</ul>
<p><strong>모두 스택에 저장됩니다.</strong> </p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7daf01cc-fce6-49ec-9987-5379ff3f29e8/image.png" /></p>
<p>→ 함수가 끝나면, 그에 해당하는 <strong>스택 프레임</strong>이 제거되고<br />→ 다시 원래 함수의 실행이 이어집니다.</p>
<blockquote>
<p>“스택은 함수가 호출되는 순간부터, 끝날 때까지의 모든 여정을 책임지는 <strong>비서 같은 존재</strong>입니다.”<br />🧠 함수를 이해하려면, 그 뒤에 있는 <strong>스택의 원리</strong>를 꼭 알아야 해요!</p>
</blockquote>
<h2 id="6-🌐-깊이-우선-탐색-vs-너비-우선-탐색">6) 🌐 깊이 우선 탐색 vs 너비 우선 탐색</h2>
<ul>
<li><p><strong>깊이 우선 탐색(DFS)</strong>:  
가능한 한 <strong>한 방향으로 깊이 들어가다가</strong>, 막히면 돌아오는 방식</p>
</li>
<li><p><strong>너비 우선 탐색(BFS)</strong>:  
<strong>수평적으로 옆으로 먼저 이동</strong>한 뒤, 아래로 내려가는 방식</p>
</li>
</ul>
<p>재귀 함수의 호출 방식은 <strong>DFS와 매우 유사</strong>합니다.<br />트리 구조를 순회할 때마다, <strong>깊게 파고들고, 돌아오는 과정</strong>에서 스택이 사용돼요!</p>
<h2 id="7-📦-스택의-위험--stack-overflow--underflow">7) 📦 스택의 위험 – Stack Overflow &amp; Underflow</h2>
<h3 id="⚠️-stack-overflow가-발생하는-이유">⚠️ Stack Overflow가 발생하는 이유</h3>
<p>재귀 호출이 너무 깊어지거나, 스택을 너무 많이 쓰면 어떻게 될까요?</p>
<blockquote>
<p>✅ <strong>스택 오버플로(Stack Overflow)</strong> 발생!  
→ 스택 메모리 영역을 초과하면서 프로그램이 강제 종료돼요.</p>
</blockquote>
<p>예:  </p>
<pre><code class="language-python">def infinite_rec():
    infinite_rec()

infinite_rec()  # 💥 StackOverflowError 발생!</code></pre>
<p>이건 마치 식당에서 <strong>접시가 천장까지 쌓여서 무너지는 상황</strong>과 같아요.</p>
<ul>
<li><p><strong>스택 오버플로(Stack Overflow)</strong><br />→ 스택 공간이 꽉 찼는데 또 push 하려 하면 발생! 😱<br />→ 재귀가 너무 깊으면 이 문제가 발생할 수 있어요.</p>
</li>
<li><p><strong>스택 언더플로(Stack Underflow)</strong><br />→ 비어있는 스택에서 pop 하려고 하면 발생! ❌</p>
</li>
</ul>
<blockquote>
<p>✅ 그래서 스택은 하드웨어에서도 엄청 중요하게 다뤄요.<br />MMU는 <strong>스택 한계(overflow)를 감지할 수 있는 장치</strong>도 갖고 있어요.</p>
</blockquote>
<h2 id="8-📏-중위--전위--후위-표기법과-스택-언어">8) 📏 중위 / 전위 / 후위 표기법과 스택 언어</h2>
<ul>
<li><strong>중위 표기법 (Infix)</strong>: 1 + 2  </li>
<li><strong>전위 표기법 (Prefix)</strong>: + 1 2  </li>
<li><strong>후위 표기법 (RPN)</strong>: 1 2 +</li>
</ul>
<blockquote>
<p>후위 표기법은 스택으로 쉽게 구현 가능해요!</p>
</blockquote>
<h4 id="예-1-2--3-4--×">예: 1 2 + 3 4 + ×</h4>
<p>→ 스택에 1, 2 push → + 연산<br />→ 스택에 3, 4 push → + 연산<br />→ 두 결과를 ×</p>
<p>이런 방식은 <strong>PostScript, Forth, RPN 계산기</strong> 등에서 사용됩니다.</p>
<h3 id="📌-한눈에-보는-요약표">📌 한눈에 보는 요약표</h3>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>재귀 함수</td>
<td>자기 자신을 호출하는 함수</td>
</tr>
<tr>
<td>subdivide</td>
<td>이미지를 쪼개서 압축하는 재귀 함수</td>
</tr>
<tr>
<td>쿼드트리</td>
<td>사분할 기반 트리 구조</td>
</tr>
<tr>
<td>깊이 우선 탐색</td>
<td>깊게 파고든 뒤 돌아오는 구조 (재귀와 비슷)</td>
</tr>
<tr>
<td>스택</td>
<td>함수 호출 시 반환 주소와 변수 저장</td>
</tr>
<tr>
<td>스택 프레임</td>
<td>스택에 저장되는 단위 (주소, 지역변수 등 포함)</td>
</tr>
<tr>
<td>스택 오버플로</td>
<td>스택이 가득 찼을 때 발생하는 오류</td>
</tr>
<tr>
<td>수식 표기법</td>
<td>중위 / 전위 / 후위 (RPN) 등 다양한 표현법</td>
</tr>
</tbody></table>
<blockquote>
<p>&quot;재귀 호출과 스택이 없다면, 함수는 단 한 번밖에 돌아갈 수 없을 거예요.&quot;<br />→ 컴퓨터는 기억하는 법도, 되돌아가는 법도 알고 있답니다!</p>
</blockquote>
<h1 id="6-🛎️-쿠키-굽는-중-초인종이-울리면--컴퓨터-인터럽트-시스템-완전-정복">6. 🛎️ 쿠키 굽는 중 초인종이 울리면? – 컴퓨터 인터럽트 시스템 완전 정복</h1>
<h2 id="1-🍪-쿠키-반죽하다가-생긴-문제-컴퓨터에도-벌어지는-일">1) 🍪 쿠키 반죽하다가 생긴 문제: 컴퓨터에도 벌어지는 일</h2>
<p>자, 상상해봅시다. 오늘은 집에 혼자 있는 날이고, 당신은 주방에서 맛있는 초콜릿 칩 쿠키를 만들고 있어요. 반죽기에서 버터를 녹이고, 설탕을 넣고, 재료를 하나하나 섞으며 레시피를 따라가죠. 그런데 이때…  </p>
<blockquote>
<p>🛎️ “딩동!”</p>
</blockquote>
<p>문 앞에서 누군가 초인종을 눌렀습니다. 중요한 소포일 수도 있고, 그냥 지나가던 세일즈맨일 수도 있어요. 그런데 문제는—쿠키 반죽 중간에 누가 왔는지 <strong>알 방법이 없다는 것</strong>입니다. 쿠키를 태우지 않으면서도 누가 왔는지 확인하려면 어떻게 해야 할까요?</p>
<p>바로 이 상황, <strong>컴퓨터에서도 그대로 일어납니다.</strong><br />컴퓨터는 &quot;한 번에 한 가지 작업&quot;을 순서대로 착실히 처리하지만, 갑자기 <strong>중요한 외부 이벤트(입력, 도착한 네트워크 패킷, 알람 등)</strong>가 발생할 수도 있죠.  </p>
<p>그럼 컴퓨터는 어떻게 초인종에 반응할까요?</p>
<blockquote>
<p>답은 바로 <strong>인터럽트(Interrupt)</strong> 시스템입니다.</p>
</blockquote>
<h2 id="2-📜-순서도-이야기-폴링polling과-그-한계">2) 📜 순서도 이야기: 폴링(polling)과 그 한계</h2>
<p>처음엔 이렇게 할 수 있습니다:</p>
<pre><code class="language-plaintext">쿠키 굽기 → 초인종이 울렸는지 확인 → 아니면 계속 → 또 확인 → 또 확인</code></pre>
<p>이런 방식은 실제로 존재해요. 이름하여 <strong>폴링(polling)</strong>. 컴퓨터가 일정 주기마다 <strong>외부 입력이 있는지 계속 검사</strong>하는 방식이죠. 초인종이 울렸는지 반복적으로 확인하는 거예요.</p>
<p>하지만 이 방식은 문제가 많아요:</p>
<ul>
<li>초인종이 안 울렸다면? 👉 확인하는 데 <strong>불필요한 시간 낭비</strong></li>
<li>초인종이 울렸지만 확인 전에 지나쳤다면? 👉 <strong>기회를 놓침</strong></li>
</ul>
<blockquote>
<p>👎 “계속 쳐다봐야 반응할 수 있는 시스템, 비효율적이죠.”</p>
</blockquote>
<p>그래서 더 똑똑한 시스템이 필요했습니다.</p>
<h2 id="3-🧠-컴퓨터의-똑똑한-반응--인터럽트-시스템의-등장">3) 🧠 컴퓨터의 똑똑한 반응 – 인터럽트 시스템의 등장</h2>
<p>이제 컴퓨터는 마치 초인종이 울릴 때만 반응하는 <strong>초인종 시스템</strong>을 갖게 됩니다.</p>
<p>이게 바로 <strong>인터럽트 시스템</strong>입니다.</p>
<ul>
<li><strong>Interrupt (인터럽트)</strong>: 현재 작업을 <strong>잠시 중단</strong>하고, 더 중요한 일에 <strong>즉시 반응</strong>할 수 있게 해주는 시스템</li>
<li>즉, 초인종이 울리면 쿠키 반죽을 <strong>잠깐 멈추고</strong> 문 앞을 확인한 뒤, <strong>다시 돌아오는 방식</strong></li>
</ul>
<h3 id="✔️-인터럽트가-필요한-이유">✔️ 인터럽트가 필요한 이유</h3>
<table>
<thead>
<tr>
<th>상황</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>키보드 입력</td>
<td>사용자가 키를 누르면 즉시 반응해야 함</td>
</tr>
<tr>
<td>타이머 알람</td>
<td>프로그램을 일정 시간 후 멈추거나 재시작해야 함</td>
</tr>
<tr>
<td>네트워크 수신</td>
<td>데이터가 도착했을 때 즉시 읽어야 함</td>
</tr>
<tr>
<td>예외 처리</td>
<td>오류 상황이 발생하면 즉시 중단하고 조치 필요</td>
</tr>
</tbody></table>
<h3 id="🔌인터럽트란">🔌인터럽트란?</h3>
<p>컴퓨터는 순서대로 명령어를 착실하게 실행합니다.<br />하지만 현실 세계는 예측 불가능하죠.</p>
<ul>
<li>키보드를 눌렀을 때</li>
<li>마우스를 클릭했을 때</li>
<li>타이머가 종료됐을 때</li>
<li>0으로 나누는 연산이 발생했을 때</li>
</ul>
<p>이런 상황에서 CPU는 현재 작업을 <strong>잠깐 멈추고</strong>,  
<strong>더 중요한 작업(초인종 응대 등)</strong>을 처리한 뒤,<br /><strong>다시 돌아와 원래 작업을 계속합니다.</strong></p>
<p>그 중심에 있는 것이 바로 <strong>인터럽트 시스템</strong>입니다.</p>
<h2 id="4-🏛️-인터럽트의-구성-요소-쿠키로-이해하는-컴퓨터-구조">4) 🏛️ 인터럽트의 구성 요소: 쿠키로 이해하는 컴퓨터 구조</h2>
<table>
<thead>
<tr>
<th>컴퓨터 구성 요소</th>
<th>쿠키 비유</th>
</tr>
</thead>
<tbody><tr>
<td>프로그램</td>
<td>쿠키 레시피</td>
</tr>
<tr>
<td>CPU</td>
<td>요리사</td>
</tr>
<tr>
<td>메모리</td>
<td>재료 창고</td>
</tr>
<tr>
<td>인터럽트 신호</td>
<td>초인종 벨</td>
</tr>
<tr>
<td>인터럽트 핸들러</td>
<td>문 열고 응대하는 행동</td>
</tr>
</tbody></table>
<blockquote>
<p>요즘 쓰이는 프로세서 대부분은 인터럽트 시스템이 들어갑니다.</p>
</blockquote>
<p><code>인터럽트 시스템</code>은 <strong>적절한 신호가 들어오면 CPU 실행을 잠깐 중단시킬 수 있는 핀이나 전기 연결을 포함</strong>한다. 핀pin은 칩에 연결된 전기적 접점을 뜻하는 말이다. </p>
<p>칩에는 핀처럼 보이는 부품이 있는 경우가 많았지만, 장치 크기가 줄어듦에 따라 다른 방식도 쓰이기 시작했다. 많은 프로세서 칩(특히 마이크로컴퓨터)에는 통합 주변장치가 들어 있고(이런 장치를 온칩on-chip I/O 장치라고도 한다), </p>
<p>이런 장치들은 내부적으로 인터럽트 시스템에 연결되어 있다.</p>
<h2 id="5-⚙️-인터럽트의-작동-흐름">5) ⚙️ 인터럽트의 작동 흐름</h2>
<p>자, 인터럽트가 어떻게 작동하는지 실제 컴퓨터 관점에서 살펴볼까요?</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a7c87921-6b3b-4334-8a35-effed361fbad/image.png" /></p>
<h3 id="1단계-인터럽트-발생">1단계: 인터럽트 발생</h3>
<ul>
<li>키보드, 네트워크, 타이머 등에서 <strong>&quot;지금 봐야 해!&quot;</strong>라는 신호가 도착</li>
</ul>
<h3 id="2단계-현재-cpu-상태-저장---직압-장ㄹ">2단계: 현재 CPU 상태 저장 - 직압 장ㄹ;</h3>
<ul>
<li>CPU는 지금 진행하던 작업을 잠깐 <strong>멈추고</strong></li>
<li><strong>프로그램 카운터(PC)</strong> 값과 <strong>레지스터 상태</strong>를 <strong>스택에 저장</strong>함</li>
<li>PC(Program Counter)  </li>
<li>레지스터 값  </li>
<li>실행 중인 코드의 정보 (→ PCB 또는 스택에 저장)</li>
</ul>
<h3 id="3단계-인터럽트-핸들러-실행">3단계: 인터럽트 핸들러 실행</h3>
<ul>
<li>미리 정해진 <strong>인터럽트 벡터</strong>를 따라</li>
<li><strong>해당 인터럽트 핸들러 함수</strong>로 점프</li>
<li>핸들러가 그 상황을 <strong>처리</strong></li>
</ul>
<h3 id="4단계-원래-작업-복귀">4단계: 원래 작업 복귀</h3>
<ul>
<li>스택에 저장해둔 <strong>PC와 레지스터 정보 복구</strong></li>
<li>중단한 지점부터 다시 프로그램 실행 재개!</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ca8af3dc-a484-4f68-8384-f8376532ac10/image.png" /></p>
<blockquote>
<p>✅ 즉, <strong>인터럽트는 함수 호출과 유사하지만</strong>, 외부 이벤트가 발생해야 작동해요.</p>
</blockquote>
<h2 id="6-🧰-인터럽트의-내부-구성-어떤-구조로-되어-있나">6) 🧰 인터럽트의 내부 구성: 어떤 구조로 되어 있나?</h2>
<h3 id="🔸-인터럽트-벡터-테이블-interrupt-vector-table-ivt">🔸 인터럽트 벡터 테이블 (Interrupt Vector Table, IVT)</h3>
<ul>
<li>인터럽트가 발생하면, CPU는 <strong>어디로 점프할지</strong> 알아야 하죠?</li>
<li>각 인터럽트에 해당하는 <strong>핸들러 주소</strong>가 저장된 테이블입니다.</li>
<li><strong>0x0000~0x00FF</strong> 같은 고정된 메모리 주소에 위치하는 경우가 많아요.</li>
</ul>
<table>
<thead>
<tr>
<th>인터럽트 번호</th>
<th>의미</th>
<th>핸들러 주소</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>나눗셈 오류</td>
<td>0x0010</td>
</tr>
<tr>
<td>1</td>
<td>키보드 입력</td>
<td>0x0020</td>
</tr>
<tr>
<td>2</td>
<td>타이머 알림</td>
<td>0x0030</td>
</tr>
<tr>
<td>3</td>
<td>외부 장치 신호</td>
<td>0x0040</td>
</tr>
</tbody></table>
<h3 id="인터럽트-구성-요소">인터럽트 구성 요소</h3>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>인터럽트 라인</td>
<td>하드웨어 신호선 (CPU로 요청 전달)</td>
</tr>
<tr>
<td>인터럽트 벡터</td>
<td>인터럽트 종류별 처리 루틴의 주소 테이블</td>
</tr>
<tr>
<td>인터럽트 핸들러</td>
<td>실제 인터럽트를 처리하는 함수</td>
</tr>
<tr>
<td>PCB / 스택</td>
<td>작업 상태 저장소 (복귀를 위해 필수!)</td>
</tr>
</tbody></table>
<h2 id="7-📦-인터럽트는-스택을-활용한다">7) 📦 인터럽트는 스택을 활용한다</h2>
<p>인터럽트도 결국은 일종의 <strong>함수 호출</strong>입니다.<br />그래서 컴퓨터는 인터럽트를 처리할 때 <strong>현재 상태를 스택에 저장</strong>합니다.</p>
<ul>
<li>PC 값 (어디까지 실행했는지)</li>
<li>주요 레지스터 (중간 계산값들)</li>
<li>인터럽트 핸들러에서 사용하는 지역 변수</li>
</ul>
<p>이 모든 걸 저장한 뒤, 작업이 끝나면 <strong>스택에서 pop</strong>해서 원래대로 돌아옵니다.</p>
<blockquote>
<p>📌 그래서 스택이 없다면 함수 호출도, 인터럽트도 제대로 작동할 수 없어요!</p>
</blockquote>
<h2 id="8-⏱️-인터럽트의-핵심-이슈--응답-시간과-복귀">8) ⏱️ 인터럽트의 핵심 이슈 – 응답 시간과 복귀</h2>
<h3 id="1-반응-시간-response-time">1. 반응 시간 (Response Time)</h3>
<ul>
<li>인터럽트가 발생했을 때, 얼마나 빨리 반응할 수 있느냐?</li>
<li>너무 느리면? → 쿠키는 타버리고, 데이터는 사라져요.</li>
</ul>
<h3 id="2-상태-복귀-state-restoration">2. 상태 복귀 (State Restoration)</h3>
<ul>
<li>인터럽트가 끝난 뒤, 원래 프로그램이 <strong>정확히 이어서</strong> 돌아가야 해요.</li>
<li>실행 중인 레지스터 값, 프로그램 흐름 등 <strong>모든 걸 복구</strong>해야 함</li>
</ul>
<h2 id="9-🔀-인터럽트에도-우선순위가-있다">9) 🔀 인터럽트에도 우선순위가 있다</h2>
<p>모든 인터럽트가 <strong>동등하게 중요한 건 아니에요.</strong></p>
<p>예를 들어,</p>
<ul>
<li>초인종보다 <strong>화재 경보기</strong>가 더 중요하겠죠?</li>
</ul>
<p>그래서 컴퓨터는 각 인터럽트에 대해 <strong>우선순위(priority)</strong>를 설정합니다.</p>
<ul>
<li>우선순위가 더 높은 인터럽트가 발생하면, <strong>낮은 인터럽트 핸들러도 중단</strong>되고 새로운 핸들러로 진입할 수 있어요. (Nested Interrupts)</li>
</ul>
<h2 id="10-🛡️-인터럽트를-잠시-막는-기술--마스킹masking">10) 🛡️ 인터럽트를 잠시 막는 기술 – 마스킹(Masking)</h2>
<p>일부 상황에서는 인터럽트를 아예 <strong>무시하거나 차단</strong>할 필요도 있어요.</p>
<ul>
<li>예: 데이터를 복사하는 아주 민감한 시점엔 방해받고 싶지 않음</li>
<li>이럴 때는 <strong>인터럽트 마스크</strong>를 설정해 특정 인터럽트를 <strong>비활성화</strong>할 수 있어요.</li>
</ul>
<blockquote>
<p>&quot;지금 바쁘니 초인종 소리 무시해주세요&quot; – 이 느낌입니다.</p>
</blockquote>
<h2 id="11-🔥-예외-처리도-인터럽트다">11) 🔥 예외 처리도 인터럽트다?</h2>
<p>인터럽트는 꼭 외부에서만 발생하지 않아요. 컴퓨터 내부에서도 <strong>예외(Exception)</strong>라는 형태로 발생할 수 있어요.</p>
<table>
<thead>
<tr>
<th>예외 상황</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>0으로 나누기</td>
<td>수학적 오류</td>
</tr>
<tr>
<td>메모리 초과</td>
<td>스택 오버플로</td>
</tr>
<tr>
<td>접근 금지</td>
<td>보호된 영역 침범</td>
</tr>
</tbody></table>
<p>이때도 인터럽트 벡터를 따라 <strong>예외 핸들러</strong>로 점프하여 문제를 처리합니다.<br />예외 상황에 대한 복구, 로깅, 사용자 메시지 출력 등이 이때 실행되죠.</p>
<h2 id="12-🎛️-인터럽트를-만드는-주체들">12) 🎛️ 인터럽트를 만드는 주체들</h2>
<p>인터럽트는 다음과 같은 장치나 요소들에 의해 생성될 수 있어요.</p>
<table>
<thead>
<tr>
<th>발생 주체</th>
<th>예시</th>
</tr>
</thead>
<tbody><tr>
<td>하드웨어</td>
<td>키보드, 마우스, 네트워크, 타이머</td>
</tr>
<tr>
<td>소프트웨어</td>
<td>시스템 콜, 유닉스 시그널, 소프트웨어 인터럽트</td>
</tr>
<tr>
<td>내부 이벤트</td>
<td>예외, 디버깅, 불법 명령 실행 등</td>
</tr>
</tbody></table>
<h2 id="13-🧵-운영체제와-인터럽트-멀티태스킹의-기반">13) 🧵 운영체제와 인터럽트: 멀티태스킹의 기반</h2>
<p>운영체제는 인터럽트를 <strong>멀티태스킹</strong>의 기반으로 사용해요.</p>
<ul>
<li>일정 시간마다 <strong>타이머 인터럽트</strong>가 발생하면</li>
<li>현재 실행 중인 프로그램을 <strong>중단</strong></li>
<li><strong>문맥 교환(Context Switch)</strong>를 수행</li>
<li>다음 프로그램으로 전환!</li>
</ul>
<p>즉, 여러분이 윈도우에서 크롬과 카카오톡을 동시에 실행할 수 있는 건 <strong>인터럽트 시스템 덕분</strong>이에요.</p>
<h2 id="14-📱-현실의-예시--인터럽트는-여기저기서-쓰인다">14) 📱 현실의 예시 – 인터럽트는 여기저기서 쓰인다</h2>
<ul>
<li>📷 카메라 앱: 버튼 누르자마자 반응</li>
<li>🧠 IoT 기기: 센서 값 변화 즉시 처리</li>
<li>🕹️ 게임: 키 입력이나 충돌 이벤트 감지</li>
<li>🖥️ 서버: 클라이언트 요청 도착 시 즉시 대응</li>
</ul>
<h2 id="⚙️-15-인터럽트의-종류">⚙️ 15) 인터럽트의 종류</h2>
<h3 id="✅-하드웨어-인터럽트">✅ 하드웨어 인터럽트</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e84e7bf4-d442-4d1a-8b00-4c204399ac2f/image.png" /></p>
<ul>
<li>외부 장치(키보드, 마우스, 타이머, 네트워크 등)가 요청</li>
<li>CPU가 외부의 신호에 반응</li>
</ul>
<h3 id="✅-소프트웨어-인터럽트-trap">✅ 소프트웨어 인터럽트 (Trap)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/33be2730-e8df-419d-9f48-83c7ad3ab9e7/image.png" /></p>
<ul>
<li>프로그램 내부에서 발생<ul>
<li>예외(Exception): 0으로 나누기, 잘못된 메모리 접근 등</li>
<li>시스템 콜(System Call): 사용자 → OS 요청</li>
</ul>
</li>
</ul>
<blockquote>
<p>📌 Trap도 인터럽트다! 단지 “소프트웨어가 발생”시켰다는 점만 다름.</p>
</blockquote>
<blockquote>
<p>출처 : <a href="https://velog.io/@woo00oo/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8Interrupt">https://velog.io/@woo00oo/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8Interrupt</a></p>
</blockquote>
<h2 id="15-🧠-한-장으로-보는-인터럽트-요약">15) 🧠 한 장으로 보는 인터럽트 요약</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>인터럽트</td>
<td>외부 이벤트에 대응하기 위해 프로그램 실행을 잠시 멈추는 메커니즘</td>
</tr>
<tr>
<td>핸들러</td>
<td>인터럽트 발생 시 실행되는 특별한 함수</td>
</tr>
<tr>
<td>스택</td>
<td>현재 상태를 저장하고 복구하는 데 사용</td>
</tr>
<tr>
<td>벡터 테이블</td>
<td>각 인터럽트 번호에 대한 핸들러 주소를 저장</td>
</tr>
<tr>
<td>우선순위</td>
<td>더 중요한 인터럽트를 먼저 처리 가능</td>
</tr>
<tr>
<td>마스킹</td>
<td>특정 인터럽트를 잠시 비활성화 가능</td>
</tr>
<tr>
<td>예외</td>
<td>내부 오류도 인터럽트처럼 처리</td>
</tr>
<tr>
<td>응답 시간</td>
<td>빠른 반응이 중요! (실시간 시스템에서 핵심)</td>
</tr>
</tbody></table>
<h2 id="🧁-마무리--쿠키를-태우지-않으려면">🧁 마무리 – 쿠키를 태우지 않으려면?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/195d7211-be51-4b51-9215-828d48fec4c4/image.png" /></p>
<p>쿠키 반죽을 하면서도 초인종에 반응할 수 있는 방법.<br />그게 바로 컴퓨터의 <strong>인터럽트 시스템</strong>입니다.</p>
<p>이 시스템 덕분에 우리는:</p>
<ul>
<li>여러 프로그램을 동시에 돌릴 수 있고</li>
<li>사용자 입력에 즉시 반응하고</li>
<li>갑작스러운 상황에도 적절히 대응할 수 있어요.</li>
</ul>
<blockquote>
<p>“컴퓨터가 똑똑한 이유?<br />쿠키를 태우지 않고, 소포도 놓치지 않는 인터럽트 시스템 덕분이에요!”</p>
</blockquote>
<h1 id="7-⏱️-cpu는-어떻게-시간을-나눌까--시분할과-주소-지정">7. ⏱️ CPU는 어떻게 시간을 나눌까? – 시분할과 주소 지정</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ef5c7237-e208-4d1a-93cc-555b9500f8d0/image.png" /></p>
<h2 id="1-🎬-멀티태스킹은-어떻게-가능한가요">1) 🎬 멀티태스킹은 어떻게 가능한가요?</h2>
<p>우리는 평소에 컴퓨터에서 여러 프로그램을 동시에 실행합니다.<br />하지만 CPU는 <strong>한 번에 하나의 명령어만 처리</strong>할 수 있어요.</p>
<blockquote>
<p>그렇다면, 어떻게 유튜브와 카카오톡을 동시에 실행할 수 있을까요?</p>
</blockquote>
<p>✅ 해답은 바로 <strong>운영체제(OS)</strong>가  </p>
<ul>
<li><strong>시간(Time)을 쪼개고 ⏱️</strong>  </li>
<li><strong>공간(Memory)을 나눠서 🧱</strong><br />각 프로그램에 조금씩 번갈아가며 CPU를 할당하는 데 있습니다.</li>
</ul>
<h2 id="2-🧠-운영체제의-역할-프로그램들의-관리자">2) 🧠 운영체제의 역할: 프로그램들의 관리자</h2>
<p>운영체제는 컴퓨터 자원을 관리하는 <strong>시스템 프로그램</strong>입니다.</p>
<p>관리자 프로그램을 <strong>운영체제 또는 운영체제 커널</strong>이라고 하고  OS와 OS가 관리하는 프로그램을 구분하기 위해 OS를 시스템 프로그램이라고 부르고 <strong>다른 모든 프로그램을 사용자 프로그램이나 프로세스</strong>라고 부릅니다. </p>
<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>운영체제(OS)</td>
<td>시스템 자원을 총괄 관리하는 관리자</td>
</tr>
<tr>
<td>커널(Kernel)</td>
<td>운영체제의 핵심 기능 집합</td>
</tr>
<tr>
<td>사용자 프로그램</td>
<td>일반 사용자가 실행하는 앱</td>
</tr>
<tr>
<td>프로세스(Process)</td>
<td>실행 중인 사용자 프로그램</td>
</tr>
</tbody></table>
<blockquote>
<p>운영체제는 <strong>CPU, 메모리, 저장장치, 입출력 장치</strong> 등을 관리하며<br />여러 프로그램이 동시에 돌아가는 환경을 만들어줍니다.</p>
</blockquote>
<blockquote>
<p><a href="https://velog.io/@prettylee620/%EB%A6%AC%EB%88%85%EC%8A%A4-%EA%B0%9C%EC%9A%94-%EC%BB%A4%EB%84%90%EC%9D%B4-%EB%AD%90%EC%97%90%EC%9A%94-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%B4">커널 관련 정리 : 리눅스 개요 : 커널이 뭐에요? 왜 필요해?</a></p>
</blockquote>
<h2 id="3-⏲️-시간-분할-시분할-스케줄링time-slicing">3) ⏲️ 시간 분할: 시분할 스케줄링(Time Slicing)</h2>
<p>운영체제는 <strong>타이머 인터럽트</strong>를 통해<br />각 프로그램이 얼마나 CPU를 썼는지 파악하고,<br /><strong>일정 시간이 지나면 다른 프로그램으로 전환</strong>시킵니다.</p>
<table>
<thead>
<tr>
<th>시분할 스케줄링 흐름</th>
</tr>
</thead>
<tbody><tr>
<td>A 프로그램 실행 시작</td>
</tr>
<tr>
<td>→ 타이머 인터럽트 발생</td>
</tr>
<tr>
<td>→ A 상태 저장</td>
</tr>
<tr>
<td>→ B 프로그램 실행</td>
</tr>
<tr>
<td>→ 다시 타이머 인터럽트</td>
</tr>
<tr>
<td>→ B 상태 저장</td>
</tr>
<tr>
<td>→ A 복귀</td>
</tr>
</tbody></table>
<blockquote>
<p>⏳ 사용자 프로그램의 실행 시간을 조절하는 스케줄링scheduling 기법을 이를 &quot;시분할(Time Slicing)&quot;이라 부르며,<br />컴퓨터는 마치 빠른 줄넘기 교대처럼 프로그램을 번갈아 실행합니다.</p>
</blockquote>
<h2 id="4-📦-상태-저장과-문맥-교환context-switch">4) 📦 상태 저장과 문맥 교환(Context Switch)</h2>
<p>각 프로그램의 <strong>현재 상태</strong>를 저장하고 복원하는 과정이 필요합니다.<br />이걸 <strong>문맥(Context)</strong>이라고 부르고, 교환 과정은 <strong>문맥 교환(Context Switch)</strong>이라 해요.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/73728c39-2538-4dfb-97f6-715999619fa2/image.png" /></p>
<blockquote>
<p>✅ 문맥 교환은 <strong>시간이 드는 작업</strong>이지만, 멀티태스킹의 핵심입니다!</p>
</blockquote>
<h2 id="5-🏠-공간-분할-여러-프로그램을-메모리에-올리는-방법">5) 🏠 공간 분할: 여러 프로그램을 메모리에 올리는 방법</h2>
<p>운영체제는 메모리를 아래처럼 나눠서 프로그램을 올립니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6cb6547d-400e-42a5-a2f1-8716e479901f/image.png" /></p>
<p>사용자 프로그램은 하나씩 차례로 메모리에 올라갑니다.</p>
<blockquote>
<p>하지만 이때 <strong>절대 주소 방식</strong>으로 작성된 프로그램은 문제가 생길 수 있어요.  </p>
</blockquote>
<p>우리가 예로 든 컴퓨터는 절대 주소 지정absolute addressing을 사용했어요. <code>절대 주소 지정</code>은 <strong>명령어 주소가 특정 메모리 주소를 가리킨다는 뜻</strong>입니다.</p>
<p>예를 들어, 1000번지에서 실행되도록 만든 프로그램을 2000번지에 올리면… 오류 발생!</p>
<h2 id="6-🧭-주소-문제-해결법-인덱스-레지스터와-상대-주소-지정">6) 🧭 주소 문제 해결법: 인덱스 레지스터와 상대 주소 지정</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/804f25a2-a99f-4feb-9c27-cbf677e64aab/image.png" /></p>
<h3 id="1-인덱스-레지스터-index-register">(1) 인덱스 레지스터 (Index Register)</h3>
<blockquote>
<p>컴퓨터 CPU 의 인덱스 레지스터 는 <strong>프로그램 실행 중 피연산자 주소를 가리키는 데 사용되는 프로세서 레지스터 (또는 할당된 메모리 위치)</strong> 입니다. </p>
</blockquote>
<p>문자열 과 배열을 단계별로 실행하는 데 유용합니다. 루프 반복 및 카운터를 보관하는 데에도 사용할 수 있습니다.</p>
<p><strong>절대 주소 지정 문제의 해결법</strong>으로 나타났어요!!</p>
<ul>
<li>컴퓨터는 명령어에 ‘직접 주소’를 넣지 않고, 간접적으로 계산해서 <strong>유효 주소(Effective Address)</strong>를 만들어내는 방식</li>
<li>이건 어떤 명령어가 어디의 데이터를 참조해야 할지를 결정하는 과정이에요.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5455336a-3619-411f-9879-8bd9ebe5f452/image.png" />
출처 : <a href="https://blog.naver.com/k97b1114/140157844146">https://blog.naver.com/k97b1114/140157844146</a></p>
<blockquote>
<p>좀 더 자세히 설명하자면, </p>
</blockquote>
<p><strong>🧾 명령어 주소 (Instruction Address)</strong></p>
<ul>
<li>명령어 안에 들어 있는 주소 부분입니다.</li>
<li>즉, <strong>기준이 되는 상대적인 주소</strong>, 또는 <strong>오프셋(offset)</strong>이라고 생각하면 돼요.</li>
<li>예: <code>LOAD 100</code> → “100번지의 데이터를 불러와줘!”</li>
</ul>
<p>하지만 이건 어디까지나 <strong>기준 주소에 더해져야 하는 상대 주소</strong>예요. 실제 위치는 아직 아니에요!</p>
<p><strong>🧮 인덱스 레지스터 (Index Register)</strong></p>
<ul>
<li>이건 OS나 CPU가 <strong>“현재 이 프로그램은 어디서부터 실행 중이다”</strong>를 알려주는 <strong>기준 시작점</strong>이에요.</li>
<li>즉, <strong>“기준이 되는 주소(=베이스)”</strong>라고 생각하면 됩니다.</li>
</ul>
<p>예를 들어, 어떤 프로그램이 <strong>3000번지부터 실행 중</strong>이라면, 인덱스 레지스터는 <code>3000</code>으로 설정됩니다.</p>
<p><strong>➕ 유효 주소 (Effective Address)</strong></p>
<ul>
<li><strong>실제로 메모리에서 접근해야 할 주소</strong>예요.</li>
<li>계산 방식은 단순해요!</li>
</ul>
<blockquote>
<p><strong>유효 주소 = 인덱스 레지스터 값 + 명령어 주소 (오프셋)</strong></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e70b14e4-eb1c-418b-b57b-47ea36cb8c85/image.png" /></p>
<p>이 말은,  </p>
<ul>
<li>이 명령어는 원래는 <strong>100번지의 데이터</strong>를 보려는 명령이었지만,  </li>
<li>지금 이 프로그램이 <strong>2000번지부터 시작</strong>했기 때문에  </li>
<li>실제로는 <strong>2000 + 100 = 2100번지의 데이터</strong>를 참조해야 한다는 뜻이에요!</li>
</ul>
<table>
<thead>
<tr>
<th>용어</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>명령어 주소 (offset)</td>
<td>명령어 안에 있는 상대 주소. “이만큼 떨어진 곳”</td>
</tr>
<tr>
<td>인덱스 레지스터</td>
<td>현재 프로그램이 시작된 기준 주소</td>
</tr>
<tr>
<td>유효 주소</td>
<td>실제로 접근하는 메모리 주소 = 기준 + 상대값</td>
</tr>
</tbody></table>
<h3 id="2-상대-주소-지정-relative-addressing">(2) 상대 주소 지정 (Relative Addressing)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8f2fedac-0d49-49b7-84b6-278bb257bd1a/image.png" /></p>
<h4 id="✅-왜-상대-주소-지정이-필요할까">✅ 왜 상대 주소 지정이 필요할까?</h4>
<ul>
<li>우리가 작성한 프로그램은 언제나 <strong>메모리의 같은 위치에서 실행되지 않아요</strong>.  
운영체제가 그때그때 프로그램을 <strong>다른 위치에 로딩</strong>할 수 있기 때문이에요.</li>
<li>하지만 프로그램 코드 안에 <strong>절대 주소</strong>가 박혀 있으면 이식성이 떨어지겠죠.</li>
<li>그래서 <strong>명령어 주소를 기준으로 상대적인 거리만 기억</strong>하도록 하면,<br />어디에 프로그램이 위치하든지 <strong>유효 주소는 정확하게 계산</strong>됩니다.</li>
</ul>
<h4 id="📦-예시">📦 예시</h4>
<ul>
<li>현재 명령어가 메모리 주소 <code>4000</code>에 위치해 있고,</li>
<li><code>+20</code> 떨어진 곳에 점프하려는 명령이 있다면,<br />→ 유효 주소는 <code>4000 + 20 = 4020</code></li>
</ul>
<p>이처럼 상대 주소 지정은 다음과 같은 장점이 있어요:</p>
<table>
<thead>
<tr>
<th>장점</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>위치 독립성</td>
<td>프로그램이 메모리의 어느 위치에 로드되든 정상적으로 동작 가능</td>
</tr>
<tr>
<td>코드 재사용성</td>
<td>다른 위치에서도 동일 코드 사용 가능 (특히 공유 라이브러리 등에서 유리)</td>
</tr>
<tr>
<td>컴파일러 최적화</td>
<td>컴파일러가 오프셋(상대 거리)만 계산하면 되므로 구현 간결</td>
</tr>
</tbody></table>
<blockquote>
<p>🔧 요즘 대부분의 컴파일러와 어셈블러는 이 상대 주소 계산을 자동으로 처리해 줍니다.<br />우리는 <code>jump +4</code> 같은 코드만 쓰면, 실제 메모리 주소 계산은 기계가 해주죠!</p>
</blockquote>
<h4 id="📌-추가-팁-상대-주소는-보통-분기branch-명령어에서-많이-쓰여요">📌 추가 팁: 상대 주소는 보통 <strong>분기(branch)</strong> 명령어에서 많이 쓰여요</h4>
<pre><code class="language-assembly">4000:  CMP A, 10       ; 비교
4001:  JE +4            ; 조건이 참이면 4005번지로 점프
4002:  ...              ; 다른 명령어
4005:  PRINT &quot;OK&quot;       ; 점프 대상</code></pre>
<p>이처럼 <strong>현재 위치를 기준으로 점프 대상을 지정</strong>하면,<br />프로그램이 어느 위치에 올라가더라도 정확히 원하는 명령으로 이동할 수 있습니다.</p>
<blockquote>
<p>🔧 요즘 컴파일러는 이런 상대 주소 계산을 자동으로 해줍니다.</p>
</blockquote>
<blockquote>
<p>주소 지정 방식 더 알아보기 : <a href="https://blog.naver.com/k97b1114/140157844146">https://blog.naver.com/k97b1114/140157844146</a></p>
</blockquote>
<h2 id="7-🔄-프로그램의-재배치relocation">7) 🔄 프로그램의 재배치(Relocation)</h2>
<p>이런 주소 지정 기술을 활용하면,<br />운영체제는 프로그램을 <strong>메모리의 어떤 위치든 자유롭게 올려서 실행</strong>할 수 있어요.</p>
<ul>
<li>절대 주소를 쓰지 않아도 되니까 메모리 충돌 없음</li>
<li>여러 프로그램이 한꺼번에 올라가도 문제 없이 동작 가능</li>
</ul>
<h2 id="8-🧠-요약-정리-운영체제가-멀티태스킹을-해내는-방법">8) 🧠 요약 정리: 운영체제가 멀티태스킹을 해내는 방법</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>운영체제(OS)</td>
<td>시스템 자원 관리자</td>
</tr>
<tr>
<td>시분할(Time Slicing)</td>
<td>CPU 시간을 잘게 나눠 여러 프로그램에 할당</td>
</tr>
<tr>
<td>타이머 인터럽트</td>
<td>일정 시간마다 스위칭을 알림</td>
</tr>
<tr>
<td>문맥 교환(Context Switch)</td>
<td>프로그램 상태를 저장하고 복원</td>
</tr>
<tr>
<td>인덱스 레지스터</td>
<td>명령어 주소에 기준값을 더해 유효 주소 계산</td>
</tr>
<tr>
<td>상대 주소 지정</td>
<td>명령어 기준으로 주소를 계산</td>
</tr>
<tr>
<td>재배치(Relocation)</td>
<td>프로그램을 메모리의 어디든 옮겨 실행 가능</td>
</tr>
</tbody></table>
<h2 id="🎬-마무리--운영체제는-모든-것을-조율하는-무대-감독">🎬 마무리 – 운영체제는 모든 것을 조율하는 무대 감독</h2>
<ul>
<li>CPU는 빠르게 실행만 하고  </li>
<li>메모리는 그냥 저장소고  </li>
<li>진짜 조율자는? 👉 운영체제!</li>
</ul>
<blockquote>
<p>“멀티태스킹이 가능한 이유?<br />운영체제가 시간과 공간을 잘 쪼개서 프로그램들을 조화롭게 조율하기 때문입니다.” 🎵</p>
</blockquote>
<h1 id="8-🧠-내-컴퓨터-메모리는-진짜가-아닐-수도-있다---mmu와-가상-메모리-이야기프로그램은-어떻게-메모리-안에서-안전하게-실행될까">8. 🧠 내 컴퓨터 메모리는 ‘진짜’가 아닐 수도 있다? –  MMU와 가상 메모리 이야기(프로그램은 어떻게 메모리 안에서 안전하게 실행될까?)</h1>
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
<h1 id="9-🛡️-사용자-모드-vs-시스템-모드--누구에게-권한이-있을까">9. 🛡️ 사용자 모드 vs 시스템 모드 – 누구에게 권한이 있을까?</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8b15c60e-885b-423c-9280-c69ae87d5a41/image.png" /></p>
<h2 id="✅-사용자에게-주는-환상과-그-이면의-시스템-보호">✅ 사용자에게 주는 ‘환상’과 그 이면의 시스템 보호</h2>
<h3 id="1-운영체제는-착각을-심어준다">1) 운영체제는 착각을 심어준다?</h3>
<p>멀티태스킹 시스템에서 여러 프로그램이 동시에 실행되고 있어도,  </p>
<blockquote>
<p><strong>각 프로그램은 ‘내가 유일하게 실행 중인 프로그램’이라고 착각합니다.</strong></p>
</blockquote>
<p>이건 <strong>MMU(메모리 관리 장치)</strong> 덕분이에요.</p>
<ul>
<li>MMU는 <strong>각 프로세스마다 독립적인 가상 주소 공간</strong>을 만들어줘요.</li>
<li>덕분에 프로세스들은 서로의 메모리에 접근할 수 없고, <strong>마치 자신만 컴퓨터를 쓰는 것처럼 보이죠.</strong></li>
</ul>
<h3 id="2-그런데-io-장치가-끼면-문제가-생긴다">2) 그런데, I/O 장치가 끼면 문제가 생긴다?</h3>
<p>맞아요.<br />타이머나 디스크 같은 <strong>I/O 장치</strong>는 <strong>시스템 전체에 영향을 주는 하드웨어</strong>라서 함부로 건드리면 곤란해져요.</p>
<p>예를 들어:</p>
<ul>
<li>운영체제는 <strong>타이머 인터럽트</strong>를 이용해 프로세스를 주기적으로 전환해요.</li>
<li>그런데 어떤 사용자 프로그램이 타이머를 <strong>“1시간에 한 번만 인터럽트해줘~”</strong>라고 바꿔버리면?<ul>
<li>😱 → <strong>다른 프로그램은 영원히 실행되지 못할 수도 있어요.</strong></li>
</ul>
</li>
</ul>
<h3 id="3-그래서-운영체제는-특권-계층을-둡니다">3) 그래서 운영체제는 ‘특권 계층’을 둡니다</h3>
<p>CPU는 두 가지 모드를 구분해요:</p>
<table>
<thead>
<tr>
<th>모드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>🧍‍♂️ 사용자 모드(User Mode)</td>
<td>일반 앱이나 사용자 코드가 실행되는 공간</td>
</tr>
<tr>
<td>🛡️ 시스템 모드(System/Kernal Mode)</td>
<td>운영체제 커널, I/O, MMU 설정 등 <strong>중요한 코드</strong>가 실행되는 공간</td>
</tr>
</tbody></table>
<p><strong>일반 프로그램은 사용자 모드에서만 실행</strong>돼요.<br />중요한 명령어(예: I/O 제어, MMU 설정 등)는 <strong>“특권 명령어(Privileged Instructions)”</strong>라서<br />👉 <strong>시스템 모드에서만 실행</strong>이 가능해요!</p>
<blockquote>
<p>👉 CPU의 모드 전환(User Mode ↔ System Mode), 그리고 특권 명령어 실행 여부 판단은 모두 <strong>운영체제 커널(Kernel)</strong>이 주도적으로 관리하고 통제</p>
</blockquote>
<blockquote>
<p><a href="https://velog.io/@prettylee620/%EB%A6%AC%EB%88%85%EC%8A%A4-%EA%B0%9C%EC%9A%94-%EC%BB%A4%EB%84%90%EC%9D%B4-%EB%AD%90%EC%97%90%EC%9A%94-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%B4">리눅스 커널 정리</a></p>
</blockquote>
<h3 id="4-사용자-→-운영체제와-대화하는-방법은">4) 사용자 → 운영체제와 대화하는 방법은?</h3>
<p>사용자 프로그램이 시스템 기능이 필요할 때는 직접 실행 못 해요.<br />대신 다음 중 하나를 사용해요:</p>
<ul>
<li><strong>트랩(trap)</strong> : 예외 상황이나 오류 발생 시, 자동으로 OS에 제어권을 넘김</li>
<li><strong>시스템 콜(system call)</strong> : 사용자 프로그램이 명시적으로 운영체제에게 요청하는 메커니즘</li>
</ul>
<p>예: <code>read()</code>, <code>write()</code>, <code>fork()</code> 등이 모두 시스템 콜!</p>
<h3 id="5-이-구조의-장점은">5) 이 구조의 장점은?</h3>
<ol>
<li>✅ <strong>운영체제를 보호</strong>: 일반 프로그램이 시스템 자원을 함부로 만지지 못함  </li>
<li>✅ <strong>프로세스 간 보호</strong>: 사용자 프로그램이 서로의 메모리나 자원을 침범할 수 없음  </li>
<li>✅ <strong>운영체제 자원 제어</strong>: 자원 할당을 운영체제가 전적으로 통제 가능</li>
</ol>
<h3 id="6-동작-간단하게">6) 동작 간단하게</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5d32cb59-dec9-4049-9cfc-89b6f4cacd89/image.png" /></p>
<p><strong>✅ 사용자 모드 → 시스템 모드 전환 흐름도 설명</strong></p>
<p>이 그림은 <strong>사용자 모드(User Mode)</strong>에서 실행 중인 프로그램이 어떻게 운영체제 커널이 실행되는 <strong>시스템 모드(System Mode)</strong>로 전환되는지를 보여주는 흐름도예요.</p>
<p><strong>🔄 전체 흐름 요약</strong></p>
<ol>
<li><p><strong>사용자 프로그램 실행 중</strong></p>
<ul>
<li>이때 CPU는 <strong>사용자 모드(User Mode)</strong>로 설정됨</li>
<li><code>read()</code>, <code>write()</code> 같은 <strong>시스템 콜</strong>은 직접 실행할 수 없음</li>
</ul>
</li>
<li><p><strong>시스템 콜 요청</strong></p>
<ul>
<li>사용자 프로그램이 시스템 리소스를 요청하면, <code>int 0x80</code> 같은 <strong>시스템 콜 인터럽트</strong> 발생</li>
<li>이 순간 <strong>트랩(trap)</strong>이 발생하면서 CPU는 모드를 전환</li>
</ul>
</li>
<li><p><strong>Mode Bit가 0 → 1로 전환</strong></p>
<ul>
<li><strong>Mode Bit</strong>는 CPU 내부의 한 비트로, 현재 CPU가 <strong>User Mode(0)</strong>인지, <strong>System Mode(1)</strong>인지 나타냄</li>
<li>이 비트를 바꾸는 건 오직 <strong>운영체제(커널 코드)</strong>만 가능</li>
</ul>
</li>
<li><p><strong>커널 모드로 진입 (System Mode)</strong></p>
<ul>
<li>이제 커널이 제어권을 잡고, I/O 명령이나 메모리 할당 같은 <strong>특권 명령어(Privileged Instructions)</strong>를 안전하게 수행</li>
<li>일반 프로그램은 이 명령어를 직접 실행할 수 없음</li>
</ul>
</li>
<li><p><strong>작업 완료 후 사용자 모드 복귀</strong></p>
<ul>
<li>작업이 끝나면 CPU의 <strong>Mode Bit를 다시 0(사용자 모드)</strong>로 바꾸고, 사용자 프로그램으로 돌아감</li>
</ul>
</li>
</ol>
<p><strong>🧠 주요 개념 요약</strong></p>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>🟦 <strong>Mode Bit</strong></td>
<td>CPU 안의 한 비트로, 현재 모드가 사용자(0)인지 시스템(1)인지 나타냄</td>
</tr>
<tr>
<td>🛑 <strong>트랩(Trap)</strong></td>
<td>예외 상황이나 시스템 콜 시 커널로 제어권이 넘어가는 동작</td>
</tr>
<tr>
<td>🧭 <strong>시스템 콜(System Call)</strong></td>
<td>사용자 프로그램이 OS 기능을 요청하는 인터페이스 (ex. 파일 읽기)</td>
</tr>
<tr>
<td>🛡️ <strong>특권 명령어(Privileged Instructions)</strong></td>
<td>MMU 설정, I/O 제어 등 시스템 모드에서만 실행 가능한 명령어</td>
</tr>
</tbody></table>
<blockquote>
<p>운영체제는 <strong>Mode Bit와 Trap 메커니즘</strong>을 활용해 사용자 프로그램과 커널 기능을 확실하게 <strong>격리하고 보호</strong>합니다.</p>
</blockquote>
<h3 id="💡-한-마디로-정리하면">💡 한 마디로 정리하면?</h3>
<blockquote>
<p>“<strong>운영체제는 사용자에게 착각을 심어주는 동시에, 철저한 보호 장치를 두어 시스템을 지킨다.</strong>”</p>
</blockquote>
<h3 id="📱-그래서-우리-프로그램은-어디서-실행되나요">📱 그래서 우리 프로그램은 어디서 실행되나요?</h3>
<ul>
<li>여러분이 만드는 앱, 웹 브라우저, 게임 등은 모두 <strong>사용자 공간(user space)</strong>에서 실행됩니다.</li>
<li>운영체제 커널은 <strong>시스템 공간(kernel space)</strong>에서 실행되며, 일반 사용자가 직접 접근할 수 없어요.</li>
</ul>
<blockquote>
<p>시스템 공간을 다룰 수 있는 사람은 ‘커널 해커’ 같은 <strong>아주 숙련된 프로그래머</strong>입니다.</p>
</blockquote>
<blockquote>
<p>&quot;이건 마치 은행 창구에서 직접 금고를 만지지 못하고, 요청서를 써서 창구 직원에게 전달하는 것과 비슷합니다.&quot;</p>
</blockquote>
<blockquote>
<p>“CPU 모드를 관리하는 건 하드웨어지만, 그 모드를 전환하고 제어하는 건 오직 운영체제 커널만 할 수 있다.”</p>
</blockquote>
<h1 id="10-🧊-냉장고-마트-창고--메모리의-식량-저장-전략">10. 🧊 냉장고, 마트, 창고 – 메모리의 식량 저장 전략</h1>
<ul>
<li><strong>레지스터</strong>: 가장 빠르고 가장 작음 (CPU 안)</li>
<li><strong>L1, L2, L3 캐시</strong>: 속도와 크기 중간 단계 (CPU와 RAM 사이)</li>
<li><strong>RAM</strong>: 주 메모리, CPU보다 느림</li>
<li><strong>디스크/SSD</strong>: 가장 느리지만 가장 큼</li>
</ul>
<h2 id="✅-컴퓨터는-왜-메모리-계층-구조를-만들었을까">✅ 컴퓨터는 왜 '메모리 계층 구조'를 만들었을까?</h2>
<h3 id="1-과거에는-cpu와-메모리-속도가-비슷했다">1) 과거에는 CPU와 메모리 속도가 비슷했다</h3>
<p>옛날에는 CPU와 메모리가 같은 속도로 동작했어요.<br />컴퓨터의 모든 부품이 한 템포로 움직이던 <strong>평화로운 시절</strong>이었죠.</p>
<blockquote>
<p>그런데 시간이 흐르며 CPU는 무섭게 빨라졌고, 메모리는 그만큼 따라오지 못했습니다.<br /><strong>“빠른 CPU가 느린 메모리를 기다리는 시대”</strong>가 시작된 거예요.</p>
</blockquote>
<p>레지스터가 전체 메모리에서 차지하는 비율은 점점 작아져 왔어요. </p>
<blockquote>
<p>프로세서는 보통 RAM으로 이뤄진 주 메모리main memory와 통신하는데, *<em>주 메모리는 프로세서보다 1/10 정도밖에 속도가 나지 않아서 느려요. *</em></p>
</blockquote>
<p>디스크 드라이브 등의 대량 저장장치는 프로세서보다 백만 배 느릴 수도 있습니다.</p>
<h3 id="2-메모리-계층-구조란">2) 메모리 계층 구조란?</h3>
<p>이런 문제를 해결하기 위해 나온 개념이 바로  </p>
<blockquote>
<p><strong>📚 메모리 계층(Memory Hierarchy)</strong></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/08caf4a4-e0d1-479c-91d3-4c731d9f8c2e/image.png" /></p>
<table>
<thead>
<tr>
<th>계층</th>
<th>비유</th>
<th>특징</th>
<th>속도</th>
</tr>
</thead>
<tbody><tr>
<td>레지스터</td>
<td>냉장고</td>
<td>아주 작고 빠름, CPU 안에 있음</td>
<td>최고속</td>
</tr>
<tr>
<td>캐시(L1~L3)</td>
<td>저장고, 미니냉장고</td>
<td>작지만 빠름, CPU 가까이</td>
<td>매우 빠름</td>
</tr>
<tr>
<td>주 메모리(RAM)</td>
<td>슈퍼마켓</td>
<td>큼직하지만 느림</td>
<td>중간</td>
</tr>
<tr>
<td>디스크(HDD/SSD)</td>
<td>창고</td>
<td>아주 큼, 엄청 느림</td>
<td>느림</td>
</tr>
</tbody></table>
<blockquote>
<p>사용자 프로그램 입장에서는 전부 &quot;메모리&quot;처럼 보이지만, 실제로는 이처럼 <strong>속도도 용량도 전혀 다릅니다.</strong></p>
</blockquote>
<h3 id="3-메모리를-기다리는-cpu를-구하라-캐시와-프리페치">3) 메모리를 기다리는 CPU를 구하라: 캐시와 프리페치</h3>
<h4 id="캐시cache는-뭘까">캐시(Cache)는 뭘까?</h4>
<ul>
<li>캐시는 CPU 바로 옆에 붙어 있는 <strong>초고속 메모리</strong></li>
<li>CPU가 자주 사용하는 데이터를 캐시에 <strong>미리 저장</strong>해두면,</li>
<li>RAM까지 가지 않고 <strong>더 빠르게 작업 가능</strong></li>
</ul>
<h4 id="프리페치prefetch">프리페치(Prefetch)?</h4>
<ul>
<li>CPU가 프로그램 실행 흐름을 <strong>예측</strong>해서, 앞으로 쓸 데이터를 <strong>미리 캐시에 가져다 놓는 것</strong></li>
<li>예: &quot;이 사람이 아침마다 시리얼을 먹네? 그럼 시리얼은 미리 꺼내놔야겠다!&quot; 같은 자동화된 습관</li>
</ul>
<h3 id="4-캐시는-왜-여러-단계로-나뉘어-있을까">4) 캐시는 왜 여러 단계로 나뉘어 있을까?</h3>
<ul>
<li><strong>L1 캐시</strong>: 아주 작고 빠름 (CPU와 거의 일심동체)</li>
<li><strong>L2 캐시</strong>: L1보다 크고 조금 느림</li>
<li><strong>L3 캐시</strong>: 더 크지만 느림, 여러 CPU 코어가 공유</li>
</ul>
<blockquote>
<p>멀어질수록 커지지만 느려지고, 가까울수록 빠르지만 작아져요.</p>
</blockquote>
<h3 id="5-캐시에도-실패가-있다">5) 캐시에도 실패가 있다?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/52cfb907-d6a3-472a-9d5d-52302793e37a/image.png" /></p>
<blockquote>
<p>출처 : <a href="https://velog.io/@skypinkhs0718/%EC%BA%90%EC%8B%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C">https://velog.io/@skypinkhs0718/%EC%BA%90%EC%8B%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C</a></p>
</blockquote>
<p>'용량이 작은' 캐시 메모리는 CPU가 사용할 법한 대상을 &quot;예측&quot;하여 저장하는데,</p>
<ul>
<li>이때 CPU가 활용해야 하는 데이터를 캐시메모리가 잘 저장하고 있다면 &quot;캐시 히트&quot;</li>
<li>반대로 CPU가 원하는 데이터가 아닌 <strong>다른 엉뚱한 데이터를 저장하여 CPU가 직접 메모리를 통해 데이터를 가져가야 하는 상황</strong>일 때를 &quot;캐시 미스&quot;라고 한다.</li>
</ul>
<table>
<thead>
<tr>
<th>용어</th>
<th>뜻</th>
</tr>
</thead>
<tbody><tr>
<td>✅ <strong>캐시 히트 (Cache Hit)</strong></td>
<td>CPU가 필요한 데이터가 캐시에 있어서 빠르게 접근 성공</td>
</tr>
<tr>
<td>❌ <strong>캐시 미스 (Cache Miss)</strong></td>
<td>캐시에 데이터가 없어서 느린 메모리나 디스크까지 가야 함</td>
</tr>
</tbody></table>
<h3 id="6-cpu가-메모리보다-10배-빠르다고-가정하면-🧠-cpu-성능을-높이기-위한-두-가지-핵심-기법">6) CPU가 메모리보다 10배 빠르다고 가정하면? 🧠 CPU 성능을 높이기 위한 두 가지 핵심 기법</h3>
<ul>
<li>CPU가 1초에 10개의 명령을 실행할 수 있는데,</li>
<li>메모리는 1초에 1개밖에 못 넘겨줘요.</li>
<li>👉 <strong>CPU는 나머지 9초 동안 '멍 때리는 셈'이죠.</strong></li>
</ul>
<p>그래서 더 복잡한 장치들이 등장합니다:</p>
<p><strong>✅ 1. Branch Prediction (분기 예측)</strong></p>
<ul>
<li><p><strong>설명</strong>: 프로그램에는 <code>if</code>, <code>for</code>, <code>while</code> 같은 <strong>분기 명령어</strong>가 자주 등장합니다.<br />CPU는 이런 분기를 만났을 때 다음 명령어가 어디로 갈지 <strong>기다리지 않고 미리 예측</strong>해서 실행 준비를 해요.</p>
</li>
<li><p><strong>예시 비유</strong>:  
마트에서 계산대가 두 줄 있을 때, 사람들이 보통 어디 줄로 가는지 예측하고 먼저 줄 서는 것과 비슷해요!</p>
</li>
<li><p><strong>효과</strong>:  </p>
<ul>
<li>분기 결과가 예측과 일치하면 👉 시간 절약!  </li>
<li>예측 실패해도 👉 다시 실행하면 되니까 전반적으로 <strong>대기 시간이 줄어듦</strong></li>
</ul>
</li>
</ul>
<p><strong>✅ 2. Out-of-Order Execution (순서 무시 실행)</strong></p>
<ul>
<li><p><strong>설명</strong>: CPU는 명령어를 무조건 위에서 아래로 실행하지 않아요.<br /><strong>먼저 실행할 수 있는 명령어부터 골라서 처리</strong>해요.<br />의존성이 없는 연산부터 먼저 끝내서 대기 시간을 줄이는 거예요.</p>
</li>
<li><p><strong>예시 비유</strong>:  
라면 끓이기 순서를 생각해보면, 물을 끓이는 동안 반찬을 꺼내는 것처럼, <strong>할 수 있는 일을 먼저 처리</strong>하는 방식이에요.</p>
</li>
<li><p><strong>효과</strong>:</p>
<ul>
<li>메모리를 기다리는 동안 놀지 않음  </li>
<li>CPU가 <strong>놀지 않고 쉴 틈 없이</strong> 일하게 해줌</li>
</ul>
</li>
</ul>
<table>
<thead>
<tr>
<th>기법</th>
<th>역할</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Branch Prediction (분기 예측)</strong></td>
<td>분기 명령(if, loop 등)이 어디로 갈지 미리 예측해서 기다리지 않음</td>
</tr>
<tr>
<td><strong>Out-of-Order Execution</strong></td>
<td>코드 순서 상관없이, 할 수 있는 명령어부터 먼저 실행함</td>
</tr>
</tbody></table>
<h3 id="7-멀티코어-환경에서는-더-어려운-문제-등장">7) 멀티코어 환경에서는 더 어려운 문제 등장</h3>
<ul>
<li>여러 CPU 코어가 <strong>같은 메모리 영역</strong>을 캐시에 가지고 있으면?</li>
<li>한 코어가 수정한 내용을 <strong>다른 코어는 모를 수 있음</strong></li>
<li>👉 이걸 해결하기 위한 개념이 바로 <strong>캐시 일관성(Cache Coherency)</strong></li>
</ul>
<p>예:  </p>
<ul>
<li>라이트 스루(Write Through): 캐시 + 메모리에 동시에 씀 → 안전하지만 느림</li>
<li>그래서 더 복잡한 <strong>캐시 일관성 프로토콜(MESI 등)</strong>이 개발됨</li>
</ul>
<h3 id="💡-한-줄-요약">💡 한 줄 요약</h3>
<blockquote>
<p><strong>메모리 계층 구조는 빠른 CPU와 느린 메모리 사이의 속도 차이를 메우기 위한 구조적 해법이다.</strong></p>
</blockquote>
<h3 id="📌-비유로-다시-정리하면">📌 비유로 다시 정리하면</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/563651eb-5ed1-4616-beed-517a69bd9724/image.png" /></p>
<table>
<thead>
<tr>
<th>계층</th>
<th>비유</th>
<th>특징</th>
</tr>
</thead>
<tbody><tr>
<td>레지스터</td>
<td>냉장고</td>
<td>공간 작음, 아주 빠름</td>
</tr>
<tr>
<td>캐시</td>
<td>주방 식품장</td>
<td>크진 않지만 빠름, 자주 쓰는 것만 저장</td>
</tr>
<tr>
<td>주 메모리</td>
<td>슈퍼마켓</td>
<td>크지만 느림</td>
</tr>
<tr>
<td>디스크</td>
<td>창고</td>
<td>매우 큼, 매우 느림</td>
</tr>
<tr>
<td>디스패처</td>
<td>식재료 분배기</td>
<td>어디서 어떤 걸 꺼내고 채울지 결정함</td>
</tr>
</tbody></table>
<p>메모리는 빠르지만 비싼 공간에서 느리지만 저렴한 공간으로 구성됩니다. 캐시 미스가 생기면 하위 계층에서 데이터를 가져오느라 시간이 더 걸립니다.</p>
<blockquote>
<p>&quot;집 – 냉장고 – 식료품 가게 – 창고
이 흐름이 컴퓨터 메모리와 정확히 닮았죠.&quot;</p>
</blockquote>
<h1 id="11-🚀-앞을-내다보는-cpu--캐시와-분기-예측의-세계">11. 🚀 앞을 내다보는 CPU – 캐시와 분기 예측의 세계</h1>
<p>멀티코어 환경에서는 캐시 일관성 문제도 생깁니다. 여러 코어가 같은 메모리를 접근할 때, 캐시에 있는 값과 메모리에 있는 값이 다를 수 있기 때문이죠. 이를 해결하기 위해:</p>
<ul>
<li><strong>Write-through</strong> 방식</li>
<li><strong>캐시 동기화 프로토콜</strong> (MESI 등)</li>
</ul>
<p>그리고 고급 프로세서는 다음 명령어를 미리 예측하는 <strong>분기 예측기</strong>와 순서를 바꿔 효율적으로 실행하는 <strong>Out-of-Order Execution</strong> 기능도 탑재합니다.</p>
<h1 id="12-👷-일은-cpu만-하는-게-아냐-cpu-혼자-다-하기엔-벅차다---그래서-등장한-코프로세서--dma">12. 👷 일은 CPU만 하는 게 아냐 CPU 혼자 다 하기엔 벅차다! - 그래서 등장한 코프로세서 &amp; DMA</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/99c44081-51c8-4f5b-aff9-7c160cd66300/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f5543ab2-d966-42a9-8ad2-b6f11c87190b/image.png" /></p>
<h2 id="1-코프로세서coprocessor-cpu의-작업-분담-파트너">1) 코프로세서(Coprocessor): CPU의 ‘작업 분담 파트너’</h2>
<blockquote>
<p>CPU는 굉장히 복잡하고 중요한 회로라서 모든 일을 혼자 처리하긴 어려워요.<br />그래서 특정 작업은 <strong>“보조 프로세서”</strong>, 즉 <strong>코프로세서</strong>에 맡깁니다.</p>
</blockquote>
<h3 id="📌-왜-코프로세서를-쓰나요">📌 왜 코프로세서를 쓰나요?</h3>
<blockquote>
<p>출처 : <a href="https://recipes.tistory.com/203">https://recipes.tistory.com/203</a></p>
</blockquote>
<p>코프로세서는 <strong>메인 CPU와 함께 동작하며, 특정 기능을 보조하거나 제어하는 하드웨어 유닛</strong>입니다.<br />ARM 구조에서는 <strong>CP15(Coprocessor 15)</strong>가 대표적이며, 아래와 같은 <strong>중요한 제어 기능</strong>을 담당합니다:</p>
<table>
<thead>
<tr>
<th>기능</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>MMU ON/OFF 제어</td>
<td>가상 메모리 사용 여부 설정</td>
</tr>
<tr>
<td>캐시 ON/OFF</td>
<td>I-Cache(명령어 캐시), D-Cache(데이터 캐시) 사용 제어</td>
</tr>
<tr>
<td>페이지 테이블 주소 설정</td>
<td>MMU가 참조할 페이지 테이블 위치 지정</td>
</tr>
<tr>
<td>권한 제어 (DACR 등)</td>
<td>메모리 접근 권한(읽기/쓰기 등) 설정</td>
</tr>
</tbody></table>
<h3 id="✅-코프로세서가-왜-필요한가">✅ 코프로세서가 왜 필요한가?</h3>
<p>ARM의 CPU 코어는 이미 연산/분기/파이프라인 등 다양한 복잡한 연산을 수행하고 있어요.<br />하지만 시스템 제어나 메모리 관리 같은 <strong>제어용 기능</strong>까지 모두 직접 담당하면:</p>
<blockquote>
<p>❌ 복잡성 증가<br />❌ CPU 자원 낭비<br />❌ 소프트웨어-하드웨어 인터페이스가 어려워짐</p>
</blockquote>
<p>그래서 <strong>제어 관련 기능만 따로 분리한 것이 코프로세서</strong>예요.</p>
<h3 id="✅-cr-레지스터가-하는-일-cp15-내부">✅ CR 레지스터가 하는 일 (CP15 내부)</h3>
<p><strong>CR (Control Register) 주요 비트 설명</strong></p>
<table>
<thead>
<tr>
<th>비트</th>
<th>기능</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>M</code></td>
<td>MMU 제어</td>
<td>ON이면 가상 주소 → 물리 주소 변환 가능</td>
</tr>
<tr>
<td><code>C</code></td>
<td>D-Cache 제어</td>
<td>데이터 캐시 사용 여부</td>
</tr>
<tr>
<td><code>I</code></td>
<td>I-Cache 제어</td>
<td>명령어 캐시 사용 여부</td>
</tr>
</tbody></table>
<blockquote>
<p>즉, CR 레지스터를 조작하면 <strong>MMU 활성화 + 캐시 활성화 여부</strong>를 소프트웨어에서 제어할 수 있습니다.</p>
</blockquote>
<h3 id="✅-mmu가-on-되면-무슨-일이-일어날까">✅ MMU가 ON 되면 무슨 일이 일어날까?</h3>
<ul>
<li>CPU는 <strong>가상 주소(Virtual Address)</strong>로 메모리에 접근합니다.</li>
<li>MMU는 가상 주소를 <strong>물리 주소(Physical Address)</strong>로 변환합니다.</li>
<li>이 변환을 위해 <strong>페이지 테이블(Page Table)</strong>을 참조합니다.</li>
</ul>
<h4 id="📌-예시">📌 예시</h4>
<table>
<thead>
<tr>
<th>가상 주소</th>
<th>실제 물리 주소</th>
<th>접근 권한</th>
</tr>
</thead>
<tbody><tr>
<td>0x13D00000</td>
<td>0x46200000</td>
<td>읽기/쓰기</td>
</tr>
<tr>
<td>0x14100000</td>
<td>0x74600000</td>
<td>읽기/쓰기</td>
</tr>
<tr>
<td>0x14300000</td>
<td>0x66300000</td>
<td>접근 불가</td>
</tr>
</tbody></table>
<h3 id="✅-캐시-사용-조건-mmu가-반드시-on이어야-함">✅ 캐시 사용 조건: MMU가 반드시 ON이어야 함</h3>
<p>왜냐하면:</p>
<ul>
<li>캐시의 주소 라인이 <strong>MMU를 통해 연결되어 있기 때문</strong>이에요.</li>
<li>즉, <strong>MMU가 OFF면 캐시도 OFF 상태처럼 작동</strong>합니다.</li>
</ul>
<h3 id="✅-하버드-아키텍처도-한몫해요">✅ 하버드 아키텍처도 한몫해요</h3>
<ul>
<li>ARM9 이후는 <strong>Harvard 방식</strong>을 많이 씁니다.</li>
<li><strong>I-Cache와 D-Cache가 분리되어</strong> 있어, 명령어와 데이터를 동시에 읽고 쓸 수 있어요.</li>
<li>병렬화 덕분에 <strong>성능이 더 향상</strong>됩니다.</li>
</ul>
<h3 id="✅-한-줄-정리">✅ 한 줄 정리</h3>
<blockquote>
<p><strong>ARM의 코프로세서(CP15)는 MMU와 캐시, 페이지 테이블, 권한 제어를 담당하는 핵심 제어기이며, 소프트웨어에서 이를 제어함으로써 시스템 메모리 관리가 가능해집니다.</strong></p>
</blockquote>
<h3 id="🧠-예시">🧠 예시</h3>
<table>
<thead>
<tr>
<th>시기</th>
<th>역할</th>
</tr>
</thead>
<tbody><tr>
<td>과거</td>
<td><strong>부동소수점 연산(FPU)</strong>을 코프로세서가 담당</td>
</tr>
<tr>
<td>요즘</td>
<td><strong>그래픽 처리(GPU)</strong>, <strong>AI 연산(NPU)</strong> 같은 복잡한 연산을 코프로세서가 처리</td>
</tr>
</tbody></table>
<blockquote>
<p>과거엔 칩 공간이 부족해서 FPU(부동소수점 유닛)를 외부 코프로세서로 빼놓았지만,<br />요즘은 하나의 칩에 GPU나 NPU가 함께 들어있는 <strong>SoC(System on Chip)</strong> 구조가 일반적이에요.</p>
</blockquote>
<h2 id="2-dmadirect-memory-access-데이터-복사-담당-특화-회로">2) DMA(Direct Memory Access): 데이터 복사 담당 특화 회로</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a4292e9b-ad50-485e-b060-45f81b62122b/image.png" /></p>
<blockquote>
<p>CPU는 계산만 잘하는 게 아니라, <strong>데이터를 이리저리 옮기는 일도 많이</strong> 해요.<br />그런데 이런 건 시간은 오래 걸리고... 두뇌는 필요 없어요! 그래서 이 일은 <strong>DMA가 맡습니다.</strong></p>
</blockquote>
<h3 id="💡-dma는-어떤-일을-하나요">💡 DMA는 어떤 일을 하나요?</h3>
<ul>
<li><strong>디스크 → 메모리</strong>, <strong>메모리 → 디바이스</strong> 사이에 데이터를 <strong>CPU 없이 직접 복사</strong>해요.</li>
<li>예:  <blockquote>
<p>“여기서 이만큼 데이터를 저기로 복사해줘. 다 끝나면 나한테 알려줘!”</p>
</blockquote>
</li>
</ul>
<h3 id="📦-왜-dma가-중요할까">📦 왜 DMA가 중요할까?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a41a3e79-91ee-433c-9539-714dc78dcd94/image.png" /></p>
<blockquote>
<p><a href="https://naeunbi698.tistory.com/195">DMA에 대한 정리 내용</a></p>
</blockquote>
<table>
<thead>
<tr>
<th>항목</th>
<th>CPU만 처리</th>
<th>DMA가 처리</th>
</tr>
</thead>
<tbody><tr>
<td>데이터 복사</td>
<td>CPU가 계속 바쁨</td>
<td>CPU는 계산에 집중 가능</td>
</tr>
<tr>
<td>효율성</td>
<td>떨어짐</td>
<td>높아짐</td>
</tr>
</tbody></table>
<blockquote>
<p>특히 디스크는 <strong>블록 단위(512B, 4KB)</strong>로 데이터를 옮기기 때문에, 대량 복사가 자주 발생해요.<br />이런 걸 <strong>CPU가 직접 처리하면 낭비</strong>라서 DMA가 대신 해주는 거예요.</p>
</blockquote>
<blockquote>
<p>전송이 완료되면 DMA모듈은 CPU에게 인터럽트 신호를 보내고 CPU는 전송의 시작과 끝 부분에만 관여</p>
</blockquote>
<h2 id="🧩-코프로세서-vs-dma">🧩 코프로세서 vs DMA</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>코프로세서</th>
<th>DMA</th>
</tr>
</thead>
<tbody><tr>
<td>하는 일</td>
<td>계산 보조 (FPU, GPU, NPU 등)</td>
<td>데이터 복사 전담</td>
</tr>
<tr>
<td>목적</td>
<td>CPU 연산 분산</td>
<td>CPU 복사 부담 줄이기</td>
</tr>
<tr>
<td>처리 대상</td>
<td>특정 연산</td>
<td>메모리 ↔ 디스크 등 데이터 전송</td>
</tr>
</tbody></table>
<h2 id="💡-정리-한-줄">💡 정리 한 줄</h2>
<blockquote>
<p><strong>CPU가 혼자 다 하지 않도록, 계산은 코프로세서에게, 데이터 복사는 DMA에게 맡긴다.</strong></p>
</blockquote>
<p>그래픽 연산은 GPU가, 단순 복사는 DMA가 맡음으로써 CPU는 더 중요한 일에 집중할 수 있습니다.</p>
<h1 id="13-🧵-흩어진-코드-조각-어떻게-실행-파일이-될까---프로그램-실행-구조와-링커">13. 🧵 흩어진 코드 조각, 어떻게 실행 파일이 될까? - 프로그램 실행 구조와 링커</h1>
<h2 id="1-📦-메모리에는-명령어만-담는-게-아니다">1) 📦 메모리에는 &quot;명령어&quot;만 담는 게 아니다!</h2>
<blockquote>
<p>메모리는 단순히 실행할 코드(명령어)뿐만 아니라, 다양한 종류의 <strong>데이터</strong>도 함께 저장합니다.</p>
</blockquote>
<table>
<thead>
<tr>
<th>구분</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>명령어(Instruction)</strong></td>
<td>CPU가 실행할 기계어 코드</td>
</tr>
<tr>
<td><strong>정적 데이터(Static Data)</strong></td>
<td>프로그램 시작 시 크기와 위치가 정해진 데이터 (예: 전역 변수, 상수)</td>
</tr>
<tr>
<td><strong>스택(Stack)</strong></td>
<td>함수 호출/복귀 시 사용하는 임시 저장 공간</td>
</tr>
<tr>
<td><strong>힙(Heap)</strong></td>
<td>실행 중 필요한 동적 메모리 할당 공간 (예: 사용자 입력, 가변 길이 리스트 등)</td>
</tr>
</tbody></table>
<h2 id="2-🧱-전통적인-메모리-배치-방식">2) 🧱 전통적인 메모리 배치 방식</h2>
<h3 id="그림-5-15-mmu가-없을-때의-메모리-배치">그림 5-15. MMU가 없을 때의 메모리 배치</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1bd5a632-3b5e-4081-9fd1-a7069db5e87c/image.png" /></p>
<table>
<thead>
<tr>
<th>구조</th>
<th>구성 설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>폰 노이만 구조</strong></td>
<td>명령어와 데이터가 <strong>같은 메모리 공간</strong>에 저장됨</td>
</tr>
<tr>
<td><strong>하버드 구조</strong></td>
<td>명령어와 데이터가 <strong>완전히 분리된 메모리 공간</strong>에 저장됨 (속도↑)</td>
</tr>
</tbody></table>
<blockquote>
<p>둘 다 구조적으로는 비슷하지만, 하버드는 명령어 캐시와 데이터 캐시를 별도로 운용할 수 있어 <strong>성능 면에서 유리</strong>해요.</p>
</blockquote>
<h2 id="3-📈-동적-메모리인-힙heap의-등장">3) 📈 동적 메모리인 힙(Heap)의 등장</h2>
<blockquote>
<p>정적 데이터는 미리 크기를 알지만, 현실 세계의 프로그램은 동적으로 변하는 데이터를 많이 다룹니다.</p>
</blockquote>
<h3 id="예">예:</h3>
<ul>
<li>메시지 큐</li>
<li>사용자 입력 리스트</li>
<li>웹 요청 버퍼 등</li>
</ul>
<p>이럴 때는 <strong>동적으로 메모리를 할당해야</strong> 하므로, 다음과 같이 메모리를 씁니다:</p>
<h3 id="그림-5-16-힙이-있는-메모리-배치">그림 5-16. 힙이 있는 메모리 배치</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/394d0291-6c37-419c-b737-ad6169ffe4df/image.png" /></p>
<pre><code>[ 메모리 최상단 ]
┌────────────┐
│   스택 (아래로 자람)   │ ← 함수 호출 시마다 증가
├────────────┤
│   힙 (위로 자람)      │ ← malloc, new 등으로 증가
├────────────┤
│   정적 데이터           │ ← 전역 변수, static 등
├────────────┤
│   명령어                │ ← 프로그램 코드
└────────────┘
[ 메모리 하단 ]</code></pre><blockquote>
<p>힙과 스택이 <strong>서로 충돌하지 않게 관리하는 것</strong>이 매우 중요합니다.<br />충돌하면 프로그램이 뻗거나, 보안 취약점이 생길 수 있어요.</p>
</blockquote>
<h2 id="4-⚙️-mmumemory-management-unit가-있다면">4) ⚙️ MMU(Memory Management Unit)가 있다면?</h2>
<p>MMU가 있으면 이런 배치를 <strong>물리 메모리와 분리된 가상 메모리 공간에서 자유롭게 구성</strong>할 수 있어요.</p>
<table>
<thead>
<tr>
<th>항목</th>
<th>MMU 없음</th>
<th>MMU 있음</th>
</tr>
</thead>
<tbody><tr>
<td>메모리 배치</td>
<td>프로그램이 직접 설계</td>
<td>OS/커널이 페이지 단위로 매핑</td>
</tr>
<tr>
<td>공간 제약</td>
<td>힙/스택 충돌 위험</td>
<td>페이지 단위 분리로 유연</td>
</tr>
<tr>
<td>보안성</td>
<td>낮음</td>
<td>접근 제어 가능 (예: read-only)</td>
</tr>
</tbody></table>
<blockquote>
<p>MMU를 활용하면 메모리 보호, 동적 확장, 접근 제어 등 <strong>더 안정적이고 유연한 운영</strong>이 가능해요.</p>
</blockquote>
<h3 id="💡-한-줄-요약-1">💡 한 줄 요약</h3>
<blockquote>
<p><strong>프로그램은 명령어뿐 아니라 정적/동적 데이터, 스택 등을 메모리에 배치하며, MMU가 있으면 이 배치를 가상 주소로 더 유연하게 구성할 수 있다.</strong></p>
</blockquote>
<h3 id="📌-용어-정리-요약표">📌 용어 정리 요약표</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8aa2cf3c-9931-469d-80ed-bcbf06fff925/image.png" /></p>
<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>정적 데이터</strong></td>
<td>프로그램 시작 시 크기 고정, 전역 변수 등</td>
</tr>
<tr>
<td><strong>동적 데이터 (힙)</strong></td>
<td>실행 중 크기 변동 가능, malloc/new</td>
</tr>
<tr>
<td><strong>스택</strong></td>
<td>함수 호출/복귀, 지역 변수</td>
</tr>
<tr>
<td><strong>폰 노이만 구조</strong></td>
<td>명령어/데이터 메모리 통합</td>
</tr>
<tr>
<td><strong>하버드 구조</strong></td>
<td>명령어/데이터 메모리 분리</td>
</tr>
<tr>
<td><strong>MMU</strong></td>
<td>가상 주소 → 물리 주소 매핑, 메모리 보호/격리</td>
</tr>
</tbody></table>
<h1 id="14-🎬-프로그램은-어디서부터-실행될까--entry-point와-런타임">14. 🎬 프로그램은 어디서부터 실행될까? – Entry Point와 런타임</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f358c500-e171-48d4-9699-45e821337cf3/image.png" /></p>
<h2 id="1-📦-함수도-나눠-쓰고-파일도-나눠-쓴다">1) 📦 함수도 나눠 쓰고, 파일도 나눠 쓴다!</h2>
<ul>
<li>프로그래머들은 자주 쓰는 함수(예: 문자열 비교, 수학 계산)를 <strong>재사용 가능한 형태로 묶어</strong> 둡니다.</li>
<li>이렇게 묶인 파일을 <strong>라이브러리(library)</strong>라고 부릅니다.</li>
<li>팀 단위 개발을 위해 하나의 프로그램도 여러 개의 <strong>소스 파일로 나누어 작성</strong>하는 경우가 많습니다.</li>
</ul>
<h2 id="2-🔗-여러-코드-조각을-하나로-묶는-과정-링크link">2) 🔗 여러 코드 조각을 하나로 묶는 과정: <strong>링크(link)</strong></h2>
<ul>
<li>여러 파일로 나뉘어 작성된 프로그램은 <strong>중간 단계 파일(매개 파일, object file)</strong>로 컴파일됩니다.</li>
<li>이를 하나로 묶어서 <strong>하나의 실행 파일(executable)</strong>을 만드는 과정을 <strong>링킹(linking)</strong>이라고 해요.</li>
<li>이 과정을 해주는 툴이 바로 <strong>링커(Linker)</strong>입니다.</li>
</ul>
<h2 id="3🧰-elf-실행-가능한-파일의-표준-형식">3)🧰 ELF: 실행 가능한 파일의 표준 형식</h2>
<blockquote>
<p>ELF(Executable and Linkable Format)는 프로그램을 여러 섹션으로 나눈 실행 파일 형식입니다.</p>
</blockquote>
<ul>
<li>📦 <strong>“팝니다” 영역</strong> → 내가 제공하는 함수 (<code>cube()</code> 같은 것)</li>
<li>🛒 <strong>“삽니다” 영역</strong> → 내가 필요한 외부 함수나 변수 (<code>printf</code>, <code>date</code> 등)</li>
</ul>
<p>링커는 이들을 <strong>서로 연결(resolve)</strong>해서 실행 가능한 형태로 만드는 역할을 합니다.</p>
<h2 id="4-🧲-정적-링크-vs-동적-링크">4) 🧲 정적 링크 vs 동적 링크</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>설명</th>
<th>장점</th>
<th>단점</th>
</tr>
</thead>
<tbody><tr>
<td><strong>정적 링크</strong></td>
<td>필요한 라이브러리를 <strong>실행 파일에 포함</strong>시킴</td>
<td>빠름, 독립 실행 가능</td>
<td>실행 파일이 커지고 중복됨</td>
</tr>
<tr>
<td><strong>동적 링크</strong></td>
<td>프로그램 실행 시 <strong>공유 라이브러리를 따로 참조</strong></td>
<td>메모리 절약, 업데이트 용이</td>
<td>실행 시점에 외부 파일 필요</td>
</tr>
</tbody></table>
<blockquote>
<p>정적 링크는 복붙,<br />동적 링크는 “공유 파일 참조”라고 생각하면 쉬워요.</p>
</blockquote>
<h2 id="5-📚-공유-라이브러리란">5) 📚 공유 라이브러리란?</h2>
<ul>
<li>여러 프로그램이 같은 라이브러리를 참조할 수 있도록 만든 <strong>공통 모듈</strong></li>
<li>동적 링크(dynamic linking)를 통해 실행 중 로드</li>
<li>메모리를 절약하고, 업데이트가 편리함</li>
</ul>
<p>📌 예시 그림 (그림 5-17)</p>
<pre><code>[ 프로그램 1 ]          [ 프로그램 2 ]
     │                         │
     └─────┐           ┌──────┘
           ↓           ↓
      [ 공통 라이브러리 ] ← MMU가 공유 관리</code></pre><blockquote>
<p>단, <strong>공유 라이브러리는 프로그램마다 독립적인 스택과 힙을 사용</strong>하도록 설계해야 합니다!</p>
</blockquote>
<h2 id="6-🎯-진입점entry-point은-첫-줄이-아니다">6) 🎯 진입점(Entry Point)은 첫 줄이 아니다?</h2>
<ul>
<li>모든 프로그램은 <strong>&quot;진입점&quot;</strong>이라는 곳에서 실행이 시작됩니다. (보통 <code>main()</code> 함수)</li>
<li>그런데 실제로는, <code>main()</code>보다 먼저 실행되는 코드가 있습니다.</li>
<li>그건 바로 <strong>런타임 라이브러리(runtime library)</strong>입니다.</li>
</ul>
<h2 id="7-⚙️-런타임-라이브러리의-역할">7) ⚙️ 런타임 라이브러리의 역할</h2>
<blockquote>
<p>프로그램 실행 직전에 준비 작업을 해주는 <strong>&quot;도우미 코드&quot;</strong>입니다.</p>
</blockquote>
<table>
<thead>
<tr>
<th>역할</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>📌 스택/힙 설정</td>
<td>메모리 레이아웃 구성</td>
</tr>
<tr>
<td>📌 정적 데이터 초기화</td>
<td>전역 변수 등 초기값 복사</td>
</tr>
<tr>
<td>📌 <code>main()</code> 호출</td>
<td>진짜 실행 시작점으로 넘김</td>
</tr>
</tbody></table>
<blockquote>
<p>고급 언어일수록 런타임 라이브러리의 역할도 많아져요 (예: 예외 처리, 객체 생성 등)</p>
</blockquote>
<h2 id="💡-한-줄-정리-1">💡 한 줄 정리</h2>
<blockquote>
<p><strong>프로그램은 여러 코드 조각과 라이브러리를 링커가 엮고, 런타임 라이브러리가 실행 환경을 마련한 후에야 진짜 실행이 시작된다.</strong></p>
</blockquote>
<h3 id="📌-용어-요약표">📌 용어 요약표</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e808dca1-a497-402f-b455-be08d4469afa/image.png" /></p>
<table>
<thead>
<tr>
<th>용어</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>라이브러리</td>
<td>자주 쓰는 함수를 모아둔 파일</td>
</tr>
<tr>
<td>링커(Linker)</td>
<td>여러 개의 오브젝트 파일을 하나의 실행 파일로 묶는 도구</td>
</tr>
<tr>
<td>ELF</td>
<td>실행 가능한 파일 포맷 (Executable and Linkable Format)</td>
</tr>
<tr>
<td>정적 링크</td>
<td>실행 파일에 직접 함수 코드 삽입</td>
</tr>
<tr>
<td>동적 링크</td>
<td>실행 중 외부 라이브러리 호출</td>
</tr>
<tr>
<td>공유 라이브러리</td>
<td>여러 프로그램이 동시에 사용하는 공통 함수 모음</td>
</tr>
<tr>
<td>런타임 라이브러리</td>
<td>프로그램 실행 전 초기화 작업을 해주는 코드 묶음</td>
</tr>
<tr>
<td>진입점(Entry Point)</td>
<td>프로그램에서 <code>main()</code> 이전에 실행되는 시작 주소</td>
</tr>
</tbody></table>
<h1 id="15-mmu로는-부족하다-세그먼테이션">15. MMU로는 부족하다 세그먼테이션</h1>
<h2 id="✅-mmumemory-management-unit와-세그멘테이션segmentation은-어떤-관계">✅ MMU(Memory Management Unit)와 세그멘테이션(Segmentation)은 어떤 관계?</h2>
<h3 id="📌-결론부터-말하자면">📌 결론부터 말하자면:</h3>
<blockquote>
<p><strong>세그멘테이션은 MMU가 수행할 수 있는 메모리 관리 방식 중 하나입니다.</strong><br />즉, <strong>MMU는 &quot;세그멘테이션&quot;이라는 방식을 구현하기 위한 하드웨어</strong>예요!</p>
</blockquote>
<h2 id="🧠-그럼-mmu가-뭐길래">🧠 그럼 MMU가 뭐길래?</h2>
<h3 id="✔️-mmu는-하드웨어-장치입니다">✔️ MMU는 하드웨어 장치입니다.</h3>
<ul>
<li><strong>Memory Management Unit</strong>: 가상 주소 → 물리 주소 변환을 담당하는 하드웨어</li>
<li>운영체제가 MMU에 설정값을 넣고, 이후 주소 변환은 MMU가 자동으로 처리</li>
</ul>
<h3 id="mmu가-할-수-있는-일들-운영체제의-설정에-따라">MMU가 할 수 있는 일들 (운영체제의 설정에 따라)</h3>
<table>
<thead>
<tr>
<th>주소 변환 방식</th>
<th>설명</th>
<th>예시</th>
</tr>
</thead>
<tbody><tr>
<td>✅ 단일 베이스/바운드</td>
<td>모든 주소에 같은 변환 적용</td>
<td>가장 단순한 방식</td>
</tr>
<tr>
<td>✅ 세그멘테이션</td>
<td>영역별(Base/Bound)로 주소 변환</td>
<td>힙, 스택, 코드 등 구분</td>
</tr>
<tr>
<td>✅ 페이징(Paging)</td>
<td>고정 크기 블록(페이지) 단위로 변환</td>
<td>현대 시스템 대부분</td>
</tr>
<tr>
<td>✅ 세그먼트+페이징</td>
<td>세그먼트를 페이지로 나눠 관리</td>
<td>Intel x86 구조 등</td>
</tr>
</tbody></table>
<blockquote>
<p>즉, <strong>MMU는 &quot;주소 변환 전략&quot;을 실행하는 하드웨어</strong>고,<br />그 전략이 &quot;세그멘테이션&quot;일 수도 있고, &quot;페이징&quot;일 수도 있고, 심지어 둘 다 쓸 수도 있어요.</p>
</blockquote>
<h2 id="✅-그럼-왜-세그멘테이션이라는-방식이-필요했을까">✅ 그럼 왜 세그멘테이션이라는 방식이 필요했을까?</h2>
<blockquote>
<p>MMU만 있다고 끝이 아닙니다.<br />MMU가 ‘어떻게 변환할 것인가’를 <strong>운영체제가 정하고</strong>, 그 방식 중 하나가 <strong>세그멘테이션</strong>이에요.</p>
</blockquote>
<h3 id="세그멘테이션이-필요한-이유">세그멘테이션이 필요한 이유:</h3>
<table>
<thead>
<tr>
<th>문제 상황</th>
<th>세그멘테이션으로 해결 가능?</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>힙/스택이 자라면서 충돌</td>
<td>✅ 해결</td>
<td>서로 다른 세그먼트로 나눔</td>
</tr>
<tr>
<td>프로그램마다 다른 메모리 구조</td>
<td>✅ 해결</td>
<td>코드/데이터/스택 분리 가능</td>
</tr>
<tr>
<td>코드 공유 (메모리 절약)</td>
<td>✅ 해결</td>
<td>코드 세그먼트를 읽기 전용으로 공유</td>
</tr>
<tr>
<td>유연한 주소 공간</td>
<td>✅ 해결</td>
<td>각 세그먼트마다 독립된 물리 위치 허용</td>
</tr>
<tr>
<td>접근 권한 제어</td>
<td>✅ 해결</td>
<td>읽기/쓰기/실행 권한 비트 설정 가능</td>
</tr>
</tbody></table>
<h2 id="✅-페이징-vs-세그멘테이션은-경쟁-관계일까">✅ 페이징 vs 세그멘테이션은 경쟁 관계일까?</h2>
<blockquote>
<p>❌ 경쟁이라기보단, <strong>각자 장단점이 다르고, 때로는 함께 쓰이기도 합니다!</strong></p>
</blockquote>
<table>
<thead>
<tr>
<th>방식</th>
<th>장점</th>
<th>단점</th>
</tr>
</thead>
<tbody><tr>
<td><strong>세그멘테이션</strong></td>
<td>논리적 구조 구분 쉬움, 유연한 크기</td>
<td>외부 단편화 발생 가능</td>
</tr>
<tr>
<td><strong>페이징</strong></td>
<td>내부 단편화 줄이고, 메모리 활용 효율적</td>
<td>논리적 구조 파악 어려움</td>
</tr>
<tr>
<td><strong>혼합 방식</strong></td>
<td>세그먼트를 페이지로 나눔</td>
<td>x86에서 사용</td>
</tr>
</tbody></table>
<h2 id="✅-실제-시스템은-어떻게-했을까">✅ 실제 시스템은 어떻게 했을까?</h2>
<table>
<thead>
<tr>
<th>시스템</th>
<th>방식</th>
</tr>
</thead>
<tbody><tr>
<td>초창기 시스템</td>
<td>단순 MMU + 단일 Base/Bound</td>
</tr>
<tr>
<td>중간 단계 시스템</td>
<td>MMU + 세그멘테이션 (x86 초기)</td>
</tr>
<tr>
<td>현대 OS (Linux, Windows)</td>
<td>MMU + 페이징 방식</td>
</tr>
<tr>
<td>고급 시스템</td>
<td>MMU + 세그멘테이션 + 페이징 (x86 호환 아키텍처 등)</td>
</tr>
</tbody></table>
<h2 id="💡-비유로-이해해보자">💡 비유로 이해해보자</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/69e1e354-ddd7-4db9-8f87-6ecd9f0cf250/image.png" /></p>
<ul>
<li><strong>MMU</strong>는 주소를 바꿔주는 <strong>네비게이션 시스템</strong>  </li>
<li><strong>세그멘테이션</strong>은 목적지를 <strong>구역별로 나누는 지도 방식</strong>  </li>
<li><strong>페이징</strong>은 지도를 <strong>블록 단위로 잘게 자른 방식</strong></li>
</ul>
<p>👉 운영체제가 &quot;이렇게 주소 관리하자&quot;라고 지시하면,<br />MMU는 그 방식에 맞게 <strong>빠르게 변환을 수행</strong>합니다.</p>
<h2 id="🔧-예시로-비교하면">🔧 예시로 비교하면</h2>
<h3 id="mmu-단독-단일-basebound">MMU 단독 (단일 Base/Bound):</h3>
<pre><code>가상 주소 = 1234
물리 주소 = Base + 1234 (단 하나의 Base만 존재)</code></pre><h3 id="세그멘테이션-사용-시-mmu--세그먼트">세그멘테이션 사용 시 (MMU + 세그먼트):</h3>
<pre><code>가상 주소 = [세그먼트 번호: 01][오프셋: 0345]
→ 세그먼트 1의 Base + 오프셋 = 물리 주소</code></pre><h2 id="🧩-최종-정리">🧩 최종 정리</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>역할</th>
</tr>
</thead>
<tbody><tr>
<td>MMU</td>
<td>주소 변환을 <strong>수행</strong>하는 하드웨어</td>
</tr>
<tr>
<td>세그멘테이션</td>
<td>MMU가 사용할 수 있는 <strong>주소 변환 방식 중 하나</strong></td>
</tr>
<tr>
<td>운영체제</td>
<td>어떤 방식으로 주소를 변환할지 결정하고 MMU를 설정</td>
</tr>
</tbody></table>
<h3 id="✅-한-줄-요약">✅ 한 줄 요약</h3>
<blockquote>
<p><strong>MMU는 주소를 바꿔주는 기계이고, 세그멘테이션은 그 기계가 따르는 규칙이다.</strong></p>
</blockquote>
<h1 id="✅-요약-표-5장-핵심-정리">✅ 요약 표: 5장 핵심 정리</h1>
<table>
<thead>
<tr>
<th>키워드</th>
<th>개념 요약</th>
</tr>
</thead>
<tbody><tr>
<td>컴퓨터 구조</td>
<td>폰 노이만 vs 하버드 (명령어/데이터 메모리 분리 여부)</td>
</tr>
<tr>
<td>멀티코어</td>
<td>전력 문제 해결책으로 등장한 다중 코어 시스템</td>
</tr>
<tr>
<td>MMU</td>
<td>가상 주소 ↔ 물리 주소 매핑 장치, 프로그램 격리 가능</td>
</tr>
<tr>
<td>스택</td>
<td>함수 호출/복귀를 위한 LIFO 저장소</td>
</tr>
<tr>
<td>인터럽트</td>
<td>외부 이벤트 처리 (예: 초인종) 시스템</td>
</tr>
<tr>
<td>가상 메모리</td>
<td>실제보다 더 큰 메모리를 제공하는 환상 시스템</td>
</tr>
<tr>
<td>스와핑</td>
<td>필요 없는 페이지를 디스크로 이동시키는 전략</td>
</tr>
<tr>
<td>시스템 공간</td>
<td>운영체제 전용, 사용자 프로그램과 분리</td>
</tr>
<tr>
<td>캐시</td>
<td>L1~L3 계층 구조, 속도와 용량의 균형</td>
</tr>
<tr>
<td>링커</td>
<td>여러 코드 조각을 하나로 묶어 실행 파일 생성</td>
</tr>
</tbody></table>
<blockquote>
<p>남은 것은 I/O뿐인데, 이 주제를 6장에서 다
룬다.</p>
</blockquote>
<h1 id=""></h1>
<h1 id="출처">출처</h1>
<ul>
<li><a href="https://imjeongwoo.tistory.com/152">https://imjeongwoo.tistory.com/152</a></li>
</ul>