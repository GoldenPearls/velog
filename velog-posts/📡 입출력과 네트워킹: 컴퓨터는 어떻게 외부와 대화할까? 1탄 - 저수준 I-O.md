<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3dfdbb65-f7fd-42c4-b724-d624c05cd8ec/image.png" /></p>
<h1 id="🧠-들어가며-컴퓨터는-세상과-소통하는-기계다">🧠 들어가며: 컴퓨터는 세상과 소통하는 기계다</h1>
<p>여러분, 컴퓨터가 단지 계산만 하는 도구라고 생각하셨나요? 사실 컴퓨터는 <strong>외부 세계와의 대화</strong>를 위해 존재한다고 해도 과언이 아닙니다. 사람과 대화하고, 공장을 움직이고, 센서로 데이터를 수집하며, 다른 컴퓨터와 통신하기도 하죠.</p>
<p>그 중심에는 <strong>입출력(I/O)</strong> 장치가 있습니다. 오늘은 컴퓨터가 어떻게 현실의 데이터를 받고, 계산하고, 다시 현실로 신호를 내보내는지를 이야기해보겠습니다.</p>
<h1 id="🧲-입력과-출력-세상과의-접점">🧲 입력과 출력: 세상과의 접점</h1>
<h2 id="기본적인-io-회로-래치와-트라이스테이트-버퍼">기본적인 I/O 회로: 래치와 트라이스테이트 버퍼</h2>
<p>앞 장에서 프로세서 코어로 들어오고 나가는 데이터를 언급하면서 언급한 적이 있었어요. 이런 입출력은 그리 어렵지 않습니다. </p>
<p>왜냐, 필요한 것은 <strong>출력을 위한</strong> <code>래치</code>와 <strong>입력을 위한</strong> <code>트라이스테이트 버퍼</code>뿐이다. </p>
<ul>
<li><strong>출력용 래치(Latch)</strong>는 상태를 유지하는 작은 기억소자입니다.</li>
<li><strong>입력용 트라이스테이트 버퍼(Three-state buffer)</strong>는 데이터를 전송할지 말지를 제어할 수 있는 회로예요.</li>
<li>초창기 컴퓨터는 <strong>모든 I/O 핀을 CPU가 직접 제어</strong>했어요. 
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e7c5ea93-261c-4147-90ce-19a9b1b0333b/image.png" /></li>
</ul>
<p>지금은 다릅니다. <strong>I/O 장치 안에 자체 프로세서가 있어서, 바이트 단위로 읽고 쓰기만 하면 되죠.</strong></p>
<p>이게 바로 프로세서 가격이 줄어들면서 이런 상황이 달라졌습니다.</p>
<blockquote>
<p>이번 글은 I/O 장치와 상호작용하는 기술을 다룹니다. 그리고 샘플링sampling에 대해 설명에 대해 설명합니다.</p>
</blockquote>
<h1 id="🔌-컴퓨터와-led의-대화-포트-b에-얽힌-소소한-이야기">🔌 컴퓨터와 LED의 대화: 포트 B에 얽힌 소소한 이야기</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/90b9392f-0e8d-4a56-a7c1-7fef514b7dc2/image.png" /></p>
<h2 id="1-💬-컴퓨터가-외부와-대화하는-방식">1) 💬 컴퓨터가 외부와 대화하는 방식</h2>
<p>옛날 옛적, 컴퓨터 속 작은 마을에 'CPU'라는 친구가 살고 있었어요. 이 친구는 계산도 잘하고, 명령도 척척 내리는 아주 똑똑한 친구였죠. 그런데, 아무리 머리가 좋아도 세상과 단절돼 있다면 아무 소용이 없잖아요?</p>
<p>그래서 CPU는 외부와 소통할 수 있는 방법을 찾게 되었어요. 바로, <strong>I/O 포트</strong>라는 대화창을 통해서요!</p>
<h2 id="2-💡-led와의-첫-만남-포트-b">2) 💡 LED와의 첫 만남: 포트 B</h2>
<p>CPU가 세상 밖으로 첫 손을 내민 곳은 <strong>포트 B</strong>라는 창구였어요. 포트 B에는 총 8개의 작은 문(PB0 ~ PB7)이 있고, 여기에 <strong>LED</strong>와 <strong>스위치</strong>가 연결되어 있었답니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8196522b-8435-4d76-bf37-4af6b860341c/image.png" /></p>
<pre><code>[CPU] ─── PB0 ───&gt; 💡 LED (빛을 내는 친구)
[CPU] &lt;── PB7 ─── 🔘 스위치 (누르면 반응하는 친구)</code></pre><h3 id="그런데-잠깐">그런데 잠깐!</h3>
<p><strong>LED는 단순한 친구가 아니에요.</strong><br />LED는 <strong>다이오드</strong>라고 불리는 반도체의 일종으로, 꼭 한 방향으로만 전기를 받겠다고 고집을 부려요. 마치 놀이공원의 회전문처럼요.</p>
<h2 id="3-⚡-안전하게-빛내기-저항이라는-조력자">3) ⚡ 안전하게 빛내기: 저항이라는 조력자</h2>
<p>그런데 말이죠, CPU가 힘껏 전기를 보내다 보면 LED가 &quot;앗 뜨거!&quot; 하며 타버릴 수도 있어요. 그래서 CPU는 <strong>저항</strong>이라는 조력자 친구를 사이에 넣었어요.</p>
<p>이 저항은 전류의 속도를 조절해주는 역할을 합니다.  </p>
<blockquote>
<p>“자자~ 너무 세게 보내면 다쳐요~” 라고 말하면서요.</p>
</blockquote>
<h3 id="계산도-필요하죠">계산도 필요하죠!</h3>
<ul>
<li>전압: 5V (CPU가 보내는 힘)</li>
<li>LED가 감당할 수 있는 전압: 0.7V  </li>
<li>원하는 전류: 10mA (0.01A)</li>
</ul>
<p>옴의 법칙에 따라 계산하면,<br /><strong>(4.2V - 0.7V) ÷ 0.01A = 350Ω</strong><br />즉, <strong>350Ω짜리 저항</strong>이 필요해요!</p>
<h2 id="4-🧠-포트-b의-세-가지-역할">4) 🧠 포트 B의 세 가지 역할</h2>
<p>이제 CPU는 포트 B를 제어하기 위해 3명의 친구를 부르기로 했어요:</p>
<table>
<thead>
<tr>
<th>레지스터 이름</th>
<th>하는 일</th>
</tr>
</thead>
<tbody><tr>
<td><strong>DDRB</strong></td>
<td>입력이냐 출력이냐 정함 (방향 설정자)</td>
</tr>
<tr>
<td><strong>PORTB</strong></td>
<td>출력 데이터를 저장 (출발 신호)</td>
</tr>
<tr>
<td><strong>PINB</strong></td>
<td>입력 데이터를 읽음 (수신 담당)</td>
</tr>
</tbody></table>
<p>이 친구들은 함께 작동해서 다음과 같은 시나리오를 연출해요.</p>
<h3 id="시나리오-🎭">시나리오 🎭</h3>
<ol>
<li><strong>DDRB에 1을 쓰면</strong> → 그 핀은 &quot;출력용&quot;이 됨  </li>
<li><strong>PORTB에 1을 쓰면</strong> → 핀에 전기가 흐르고, LED가 “짠~” 하고 켜짐  </li>
<li><strong>PINB를 읽으면</strong> → 버튼이 눌렸는지 여부를 알 수 있음</li>
</ol>
<p>즉, CPU는 <strong>&quot;PORTB0(PBo) = 1;&quot;</strong> 이렇게 한 줄만 써도, LED에게 &quot;불 켜!&quot;라고 말할 수 있는 거죠.</p>
<blockquote>
<p>장치에 따라 전압 강하 등 이 달라질 수 있기 때문에 사용하려는 LED나 다른 구성요소의 데이터시트를 꼭 읽어봐야 한답니다.</p>
</blockquote>
<h2 id="5-🛠️-안에-뭐가-들었을까-avr-포트-b-내부-구조">5) 🛠️ 안에 뭐가 들었을까? (AVR 포트 B 내부 구조)</h2>
<p>사실 이 회로 안을 들여다보면, 전혀 복잡하지 않아요. 익숙한 <strong>플립플롭</strong>, <strong>디먹스</strong>, <strong>트라이스테이트 버퍼</strong>들이 서로 조화를 이루며 돌아갑니다.</p>
<h4 id="여기서-잠깐-🛠️-플립플롭-디먹스-트라이스테이트-버퍼-기억이-안나는-나를-위한-정리">여기서 잠깐 🛠️ <strong>플립플롭</strong>, <strong>디먹스</strong>, <strong>트라이스테이트 버퍼</strong> 기억이 안나는 나를 위한 정리!</h4>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/fd9d05d2-fd1c-4bb0-87f7-2b7e04335e34/image.png" /></p>
<table>
<thead>
<tr>
<th>항목</th>
<th><strong>플립플롭 (Flip-Flop)</strong></th>
<th><strong>디먹스 (DeMUX)</strong></th>
<th><strong>트라이스테이트 버퍼 (Tri-State Buffer)</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>기본 기능</strong></td>
<td>1비트 저장 (메모리 역할)</td>
<td>하나의 입력을 여러 출력 중 하나로 전달</td>
<td>출력할지 말지 제어 가능한 버퍼</td>
</tr>
<tr>
<td><strong>용도</strong></td>
<td>레지스터, 상태 저장</td>
<td>신호 분배, 주소 지정</td>
<td>버스 제어, 공유 회로에서 출력 관리</td>
</tr>
<tr>
<td><strong>제어 입력</strong></td>
<td>클럭(Clock) 신호</td>
<td>선택(select) 신호</td>
<td>출력 활성화(Enable) 신호</td>
</tr>
<tr>
<td><strong>출력 상태</strong></td>
<td>항상 출력 유지 (Q, ~Q)</td>
<td>선택된 한 출력을 High or Low로 설정</td>
<td>High, Low, 혹은 High Impedance (Z)</td>
</tr>
<tr>
<td><strong>대표 회로</strong></td>
<td>D 플립플롭, JK 플립플롭</td>
<td>1→4 디먹스, 1→8 디먹스 등</td>
<td>제어 가능한 버퍼</td>
</tr>
<tr>
<td><strong>비유</strong></td>
<td>&quot;기억하는 친구&quot; – 말한 걸 잊지 않음</td>
<td>&quot;우체국 직원&quot; – 하나의 편지를 골라 보냄</td>
<td>&quot;출입문 관리자&quot; – 문을 열지 닫을지 결정</td>
</tr>
<tr>
<td><strong>심볼(기호)</strong></td>
<td>🧠</td>
<td>📬</td>
<td>🚪</td>
</tr>
</tbody></table>
<blockquote>
<ul>
<li><strong>플립플롭</strong>: &quot;나는 기억력이 좋아! 한 번 들은 건 클럭 신호로 저장해둬!&quot;</li>
</ul>
</blockquote>
<ul>
<li><strong>디먹스</strong>: &quot;어디로 보내줄까? 선택한 곳 하나만 열어줄게.&quot;</li>
<li><strong>트라이스테이트 버퍼</strong>: &quot;나 지금 출력할지 말지 결정 중이야. Enable 되면 말할게!&quot;</li>
</ul>
<ol>
<li><p><strong>플립플롭 → 레지스터</strong></p>
<ul>
<li>📌 <strong>“레지스터는 플립플롭으로 구성되어 있다.”</strong>  </li>
<li>→ 각각의 플립플롭이 1비트 저장, 여러 개 모이면 8비트, 16비트 레지스터!</li>
</ul>
</li>
<li><p><strong>트라이스테이트 버퍼 → 공유 버스 제어</strong></p>
<ul>
<li>📌 <strong>“멀티프로세서 버스에서는 트라이스테이트 버퍼가 핵심이다.”</strong>  </li>
<li>→ 여러 장치가 하나의 버스를 사용할 때, 동시에 신호를 내지 않도록 조율하는 '출입문 관리자'</li>
</ul>
</li>
<li><p><strong>디먹스 → 멀티플렉싱 응용</strong></p>
<ul>
<li>📌 <strong>“디먹스는 1개의 신호로 여러 개의 LED를 순차적으로 켜기로 멀티플렉싱에 응용된다.”</strong>  </li>
<li>→ 빠르게 순서를 바꿔가며 하나씩 켜서, 사람 눈에는 동시에 켜진 것처럼 보이게 하는 기법 (잔상 효과 활용!)</li>
</ul>
</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/bd4a2fdb-fa6b-471f-9b43-46a07eea2f4e/image.png" /></p>
<pre><code>[DDRB] → 이건 방향을 정해줘요
[PORTB] → 여기에 데이터를 써요
[PINB] → 여기에 상태가 보여요</code></pre><p>CPU는 주소버스를 타고 이 레지스터들을 찾아가 데이터를 주고받습니다. 마치 도서관에서 책을 찾아가는 것처럼요.</p>
<h2 id="6-💡-실생활-예제-led-깜빡이기">6) 💡 실생활 예제: LED 깜빡이기</h2>
<pre><code class="language-c">DDRB |= (1 &lt;&lt; PB0);    // PB0을 출력으로 설정
while (1) {
  PORTB |= (1 &lt;&lt; PB0);  // PB0에 1: 불 켜기
  _delay_ms(500);
  PORTB &amp;= ~(1 &lt;&lt; PB0); // PB0에 0: 불 끄기
  _delay_ms(500);
}</code></pre>
<p>이렇게 간단한 코드 하나로, <strong>LED는 마치 신호등처럼 깜빡이기 시작합니다.</strong></p>
<h2 id="📝-요약하자면">📝 요약하자면!</h2>
<table>
<thead>
<tr>
<th>포인트</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>포트 B</strong></td>
<td>CPU가 외부와 소통하는 창구</td>
</tr>
<tr>
<td><strong>DDRB</strong></td>
<td>포트의 방향(입력/출력)을 결정</td>
</tr>
<tr>
<td><strong>PORTB</strong></td>
<td>출력을 위한 전압을 설정</td>
</tr>
<tr>
<td><strong>PINB</strong></td>
<td>입력 상태를 읽는 창구</td>
</tr>
<tr>
<td><strong>LED 회로 구성</strong></td>
<td>저항과 직렬 연결 필수 (350Ω 등)</td>
</tr>
<tr>
<td><strong>실전 코드</strong></td>
<td>불 켜고 끄는 타이밍 제어 가능</td>
</tr>
</tbody></table>
<blockquote>
<p>“컴퓨터는 세상을 계산으로만 이해하지 않아요. 손을 내밀고, 신호를 주고받으며, 진짜로 ‘대화’를 나누고 있는 거랍니다.”</p>
</blockquote>
<h1 id="🎛️-버튼은-왜-말을-더듬을까--디바운싱의-비밀">🎛️ 버튼은 왜 말을 더듬을까? – 디바운싱의 비밀**</h1>
<h2 id="1-🧑💻-컴퓨터야-나-눌렀어-버튼의-신호는-정말-단순할까">1) 🧑‍💻 “컴퓨터야, 나 눌렀어!” 버튼의 신호는 정말 단순할까?</h2>
<p>여러분, 우리가 어떤 기기를 사용할 때 &quot;딸깍&quot; 누르는 그 <strong>버튼</strong>,  
컴퓨터는 그걸 정말 한 번만 눌렀다고 알아들을까요?</p>
<blockquote>
<p><strong>절대 아닙니다.</strong><br />실제로는 이렇게 말하거든요:</p>
</blockquote>
<blockquote>
<p>“눌렀...어..? 아니 눌렀다니까! 어...? 다시 눌렀나...? 아냐아냐 지금 눌렀지...!”</p>
</blockquote>
<p>이 현상을 우리는 <strong>바운스(bounce)</strong>라고 불러요.</p>
<h2 id="2-🔩-버튼-속-금속-접점의-튀는-성격">2) 🔩 버튼 속 금속 접점의 튀는 성격</h2>
<p>버튼 안에는 아주 작은 금속 조각이 있어요.<br />이 조각이 버튼을 누르면 '찰싹!' 접점에 붙어서 회로가 닫히고 전류가 흐르게 되죠.<br />그런데 문제는… <strong>이 금속 조각이 성질이 급해서</strong>,  
접촉할 때 “찰싹찰싹찰싹” 튀는 현상이 생깁니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0f3a6780-8992-4f67-a77e-00f665054794/image.png" /></p>
<p>이게 바로 <strong>신호가 몇 밀리초 동안 '0→1→0→1→0'으로 튀는 바운스 현상</strong>이에요.</p>
<h2 id="3-🚨-인터럽트로-연결하면-더-골치-아파져요">3) 🚨 인터럽트로 연결하면 더 골치 아파져요!</h2>
<p>대부분의 시스템은 버튼을 <strong>인터럽트 핀(IRQ)</strong>에 연결해요.<br />“이벤트 발생 시 바로 반응하라”는 의미죠.</p>
<p>그런데 버튼을 한 번만 눌렀는데…  </p>
<blockquote>
<p>💣 인터럽트가 두 번, 세 번, 네 번이나 호출되는 거예요!</p>
</blockquote>
<p>CPU 입장에선 <strong>버튼 하나 눌렀을 뿐인데 마치 스팸처럼 연속 호출당하는 셈이죠.</strong></p>
<h2 id="4-🧘♀️-그럼-어떻게-잠잠하게-만들까--디바운싱-기법-등장">4) 🧘‍♀️ 그럼 어떻게 잠잠하게 만들까? – 디바운싱 기법 등장</h2>
<p>바운스를 잠재우기 위한 방법은 바로 <strong>디바운싱(debouncing)</strong>이에요.  </p>
<blockquote>
<p>즉, “이 녀석이 정말 제대로 눌린 건지, 한동안 잠잠한지”를 확인하는 거예요.</p>
</blockquote>
<h3 id="✅-디바운싱-방법-1-타이머-지연">✅ 디바운싱 방법 1: 타이머 지연</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e43d4d35-7fb7-4e03-b754-020193c39cff/image.png" /></p>
<ol>
<li>버튼이 눌림 (인터럽트 발생)</li>
<li>바로 처리하지 않고, <strong>타이머로 잠깐 기다려요</strong> (예: 10ms)</li>
<li>그 뒤에 상태가 그대로면 “아~ 진짜 눌렸구나!” 판단</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7f194bc9-5931-4e63-870e-86ea76dc68b8/image.png" /></p>
<blockquote>
<p>🔔 하지만 이 방법은 <strong>정확한 시간 설정이 어려워요.</strong>  </p>
</blockquote>
<p>버튼이 닳거나 기기 종류에 따라 바운스 시간이 다르기 때문이죠.</p>
<p>아주 좋은 질문이에요! 이 문장은 조금 복잡하게 들릴 수 있지만, <strong>핵심은 ‘버튼이 여러 개여도, 인터럽트 핀은 부족하다 → 그래서 소프트웨어로 처리하자’는 이야기</strong>입니다. 더 친절하게 풀어볼게요 😊</p>
<h4 id="🔌-상황-정리-버튼은-많은데-인터럽트-핀은-적다">🔌 상황 정리: 버튼은 많은데, 인터럽트 핀은 적다?</h4>
<ol>
<li>현실적인 문제</li>
</ol>
<ul>
<li>하나의 마이크로컨트롤러(예: AVR, ARM 등)에는 <strong>인터럽트를 받을 수 있는 핀(IRQ 핀)</strong>이 <strong>한정되어 있어요</strong>.</li>
<li>그런데 여러분이 실제로 만들 장치에는 <strong>버튼이 2개, 4개, 10개, 심지어 수십 개</strong>일 수도 있죠!</li>
</ul>
<blockquote>
<p>❗ 그럼 버튼마다 IRQ 핀을 연결할 수 없겠죠?</p>
</blockquote>
<p><strong>💡 해결책 1: 하드웨어적 공유 (복잡, 비용 증가)</strong></p>
<ul>
<li><strong>하드웨어 회로를 설계해서 인터럽트 신호를 묶어주는 방법</strong>도 있어요.</li>
<li>하지만 이건 <strong>회로도 복잡해지고</strong>, 부품도 늘어나니까 <strong>비용이 올라가요</strong>.</li>
</ul>
<p><strong>🧠 해결책 2: 소프트웨어로 똑똑하게 처리 (👍 추천 방식)</strong></p>
<blockquote>
<p><strong>“인터럽트 핀을 버튼마다 따로 두는 대신, 타이머 인터럽트를 활용해서 모든 버튼을 소프트웨어로 주기적으로 검사하자!”</strong></p>
</blockquote>
<p><strong>어떻게 하냐고요?</strong></p>
<ul>
<li>대부분의 시스템에는 이미 <strong>타이머 인터럽트</strong>라는 것이 있어요.</li>
<li>예: <strong>1밀리초마다 인터럽트를 발생</strong>하도록 설정 가능.</li>
</ul>
<blockquote>
<p>이 타이머 인터럽트가 발생할 때마다 모든 버튼들의 상태를 한 번씩 확인하는 거예요.
그리고 <strong>FIR 필터 방식</strong>이나 <strong>단순 비교 방식</strong>으로 <strong>바운스를 제거하면서 버튼의 눌림을 감지</strong>하는 거죠.</p>
</blockquote>
<p><strong>📦 비유해볼까요?</strong></p>
<p>원래는 버튼이 눌릴 때마다 &quot;나 눌렸어!&quot; 하고 <strong>직접 CPU를 깨웠는데</strong>,  
이제는 <strong>주기적으로 순찰 도는 감시 로봇</strong>이 와서 “얘 눌렸니?” 하고 체크해주는 방식이 되는 거예요.</p>
<blockquote>
<p><strong>버튼이 많아도, 인터럽트 핀은 적으니 → 이미 있는 ‘타이머 인터럽트’에 슬쩍 더부살이하면서, 모든 버튼을 소프트웨어로 주기적으로 검사해서 디바운싱까지 처리하자!</strong></p>
</blockquote>
<h3 id="✅-디바운싱-방법-2-fir-필터를-이용한-소프트웨어-큐-방식">✅ 디바운싱 방법 2: FIR 필터를 이용한 소프트웨어 큐 방식</h3>
<p>이 방법은 <strong>간단하지만 강력한 무기</strong>에요.<br />바로 <strong>FIR 필터 큐(Finite Impulse Response Queue)</strong>를 이용하는 방식이죠.</p>
<p>물론입니다! 😊 지금까지 설명한 <strong>현대 I/O 디바운싱 방식들</strong>을 한눈에 보기 쉽게 정리해드릴게요.</p>
<h3 id="✅-현대-시스템에서-버튼-디바운싱-처리-방식-총정리">✅ <strong>현대 시스템에서 버튼 디바운싱 처리 방식 총정리</strong></h3>
<table>
<thead>
<tr>
<th>분류</th>
<th>방식</th>
<th>주요 특징</th>
<th>사용 사례</th>
</tr>
</thead>
<tbody><tr>
<td>🧰 <strong>하드웨어 방식</strong></td>
<td><strong>슈미트 트리거(Schmitt Trigger)</strong> <br /> 논리 게이트(74HC14 등)</td>
<td>- 물리적 전압 임계값 설정<br />- 회로 레벨에서 튐 제거<br />- 빠르고 안정적</td>
<td>키보드, 마우스, 산업용 버튼</td>
</tr>
<tr>
<td>🧠 <strong>MCU 펌웨어 방식</strong></td>
<td><strong>타이머/카운터 기반 디바운싱</strong></td>
<td>- 버튼 눌림 후 일정 시간 대기<br />- 일정 시간 동안 같은 상태 유지 시 ‘안정’ 판단</td>
<td>데스크탑 키보드, 게임패드, 리모컨</td>
</tr>
<tr>
<td>🔄 <strong>소프트웨어 필터</strong></td>
<td><strong>FIR 필터 (큐 기반)</strong></td>
<td>- 일정 시간 동안의 입력 상태를 큐에 저장<br />- OR/XOR 등으로 변화 판단</td>
<td>아두이노, AVR, 저가형 임베디드</td>
</tr>
<tr>
<td>📊 <strong>디지털 필터링</strong></td>
<td><strong>이동 평균, 상태 머신(FSM)</strong></td>
<td>- 시간 기반 패턴 분석<br />- 여러 상태를 두고 천천히 전이</td>
<td>스마트워치, 스마트홈 디바이스</td>
</tr>
<tr>
<td>📱 <strong>터치 기반 입력</strong></td>
<td><strong>노이즈 필터 + 제스처 인식</strong></td>
<td>- 접촉 시간, 면적, 연속성 고려<br />- 제스처 구분(탭/스와이프 등)</td>
<td>스마트폰, 태블릿, 터치 패널</td>
</tr>
</tbody></table>
<h3 id="🔑-핵심-요약-한줄씩">🔑 핵심 요약 한줄씩!</h3>
<ul>
<li><strong>FIR 필터</strong>는 소프트웨어에서 가장 간단하면서도 강력한 방식! (교육용, DIY에서 자주 사용)</li>
<li><strong>슈미트 트리거</strong>는 회로 자체에서 튐을 차단해주는 &quot;물리적 진정제&quot;</li>
<li><strong>MCU 펌웨어 기반 타이머</strong>는 버튼마다 인터럽트를 쓰기 어려울 때 가장 널리 쓰임</li>
<li><strong>FSM/디지털 필터</strong>는 고급 기기에서 예측 가능한 입력만 받아들이도록 설계</li>
<li><strong>터치 디바이스</strong>는 바운스를 넘어서 &quot;사용자의 의도&quot;까지 해석해야 함</li>
</ul>
<blockquote>
<p>“바운스는 기술이 발전해도 여전히 존재하지만,<br />이제는 하드웨어와 소프트웨어가 함께 손잡고, 똑똑하게 잡아내고 있답니다!”</p>
</blockquote>
<h2 id="5-📦-fir-필터-디바운서-큐에서-입을-모으는-친구들">5) 📦 FIR 필터 디바운서: 큐에서 입을 모으는 친구들</h2>
<h3 id="🧩-상황-버튼이-8개나-있어요">🧩 상황: 버튼이 8개나 있어요!</h3>
<ul>
<li>예를 들어, 포트 B에 <strong>8개의 버튼</strong>이 물려 있다고 상상해보세요.</li>
<li>이 버튼들의 상태는 <code>INB</code>라는 <strong>8비트 변수</strong>로 읽혀요.<ul>
<li>예: <code>INB = 0b01000100</code> → 2번과 6번 버튼이 눌림</li>
</ul>
</li>
</ul>
<p>그런데 문제는...</p>
<blockquote>
<p>이 버튼들도 <strong>각자 바운스를 심하게 해요!</strong></p>
</blockquote>
<h3 id="💥-문제-8개의-버튼이-동시에-말-더듬기-시작하면">💥 문제: 8개의 버튼이 동시에 말 더듬기 시작하면?</h3>
<p>CPU는 정말 헷갈립니다.<br />“누가 진짜로 눌린 거야? 누가 헛소리 한 거야?”</p>
<h3 id="✅-해결책-fir-필터-큐로-전체-버튼-상태를-안정화시키자">✅ 해결책: FIR 필터 큐로 전체 버튼 상태를 안정화시키자!</h3>
<p>버튼 상태를 읽는 순간마다 이렇게 저장한다고 상상해볼게요:</p>
<pre><code>[1틱 전: 1] → [2틱 전: 1] → [3틱 전: 0] → [4틱 전: 1] ...</code></pre><p>각각을 배열(filter[0], filter[1], ...)에 저장하면서,<br /><strong>계속 오른쪽으로 이동하며 최신 값을 업데이트</strong>하는 거예요.</p>
<p>마치 <strong>회의 중 여러 명이 손을 들고 있고</strong>,  
&quot;이번에 진짜 눌렀는지&quot;를 결정할 때는 이렇게 묻는 거죠:</p>
<blockquote>
<p>“자자~ 다 같이 손 들었으면 진짜 눌린 거야!”</p>
</blockquote>
<p>모든 값을 OR 연산하면 <strong>한 번이라도 1이 있으면 1로 인식</strong>하고,<br />그걸 current 값으로 넣고, 이전 상태(previous)와 비교해서 <strong>진짜 변화가 있었는지</strong> 확인합니다.</p>
<h3 id="🧑💻-코드와-의미-해석">🧑‍💻 코드와 의미 해석</h3>
<pre><code class="language-c">unsigned char filter[FILTER_SIZE];
unsigned char changed;
unsigned char current;
unsigned char previous;

previous = current;
current = 0;

// 큐의 값들을 하나씩 밀면서 최신 값을 업데이트
for (int i = FILTER_SIZE - 1; i &gt; 0; i--) {
    filter[i] = filter[i - 1];
    current |= filter[i]; // OR 연산으로 하나라도 1이면 1
}
filter[0] = INB;
current |= filter[0];

// 이전 상태와 비교하여 진짜로 바뀌었는지 확인
changed = current ^ previous;</code></pre>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>INB</code></td>
<td>현재 버튼 8개의 입력 상태 (예: <code>0b01010001</code>)</td>
</tr>
<tr>
<td><code>filter[]</code></td>
<td>이전 입력 상태들이 담긴 큐 (FIFO 구조)</td>
</tr>
<tr>
<td><code>current</code></td>
<td>최근 입력을 기반으로 정제된 ‘안정된 상태’</td>
</tr>
<tr>
<td><code>previous</code></td>
<td>이전 틱의 <code>current</code> 상태</td>
</tr>
<tr>
<td><code>changed</code></td>
<td>이번 틱과 저번 틱 비교 → 누가 눌렸거나 뗐는지 감지</td>
</tr>
</tbody></table>
<h3 id="🎨-시각적-흐름-요약">🎨 시각적 흐름 요약</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/cb375ff0-7dd6-41ec-b9af-b6b19fd760a4/image.png" /></p>
<pre><code>[INB] → filter[0] → filter[1] → filter[2] ... → OR → current
                         ↓
                   previous와 XOR
                         ↓
                   changed 발생 여부</code></pre><h3 id="✨-요약-정리">✨ 요약 정리</h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td><strong>문제</strong></td>
<td>버튼을 누르면 접점이 튀면서 여러 번 눌린 것처럼 인식됨 (바운스 현상)</td>
</tr>
<tr>
<td><strong>원인</strong></td>
<td>금속 조각이 반동으로 접촉/비접촉 반복</td>
</tr>
<tr>
<td><strong>타이머 기반 해결</strong></td>
<td>인터럽트 후 잠시 기다리고 상태 확인</td>
</tr>
<tr>
<td><strong>FIR 필터 방식</strong></td>
<td>일정 기간 동안 값을 큐에 저장하고 OR + XOR로 변화 감지</td>
</tr>
<tr>
<td><strong>장점</strong></td>
<td>낡은 버튼에도 강건, 여러 버튼 동시 처리 가능</td>
</tr>
</tbody></table>
<blockquote>
<p><strong>“버튼도 말을 더듬는다. 하지만 컴퓨터는 충분히 인내심이 있어서, 다 듣고 나서야 ‘진짜 눌렀다’고 믿어준다.”</strong></p>
</blockquote>
<hr />
<h1 id="📟-7세그먼트-디스플레이-어떻게-작동할까">📟 7세그먼트 디스플레이, 어떻게 작동할까?</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2e271363-6bf4-429f-856c-5a0757a78ff2/image.png" /></p>
<h2 id="🧱-1-단순한-화면도-복잡한-기술이-숨어-있다">🧱 1) 단순한 화면도, 복잡한 기술이 숨어 있다</h2>
<p>우리가 흔히 보는 <strong>알람시계, 전자레인지, 세탁기</strong>의 숫자 표시창은<br />PC 모니터 같은 복잡한 디스플레이가 아니라, <strong>7세그먼트 디스플레이</strong>라는 간단한 장치를 사용합니다.</p>
<p>이런 디스플레이는 복잡한 그래픽 없이도 <strong>숫자나 간단한 기호</strong>를 보여줄 수 있어서<br />많은 저가형 전자제품에서 널리 쓰이고 있어요.</p>
<h2 id="🔢-2-7세그먼트-디스플레이의-구조">🔢 2) 7세그먼트 디스플레이의 구조</h2>
<h3 id="💡-7개--1개의-led">💡 7개 + 1개의 LED</h3>
<ul>
<li>숫자 8 모양으로 <strong>A~G까지 7개의 LED</strong>가 배열됨  </li>
<li>소수점을 위한 <strong>DP(Dot Point)</strong> LED도 1개 포함</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/20766686-adc8-42e7-834c-7b090d35fb76/image.png" /></p>
<p>이 LED들을 적절히 켜고 끄면 숫자 0~9나 일부 문자를 만들 수 있어요.</p>
<h3 id="⚡-공통-캐소드-방식">⚡ 공통 캐소드 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7266a90e-d6c9-447c-83e6-117fe26ab7de/image.png" /></p>
<ul>
<li><strong>모든 LED의 음극(캐소드)</strong>을 하나로 묶어 그라운드에 연결</li>
<li>각 LED의 <strong>양극(애노드)</strong>에는 별도의 핀을 연결해 제어</li>
</ul>
<p>➡️ 프로세서는 각 세그먼트의 <strong>애노드에 전압(1)</strong>을 주고,<br /><strong>캐소드를 GND(0)</strong>로 연결하면 해당 LED가 켜집니다.</p>
<blockquote>
<p>참고 : 
+극 : 애노드(Anode)
-극 : 캐소드(Cathode)</p>
</blockquote>
<pre><code>[전압 1] → [애노드 → LED → 캐소드] → [GND(0)]
</code></pre><h3 id="🔌-그런데-문제가-하나">🔌 그런데 문제가 하나!</h3>
<ul>
<li>LED 8개(디스플레이 1개 = 8개의 LED 제어 = 8개 제어선 필요) × 디스플레이 4개(알람 숫자 00 :00) = 총 32개 핀?</li>
<li>대부분의 마이크로컨트롤러는 그렇게 많은 <strong>출력 포트 핀</strong>이 없습니다.</li>
</ul>
<h2 id="🔀-3-멀티플렉싱multiplexing으로-핀-줄이기">🔀 3) 멀티플렉싱(Multiplexing)으로 핀 줄이기!</h2>
<blockquote>
<p><strong>&quot;핀은 적게 쓰고, 디스플레이는 많이 보여주자!&quot;</strong></p>
</blockquote>
<h3 id="📌-멀티플렉싱-기본-아이디어">📌 멀티플렉싱 기본 아이디어</h3>
<ul>
<li><strong>모든 디스플레이의 애노드는 병렬로 공유</strong></li>
<li><strong>캐소드만 각 디스플레이별로 분리</strong></li>
</ul>
<p>즉, 세그먼트 A<del>G는 모두 한 세트의 포트(A0</del>A7)를 쓰고,<br />디스플레이 1<del>4는 포트 B0</del>B3으로 제어함</p>
<pre><code class="language-plaintext">A0~A7 → 모든 디스플레이의 A~G 애노드 공통
B0~B3 → 각각의 디스플레이 캐소드 선택</code></pre>
<h2 id="👀-4-사람-눈의-착각-잔상-효과">👀 4) 사람 눈의 착각, 잔상 효과!</h2>
<blockquote>
<p><strong>“디스플레이를 계속 켜놓지 않아도, 우리는 켜져 있다고 느낀다?”</strong></p>
</blockquote>
<ul>
<li>사람이 인식하는 잔상 시간은 <strong>1/24초 정도</strong></li>
<li>이를 이용해 <strong>디스플레이를 빠르게 하나씩 켰다 껐다</strong>하면<br />마치 <strong>모든 디스플레이가 동시에 켜진 것처럼</strong> 느껴져요!</li>
</ul>
<p>➡️ 이 기술이 바로 <strong>멀티플렉싱 디스플레이의 핵심 원리</strong></p>
<h3 id="🔁-동작-방식-요약">🔁 동작 방식 요약</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/99c0d96e-9c00-44d7-a2d5-d4fe34dfee43/image.png" /></p>
<ol>
<li>디스플레이 1번의 캐소드를 0으로 설정 (나머지는 끔)</li>
<li>1번 디스플레이에 해당하는 세그먼트를 켬</li>
<li>짧은 시간 후 디스플레이 2번으로 전환</li>
<li>이걸 반복해서 <strong>4개 디스플레이를 순환하며 깜빡임</strong></li>
</ol>
<h2 id="⏱️-5-소프트웨어-타이머로-구현">⏱️ 5) 소프트웨어 타이머로 구현</h2>
<ul>
<li>타이머 인터럽트를 짧은 간격(예: 2ms)마다 발생시키고</li>
<li>각 인터럽트에서 <strong>다음 디스플레이로 순서 변경</strong></li>
<li>이 과정을 빠르게 반복하면 모든 디스플레이가 &quot;항상 켜진 듯&quot; 보입니다</li>
</ul>
<h2 id="💡-6-32개가-12개-되는-매직-멀티-플렉싱">💡 6) 32개가 12개 되는 매직 멀티 플렉싱</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1d5b93cc-4864-4522-8060-b67b77547b34/image.png" /></p>
<ol>
<li><strong>핀 수 계산이 32개가 되는 이유는 이거예요:</strong></li>
</ol>
<pre><code class="language-plaintext">디스플레이 4개 × 각 디스플레이에 LED 8개 = LED 32개</code></pre>
<p>즉, <strong>핀 = LED 개수</strong>라고 단순하게 보는 계산이에요.</p>
<blockquote>
<p>하지만 <strong>현실에서는 그렇게 1:1로 핀을 다 쓰지 않아요.</strong></p>
</blockquote>
<h3 id="🔧-현실에서는-어떻게-하냐">🔧 현실에서는 어떻게 하냐?</h3>
<h4 id="멀티플렉싱을-사용합니다">멀티플렉싱을 사용합니다!</h4>
<ul>
<li><p><strong>세그먼트 A~G, DP는 모든 디스플레이가 ‘공유’</strong>
→ 포트 A로 묶음 (핀 8개)</p>
</li>
<li><p><strong>디스플레이 자릿수(1~4)는 하나씩 선택</strong>
→ 포트 B로 제어 (핀 4개)</p>
</li>
</ul>
<h2 id="7-보충-정리--마이크로컨트롤러mcu-microcontroller-unit란">7) 보충 정리 : 마이크로컨트롤러(MCU, Microcontroller Unit)란?</h2>
<blockquote>
<p><strong>작은 컴퓨터</strong>라고 생각하시면 됩니다.<br />CPU, 메모리, 입출력 기능까지 한 칩에 들어있는 <strong>초소형 컴퓨터</strong>예요.</p>
</blockquote>
<h3 id="💡-마이크로컨트롤러의-구성">💡 마이크로컨트롤러의 구성</h3>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>역할</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>CPU</strong></td>
<td>계산/제어</td>
<td>아주 단순한 명령어 셋을 처리</td>
</tr>
<tr>
<td><strong>RAM</strong></td>
<td>데이터 저장</td>
<td>프로그램 실행 중 임시 데이터 저장</td>
</tr>
<tr>
<td><strong>ROM/Flash</strong></td>
<td>프로그램 저장</td>
<td>펌웨어, 실행 코드 저장</td>
</tr>
<tr>
<td><strong>I/O 핀</strong></td>
<td>외부와 연결</td>
<td>센서, 버튼, LED, 모터 등과 연결</td>
</tr>
</tbody></table>
<p>➡️ 하나의 칩에 이 모든 것이 <strong>올인원으로 들어 있음</strong>!</p>
<h3 id="🖥️-그렇다면-데스크탑-컴퓨터에서는">🖥️ 그렇다면 데스크탑 컴퓨터에서는?</h3>
<p>데스크탑, 노트북에 있는 <strong>중앙처리장치(CPU)</strong>와 <strong>마이크로컨트롤러(MCU)</strong>는 <strong>역할과 위치가 완전히 다릅니다.</strong></p>
<table>
<thead>
<tr>
<th>비교</th>
<th>MCU (마이크로컨트롤러)</th>
<th>CPU (중앙처리장치)</th>
</tr>
</thead>
<tbody><tr>
<td>주 용도</td>
<td>장치 제어, 센서/버튼 처리</td>
<td>복잡한 연산, 운영체제 구동</td>
</tr>
<tr>
<td>위치</td>
<td>키보드, 마우스, 냉장고 등 장치 내부</td>
<td>메인보드의 CPU 소켓</td>
</tr>
<tr>
<td>성능</td>
<td>낮음 (8~32비트, MHz 단위)</td>
<td>높음 (64비트, GHz 단위)</td>
</tr>
<tr>
<td>예시</td>
<td>ATmega328, STM32, ESP32</td>
<td>Intel i7, AMD Ryzen 등</td>
</tr>
</tbody></table>
<h3 id="🧭-컴퓨터-안에도-마이크로컨트롤러가-있다">🧭 컴퓨터 안에도 마이크로컨트롤러가 있다?</h3>
<p>맞습니다!</p>
<table>
<thead>
<tr>
<th>장치</th>
<th>MCU 역할</th>
</tr>
</thead>
<tbody><tr>
<td><strong>키보드</strong></td>
<td>어떤 키가 눌렸는지 감지 → USB로 신호 전송</td>
</tr>
<tr>
<td><strong>마우스</strong></td>
<td>움직임/클릭 감지 → USB로 신호 전송</td>
</tr>
<tr>
<td><strong>모니터 내부</strong></td>
<td><code>밝기, 전원 상태 등 제어</code></td>
</tr>
<tr>
<td><strong>노트북 배터리</strong></td>
<td>충전 상태 모니터링, 과전압 방지</td>
</tr>
<tr>
<td><strong>BIOS/UEFI 칩</strong></td>
<td>펌웨어 구동 (여기에도 MCU적인 구조가 존재)</td>
</tr>
</tbody></table>
<h3 id="🧸-쉽게-비유하면">🧸 쉽게 비유하면?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b47c2517-7f7c-4190-b368-f03c85d289e4/image.png" /></p>
<blockquote>
<p><strong>CPU는 사장</strong>,  
<strong>MCU는 기계 옆에서 버튼을 누르고 센서를 읽는 작업자</strong>라고 보면 됩니다.</p>
</blockquote>
<p>CPU는 <strong>운영체제와 복잡한 연산</strong>을 처리하고,<br />MCU는 <strong>단순 반복적인 장치 제어</strong>를 조용히 처리하죠.</p>
<h3 id="✅-마이크로컨트롤러-요약">✅ 마이크로컨트롤러 요약</h3>
<table>
<thead>
<tr>
<th>질문</th>
<th>답변</th>
</tr>
</thead>
<tbody><tr>
<td>마이크로컨트롤러는 컴퓨터에 있어요?</td>
<td>✅ 주변장치(키보드, 마우스 등)에 내장돼 있어요</td>
</tr>
<tr>
<td>CPU랑 같은 건가요?</td>
<td>❌ 아니요, MCU는 저성능/제어용, CPU는 고성능 연산용</td>
</tr>
<tr>
<td>MCU는 어떤 역할 해요?</td>
<td>버튼 읽기, LED 제어, 센서 입력 처리 등 단순 제어</td>
</tr>
<tr>
<td>MCU가 필요한 경우는?</td>
<td>임베디드 장치, IoT 제품, 전자회로 설계 등</td>
</tr>
</tbody></table>
<blockquote>
<p>&quot;우리가 키보드를 눌렀을 때, 사무실 컴퓨터의 사장이 반응하는 게 아니라,<br />그 키보드 안에 있던 작은 MCU가 먼저 응답하고, 깔끔하게 정리된 보고서를 CPU에게 전달하는 겁니다.&quot;</p>
</blockquote>
<h2 id="✅-핵심-요약표">✅ 핵심 요약표</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>7세그먼트 구조</strong></td>
<td>A~G의 7개 LED + 소수점(DP) LED</td>
</tr>
<tr>
<td><strong>제어 방식</strong></td>
<td>애노드에 전압(1), 캐소드에 GND(0)</td>
</tr>
<tr>
<td><strong>공통 캐소드 디스플레이</strong></td>
<td>모든 캐소드를 하나로 묶고 애노드로 개별 제어</td>
</tr>
<tr>
<td><strong>멀티플렉싱</strong></td>
<td>하나씩 빠르게 번갈아 켜서 전체가 켜진 듯 보이게</td>
</tr>
<tr>
<td><strong>시각적 착시 활용</strong></td>
<td>1/24초 이내로 번갈아 켜면 사람 눈에는 모두 켜진 것처럼 인식</td>
</tr>
<tr>
<td><strong>실제 구현</strong></td>
<td>타이머 인터럽트 + 반복 루프</td>
</tr>
</tbody></table>
<blockquote>
<p>“복잡해 보이는 전자 시계도, 사실은 착각의 기술과 핀 아끼기의 예술입니다.”</p>
</blockquote>
<h2 id="보충-정리--모니터-mcu인가">보충 정리 : 모니터 MCU인가?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8c39a776-28e4-4c04-8bb1-d2f67dc909ab/image.png" /></p>
<p>참고로 ✅<code>모니터</code>는 MCU처럼 'PORTA로 직접 LED 제어'하지 않습니다. 구조가 훨씬 더 복잡하고, 제어 방식도 완전히 다르기 때문이에요.</p>
<blockquote>
<p>하지만 모니터는 전체 화면 표현은 MCU로 하지 않지만, 일부 기능(밝기, 전원, 버튼 등)은 MCU로 제어합니다.</p>
</blockquote>
<h3 id="1-📺-화면-출력영상-처리">1. 📺 <strong>화면 출력(영상 처리)</strong></h3>
<ul>
<li>모니터가 영상 신호(HDMI, DP 등)를 받아서</li>
<li>내부 <strong>T-CON (Timing Controller)</strong> 칩과 <strong>드라이버 IC</strong>가  
수백만 개의 픽셀(LED 혹은 액정)을 <strong>자동으로 정밀하게 제어</strong>합니다.</li>
</ul>
<p>❌ 이건 <strong>MCU처럼 단순한 디지털 핀 제어로는 절대 불가능</strong>합니다.</p>
<h3 id="2-⚙️-밝기-조절-전원-제어-메뉴-버튼-osdon-screen-display">2. ⚙️ <strong>밝기 조절, 전원 제어, 메뉴 버튼, OSD(On-Screen Display)</strong></h3>
<p>이런 기능은 대부분 모니터 내부에 있는 <strong>소형 MCU</strong>가 처리합니다.</p>
<table>
<thead>
<tr>
<th>기능</th>
<th>MCU 사용 여부</th>
</tr>
</thead>
<tbody><tr>
<td>전원 On/Off</td>
<td>✅ 내부 MCU가 처리</td>
</tr>
<tr>
<td>밝기/명암 설정</td>
<td>✅ MCU가 EEPROM/센서와 함께 처리</td>
</tr>
<tr>
<td>OSD 메뉴 표시</td>
<td>✅ MCU가 설정값 기반으로 실행</td>
</tr>
<tr>
<td>터치 버튼/리모컨 수신</td>
<td>✅ MCU가 버튼 입력을 감지함</td>
</tr>
</tbody></table>
<p>➡️ 즉, <strong>영상이 아닌 보조 기능들은 MCU가 따로 관리</strong>합니다.</p>
<h3 id="📦-모니터-내부-구조-예시">📦 모니터 내부 구조 예시</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a580d670-ee06-4aa4-b878-607716c1ef14/image.png" /></p>
<pre><code>[입력 신호 (HDMI/DP)]
        ↓
    [Scaler IC] → 영상 처리
        ↓
    [T-CON 칩] → 타이밍 조절
        ↓
    [Panel Driver IC] → 픽셀 제어

그리고 별도로 ↓

    [MCU] → 버튼, 밝기, 설정, 전원, OSD</code></pre><h3 id="🤖-mcu가-하는-일-예시">🤖 MCU가 하는 일 예시</h3>
<table>
<thead>
<tr>
<th>MCU 내 코드</th>
<th>하는 일</th>
</tr>
</thead>
<tbody><tr>
<td><code>if (brightness_btn == pressed)</code></td>
<td>밝기 값 10 증가</td>
</tr>
<tr>
<td><code>if (power_btn == pressed)</code></td>
<td>전체 시스템 전원 off</td>
</tr>
<tr>
<td><code>readLightSensor()</code></td>
<td>주변 밝기에 따라 화면 밝기 자동 조정</td>
</tr>
</tbody></table>
<h3 id="✅-결론-정리">✅ 결론 정리</h3>
<table>
<thead>
<tr>
<th>질문</th>
<th>답변</th>
</tr>
</thead>
<tbody><tr>
<td>모니터는 전체적으로 MCU 방식인가요?</td>
<td>❌ 아니요. 영상 제어는 전용 IC와 고속 회로가 담당</td>
</tr>
<tr>
<td>일부 MCU가 들어가긴 하나요?</td>
<td>✅ 네! 버튼, 밝기 조절 등 주변 제어용으로 들어갑니다</td>
</tr>
<tr>
<td>MCU는 어떤 역할을 하나요?</td>
<td>설정 관리, 버튼/센서 처리, 사용자 입력 처리 등</td>
</tr>
<tr>
<td>MCU 방식으로 화면 제어할 수 있나요?</td>
<td>❌ 현실적으로 불가능. 수백만 픽셀 제어엔 고속 신호 필요</td>
</tr>
</tbody></table>
<h2 id="7-그렇다면-p226에-7세그먼트-디스플레이는-모니터와-관련이-별로-없는데-왜-나올까-굳이-따지자면-iot쪽-아닌가">7) 그렇다면, P.226에 7세그먼트 디스플레이는 모니터와 관련이 별로 없는데 왜 나올까? 굳이 따지자면 IOT쪽 아닌가?</h2>
<p>이 장(7세그먼트 디스플레이와 멀티플렉싱)은 단순히 <strong>LED를 켜는 회로</strong> 얘기 같지만,<br />그 속엔 <strong>임베디드 시스템</strong>, <strong>소프트웨어 제어</strong>, <strong>하드웨어 자원 최적화</strong> 등<br /><strong>IoT(사물인터넷)</strong>과 매우 밀접한 핵심 개념이 들어 있어요.</p>
<p>✅ <strong>제한된 자원으로 세상을 제어하는 법, 그리고 그 기술의 뿌리</strong></p>
<h3 id="📌-핵심-메시지를-정리하면">📌 핵심 메시지를 정리하면:</h3>
<table>
<thead>
<tr>
<th>숨은 저의</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>1. &quot;LED 제어는 단순한 물리 현상이 아니다.&quot;</strong></td>
<td>MCU가 코드를 통해 하드웨어를 제어하며, 이 과정은 디지털 제어의 본질이자 IoT 기기의 기본 구조</td>
</tr>
<tr>
<td><strong>2. &quot;모든 디바이스에 CPU처럼 똑똑한 칩은 없다.&quot;</strong></td>
<td>저렴하고 단순한 MCU에서도 <strong>효율적인 자원 관리(핀 수 최소화, 전류 제어)</strong>를 해야 하며, 이건 실전적인 고민</td>
</tr>
<tr>
<td><strong>3. &quot;소프트웨어가 하드웨어를 보완한다.&quot;</strong></td>
<td>부족한 핀 수는 <strong>멀티플렉싱 + 타이머 + 잔상효과</strong>로 커버함 → 이게 바로 소프트웨어적 문제 해결 능력</td>
</tr>
<tr>
<td><strong>4. &quot;이것이 IoT 세상의 기본 단위다.&quot;</strong></td>
<td>수많은 IoT 기기들이 <strong>버튼을 누르면 LED가 켜지고, 숫자를 표시</strong>하는 구조로 이루어짐 → 이게 현실 제어의 시작점</td>
</tr>
</tbody></table>
<h3 id="🤖-이-장은-사실상-iot-시스템의-축소판">🤖 이 장은 사실상 “IoT 시스템의 축소판”</h3>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>현실 장치 예시</th>
</tr>
</thead>
<tbody><tr>
<td><strong>7세그먼트 디스플레이</strong></td>
<td>스마트 계량기, 온도계, 알람시계</td>
</tr>
<tr>
<td><strong>MCU + 포트 제어</strong></td>
<td>아두이노, ESP32, 리모컨 내부 칩</td>
</tr>
<tr>
<td><strong>멀티플렉싱</strong></td>
<td>키패드, 디지털 숫자창, IoT UI 디스플레이</td>
</tr>
<tr>
<td><strong>타이머 + 반복 루틴</strong></td>
<td>깜빡이는 LED, 자동 시간 표시 등</td>
</tr>
<tr>
<td><strong>잔상효과 활용</strong></td>
<td>사용자 경험 UX 기법 중 하나</td>
</tr>
</tbody></table>
<h3 id="✨-요약-이-장이-말해주는-진짜-의미">✨ 요약: 이 장이 말해주는 진짜 의미</h3>
<blockquote>
<p>&quot;<strong>컴퓨터가 눈에 보이는 물리 세계를 어떻게 제어할 수 있을까?</strong><br />그 첫걸음은 아주 작고 단순한 LED 하나를 켜는 데서 시작한다.&quot;</p>
</blockquote>
<p>그리고 그 LED 하나를 “스마트하게” 켜는 기술이<br />바로 <strong>임베디드 시스템 + IoT 기술의 기초</strong>예요.</p>
<blockquote>
<p><strong>&quot;7세그먼트 디스플레이는 단지 숫자를 보여주는 창이 아니라,<br />작은 컴퓨터가 세상을 제어하는 방식 그 자체를 보여주는 창문이다.&quot;</strong></p>
</blockquote>
<h3 id="✔️-답은-이렇습니다">✔️ 답은 이렇습니다:</h3>
<blockquote>
<p><strong>IoT는 컴퓨터의 일부 영역이고, 확장판이기도 해요.</strong><br />단지 우리가 흔히 생각하는 <strong>‘데스크탑 컴퓨터’나 ‘노트북’ 같은 컴퓨터와는 역할이 다를 뿐</strong>이에요.</p>
</blockquote>
<h3 id="💻-컴퓨터의-정의부터-다시-생각해봅시다">💻 <strong>&quot;컴퓨터&quot;의 정의부터 다시 생각해봅시다.</strong></h3>
<blockquote>
<p><strong>컴퓨터란?</strong><br />👉 “입력(Input)을 받아 처리(Process)하고 결과(Output)를 내보내는 전자 장치”</p>
</blockquote>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>어떤 기기에도 다 있음</th>
</tr>
</thead>
<tbody><tr>
<td>CPU (처리기)</td>
<td>명령어 실행</td>
</tr>
<tr>
<td>메모리 (RAM, ROM)</td>
<td>임시저장, 코드 보관</td>
</tr>
<tr>
<td>I/O 장치</td>
<td>버튼, 센서, 네트워크 등</td>
</tr>
<tr>
<td>전원</td>
<td>배터리, 어댑터 등</td>
</tr>
</tbody></table>
<p>➡️ 이런 요소들이 들어 있으면 사실상 <strong>그것도 ‘컴퓨터’입니다.</strong></p>
<h3 id="🌐-그러면-iot는">🌐 그러면 IoT는?</h3>
<blockquote>
<p><strong>IoT = &quot;사물(Thing)&quot; + &quot;컴퓨팅 능력&quot; + &quot;네트워크&quot;</strong></p>
</blockquote>
<ul>
<li>IoT 기기도 CPU, 메모리, I/O를 갖추고 있어요.</li>
<li>단지, 사람이 마우스와 키보드로 쓰는 게 아니라,
<strong>센서나 버튼으로 입력을 받고, 네트워크를 통해 반응</strong>하는 거예요.</li>
</ul>
<h3 id="📦-예시-컴퓨터-vs-iot-비교">📦 예시: 컴퓨터 vs IoT 비교</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2ea90af1-5885-4c38-8bde-5ab0fbc08bfd/image.png" /></p>
<table>
<thead>
<tr>
<th>항목</th>
<th>데스크탑 컴퓨터</th>
<th>IoT 디바이스</th>
</tr>
</thead>
<tbody><tr>
<td>CPU</td>
<td>고성능 (i7 등)</td>
<td>저전력 MCU (AVR, ESP32 등)</td>
</tr>
<tr>
<td>입출력</td>
<td>키보드/마우스/모니터</td>
<td>버튼/센서/LED</td>
</tr>
<tr>
<td>주된 용도</td>
<td>앱 실행, 인터넷, 업무</td>
<td>환경 감지, 제어, 자동화</td>
</tr>
<tr>
<td>운영체제</td>
<td>Windows, macOS, Linux</td>
<td>대부분 Bare-metal, FreeRTOS 등</td>
</tr>
<tr>
<td>인터넷 연결</td>
<td>사용자가 직접</td>
<td>자동/센서기반 연결 (WiFi, BLE 등)</td>
</tr>
</tbody></table>
<p>➡️ <strong>둘 다 &quot;컴퓨터&quot;이지만, 방향과 대상이 다르다!</strong></p>
<h3 id="🔌-핵심은-이거예요">🔌 핵심은 이거예요:</h3>
<blockquote>
<p>✅ <strong>IoT는 컴퓨터 구조의 &quot;축소판 + 제어판&quot;입니다.</strong><br />복잡한 화면 대신 LED, 마우스 대신 센서, 스피커 대신 릴레이를 쓰는 것뿐이에요.</p>
</blockquote>
<h3 id="🔁-그래서-결론적으로는">🔁 그래서 결론적으로는…</h3>
<table>
<thead>
<tr>
<th>질문</th>
<th>답변</th>
</tr>
</thead>
<tbody><tr>
<td>IoT랑 컴퓨터는 완전히 별개인가요?</td>
<td>❌ 아니요, 기본 구조는 같습니다.</td>
</tr>
<tr>
<td>그럼 왜 다르게 느껴지나요?</td>
<td>사용 용도, 처리 방식, 입출력 수단이 다르기 때문이에요.</td>
</tr>
<tr>
<td>7세그먼트처럼 버튼, LED 제어는 컴퓨터가 할 수 있어요?</td>
<td>✅ 가능합니다. 다만 MCU 같은 소형 컴퓨터가 더 효율적일 뿐이에요.</td>
</tr>
</tbody></table>
<blockquote>
<p>“IoT는 컴퓨터 구조를 가장 작게 응축해서, 세상을 제어할 수 있게 만든 기술이에요.<br />즉, <strong>세상을 읽고 반응하는 '작은 컴퓨터들'의 네트워크</strong>죠.”</p>
</blockquote>
<h1 id="🎛️-버튼과-디스플레이가-함께-있는-기기의-비밀--멀티플렉싱의-응용편">🎛️ <strong>버튼과 디스플레이가 함께 있는 기기의 비밀 – 멀티플렉싱의 응용편</strong></h1>
<blockquote>
<p><strong>“입력(버튼)과 출력(디스플레이)을 동시에 하나의 구조로 스캔하면서, 핀 수를 줄이자!”</strong></p>
</blockquote>
<h2 id="🧩-문제-상황">🧩 문제 상황</h2>
<p>디지털 기기를 만들고 있었어요. 숫자도 보여줘야 하고, 버튼도 많아야 해요.<br />예를 들어 이런 상황이죠:</p>
<ul>
<li>숫자 4개짜리 디스플레이 (00:00 스타일)</li>
<li>버튼은 전화기처럼 12개 (1~9, *, 0, #)</li>
</ul>
<blockquote>
<p>❗ 근데 마이크로컨트롤러의 <strong>포트 핀 수가 부족합니다!</strong></p>
</blockquote>
<ul>
<li>디스플레이: 8핀 필요 (A~G + DP)</li>
<li>버튼: 12핀 필요<br />총 20핀 이상? → MCU가 감당 못함 😰</li>
</ul>
<h2 id="💡-해법-버튼과-디스플레이를-함께-멀티플렉싱한다">💡 해법: 버튼과 디스플레이를 <strong>함께 멀티플렉싱한다!</strong></h2>
<p>이건 마치…</p>
<blockquote>
<p>“버튼과 디스플레이가 같은 통로를 같이 쓰고,<br /><strong>시간을 나눠가면서 동작</strong>하게 만든 구조예요.”</p>
</blockquote>
<h2 id="🔧-회로-구조-요약">🔧 회로 구조 요약</h2>
<ul>
<li>디스플레이 A<del>G 세그먼트 핀 → **포트 A (A0</del>A7)**  </li>
<li>디스플레이 선택 (자리 1<del>4) → **포트 B (B0</del>B3)**  </li>
<li>버튼 입력 → <strong>포트 C (C0~C2)</strong></li>
</ul>
<p>디스플레이를 하나 선택할 때,<br />그와 연결된 <strong>버튼 열</strong>도 같이 연결되도록 구성했어요.</p>
<pre><code class="language-plaintext">[공통 세그먼트 출력 (A)] → 디스플레이와 버튼 공통
[선택 핀 (B)] → 현재 디스플레이 자리 AND 해당 버튼 줄 선택
[입력 핀 (C)] → 버튼이 눌렸는지 확인</code></pre>
<h2 id="📲-동작-방식-예-디스플레이-1번과-버튼-13-열-선택-시">📲 동작 방식 (예: 디스플레이 1번과 버튼 1~3 열 선택 시)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2e67990f-cb00-4546-9a36-466c5a943bb3/image.png" /></p>
<ol>
<li>포트 B0만 0으로 설정 → 디스플레이 1번 선택됨</li>
<li>동시에 B0와 연결된 버튼 줄 활성화됨</li>
<li>포트 C 입력을 읽어서 어떤 버튼이 눌렸는지 확인</li>
<li>다음 인터럽트에서 디스플레이 2번(B1)로 넘어감 → 순환 반복</li>
</ol>
<h2 id="👁️-잔상-효과--스캔--사용자는-모른다">👁️ 잔상 효과 + 스캔 = 사용자는 모른다</h2>
<ul>
<li>디스플레이도 멀티플렉싱으로 빠르게 번갈아 켜니까 전부 켜진 것처럼 보이고,</li>
<li>버튼도 같은 타이밍으로 스캔하니 <strong>따로 핀을 쓰지 않고도 모든 입력이 감지</strong>됨!</li>
</ul>
<h2 id="🧠-주의할-점">🧠 주의할 점</h2>
<ul>
<li>입력 버튼들은 <strong>풀업 저항</strong>으로 항상 1 상태 유지</li>
<li>눌렸을 때만 0으로 떨어짐</li>
<li>실전에서는 <strong>오픈 드레인/오픈 컬렉터</strong>를 쓰지 않으면 충돌이 날 수 있어요<br />→ 여러 줄이 동시에 0/1을 연결하게 되면 회로 손상 가능 😵</li>
</ul>
<h2 id="✅-요약표">✅ 요약표</h2>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>포트 A</td>
<td>디스플레이 세그먼트 출력 (A~G, DP)</td>
</tr>
<tr>
<td>포트 B</td>
<td>디스플레이 자리 선택 + 버튼 줄 선택</td>
</tr>
<tr>
<td>포트 C</td>
<td>버튼 입력 스캔</td>
</tr>
<tr>
<td>멀티플렉싱 방식</td>
<td>디스플레이 하나를 켤 때마다 해당 버튼 줄도 연결</td>
</tr>
<tr>
<td>장점</td>
<td>포트를 많이 쓰지 않고도 디스플레이 + 버튼 모두 처리</td>
</tr>
<tr>
<td>핵심 기법</td>
<td>시간 분할 스캔, 풀업 저항, 입력 감지와 출력 전환 동기화</td>
</tr>
</tbody></table>
<h2 id="🔍-마지막-질문">🔍 마지막 질문</h2>
<blockquote>
<p>&quot;디스플레이가 조금 이상해 보일 것이다. 그 이유는?&quot;</p>
</blockquote>
<ul>
<li>여러 버튼을 <strong>동시에 누르면</strong>,  </li>
<li><strong>디스플레이의 멀티플렉싱 순서와 충돌</strong>이 생기면서<br />→ 세그먼트에 <strong>원하지 않은 값</strong>이 출력될 수 있어요</li>
</ul>
<p>예:<br />1번 버튼을 누르고 있는데, 그 버튼 줄이 선택된 상태에서<br />디스플레이 자리 바뀌면 다른 자리에 영향이 생길 수도 있음<br />→ <strong>버튼이 세그먼트 상태에 영향을 주는 순간적인 오작동</strong></p>
<blockquote>
<p>“이 회로는 마치, 하나의 무대에서 디스플레이와 버튼이 번갈아가며 조명과 마이크를 공유하며 연기하는 연극 같아요.<br />타이밍만 잘 맞추면 아주 적은 장비로 멋진 무대를 만들 수 있답니다.”</p>
</blockquote>
<hr />
<h1 id="💡-알람시계의-밝기는-어떻게-조절할까">💡 <strong>알람시계의 밝기는 어떻게 조절할까?</strong></h1>
<p>이 부분은 <strong>알람시계나 LED 디스플레이의 '밝기 조절'</strong>을 어떻게 구현할 수 있는지에 대한 이야기예요. 핵심 개념은 바로 <strong>듀티 사이클(duty cycle)</strong>이라는 용어입니다.</p>
<h2 id="📺-디스플레이는-단순히-켜고-끄는-것만으로도-밝기가-달라진다">📺 <strong>디스플레이는 단순히 &quot;켜고 끄는&quot; 것만으로도 밝기가 달라진다</strong></h2>
<p>알람시계처럼 작은 전자기기는 보통 <strong>7세그먼트 디스플레이</strong>를 사용하죠.<br />이런 디스플레이는 사실 항상 켜져 있는 것처럼 보이지만, 실제로는 <strong>아주 빠르게 켜졌다 꺼졌다를 반복</strong>합니다.<br />그리고 이 <strong>&quot;켜져 있는 비율&quot;이 바로 밝기를 조절하는 핵심</strong>이에요.</p>
<h2 id="🔁-듀티-사이클이란">🔁 <strong>듀티 사이클이란?</strong></h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ae8877e6-9bd6-44f4-911c-77bafc890bbd/image.png" /></p>
<blockquote>
<p><strong>LED가 켜져 있는 시간 / 전체 주기 시간 × 100%</strong></p>
</blockquote>
<p>모니터에서 밝기 제어, 전원 ON/OFF 등 물리 제어</p>
<h2 id="📊-그림-6-11의-의미">📊 그림 6-11의 의미</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/93235853-0e31-4c37-b414-b6f55a0997da/image.png" /></p>
<h3 id="왼쪽-그림">왼쪽 그림</h3>
<ul>
<li>B0 ~ B3 (4자리 디스플레이 자리 선택)</li>
<li>각 자리마다 <strong>1/4 시간 동안만 켜짐</strong></li>
<li>예: <code>B0 → B1 → B2 → B3</code> 순으로 1칸씩 스캔하며 각 자리 25%씩 ON</li>
</ul>
<p>➡️ <strong>평균 밝기 = 기준 밝기 (기본)</strong></p>
<h3 id="오른쪽-그림">오른쪽 그림</h3>
<ul>
<li>전체 시간을 더 잘게 쪼갬 (8분할)</li>
<li>각 자리마다 <strong>1/8 시간만 켜짐</strong></li>
<li>예: <code>B0 켬 → B0 끔 → B1 켬 → B1 끔 → ...</code></li>
</ul>
<p>➡️ <strong>전체적으로 평균 밝기 절반 수준</strong>으로 줄어듦</p>
<blockquote>
<p><strong>❓ &quot;B0~B3 순서로 1/4씩 켠다&quot;는 건 도대체 무슨 말일까요? 정말 난해하군요.. 휴</strong></p>
</blockquote>
<p>이건 <strong>멀티플렉싱(Multiplexing)</strong> 개념이에요.</p>
<p>7세그먼트 디스플레이는<br /><strong>한 번에 모든 자리를 동시에 켜지 않고,</strong><br /><strong>하나씩 아주 빠르게 번갈아가며 켜는 방식</strong>을 씁니다.</p>
<p><strong>🔁 어떻게 돌아가는지 예를 들어볼게요:</strong></p>
<p>디스플레이 자리가 4개 있다고 가정 (예: 시계 12:34)</p>
<table>
<thead>
<tr>
<th>시간 틱</th>
<th>켜지는 자리</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>t0</td>
<td>B0</td>
<td>첫 번째 숫자 자리만 켜짐</td>
</tr>
<tr>
<td>t1</td>
<td>B1</td>
<td>두 번째 자리만 켜짐</td>
</tr>
<tr>
<td>t2</td>
<td>B2</td>
<td>세 번째 자리만 켜짐</td>
</tr>
<tr>
<td>t3</td>
<td>B3</td>
<td>네 번째 자리만 켜짐</td>
</tr>
<tr>
<td>t4~t7</td>
<td>반복</td>
<td>순서대로 계속 순환</td>
</tr>
</tbody></table>
<ul>
<li>실제로는 <strong>한 자리만 켜고, 나머지는 꺼져 있어요</strong></li>
<li>그런데 <strong>이걸 아주 빠르게 (예: 1ms마다)</strong> 반복하면?</li>
<li><strong>사람 눈은 4개 모두 항상 켜져 있는 것처럼 착각</strong>합니다<br />(→ 잔상 효과! Persistence of Vision)</li>
</ul>
<table>
<thead>
<tr>
<th>질문</th>
<th>답변</th>
</tr>
</thead>
<tbody><tr>
<td>컴퓨터 밝기 조절은 MCU가 해요?</td>
<td>✅ 모니터 안의 MCU가 PWM 신호로 조절해요</td>
</tr>
<tr>
<td>B0~B3 순서로 1/4만 켜진다는 건?</td>
<td>✅ 각 디스플레이를 빠르게 번갈아가며 켜는 방식 (멀티플렉싱)</td>
</tr>
<tr>
<td>그럼 전체 밝기는 어디서 정하죠?</td>
<td>✅ 각 자리별로 켜지는 시간(듀티 사이클)을 줄이면 밝기 낮아짐</td>
</tr>
</tbody></table>
<p>&quot;모니터든 알람시계든, 밝기란 건 결국 '얼마나 자주 켜져 있는가'에 달려 있어요.<br />그리고 그 조절은 항상, 아주 조용히 MCU가 해주고 있답니다.&quot;</p>
<blockquote>
<p><strong>그래서 &quot;각 자리마다 1/4 시간 동안 켜져 있다&quot;는 말은?</strong>
전체 사이클 중, 각 디스플레이는 자신의 차례일 때만 켜진다.
→ 즉, 4등분된 시간 중 1/4만 ON
→ 이게 기본 밝기 수준이 되는 거예요</p>
</blockquote>
<h2 id="👁️-왜-밝아-보이는가-→-인간의-잔상-효과">👁️ 왜 밝아 보이는가? → 인간의 잔상 효과</h2>
<ul>
<li>디스플레이가 실제로는 껐다 켰다 반복하지만</li>
<li>사람이 느끼기엔 <strong>'평균적으로 켜져 있는 시간의 비율'이 밝기로 느껴짐</strong></li>
</ul>
<h2 id="🎯-중요한-포인트">🎯 중요한 포인트</h2>
<ul>
<li><strong>밝기는 디지털 출력값(1/0)의 세기가 아니라, 켜져 있는 &quot;시간의 비율&quot;</strong></li>
<li><strong>PWM(Pulse Width Modulation, 펄스 폭 변조)</strong> 기법과 비슷한 원리</li>
<li><strong>사람 눈은 순간적인 on/off를 인식하지 못하고 전체 밝기로 느낀다</strong></li>
</ul>
<blockquote>
<p>“밝기는 전구의 세기가 아니라, <strong>얼마나 오래 켜져 있느냐</strong>에 달려 있어요.<br />사람 눈은 속지 않지만, 잔상엔 잘 속거든요!”</p>
</blockquote>
<h2 id="정리">정리</h2>
<h3 id="mcu와-pwm">MCU와 PWM</h3>
<p>❓ 컴퓨터에서 밝기를 조절하는 건 MCU가 하는 거야?</p>
<p>🔌 네! <strong>맞습니다. 대부분의 모니터 내부에는 작은 MCU가 들어 있습니다.</strong></p>
<blockquote>
<p>우리가 &quot;노트북 밝기 조절&quot; 키를 누르면:</p>
<p>→ OS가 그걸 감지<br />→ 디스플레이 장치 드라이버가 명령을 내림<br />→ <strong>모니터 내부 MCU가 PWM 신호의 듀티 사이클을 조절</strong><br />→ 백라이트의 밝기를 조절</p>
</blockquote>
<p>즉, <strong>밝기를 실제로 바꾸는 건, 모니터 안에 있는 MCU + PWM 회로</strong>예요.<br />우리는 간접적으로 명령만 내리는 셈이에요.</p>
<p><strong>그럼 PWM도 있을까?</strong></p>
<blockquote>
<p>✅ 네! <strong>밝기 조절(PWM)</strong>을 위해 거의 항상 사용됩니다.</p>
</blockquote>
<p><strong>💡 왜 PWM을 쓰냐면요:</strong></p>
<ul>
<li>LED 백라이트 밝기를 조절하려면 전류를 조절해야 해요.</li>
<li>그런데 전류를 “애매하게 흘리는” 건 어렵고, 비효율적이에요.</li>
<li>대신, 빠르게 켰다 껐다 반복해서 <strong>시간 비율로 밝기를 조절하는 게 PWM!</strong></li>
<li>LED를 계속 켜는 게 아니라, 빠르게 깜빡이며 ‘얼마나 자주 켤지’를 정하는 방식</li>
</ul>
<hr />
<h1 id="🔁-회전-위치를-숫자로-읽는다--인코더와-그레이-코드-이야기">🔁 회전 위치를 숫자로 읽는다? – 인코더와 그레이 코드 이야기</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6b18022c-46ad-44a4-9bf4-68e5307b9bde/image.png" /></p>
<h2 id="🎯-1-문제-정의-회전축의-위치를-어떻게-알아낼까">🎯 1) <strong>문제 정의: 회전축의 위치를 어떻게 알아낼까?</strong></h2>
<p>어떤 장치의 회전축(바퀴, 모터축, 손잡이 등)의 <strong>각도나 위치</strong>를 알아내려면?</p>
<p>✅ <strong>센서가 필요</strong>합니다.<br />그중 대표적인 게 바로 <strong>로터리 인코더(Rotary Encoder)</strong>예요.</p>
<h2 id="⚙️-2-로터리-인코더란">⚙️ 2) 로터리 인코더란?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/38bdd26f-5032-4c8b-977e-c9e1f14e9f46/image.png" /></p>
<blockquote>
<p><strong>회전하는 디스크에 '검은색/흰색 패턴'을 인쇄하고,<br />광센서가 그것을 읽어 ‘어디쯤 돌아갔는지’를 감지하는 장치</strong></p>
</blockquote>
<h3 id="💡-예시">💡 예시:</h3>
<ul>
<li>검은색 = 1  </li>
<li>흰색 = 0  </li>
<li>인코더 바퀴에 <strong>3개의 트랙(비트)</strong>을 그려놓으면<br />→ 총 <strong>8개의 상태(2³ = 8)</strong>를 표현할 수 있어요!</li>
</ul>
<table>
<thead>
<tr>
<th>위치</th>
<th>센서 값 (3비트)</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>000</td>
</tr>
<tr>
<td>1</td>
<td>001</td>
</tr>
<tr>
<td>2</td>
<td>010</td>
</tr>
<tr>
<td>3</td>
<td>011</td>
</tr>
<tr>
<td>4</td>
<td>100</td>
</tr>
<tr>
<td>5</td>
<td>101</td>
</tr>
<tr>
<td>6</td>
<td>110</td>
</tr>
<tr>
<td>7</td>
<td>111</td>
</tr>
</tbody></table>
<h2 id="😵-그런데-문제가-생긴다">😵 그런데 문제가 생긴다!?</h2>
<p>인코더가 회전하면서 위치가 바뀌는 <strong>딱 그 순간</strong>,  
3개의 센서가 동시에 딱 바뀌어야 하지만…  </p>
<blockquote>
<p>❗ 현실은 그렇지 않아요!</p>
</blockquote>
<ul>
<li>기계적 미세 오차</li>
<li>센서 반응 시간 지연</li>
<li>전기 신호 전파 시간 차이</li>
</ul>
<p>➡️ 결과적으로 <strong>2비트 이상이 동시에 바뀌는 순간</strong>,  
순간적으로 <strong>엉뚱한 값이 읽혀지기도 함</strong></p>
<h3 id="📉-예">📉 예:</h3>
<ul>
<li>3(011)에서 4(100)으로 바뀌어야 하는데  </li>
<li>센서 반응 순서 때문에  </li>
<li>➜ 011 → 001 → 101 → 100  </li>
<li>중간에 이상한 값이 튀어나오는 것처럼 읽힘 😵</li>
</ul>
<p><strong>💥 그럼 어떤 문제가 생길까?</strong>
프로그램 입장에서는
“엥? 3 → 1 → 5 → 4…??”
→ 진짜로 바퀴가 뒤로 돌았나 착각할 수도 있어요</p>
<blockquote>
<p>⚠️ 이건 로봇 제어, 기계 자동화, 모터 제어에서 치명적인 오류를 만듭니다</p>
</blockquote>
<h2 id="🧠-3-해결책-그레이-코드gray-code">🧠 3) 해결책: 그레이 코드(Gray Code)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/44673022-00c6-4d4e-851c-8c411a87e588/image.png" /></p>
<h3 id="✅-그레이-코드는-각-단계에서-딱-1비트만-바뀌게-설계된-이진-코드예요">✅ 그레이 코드는 “각 단계에서 딱 <strong>1비트만</strong> 바뀌게 설계된 이진 코드”예요.</h3>
<table>
<thead>
<tr>
<th>회전 위치</th>
<th>그레이 코드</th>
<th>변화된 비트</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>000</td>
<td>—</td>
</tr>
<tr>
<td>1</td>
<td>001</td>
<td>1개만 다름</td>
</tr>
<tr>
<td>2</td>
<td>011</td>
<td>1개만 다름</td>
</tr>
<tr>
<td>3</td>
<td>010</td>
<td>1개만 다름</td>
</tr>
<tr>
<td>4</td>
<td>110</td>
<td>1개만 다름</td>
</tr>
<tr>
<td>5</td>
<td>111</td>
<td>1개만 다름</td>
</tr>
<tr>
<td>6</td>
<td>101</td>
<td>1개만 다름</td>
</tr>
<tr>
<td>7</td>
<td>100</td>
<td>1개만 다름</td>
</tr>
</tbody></table>
<p>이걸 디스크에 인쇄하면?</p>
<p>➡️ 센서가 읽을 때, <strong>한 비트씩만 천천히 변하니까 안정적이고 오류도 거의 없음!</strong></p>
<h2 id="4-그레이-코드-인코더는-이렇게-생겼다">4) 그레이 코드 인코더는 이렇게 생겼다</h2>
<ul>
<li>여전히 <strong>흰색 = 0, 검은색 = 1</strong></li>
<li>디스크에는 그레이 코드에 맞춰 <strong>패턴이 인쇄</strong></li>
<li>센서는 그걸 읽어 <strong>위치를 안정적으로 감지</strong></li>
</ul>
<blockquote>
<p>✅ <strong>센서가 3개라도, 한 번에 바뀌는 건 1개뿐!</strong><br />→ 중간에 잘못된 상태로 읽힐 확률이 크게 줄어요</p>
</blockquote>
<h2 id="보충-설명--우리가-쓰는-컴퓨터에서-대체-어디에-그레이-코드가-쓰이냐-논리-회로-배울-땐-이런-얘기-없었는데">보충 설명 : “우리가 쓰는 컴퓨터에서 대체 어디에 ‘그레이 코드’가 쓰이냐? 논리 회로 배울 땐 이런 얘기 없었는데?”</h2>
<h3 id="🎯-정답부터-말하자면">🎯 정답부터 말하자면:</h3>
<blockquote>
<p><strong>그레이 코드는 우리가 쓰는 ‘PC 내부 논리회로’에서는 거의 안 쓰이지만,</strong><br /><strong>컴퓨터와 연결된 주변 기기(하드웨어 센서, 모터, 디지털 장비 등) 안에서는 많이 쓰여요.</strong></p>
</blockquote>
<p>즉, <strong>&quot;CPU 연산&quot; 같은 순수 논리회로에서는 안 보이지만</strong>,  
<strong>&quot;컴퓨터와 현실을 연결해주는 회로&quot;에서는 필수</strong>입니다.</p>
<h3 id="🧠-왜-논리회로-교과서에서는-안-나왔을까">🧠 왜 논리회로 교과서에서는 안 나왔을까?</h3>
<ul>
<li>논리회로 수업은 보통 <strong>순수한 CPU 내부 연산 구조</strong>를 다루기 때문이에요.</li>
<li>그레이 코드는 <strong>디지털/아날로그 중간 경계</strong>, 즉 <strong>하드웨어 센서 쪽</strong>에서 필요한 코드입니다.</li>
<li><strong>회로 설계자나 임베디드 개발자</strong>, 혹은 <strong>로봇 제어 개발자</strong>들이 쓰는 영역이죠.</li>
</ul>
<h3 id="💡-한마디로-요약하면">💡 한마디로 요약하면?</h3>
<blockquote>
<p>&quot;그레이 코드는 컴퓨터 안에 있는 게 아니라,<br /><strong>컴퓨터가 현실을 읽기 위해 귀를 기울이는 부분</strong>에 쓰인다.&quot;</p>
</blockquote>
<p>즉, 마우스를 돌리거나, 게임패드를 기울이거나, 3D 프린터가 출력할 때<br />→ 내부에서 인코더가 위치를 읽고<br />→ <strong>그걸 오류 없이 컴퓨터로 보내주기 위해</strong><br />→ <strong>그레이 코드가 쓰이고 있는 거예요!</strong></p>
<blockquote>
<p>“그레이 코드는 컴퓨터가 바퀴 소리를 정확히 이해하려고 만든 언어예요.<br />우리 눈엔 안 보여도, 기계는 그걸로 소통하고 있어요.”</p>
</blockquote>
<p><strong>정확히 말하자면 그레이 코드는 마우스에는 잘 안쓰입니다! 밑에 나오는 쿼드러처를 쓰죠!</strong></p>
<h2 id="✅-정리-요약">✅ 정리 요약</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>로터리 인코더</td>
<td>회전각을 감지하는 센서 디스크 시스템</td>
</tr>
<tr>
<td>기존 문제</td>
<td>여러 비트가 동시에 바뀌면서 <strong>불안정한 중간값</strong>이 발생</td>
</tr>
<tr>
<td>해결책</td>
<td>그레이 코드 → <strong>한 번에 한 비트만 변경되도록 설계된 이진 코드</strong></td>
</tr>
<tr>
<td>효과</td>
<td>센서에서 신호를 안정적으로 읽을 수 있음</td>
</tr>
</tbody></table>
<blockquote>
<p>“디지털 세상도 회전할 땐 흔들릴 수 있어요.<br />그걸 안정시켜주는 똑똑한 언어가 바로 <strong>그레이 코드</strong>랍니다.”</p>
</blockquote>
<h1 id="🎛️-회전-방향만-알고-싶을-때--쿼드러처-인코딩-이야기">🎛️ 회전 방향만 알고 싶을 때? – 쿼드러처 인코딩 이야기</h1>
<h2 id="✅-1-문제-절대-위치는-몰라도-돼-변화와-방향만-알면-돼">✅ 1. 문제: 절대 위치는 몰라도 돼, 변화와 방향만 알면 돼!</h2>
<blockquote>
<p>예: 자동차 라디오 볼륨 놉  </p>
</blockquote>
<ul>
<li>차가 꺼졌을 때 돌려도 <strong>위치가 고정되어 있지 않음</strong></li>
<li>하지만 시동이 걸리면, <strong>돌리는 방향과 변화량만으로 볼륨이 조정됨</strong></li>
</ul>
<p>➡️ 이게 바로 <strong>절대 위치 대신 ‘상대 방향’만 알면 되는 시스템</strong>입니다.</p>
<h2 id="🔄-2-2비트-그레이-코드의-변형-쿼드러처-인코딩">🔄 2. 2비트 그레이 코드의 변형: 쿼드러처 인코딩</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e12b24e0-a9bf-4aab-ab54-f4193f5c71e3/image.png" /></p>
<p>| 쿼드러처 인코딩 = &quot;변화 방향 + 움직임 감지용 회전 신호 체계&quot; |</p>
<ul>
<li>센서가 2개 (A, B)</li>
<li>각 센서가 1비트씩 → 총 2비트</li>
<li>패턴: <code>00 → 01 → 11 → 10 → 00 ...</code> (시계 방향)</li>
<li>반대 방향은 역순: <code>00 → 10 → 11 → 01 → 00 ...</code></li>
</ul>
<h3 id="🧭-이걸-보면-방향이-보인다">🧭 이걸 보면 방향이 보인다!</h3>
<table>
<thead>
<tr>
<th>변화 패턴</th>
<th>방향</th>
</tr>
</thead>
<tbody><tr>
<td>00 → 01 → 11 → 10</td>
<td>시계 방향</td>
</tr>
<tr>
<td>00 → 10 → 11 → 01</td>
<td>반시계 방향</td>
</tr>
</tbody></table>
<h2 id="🧠-3-그럼-쿼드러처가-왜-특별해">🧠 3. 그럼 쿼드러처가 왜 특별해?</h2>
<blockquote>
<p><strong>비트가 &quot;하나씩만&quot; 바뀌고</strong>,  
<strong>변화하는 순서에 따라 회전 방향을 정확히 알 수 있음!</strong></p>
</blockquote>
<ul>
<li>현재 상태 + 직전 상태 → 4비트 (2 + 2)</li>
<li>이걸 조합한 테이블이 바로 표 6-1 (총 16가지 상태)</li>
<li>여기서 정해진 &quot;정상/비정상&quot; 또는 &quot;시계/반시계 방향&quot; 판별 가능</li>
</ul>
<h2 id="🎮-4-어디에-쓰이냐고요">🎮 4. 어디에 쓰이냐고요?</h2>
<table>
<thead>
<tr>
<th>장치</th>
<th>사용 이유</th>
</tr>
</thead>
<tbody><tr>
<td>🖱️ 컴퓨터 마우스</td>
<td>휠 스크롤 방향 감지 (회전 방향과 속도)</td>
</tr>
<tr>
<td>🎛️ 오디오 볼륨 다이얼</td>
<td>절대 위치 없이도 볼륨 조절 가능</td>
</tr>
<tr>
<td>🔁 로터리 노브</td>
<td>터치 없는 조작기 (차량, 오븐, 리모컨 등)</td>
</tr>
<tr>
<td>🤖 로봇 바퀴 센서</td>
<td>몇 바퀴 돌았는지, 어느 방향인지 감지</td>
</tr>
</tbody></table>
<p>➡️ ✨ <strong>모터나 바퀴의 '속도'와 '방향'을 추적할 때도 매우 중요!</strong></p>
<h2 id="5-마우스가-된다고">5. 마우스가 된다고?</h2>
<blockquote>
<p>책 마지막에 나온 말이 바로 하이라이트예요:</p>
</blockquote>
<blockquote>
<p><strong>&quot;쿼드러처 인코더 2개를 90도 엇갈리게 배치하고, 가운데 고무 공을 두면 컴퓨터 마우스다!&quot;</strong></p>
</blockquote>
<p>정확히 맞습니다!  
옛날 볼마우스는 고무 공이 회전 → X축, Y축 인코더가 각각 쿼드러처 방식으로 움직임 감지<br />➡️ 방향과 속도 계산 완료 ✅</p>
<h2 id="📌-요약-정리">📌 요약 정리</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>쿼드러처 인코딩</td>
<td>2비트 회전 인코딩 방식, 방향과 변화량 감지</td>
</tr>
<tr>
<td>절대 위치 필요?</td>
<td>❌ 아님. 상대 변화만 알면 됨</td>
</tr>
<tr>
<td>센서 수</td>
<td>2개면 충분 (A채널, B채널)</td>
</tr>
<tr>
<td>동작 방식</td>
<td>순서 변화로 방향 판별</td>
</tr>
<tr>
<td>실제 활용</td>
<td>마우스 휠, 다이얼, 스크롤, 로봇 바퀴</td>
</tr>
</tbody></table>
<blockquote>
<p>“컴퓨터는 바퀴의 위치를 꼭 알아야 하는 게 아니에요.<br /><strong>‘방금 돌았는지, 어떤 방향으로 돌았는지’</strong> 그것만 알면 충분하답니다!”</p>
</blockquote>
<h2 id="쿼드러처와-그레이-코드의-차이">쿼드러처와 그레이 코드의 차이</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c755a8c0-06d0-4759-af68-6efbdbbdd863/image.png" /></p>
<p><strong>“언제, 어디에” 쓰는지가 쿼드러처 인코더와 다를 뿐이에요.</strong></p>
<h3 id="🧭-그레이-코드-인코더-vs-쿼드러처-인코더-언제-쓰는가">🧭 그레이 코드 인코더 vs 쿼드러처 인코더: 언제 쓰는가?</h3>
<table>
<thead>
<tr>
<th>구분</th>
<th><strong>그레이 코드 인코더</strong></th>
<th><strong>쿼드러처 인코더</strong></th>
</tr>
</thead>
<tbody><tr>
<td>🔍 목적</td>
<td><strong>절대 위치</strong>를 정확하게 읽기</td>
<td><strong>상대적 움직임/방향</strong>만 추적</td>
</tr>
<tr>
<td>🧠 기억</td>
<td>전원이 꺼져도 <strong>위치 기억 가능</strong></td>
<td>전원이 꺼지면 위치 정보 사라짐</td>
</tr>
<tr>
<td>🎯 쓰임새</td>
<td>고정된 각도를 추적 (절대 위치 제어)</td>
<td>돌린 방향, 변화량만 알면 됨</td>
</tr>
<tr>
<td>🛠️ 센서 수</td>
<td><strong>n비트 → n개 센서</strong> (예: 8비트 = 8개 센서)</td>
<td><strong>항상 2개</strong> (A채널, B채널)</td>
</tr>
<tr>
<td>⚙️ 장점</td>
<td>안정적, 중간상태 오류 없음</td>
<td>센서 수 적고 싸고 단순함</td>
</tr>
<tr>
<td>🧪 단점</td>
<td>센서 많고 복잡</td>
<td>잡음에 민감, 초기 위치 모름</td>
</tr>
<tr>
<td>📦 사용처</td>
<td>산업용 로봇, CNC 기계, 태양광 추적기 등</td>
<td>마우스, 볼륨 노브, 휠, 스크롤</td>
</tr>
</tbody></table>
<h3 id="🧠-정리하면-이런-거예요">🧠 정리하면 이런 거예요:</h3>
<ul>
<li><p><strong>정밀한 기계에서 “지금 정확히 어디에 있는지”가 중요한 경우</strong><br />→ ✅ <strong>그레이 코드 인코더 사용</strong></p>
</li>
<li><p><strong>움직였는지만 알면 되는 경우 (회전 방향, 휠)</strong><br />→ ✅ <strong>쿼드러처 인코더 사용</strong></p>
</li>
</ul>
<h3 id="💬-예를-들어-이렇게-쓰여요">💬 예를 들어 이렇게 쓰여요:</h3>
<table>
<thead>
<tr>
<th>장치</th>
<th>인코더 방식</th>
<th>이유</th>
</tr>
</thead>
<tbody><tr>
<td>🖱️ 마우스 휠</td>
<td>쿼드러처</td>
<td>방향만 알면 됨</td>
</tr>
<tr>
<td>🎛️ 오디오 노브</td>
<td>쿼드러처</td>
<td>위치보다 변화량이 중요</td>
</tr>
<tr>
<td>🤖 로봇 관절</td>
<td>그레이 코드</td>
<td>절대 각도 추적 필요</td>
</tr>
<tr>
<td>🌞 태양광 패널 회전</td>
<td>그레이 코드</td>
<td>정확한 방향 유지 필요</td>
</tr>
<tr>
<td>🏭 공장 기계 위치 측정</td>
<td>그레이 코드</td>
<td>정해진 좌표에서 멈춰야 함</td>
</tr>
</tbody></table>
<h3 id="✅-결론">✅ 결론!</h3>
<p><strong>6-14의 그레이 코드 인코더는 &quot;절대 위치 추적용&quot;으로 지금도 많이 쓰입니다.</strong><br />단지 <strong>마우스나 볼륨 조절</strong>처럼 <strong>방향만 필요한 곳</strong>에서는 더 단순한 <strong>쿼드러처 인코더</strong>를 쓰는 거예요!</p>
<blockquote>
<p>“둘 다 센서이지만, 목적이 달라요.<br /><strong>그레이 코드는 '어디 있는지'</strong>,**쿼드러처는 '어디로 움직였는지'를 알려줍니다.” </p>
</blockquote>
<hr />
<h1 id="📡-병렬에서-직렬로-선을-줄이기-위한-통신의-진화-이야기">📡 병렬에서 직렬로: 선을 줄이기 위한 통신의 진화 이야기</h1>
<h2 id="💡-1-병렬-통신은-led-회로에서-시작된다">💡 [1] 병렬 통신은 LED 회로에서 시작된다</h2>
<blockquote>
<p>병렬 통신은 ‘LED 제어’의 확장판이었다</p>
</blockquote>
<p>포트 B에 8개의 LED를 연결하고 아스키 문자를 표현한다?  </p>
<p>이건 사실상 <strong>병렬 데이터 전송</strong>과 똑같은 구조예요.</p>
<p><strong>병렬(Parallel)</strong>이라는 말은, 각각의 데이터 비트를 <strong>동시에 보내기 위해 각기 다른 선을 사용하는 방식</strong>입니다.</p>
<p>실제로 예전 컴퓨터에는 <strong>IEEE 1284 병렬 포트</strong>가 있었어요.<br />→ 프린터, 스캐너 연결할 때 사용</p>
<h2 id="🚨-2-병렬-방식의-진짜-딜레마">🚨 [2] 병렬 방식의 진짜 딜레마</h2>
<blockquote>
<p>빠른 대신 선이 너무 많고, 동기화가 어렵다</p>
</blockquote>
<ul>
<li>예전 컴퓨터엔 <strong>IEEE 1284 병렬 포트</strong>가 있었고, 프린터와 스캐너를 여기에 연결했죠.</li>
<li>병렬 포트에는 아스키 문자를 전송하기 위한 <strong>8개의 데이터 선</strong>이 존재했어요.</li>
<li>하지만 데이터 선만으로는 부족했습니다.</li>
</ul>
<blockquote>
<p>❓ <strong>문제는?</strong><br />“지금 선에 흐르는 값이 진짜 유효한 데이터인지” 알기 어려워요.</p>
</blockquote>
<h2 id="🧭-3-스트로브-신호-지금이다를-알려주는-신호">🧭 [3] 스트로브 신호: ‘지금이다!’를 알려주는 신호</h2>
<blockquote>
<p>병렬 포트는 그래서 스트로브 선이 따로 있었어요</p>
</blockquote>
<ul>
<li>예를 들어 “ABC”를 보내는데, 선을 감지해서 “AABC”가 될 수도 있어요.</li>
<li>→ 스트로브(strobe) 신호가 0이 되는 순간, 8개 선의 값이 ‘유효하다’고 알려주는 구조</li>
</ul>
<p>📊 그림 6-16처럼 각 데이터 비트가 동시에 들어오고, </p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/47c15033-145c-4665-9b6d-c4559dd6ecf1/image.png" /></p>
<p>스트로브 신호가 ‘타이밍’을 알려주는 식으로 동작합니다.</p>
<h2 id="⚠️-4-선이-많으면-문제가-너무-많다">⚠️ [4] 선이 많으면 문제가 너무 많다</h2>
<blockquote>
<p>케이블이 두껍고 비싸며, 잡음에도 약함</p>
</blockquote>
<ul>
<li>병렬 포트의 커넥터: 핀 25개  </li>
<li>IDE 케이블: 선 40개  </li>
<li>단점:<ul>
<li>가격 상승 (구리 많이 듬)</li>
<li>신호 간섭, 전파 지연</li>
<li>긴 거리 전송에는 부적합</li>
</ul>
</li>
</ul>
<h2 id="🔄-5-🧠-직렬-통신이-등장한다">🔄 [5] 🧠 직렬 통신이 등장한다!</h2>
<blockquote>
<p>데이터를 <strong>하나의 선</strong>으로, <strong>시간을 나눠서(bit by bit)</strong> 보내면 어떨까?</p>
</blockquote>
<ul>
<li>전송에 쓰는 선은 1~2개로 줄이고,</li>
<li>각 비트를 <strong>시간 순서대로 줄 세워서</strong> 보내는 방식</li>
<li>핵심 기술 = <strong>시프트 레지스터 (Shift Register)</strong></li>
</ul>
<h3 id="필요한-건">필요한 건?</h3>
<ul>
<li><strong>시계(clock)</strong> 또는 <strong>시작 신호(start bit)</strong></li>
<li><strong>수신자와 송신자 동기화(sync)</strong></li>
</ul>
<pre><code>보내고 싶은 데이터: 0x42 = 01000010
→ 선 한 가닥에 시간 순서대로 0, 1, 0, 0, 0, 0, 1, 0</code></pre><h2 id="⚙️-6-시프트-레지스터의-마법">⚙️ [6] 시프트 레지스터의 마법</h2>
<blockquote>
<p>한 비트씩 밀고 당겨서 직렬 전송 구현하기</p>
</blockquote>
<ul>
<li><strong>송신자</strong>: 비트를 하나씩 밀어서(out) 내보냄</li>
<li><strong>수신자</strong>: 비트를 하나씩 당겨서(in) 읽어들임</li>
</ul>
<p>→ 이것이 <strong>직렬 통신의 기본 구조</strong><br />→ SPI, I2C, UART 등도 다 이 원리를 변형한 것</p>
<p>📘 그림 6-17처럼:</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f12bce7e-2a15-4b2d-8dff-5c1c44c699b3/image.png" /></p>
<p>이때 <strong>동기화(Clock 동기)</strong>가 정말 중요합니다.<br />→ 한 타이밍만 어긋나도 데이터가 전부 어긋남 😵</p>
<h2 id="⏱️-7-마크mark와-스페이스space-통신의-박자-맞추기">⏱️ [7] 마크(Mark)와 스페이스(Space): 통신의 ‘박자 맞추기’</h2>
<blockquote>
<p>수영 경기의 총성과 같은 시작 비트 개념!</p>
</blockquote>
<ul>
<li>라인은 기본적으로 High(1), 즉 &quot;마크&quot; 상태 유지</li>
<li>시작할 땐 Low(0)로 떨어져서 &quot;스페이스&quot; → <strong>Start Bit</strong></li>
<li>그 다음 8비트 데이터, Stop Bit(High)로 마무리</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9a69b83a-2c84-4228-9ba5-714a90151da8/image.png" /></p>
<pre><code>1) 라인은 기본적으로 High 상태 유지 (Idle)
2) Start bit = Low로 떨어짐 (신호 시작 총성!)
3) 그 뒤로 8비트 데이터
4) Stop bit = 다시 High (휴식)</code></pre><p>이걸 <strong>마크(Mark)-스페이스(Space) 방식</strong>이라고 부릅니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a7a4b82f-df0b-487a-af73-8245ddfb96f9/image.png" /></p>
<p>마치 수영 경기에서 총소리에 반응해 타이머를 시작하는 것처럼 작동해요</p>
<h2 id="🧠-8-시간을-나눠-쓰는-기술-시간-분할-멀티플렉싱">🧠 [8] 시간을 나눠 쓰는 기술: 시간 분할 멀티플렉싱</h2>
<blockquote>
<p>한 선에 여러 비트를 시간 순서로 나눠 넣는다</p>
</blockquote>
<p>이 기술은 <strong>시프트 레지스터 + 클럭 신호</strong>와 함께,<br /><strong>슬롯 개념</strong>으로 멀티플렉싱까지 가능합니다.</p>
<p>→ <strong>TDM(Time Division Multiplexing)</strong></p>
<h2 id="🧪-9-속도를-나타내는-단위-보-레이트baud-rate">🧪 [9] 속도를 나타내는 단위: 보 레이트(Baud Rate)</h2>
<blockquote>
<p>초당 비트 수와는 다릅니다!</p>
</blockquote>
<ul>
<li>보 레이트는 ‘초당 기호(심볼) 수’</li>
<li>1비트가 1심볼이면 같지만,</li>
<li>심볼당 2비트, 4비트를 보내면? → <strong>비트 수 &gt; 보 레이트</strong></li>
</ul>
<h2 id="📟-10-텔레타이프-전자-없이-동작한-직렬-통신의-원조">📟 [10] 텔레타이프: 전자 없이 동작한 직렬 통신의 원조</h2>
<blockquote>
<p>키보드 + 프린터가 하나였던 시대의 기계적 혁신</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b6bb28ca-c317-415f-bc2f-31f82e4eec8f/image.png" /></p>
<ul>
<li>텔레타이프 내부에는 아무런 전자 부품이 들어 있지 않고, 축을 회전시키는 모터에 의해 작동된다.</li>
<li>캠과 레버로 작동한 기계식 문자 출력</li>
<li>신호가 오면 ‘덜컥’거리며 잉크 리본을 때려 글자 출력</li>
<li>비동기 통신의 출발점</li>
</ul>
<p>누른 키에 따라 각기 다른 전기 접점을 움직이도록 축이 돌아가고, 그에 따라 아스키 코드가 만들어집니다.</p>
<p><strong>텔레타이프의 또 다른 멋진 트릭은 반이중half-duplex 연결입니다.</strong></p>
<h3 id="🗣️-반이중-↔-전이중-서로-말하는-방식의-차이">🗣️ 반이중 ↔ 전이중: 서로 말하는 방식의 차이</h3>
<blockquote>
<p>무전기 vs 전화기 차이와 같다</p>
</blockquote>
<table>
<thead>
<tr>
<th>모드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>반이중(Half-duplex)</strong></td>
<td>한 번에 한 방향만 가능 (“오버!”)</td>
</tr>
<tr>
<td><strong>전이중(Full-duplex)</strong></td>
<td>양방향 동시 가능 (전화처럼)</td>
</tr>
</tbody></table>
<h2 id="🧩-11-uart-직렬-통신의-표준-인터페이스">🧩 [11] UART: 직렬 통신의 표준 인터페이스</h2>
<blockquote>
<p>Universal Asynchronous Receiver-Transmitter</p>
</blockquote>
<ul>
<li>송신기 + 수신기를 통합한 하드웨어</li>
<li>2개의 선 (TX/RX)만으로 통신 가능</li>
<li>소프트웨어로 흉내 내는 방식: <strong>비트 뱅잉(Bit-Banging)</strong></li>
</ul>
<h2 id="🔌-12-rs-232부터-usb까지-시리얼-포트의-계보">🔌 [12] RS-232부터 USB까지: 시리얼 포트의 계보</h2>
<blockquote>
<p>직렬 포트도 계속 진화해 왔다</p>
</blockquote>
<table>
<thead>
<tr>
<th>표준</th>
<th>특징</th>
</tr>
</thead>
<tbody><tr>
<td>RS-232</td>
<td>초기 시리얼 통신, 고전압 방식</td>
</tr>
<tr>
<td>RS-485</td>
<td>잡음 강한 산업용 차동 신호</td>
</tr>
<tr>
<td><strong>USB</strong></td>
<td>직렬 통신의 최종 진화형, 빠르고 범용</td>
</tr>
</tbody></table>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/98428ea1-78b1-4a56-9939-40ed44bea444/image.png" /></p>
<h2 id="⚖️-13-병렬-vs-직렬-최종-비교-요약">⚖️ [13] 병렬 vs 직렬, 최종 비교 요약</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/87f6fd45-9d64-47cb-96be-4da660c0b8da/image.png" /></p>
<table>
<thead>
<tr>
<th>항목</th>
<th>병렬 (Parallel)</th>
<th>직렬 (Serial)</th>
</tr>
</thead>
<tbody><tr>
<td><strong>속도</strong></td>
<td>✔ 여러 비트를 한 번에 보냄 → 이론상 빠름</td>
<td>❌ 한 비트씩 순차 전송</td>
</tr>
<tr>
<td><strong>선 개수</strong></td>
<td>❌ 많이 필요함 (ex. 8비트 데이터면 8+α 선 필요)</td>
<td>✔ 보통 2~4선이면 충분</td>
</tr>
<tr>
<td><strong>하드웨어 가격</strong></td>
<td>❌ 선 많아서 비쌈 (커넥터, PCB 비용 증가)</td>
<td>✔ 선 적어서 저렴함</td>
</tr>
<tr>
<td><strong>노이즈/간섭</strong></td>
<td>❌ 동기화, 간섭 문제 생기기 쉬움</td>
<td>✔ 비교적 강건</td>
</tr>
<tr>
<td><strong>거리 전송</strong></td>
<td>❌ 짧은 거리에서만 안정적</td>
<td>✔ 장거리 통신에 유리</td>
</tr>
<tr>
<td><strong>구현 복잡도</strong></td>
<td>✔ 간단한 경우도 있지만 → 크면 동기화 어려움</td>
<td>✔ 직관적, 간결함</td>
</tr>
</tbody></table>
<h3 id="🖥️-그런데-왜-병렬-코딩은-인기일까">🖥️ 그런데 왜 <strong>병렬 코딩</strong>은 인기일까?</h3>
<p>여기서 말하는 <strong>병렬 코딩</strong>은 <strong>데이터를 동시에 처리하는 CPU 코어의 병렬 처리</strong>를 말합니다.
이는 <strong>하드웨어가 직렬이냐 병렬이냐</strong>와는 좀 다른 이야기예요!</p>
<h3 id="🧠-병렬-코딩-vs-병렬-통신">🧠 병렬 코딩 vs 병렬 통신</h3>
<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>병렬 통신</td>
<td>데이터를 여러 선을 통해 <strong>동시에 전송</strong>하는 하드웨어 방식</td>
</tr>
<tr>
<td>병렬 코딩 / 병렬 처리</td>
<td>여러 <strong>CPU 코어나 스레드</strong>가 동시에 다른 작업을 수행하는 방식 (소프트웨어적 접근)</td>
</tr>
</tbody></table>
<p>예를 들어 병렬 통신은 키보드가 데이터를 보내는 방식에 대한 이야기이고,<br />병렬 코딩은 사진을 여러 조각으로 나눠 <strong>동시에 필터 처리</strong>하는 것 같은 이야기예요!</p>
<h3 id="📌-병렬-통신은-그래서-어디서-사라졌나">📌 병렬 통신은 그래서 어디서 사라졌나?</h3>
<p>과거:  </p>
<ul>
<li>프린터: 병렬 포트 (IEEE 1284)  </li>
<li>디스크: IDE (40핀 병렬 인터페이스)</li>
</ul>
<p>지금:  </p>
<ul>
<li>프린터: USB (직렬)  </li>
<li>디스크: SATA (직렬)  </li>
<li>모니터: HDMI, DisplayPort (모두 직렬 기반)  </li>
</ul>
<blockquote>
<p>요즘 세상은 대부분 <strong>속도 높이고, 비용 줄이고, 노이즈 줄이기 위해</strong> 병렬 통신 대신 <strong>직렬 방식</strong>을 씁니다.</p>
</blockquote>
<blockquote>
<p>“<strong>병렬 처리(코딩)</strong>는 멀티코어 시대의 핵심이고,<br /><strong>병렬 통신(하드웨어)</strong>은 지금도 쓰이긴 하지만, 많은 곳에서 <strong>직렬로 진화</strong>하고 있어요!”</p>
</blockquote>
<h2 id="보충-설명--직렬-통신-글에서-말하고-싶은-핵심-주제">보충 설명 : 직렬 통신 글에서 말하고 싶은 핵심 주제</h2>
<h3 id="📚-이-글의-구조와-요지">📚 이 글의 구조와 요지</h3>
<table>
<thead>
<tr>
<th>구간</th>
<th>주제</th>
<th>핵심 요지</th>
</tr>
</thead>
<tbody><tr>
<td>⚙️ [6] 시프트 레지스터</td>
<td>직렬 통신의 기본 동작 원리</td>
<td>데이터를 한 비트씩 밀어내고 받아서 전송</td>
</tr>
<tr>
<td>⏱️ [7] 마크/스페이스</td>
<td>비동기 직렬 통신 타이밍</td>
<td>Start Bit와 Stop Bit로 데이터 타이밍 맞춤</td>
</tr>
<tr>
<td>🧠 [8] 시간 분할</td>
<td>멀티플렉싱 개념 도입</td>
<td>한 선으로 여러 데이터 흐름을 시간에 나눠 전송</td>
</tr>
<tr>
<td>🧪 [9] 보 레이트</td>
<td>속도 개념 명확히 하기</td>
<td>보 레이트 = 초당 심볼 수, bps와 다를 수 있음</td>
</tr>
<tr>
<td>📟 [10] 텔레타이프</td>
<td>직렬 통신의 역사</td>
<td>타자기 + 전신 → 직렬 방식으로 메시지 전달</td>
</tr>
<tr>
<td>🗣️ 반이중 vs 전이중</td>
<td>통신 방향성 설명</td>
<td>무전기처럼 한 번에 한쪽만 말하는 반이중, 전화처럼 동시에 가능한 전이중</td>
</tr>
<tr>
<td>🧩 [11] UART</td>
<td>직렬 통신을 위한 표준 하드웨어</td>
<td>Start~Stop 방식, 2선으로 구현 가능</td>
</tr>
<tr>
<td>🔌 [12] 시리얼 포트 계보</td>
<td>직렬 통신 기술의 발전</td>
<td>RS-232 → RS-485 → USB로 발전해옴</td>
</tr>
<tr>
<td>⚖️ [13] 병렬 vs 직렬</td>
<td>요약 비교</td>
<td>요즘은 선이 적고 안정적인 <strong>직렬 통신이 주력</strong></td>
</tr>
</tbody></table>
<h3 id="💡-그럼-왜-이런-얘기를-하느냐">💡 그럼 왜 이런 얘기를 하느냐?</h3>
<p>지금 우리가 사용하는:</p>
<ul>
<li>💻 <strong>USB 포트</strong></li>
<li>📱 <strong>스마트폰 데이터 통신</strong></li>
<li>⌨️ <strong>키보드 입력</strong></li>
<li>🧠 <strong>센서 연결 (I2C, SPI 등)</strong></li>
</ul>
<p>→ 이 모든 것들은 <strong>직렬 통신 기술의 후손들</strong>이에요.</p>
<p>즉, 이 글은 우리 일상 속 컴퓨터와 전자기기 통신의 <strong>기술적 뿌리와 발전 경로</strong>를 설명해주는 겁니다.</p>
<h3 id="🧾-한-줄-요약">🧾 한 줄 요약</h3>
<blockquote>
<p>“선 많고 복잡한 병렬 통신에서 → 선 줄이고 안정성 높인 직렬 통신으로 넘어왔고,<br />지금 우리가 쓰는 USB, UART 같은 것들은 다 그 연장선에 있는 기술이다.”</p>
</blockquote>
<h3 id="❓혹시-궁금할-수-있는-포인트도-미리-정리해드릴게요">❓혹시 궁금할 수 있는 포인트도 미리 정리해드릴게요:</h3>
<table>
<thead>
<tr>
<th>궁금한 점</th>
<th>간단 설명</th>
</tr>
</thead>
<tbody><tr>
<td>시프트 레지스터가 왜 중요해?</td>
<td>직렬 통신에서 데이터를 한 비트씩 밀어내는 구조를 만듦</td>
</tr>
<tr>
<td>왜 마크-스페이스 방식이라 불러?</td>
<td>옛날 전신에서 '마크 = 잉크 점', '스페이스 = 공백'이었기 때문</td>
</tr>
<tr>
<td>텔레타이프가 왜 나와?</td>
<td>현대 직렬 통신의 원조, 전자 없이 물리적으로 동작한 기계식 UART</td>
</tr>
<tr>
<td>보 레이트와 bps가 왜 달라?</td>
<td>한 심볼이 꼭 1비트만 나타내는 건 아니기 때문 (예: 4단계 신호 = 2비트)</td>
</tr>
</tbody></table>
<h2 id="🧾-결론-요약">🧾 결론 요약:</h2>
<blockquote>
<p>“더 많은 선 = 더 빠름”의 시대는 끝났습니다.<br />이제는 “적은 선으로 똑똑하게” 전송하는 직렬 통신이 대세예요.</p>
</blockquote>
<p>💬 USB, UART, I2C, SPI… 우리가 쓰는 대부분의 기기가 이미<br /><strong>직렬 통신을 사용하고 있다는 것</strong>, 기억하세요!</p>
<h3 id="❓-직렬-통신은-선을-줄이니까-좋은-건-알겠는데-그럼-느려지는-거-아냐">❓ “직렬 통신은 선을 줄이니까 좋은 건 알겠는데… 그럼 느려지는 거 아냐?”</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3fd81ff2-285e-4bfb-91bb-d1a74af57acd/image.png" /></p>
<p>→ <strong>맞습니다. &quot;이론적으로는&quot; 병렬이 빠르고 직렬은 느릴 수 있어요.</strong><br />하지만, <strong>실제 현실에서는 직렬 통신이 더 빠르고 효율적인 경우가 많습니다.</strong>  </p>
<p><strong>✅ 병렬 통신이 빠르긴 하지만…</strong></p>
<table>
<thead>
<tr>
<th>병렬 통신의 이론적 장점</th>
</tr>
</thead>
<tbody><tr>
<td>✔️ 8비트 데이터 → 8개의 선으로 한 번에 보냄</td>
</tr>
<tr>
<td>✔️ 시간당 더 많은 데이터 전송 가능</td>
</tr>
</tbody></table>
<p><strong>❗ 하지만 현실은?</strong></p>
<ul>
<li><strong>신호가 동시에 도착하지 않음 (타이밍 차, 전파 지연)</strong></li>
<li>선이 많으면 <strong>간섭(crosstalk)</strong> 발생</li>
<li>PCB 설계도 복잡하고 비용 높음</li>
<li><strong>멀리 전송할수록 문제가 더 커짐</strong></li>
</ul>
<blockquote>
<p>➡️ <strong>빠른 대신 불안정하고, 설계가 까다롭고 비쌈</strong></p>
</blockquote>
<p><strong>✅ 직렬 통신은 느릴 것 같지만…</strong></p>
<table>
<thead>
<tr>
<th>직렬 통신의 현실적 장점</th>
</tr>
</thead>
<tbody><tr>
<td>✔️ 선이 적어 <strong>간섭, 잡음에 강함</strong></td>
</tr>
<tr>
<td>✔️ 장거리 전송에 적합</td>
</tr>
<tr>
<td>✔️ 고속으로 클럭을 높이기 쉬움</td>
</tr>
<tr>
<td>✔️ 설계 간단 + 비용 저렴 + 내구성 좋음</td>
</tr>
</tbody></table>
<p><strong>🧠 예를 들어 볼게요</strong></p>
<ol>
<li>병렬 예시: 옛날 하드디스크 인터페이스 IDE</li>
</ol>
<ul>
<li>40핀 케이블, 잡음 많음, 거리 짧음  </li>
<li>최대 전송 속도: 133MB/s</li>
</ul>
<ol start="2">
<li>직렬 예시: 현재의 SATA</li>
</ol>
<ul>
<li>단 7핀 케이블, 잡음 적고 선 얇음  </li>
<li>속도: 최대 600MB/s (SATA 3 기준)</li>
</ul>
<p>➡️ 병렬보다 <strong>직렬이 훨씬 빠르고 안정적</strong>입니다!</p>
<p><strong>🔍 왜 더 빠른가요?  **
**= 고속 직렬 통신(High-Speed Serial Communication)</strong> 기술 때문이에요</p>
<table>
<thead>
<tr>
<th>기술</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>클럭 동기화</strong></td>
<td>직렬은 <strong>고정된 속도</strong>로 안정된 신호 전달 가능</td>
</tr>
<tr>
<td><strong>차동 신호</strong></td>
<td>두 선을 반대로 흐르게 해서 <strong>잡음 제거</strong></td>
</tr>
<tr>
<td><strong>멀티채널 직렬화</strong></td>
<td>여러 데이터 스트림을 직렬화해서 보내고, 다시 복원</td>
</tr>
<tr>
<td><strong>비트 레벨 전송</strong></td>
<td>직렬은 데이터를 더 <strong>작고 빠르게</strong> 쪼개서 전송 가능</td>
</tr>
</tbody></table>
<p><strong>📌 핵심 요약</strong></p>
<table>
<thead>
<tr>
<th>구분</th>
<th>병렬 통신</th>
<th>직렬 통신</th>
</tr>
</thead>
<tbody><tr>
<td>이론 속도</td>
<td>높음</td>
<td>낮음</td>
</tr>
<tr>
<td>실제 구현 속도</td>
<td>낮음 (신호 간섭, 지연)</td>
<td>높음 (고속 직렬화 기술)</td>
</tr>
<tr>
<td>거리</td>
<td>짧음</td>
<td>김</td>
</tr>
<tr>
<td>안정성</td>
<td>낮음</td>
<td>높음</td>
</tr>
<tr>
<td>사용 예시</td>
<td>예전 프린터, IDE 등</td>
<td>USB, SATA, HDMI, I2C 등</td>
</tr>
</tbody></table>
<p><strong>✅ 결론</strong></p>
<blockquote>
<p><strong>직렬 통신은 ‘1개씩 보내서 느릴 것 같지만’,<br />기술 발전으로 병렬보다 빠르고 효율적인 경우가 많습니다.</strong></p>
</blockquote>
<p><strong>💬 한 문장 정리</strong></p>
<blockquote>
<p><strong>“직렬 통신은 느린 게 아니라, ‘덜 복잡한 방식으로 더 빠르게 가는 길’을 택한 것”입니다.</strong></p>
</blockquote>
<h1 id="📡-마크-스페이스-방식의-한계와-변조modulation의-등장">📡 마크-스페이스 방식의 한계와 변조(Modulation)의 등장</h1>
<p>이 내용은 <strong>직렬 통신 방식의 한계</strong>, 특히 <strong>마크-스페이스 방식의 단점</strong>을 극복하기 위해 등장한 <strong>변조(Modulation)</strong> 기술과 <strong>모뎀(Modem)</strong>의 원리를 설명하는 중요한 파트</p>
<h2 id="✅-1-마크-스페이스-방식의-한계">✅ 1) 마크-스페이스 방식의 한계</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>마크(Mark)</strong></td>
<td>선이 High 상태(1)일 때</td>
</tr>
<tr>
<td><strong>스페이스(Space)</strong></td>
<td>선이 Low 상태(0)일 때</td>
</tr>
<tr>
<td><strong>문제</strong></td>
<td>전송 거리가 길어지면 신호가 흐려져서 <strong>마크/스페이스 구분이 어려워짐</strong></td>
</tr>
<tr>
<td><strong>적용 불가 환경</strong></td>
<td>장거리 전화선, 전파 기반 통신 등에서는 신호가 왜곡됨</td>
</tr>
</tbody></table>
<h2 id="✅-2-해결책-변조modulation-개념의-도입">✅ 2) 해결책: 변조(Modulation) 개념의 도입</h2>
<blockquote>
<p><strong>우리가 보내려는 디지털 데이터를 어떤 '파동'에 실어 보내는 방식</strong></p>
</blockquote>
<h3 id="🌀-반송파-carrier">🌀 반송파 (Carrier)</h3>
<ul>
<li>기본이 되는 <strong>사인파(주파수 + 진폭)</strong>  </li>
<li>데이터를 실어 보낼 <strong>“통신용 파도”</strong></li>
</ul>
<h3 id="🔄-변조-modulation">🔄 변조 (Modulation)</h3>
<ul>
<li>디지털 신호를 반송파에 실어서 보내는 과정  </li>
<li>데이터를 단순한 전압 신호가 아니라 <strong>특정한 주파수 변화</strong>로 표현</li>
</ul>
<h2 id="✅-3-대표적-변조-방식-fsk-주파수-편이-변조">✅ 3) 대표적 변조 방식: FSK (주파수 편이 변조)</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>FSK (Frequency Shift Keying)</td>
<td>0과 1을 서로 다른 주파수로 표현</td>
</tr>
<tr>
<td>예시</td>
<td>마크(1) = 1270Hz, 스페이스(0) = 1070Hz</td>
</tr>
<tr>
<td>특징</td>
<td>전화선에서도 안정적으로 전송 가능</td>
</tr>
</tbody></table>
<p>📘 Bell 103A 모뎀 (1960년대)<br />→ 전화선 기반 통신에서 FSK 방식으로 <strong>전이중(Full-Duplex)</strong> 통신을 구현<br />→ <strong>300 Baud 속도</strong>로 문자 데이터를 주파수로 변조해서 송수신</p>
<h2 id="✅-4-사인파란">✅ 4) 사인파란?</h2>
<ul>
<li>모든 파동의 기본</li>
<li>수학적으로 원을 회전시키는 점의 y좌표를 시간 순서로 표현하면 → 사인파</li>
<li>사인파의 구성 요소:</li>
</ul>
<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>진폭 (Amplitude)</strong></td>
<td>파동의 세기 (높이)</td>
</tr>
<tr>
<td><strong>주파수 (Frequency)</strong></td>
<td>1초에 반복되는 횟수 (단위: Hz)</td>
</tr>
<tr>
<td><strong>파장 (Wavelength)</strong></td>
<td>파동 한 주기의 길이</td>
</tr>
<tr>
<td><strong>속도 (v)</strong></td>
<td>파동이 전파되는 속도 (v = λ × f)</td>
</tr>
</tbody></table>
<h2 id="✅-5-복조-demodulation와-모뎀modem">✅ 5) 복조 (Demodulation)와 모뎀(Modem)</h2>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>복조</strong></td>
<td>주파수로 실려온 신호에서 다시 0과 1로 디지털 신호 복원</td>
</tr>
<tr>
<td><strong>모뎀(Modem)</strong></td>
<td>변조(Modulation) + 복조(Demodulation)를 수행하는 장치</td>
</tr>
</tbody></table>
<p>🎧 영화 속 <strong>다이얼업 모뎀 소리</strong><br />→ 전화선에 신호가 실리며 생긴 <strong>FSK 변조 주파수</strong>의 실제 음향</p>
<h2 id="📡-모뎀-vs-공유기-차이-정리">📡 모뎀 vs 공유기 차이 정리</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/970dd3d1-a952-4de2-99ca-714bfbf409ad/image.png" /></p>
<h3 id="1-🛠-기능-비교">1. 🛠 기능 비교</h3>
<table>
<thead>
<tr>
<th>구분</th>
<th><strong>모뎀</strong></th>
<th><strong>공유기</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>외형</strong></td>
<td>안테나 없음 / 박스형</td>
<td>안테나 있음 / 다양한 크기</td>
</tr>
<tr>
<td><strong>기능</strong></td>
<td>- 아날로그 ↔ 디지털 신호 변환<br />- 홈 네트워크를 인터넷에 연결<br />- 컴퓨터, 스마트폰, 태블릿 등과 직접 연결<br />- 모뎀 없으면 인터넷 자체 사용 불가</td>
<td>- 여러 장치를 하나의 네트워크로 연결<br />- 와이파이, 방화벽, DHCP 등 네트워크 기능<br />- 유선/무선 연결 모두 지원 가능</td>
</tr>
<tr>
<td><strong>중요 포인트</strong></td>
<td>외부 인터넷망을 연결하는 핵심 장치</td>
<td>내부 네트워크를 구성해주는 장치</td>
</tr>
</tbody></table>
<h3 id="2-🌟-장단점-비교">2. 🌟 장단점 비교</h3>
<table>
<thead>
<tr>
<th>구분</th>
<th><strong>모뎀</strong></th>
<th><strong>공유기</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>장점</strong></td>
<td>- LAN과 인터넷 연결 시 유용<br />- 호환성 좋고 데이터 교환에 최적</td>
<td>- 여러 장치와 네트워크 공유<br />- 생산성 향상<br />- 다리 역할(브리지 기능) 수행 가능</td>
</tr>
<tr>
<td><strong>단점</strong></td>
<td>- 신호 간섭 시 품질 저하<br />- 연결 거리 제한</td>
<td>- 연결 장치 수 많으면 속도 저하 우려</td>
</tr>
</tbody></table>
<h3 id="3-🔍-구분-방법">3. 🔍 구분 방법</h3>
<table>
<thead>
<tr>
<th>항목</th>
<th><strong>모뎀</strong></th>
<th><strong>공유기</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>안테나</strong></td>
<td>❌ 없음</td>
<td>✅ 있음</td>
</tr>
<tr>
<td><strong>설치 위치</strong></td>
<td>신발장, 다용도실, TV 근처 등<br />다세대 주택 지하 1층(외부 설치 포함)</td>
<td>TV/PC 근처, 집 내부</td>
</tr>
</tbody></table>
<ul>
<li><strong>모뎀(MODEM)</strong>은 &quot;인터넷과 집을 연결&quot;하는 관문이고,  </li>
<li><strong>공유기(Router)</strong>는 &quot;집 안에서 여러 장치가 인터넷을 공유&quot;하도록 해주는 다리입니다.</li>
</ul>
<blockquote>
<p>모뎀은 ‘밖과 연결’, 공유기는 ‘안에서 나눔’에 초점이 있다고 보면 됩니다.</p>
</blockquote>
<h3 id="🏠-가정용-인터넷-연결-구조-설명">🏠 가정용 인터넷 연결 구조 설명</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/aa740b20-408e-4369-a191-5d6af0aca670/image.png" /></p>
<ol>
<li>외부 통신망 → 집으로 들어오는 <strong>케이블</strong></li>
</ol>
<ul>
<li>벽면에서 나오는 <strong>인터넷 회선</strong>(케이블, 광케이블 등)</li>
<li>이것은 <strong>ISP(인터넷 제공업체)</strong>로부터 오는 인터넷 신호입니다.</li>
</ul>
<ol start="2">
<li>📡 <strong>모뎀(MODEM)</strong></li>
</ol>
<ul>
<li>이 신호는 아날로그 형태이기 때문에,<br /><strong>모뎀이 디지털 신호로 변환해주는 장치</strong>입니다.</li>
<li>즉, <strong>인터넷을 집 안으로 들여오는 관문 역할</strong>을 해요.</li>
<li>여기까지는 <strong>&quot;하나의 장치만 연결 가능&quot;</strong>합니다.</li>
</ul>
<ol start="3">
<li>🔄 <strong>공유기(Router)</strong> 또는 <strong>라우터</strong></li>
</ol>
<ul>
<li>모뎀에서 나온 인터넷 신호를 받아서,</li>
<li>집 안의 여러 기기에 <strong>분배(공유)</strong>해주는 역할을 합니다.</li>
<li>보통 2가지 방식으로 연결됩니다:<ul>
<li><strong>이더넷 케이블을 통한 유선 연결</strong></li>
<li><strong>2.4GHz / 5GHz 주파수의 무선 연결 (Wi-Fi)</strong></li>
</ul>
</li>
</ul>
<p>📌 <strong>공유기는 &quot;분배기 + 방화벽 + DHCP&quot; 역할도 합니다.</strong></p>
<ol start="4">
<li>🎯 최종적으로 기기 연결</li>
</ol>
<table>
<thead>
<tr>
<th>기기</th>
<th>연결 방식</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>데스크탑 PC</td>
<td>유선 연결</td>
<td>안정적이고 빠름</td>
</tr>
<tr>
<td>스마트폰 / 태블릿</td>
<td>무선 연결</td>
<td>Wi-Fi로 연결, 이동성 좋음</td>
</tr>
</tbody></table>
<p><strong>🔁 요약 정리</strong></p>
<pre><code class="language-plaintext">[외부 인터넷 회선]
      ↓
   [모뎀]
      ↓
   [공유기]
   ↓        ↓
유선       무선
↓            ↓
PC        스마트폰 등</code></pre>
<h3 id="💬-한-문장-정리">💬 한 문장 정리</h3>
<blockquote>
<p>“마크-스페이스 방식은 짧은 거리에서는 유효하지만,<br />장거리 통신에서는 <strong>주파수 기반의 변조 방식(FSK)</strong>이 필요합니다.<br />그래서 등장한 게 바로 ‘모뎀’입니다!”</p>
</blockquote>
<h1 id="🔌-usb-통신-단순하지만-똑똑하다">🔌 USB 통신, 단순하지만 똑똑하다</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c5e34d99-632e-47d9-90ec-bd00a79a54b2/image.png" /></p>
<blockquote>
<p>&quot;USB는 그저 전원 주는 케이블이 아닙니다.<br />내부엔 정해진 규칙과 체계가 있는 <strong>네트워크 구조</strong>가 숨어있어요.&quot;</p>
</blockquote>
<h2 id="✅-1-usb는-버스지만-자율적이지-않다">✅ 1) USB는 '버스'지만 '자율적'이지 않다</h2>
<table>
<thead>
<tr>
<th>❌ 오해</th>
<th>✅ 실제</th>
</tr>
</thead>
<tbody><tr>
<td>모든 장치가 동등하게 자유롭게 말할 수 있음</td>
<td>👉 아니다! <strong>컨트롤러가 모든 걸 관리</strong>함</td>
</tr>
</tbody></table>
<h3 id="🔧-기본-구조">🔧 기본 구조</h3>
<ul>
<li><strong>호스트(컨트롤러)</strong>: 컴퓨터, 스마트폰 등 USB 통신을 총괄하는 쪽</li>
<li><strong>종단점(endpoint)</strong>: 키보드, 마우스, USB 메모리 등 <strong>주어진 지시에만 반응</strong>하는 쪽</li>
<li>USB는 모든 장치가 <strong>동등한 권한을 갖지 않음</strong></li>
</ul>
<blockquote>
<p>즉, <strong>컨트롤러(주인)만이 말하고 질문하고 데이터 요청을 보냅니다.<br />장치(종단점)는 응답만 합니다.</strong></p>
</blockquote>
<h2 id="📨-2-패킷packet-기반-전송">📨 2) 패킷(PACKET) 기반 전송</h2>
<blockquote>
<p>&quot;우체국 소포처럼, USB도 '패킷' 단위로 통신해요.&quot;</p>
</blockquote>
<h3 id="📦-패킷의-구성">📦 패킷의 구성</h3>
<ul>
<li><strong>헤더(Header)</strong>: 발신자, 수신자, 타입 등 정보 포함<br />(ex. 소포 겉면 주소처럼)</li>
<li><strong>페이로드(Payload)</strong>: 실제 데이터<br />(ex. 소포 안에 들어 있는 물건)</li>
</ul>
<h3 id="📌-왜-중요한가">📌 왜 중요한가?</h3>
<ul>
<li>데이터가 엉켜도 어느 장치로, 어떤 용도인지 알 수 있음  </li>
<li>비트 스트림을 마구 흘리는 방식이 아니라, <strong>정리된 트래픽 흐름</strong>이라는 것</li>
</ul>
<h2 id="🎵-3-실시간-오디오·영상도-ok-isochronous-transfer">🎵 3) 실시간 오디오·영상도 OK: Isochronous Transfer</h2>
<blockquote>
<p>&quot;음향·영상은 '실시간'으로 흘러야 하잖아요?&quot;</p>
</blockquote>
<p>USB는 단순히 파일만 보내는 게 아닙니다.<br /><strong>시간에 민감한 데이터 (예: 오디오/비디오 스트리밍)</strong>도 처리할 수 있도록 특별한 전송 방식이 있습니다.</p>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Isochronous Transfer</strong></td>
<td>등시성 전송. <strong>데이터 전송 타이밍 보장</strong> 필요</td>
</tr>
<tr>
<td><strong>대역폭 예약</strong></td>
<td>장치가 &quot;1초에 1MB 필요해요&quot;라고 요구 가능</td>
</tr>
<tr>
<td><strong>컨트롤러가 결정</strong></td>
<td>대역폭 여유가 없으면 요청 거절할 수 있음</td>
</tr>
</tbody></table>
<blockquote>
<p>예: USB로 연결된 마이크, 웹캠, 실시간 게임패드 등은 이 방식을 사용해요.</p>
</blockquote>
<h2 id="📋-전체-흐름-요약">📋 전체 흐름 요약</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5268fc2f-54c2-4709-bc07-3050cd9f8f65/image.png" /></p>
<pre><code class="language-plaintext">[Host] 컴퓨터/스마트폰  
   ↓   컨트롤러가 관리  
[Device] 키보드, 마우스, 외장하드 등  
   ↑   컨트롤러가 요청하면 응답</code></pre>
<ul>
<li>전송 단위는 <strong>Packet</strong></li>
<li>전송 방식은 <strong>Control, Bulk, Interrupt, Isochronous</strong>로 구분</li>
<li>장치는 임의로 말하지 않음 = <strong>USB는 중앙 집중형 구조</strong></li>
</ul>
<h2 id="🧾-핵심-요약">🧾 핵심 요약</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>컨트롤러 중심</strong></td>
<td>호스트(PC)가 모든 전송 흐름을 제어</td>
</tr>
<tr>
<td><strong>패킷 기반</strong></td>
<td>데이터는 항상 패킷(소포) 형태로 정리되어 전달됨</td>
</tr>
<tr>
<td><strong>등시성 전송 지원</strong></td>
<td>시간 민감한 데이터(오디오/영상)를 위한 전송 방식</td>
</tr>
<tr>
<td><strong>대역폭 예약 가능</strong></td>
<td>장치가 필요한 통신량을 미리 요청할 수 있음</td>
</tr>
</tbody></table>
<h2 id="💬-정리-한-문장">💬 정리 한 문장</h2>
<blockquote>
<p><strong>USB는 단순한 전선이 아니라,<br />네트워크처럼 구조화된 지능형 통신 시스템입니다.</strong><br />(컨트롤러 중심, 패킷 전송, 시간 예약까지 가능한 고급 통신 구조)</p>
</blockquote>
<h2 id="보충정리-두-가지-의미의-usb">보충정리 두 가지 의미의 USB</h2>
<h3 id="🔌-1-usb는-두-가지로-나뉜다">🔌 1. USB는 두 가지로 나뉜다</h3>
<table>
<thead>
<tr>
<th>구분</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>① 인터페이스로서의 USB</strong></td>
<td>데이터를 주고받는 <strong>전송 방식(프로토콜)</strong>. <br />예: USB 2.0, 3.0, 3.2, Type-C 등</td>
</tr>
<tr>
<td><strong>② 저장장치로서의 USB</strong></td>
<td>플래시 기반 저장장치(SSD/USB 메모리 등)를 <br />USB 방식으로 연결한 물리적 장치</td>
</tr>
</tbody></table>
<h3 id="📦-2-우리가-꽂는-usb-ssd는-어떤-구조">📦 2. 우리가 꽂는 &quot;USB SSD&quot;는 어떤 구조?</h3>
<p>USB 저장장치(USB SSD)는 다음 두 가지 구성으로 되어 있어요:</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/aee13867-2d12-4c59-b258-2b9b9f062e27/image.png" /></p>
<pre><code>[컨트롤러 칩] ← USB 프로토콜 처리
       ↓
[낸드 플래시 메모리] ← 실제 데이터 저장 공간</code></pre><h4 id="✅-핵심-구성요소">✅ 핵심 구성요소</h4>
<table>
<thead>
<tr>
<th>구성 요소</th>
<th>기능</th>
</tr>
</thead>
<tbody><tr>
<td><strong>USB 컨트롤러</strong></td>
<td>PC에서 오는 USB 신호(패킷)를 해석하고<br />내부 저장장치로 전달</td>
</tr>
<tr>
<td><strong>NAND 플래시</strong></td>
<td>데이터를 전기적으로 저장하는 고속 메모리</td>
</tr>
<tr>
<td><strong>(보조: DRAM 캐시)</strong></td>
<td>쓰기 속도 가속을 위한 임시 저장 공간 (일부 SSD에만 있음)</td>
</tr>
</tbody></table>
<h3 id="⚙️-3-usb-ssd와-일반-ssd의-기술적-차이">⚙️ 3. USB SSD와 일반 SSD의 기술적 차이</h3>
<table>
<thead>
<tr>
<th>항목</th>
<th><strong>USB SSD</strong></th>
<th><strong>SATA / NVMe SSD</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>연결 방식</strong></td>
<td>USB (2.0, 3.0, Type-C 등)</td>
<td>SATA, PCIe</td>
</tr>
<tr>
<td><strong>인터페이스</strong></td>
<td>USB Mass Storage / UASP</td>
<td>SATA 또는 NVMe</td>
</tr>
<tr>
<td><strong>속도</strong></td>
<td>USB 3.2 기준 최대 10~20Gbps</td>
<td>NVMe는 최대 64Gbps 이상</td>
</tr>
<tr>
<td><strong>OS 인식 방식</strong></td>
<td>Removable device</td>
<td>Fixed disk (운영체제는 다르게 취급함)</td>
</tr>
<tr>
<td><strong>용도</strong></td>
<td>휴대성 중심 (백업, 휴대용 부트 등)</td>
<td>내부 저장장치 중심 (OS 설치 등)</td>
</tr>
</tbody></table>
<h3 id="🧠-4-usb-ssd는-어떻게-작동하나요">🧠 4. USB SSD는 어떻게 작동하나요?</h3>
<p><strong>전송 흐름 예시:</strong></p>
<pre><code>[PC]  
 ↓ USB 프로토콜 (패킷 기반 요청)  
[USB 컨트롤러]  
 ↓  
[NAND 플래시 메모리] (읽기/쓰기)</code></pre><ul>
<li>PC는 USB 프로토콜을 따라 <strong>파일 전송 요청 패킷</strong>을 보냅니다.  </li>
<li>컨트롤러는 이를 해석해서 <strong>NAND 메모리에 읽기/쓰기 작업을 지시</strong>합니다.  </li>
<li>이때 패킷은 단순한 신호가 아니라<br /><strong>주소 정보, 파일 내용, 에러 체크 코드</strong> 등이 포함된 구조화된 데이터예요.</li>
</ul>
<table>
<thead>
<tr>
<th>질문</th>
<th>답변</th>
</tr>
</thead>
<tbody><tr>
<td>USB는 무엇인가요?</td>
<td>통신 방식이자 커넥터 형태입니다. (버스 구조)</td>
</tr>
<tr>
<td>USB SSD는 어떤 구조인가요?</td>
<td>USB 컨트롤러 + NAND 플래시 조합</td>
</tr>
<tr>
<td>일반 SSD와 기술적 차이점은?</td>
<td>연결 방식, 속도, 내부 통신 방식이 다릅니다</td>
</tr>
<tr>
<td>USB SSD도 패킷 기반 통신인가요?</td>
<td>✅ 맞습니다! USB도 TCP처럼 <strong>헤더 + 페이로드</strong> 구조의 패킷을 사용합니다</td>
</tr>
</tbody></table>
<blockquote>
<p><strong>USB SSD는 ‘저장장치’지만, 그 속엔 USB라는 통신 프로토콜이 뛰고 있습니다.<br />단순한 전선이 아니라, 네트워크처럼 동작하는 구조화된 장치예요.</strong></p>
</blockquote>