<h1 id="정리하게-된-배경">정리하게 된 배경</h1>
<p>이전에 업무 도중 <code>read lock</code>이 걸린 적이 있었다. 내가 걸린 것은 아니었긴 한데.. </p>
<blockquote>
<p>한 테이블에 한 명의 개발자는 update를 1명의 다른 개발자는 select문 하고 있는 상황인데 select 때 commit을 하지 않으면서 lock이 걸림 결국, select 때, 꼭 트랜잭션을 끝내기 위해 rollback이나 commit을 해줘야 한다고 한다.</p>
</blockquote>
<p>나는 이전까지 update, delete, insert만 조심하면 되는 줄 알았는데 select도 조심해줘야 한다는 사실이 좀 놀라웠다.</p>
<p>그래서 그때, 찾아보고 정리해야지 하다가 읽어보기만 하고 정리는 따로 하지 않게 되어 글또 7회차 글 낼 때도 되었고 해서 전체적인 lock에 대해 정리하고 그리고 <strong>실무에서 데이터 베이스 테이블은 거의 외래키를 쓰지 않는데</strong> 그 이유도 lock과도 관련이 있으니 정리하여 보자.</p>
<p>뿐만 아니라 <code>Lock</code>은 <strong>데이터 정합성을 보장하고 동시성 이슈를 해결할 수 있는 방식 중 하나</strong>이며 서버 개발에서 가장 중요한 부분이라고 한다. 또한 Lock을 다루면서 DeadLock이 발생하는 케이스와 이를 예방하는 방법 또한 알아보자</p>
<blockquote>
<p>Lock 해결은 dba가 해주지만, </p>
</blockquote>
<ul>
<li>LOCK은 좋은 걸까?⭕ 나쁜 걸까?❌ 뭔가 인식은 안 좋아보니까</li>
<li>어떤 때 발생하는 지</li>
<li>어떻게 사용되는지</li>
<li>어떻게 예방하는지
등은 서버 개발의 중요하니 정리하는 것이 좋은 것 같음</li>
</ul>
<h1 id="✏️1-lock-개요">✏️1. Lock 개요</h1>
<p>일반적으로 하나의 DB 서버에는 여러대의 애플리케이션이 붙어서 동시에 접근하여 데이터를 읽고 쓰게 된다. </p>
<p>이러한 상황에서는 <code>Race Condition(경합상태)</code>와 같은 동시성 이슈가 발생할 수 있는데, MySQL을 비롯한 관계형 데이터베이스는 이러한 상황에서 애플리케이션의 <code>고가용성</code>(HA(high availability) : 서버, 네트워크, 프로그램 등의 정보 시스템이 상당히 <strong>오랜 기간 동안 지속적으로 정상 운영이 가능한 성질</strong>)을 보장하기 위해 다양한 형태의 Lock을 제공한다.</p>
<p><strong>Lock</strong>은 결국 <strong>트랜잭션</strong> 처리에서 <strong>서로 충돌 없이</strong> 안전하게 데이터를 읽고 쓸 수 있도록 순서를 보장해주는 장치이다.</p>
<blockquote>
<p><code>Lock</code>은 DB 내부(예: S락, X락, Intention Lock)와 애플리케이션 레벨(낙관적 락, 비관적 락) 양쪽에서 다양하게 적용되며, 데이터 무결성과 고가용성을 확보하기 위한 핵심 기법이다.</p>
</blockquote>
<p><code>Lock의 종류</code>에는 S락·X락·Intention Lock은 DB 엔진 내부에서 실제로 “어떤 데이터를 잠그는가”에 관한 <strong>물리적 락</strong>이 있고, <code>낙관적/비관적 락</code> 그 위에서 애플리케이션 트랜잭션이 “언제, 어떤 방식으로 충돌을 방지할 것인가”를 결정하는 <strong>동시성 제어 기법의 락</strong>이 있다.</p>
<h2 id="1-race-condition경합-상태">1) Race Condition(경합 상태)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b615c137-300c-426c-8f34-42924c769074/image.png" /></p>
<blockquote>
<p>여러 트랜잭션이 동일 자원(테이블·Row·메모리 영역)을 동시에 수정·조회하려 하면서 예상치 못한 충돌이 발생하는 상황</p>
</blockquote>
<ul>
<li>예: 동시에 같은 계좌에서 돈을 인출할 때, 각각 읽은 잔액이 정확히 반영되지 않아 잘못된 결과를 초래할 수 있음</li>
<li>Lock을 통해 “내가 수정하는 동안 다른 트랜잭션은 접근하지 못하게” 만드는 등, 동시성 문제를 제어</li>
</ul>
<h2 id="2-deadlock교착-상태이란">2) DeadLock(교착 상태)이란?</h2>
<blockquote>
<p>둘 이상의 트랜잭션이 서로가 보유한 자원을 해제해주길 기다리다가 무한 대기에 빠지는 상태</p>
</blockquote>
<ul>
<li>예: 트랜잭션 A가 Row1을 잠그고 Row2에 대한 락을 기다리는 중, 트랜잭션 B가 Row2를 잠그고 Row1에 대한 락을 기다려 서로 대기</li>
<li>DBMS는 일정 시간이 지나면 교착 상태를 감지해, 한쪽 트랜잭션을 롤백 처리해 DeadLock을 해소</li>
</ul>
<h1 id="2-물리적-lock-유형">2. 물리적 Lock 유형</h1>
<blockquote>
<p>여기서는 mysql 기준으로 정리해보고자 한다.</p>
</blockquote>
<h2 id="1-shared-lock-s--공유-잠금">1) Shared Lock (S) : 공유 잠금</h2>
<p>흔히 <strong>읽기 락(Read Lock)</strong> 이라고 불리며, 특정 Row(레코드)에 걸리는 락이다. S라고도 한다. <strong>읽는 동안(Read) 다른 트랜잭션이 해당 Row를 수정하지 못하도록</strong> 방지하기 위해 해당 Row에 대해 변경이 일어나지 않도록 구성하는 Read Lock으로 활용된다. 보통 SELECT ... LOCK IN SHARE MODE 로 획득</p>
<p>만약 해당 Row에 이 Shared Lock이 걸려있다면 Row를 Write하거나 Update하는 Lock은 사용할 수 없다. 특정 Row(레코드)에 S락이 걸려 있는 동안에는, 해당 Row가 <strong>수정(UPDATE, DELETE 등)</strong>되지 않도록 보호한는 것이다.</p>
<blockquote>
<p>잠금이 걸린 상태에서는 다른 트랜잭션이 해당 Row에 대해 쓰기나 갱신을 시도할 수 없으므로, <strong>읽는 동안 항상 동일한 결과를 얻을 수 있다.</strong> </p>
</blockquote>
<p>예를 들어 동일한 Row에 접근하는 두 트랜잭션 A와 B가 동시에 발생했다고 가정하자. 트랜잭션 A는 특정 Row에 대해 SELECT를 한다. 반면 B는 동일한 Row에 UPDATE를 한다.
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e82f11a1-8db0-4b69-928c-5b9dbcb65f93/image.png" /></p>
<p>*<em>Q. 이 상황에서 A가 Read Lock을 획득하고 Row를 조회하는 동안 B가 UPDATE를 호출하면? *</em>
1️⃣ A가 먼저 Read Lock을 획득하고 있으므로 B의 요청은 <code>대기</code>한다. 
2️⃣ 이후 A가 정상적으로 데이터를 조회하고나서 해당 Row에 대해 Lock을 반납하면 B의 UPDATE 구문이 호출된다.</p>
<blockquote>
<p><code>SELECT 작업</code>과 <code>UPDATE 작업</code>을 수행하는 트랜잭션이 발생하는 것과 달리 <strong>SELECT 작업을 하는 여러 개의 트랜잭션은 동시에 Shared Lock을 획득(공유)할 수 있다.</strong> </p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/00650496-27b8-4e3b-b049-f24dc6e06442/image.png" /></p>
<p>예를 들어 이번에는 동일한 Row를 조회하는 두 트랜잭션 A와 B가 동시에 발생했다고 가정하자. A는 특정 Row에 대해 SELECT를 한다. B도 동일한 Row에 SELECT를 한다. 이 경우 단순 데이터 조회이므로 굳이 B가 대기할 필요가 없다. B도 Shared Lock을 획득하고 해당 Row를 조회한다. 이미 트랜잭션 A가 어떤 Row에 S락을 걸어둔 상태에서, 트랜잭션 B도 똑같이 S락을 획득할 수 있음</p>
<blockquote>
<p><code>Shared Lock</code>의 목적이 항상 동일한 읽기 결과를 보장하기 위함이며, 제한 없이 데이터를 읽을 수 있지만, <strong>다른 트랜잭션이 해당 데이터를 수정할 수 없게 된다.</strong></p>
</blockquote>
<ul>
<li>S락: “읽는 동안 다른 사람이 수정 못 하게 보호”</li>
<li>S락끼리는 호환(둘 다 읽기 작업이니 충돌이 없음)</li>
</ul>
<h2 id="2-exclusive-lock-x--배타적-잠금">2) Exclusive Lock (X) : 배타적 잠금</h2>
<p>Shared Lock과 같이 Row 레벨(= 하나의 Row)에 적용되는 Lock 유형이지만 이 <strong>LocK은 Write/Update Lock</strong>으로 활용된다. X라고도 한다.</p>
<p>예를 들어 동일한 Row에 접근하는 두 트랜잭션 A와 B가 동시에 발생했다고 가정하자. A는 특정 Row에 대해 SELECT를 한다. (Shared Lock을 획득한다.) 반면 B는 동일한 Row에 <code>UPDATE</code>를 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/fb0304cd-df8a-44ab-b48d-14220fdbb266/image.png" /></p>
<p>*<em>Q. 이 상황에서 A가 Read Lock을 획득하고 Row를 조회하는 동안 B가 UPDATE를 호출하면? *</em>
1️⃣ A가 Shared Lock을 획득하고 있으므로 B는 UPDATE를 호출하기 전에 Exclusivce Lock을 대기한다.<br />2️⃣ A가 정상적으로 데이터를 조회하고나서 해당 Row에 대해 Shared Lock을 반납한다. 
3️⃣ 이후 B는 Exclusvice Lock을 획득하고 UPDATE 구문이 호출된다.</p>
<blockquote>
<p>즉, 동일한 Row에 대해 작업하는 여러 개의 트랜잭션은 <strong>서로 동시에 Shared Lock과 Exclusive Lock을 획득할 수 없다.</strong></p>
</blockquote>
<p><strong>쉽게 말해 동일한 Row에 대해 A가 Shared Lock을 획득하면서 B가 Exclusive Lock을 획득할 수 없다.</strong> Shared Lock을 여러 트랜잭션이 동시에 가질 수 있지만 <code>Exclusive Lock</code>은 오직 한 트랜잭션만이 가질 수 있다.</p>
<p>SELECT ... FOR UPDATE는 Row에 대해 이 Exclusive Lock을 거는데 다른 Lock을 사용하는 트랜잭션에서는 항상 대기하게 된다. (또다른(SELECT ... FOR UPDATE도 대기해야한다.)</p>
<ul>
<li>X락: “쓰는 동안 다른 사람이 읽거나 쓰지 못하게 보호”<strong>(하지만, MariaDB나 MySql의 InnDB는 읽을 수 있다 그 이유는 아래에서 설명)</strong></li>
</ul>
<h3 id="⛔-참고--select와-s락에-대한-오해">⛔ 참고 : SELECT와 S락에 대한 오해</h3>
<p>1번 트랜잭션이 A레코드의 쓰기락을 얻었음에도 2번 트랜잭션은 아무 일 없이 A레코드를 조회하는데 성공한다. 왜일까?</p>
<p>SELECT와 S락에 대한 오해를 하면 안된다.</p>
<p>SELECT 한다는 것이 S락을 건다는 의미가 아니다.
<strong>SELECT, 즉 읽는 것(또는 조회)이란 어떤 '행위'일 뿐이지 '락'을 의미하진 않는다.</strong></p>
<h2 id="3-intention-lock-is-ix">3) Intention Lock (IS, IX)</h2>
<h3 id="intention-lock이란">Intention Lock이란?</h3>
<p><strong>Table 레벨</strong>에서 걸리는 Lock 유형으로 <strong>Shared Lock</strong>의 의도(= Intention Shared)인 경우 <strong>IS</strong>, <strong>Exclusive Lock</strong>의 의도(= Intention Exclusive)인 경우 <strong>IX</strong>  </p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/df8d0df6-9bd2-4b9c-86ef-156cfebaee69/image.png" /></p>
<blockquote>
<p><code>테이블 전체</code>에 “이 테이블의 특정 Row에 Shared/Exclusive Lock을 걸겠다”는 의사를 미리 표시하여 <strong>Lock 충돌</strong>을 사전에 감지하고 <strong>DeadLock</strong>을 예방하는 목적</p>
</blockquote>
<h3 id="⭐-동작-방식">⭐ 동작 방식</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1eba912b-0218-4ae5-98d7-1edd4bd2d6a6/image.png" /></p>
<ol>
<li><strong>SELECT 쿼리</strong>: 테이블에 <strong>IS Lock</strong>을 걸고, 실제 Row에는 <strong>S Lock</strong>을 획득  </li>
<li><strong>INSERT/UPDATE/DELETE 쿼리</strong>: 테이블에 <strong>IX Lock</strong>을 걸고, 실제 Row에는 <strong>X Lock</strong>을 획득  </li>
<li>테이블 레벨에서 먼저 IS/IX 락을 잡음으로써, 다른 트랜잭션이 해당 테이블에 대해 무리하게 스키마 변경(ALTER TABLE 등)이나 충돌성 락을 설정하려 하면 <strong>대기</strong>하게 만듦</li>
</ol>
<h3 id="예시-상황">예시 상황</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5c01a01f-434d-4565-b579-90b1a26391bf/image.png" /></p>
<ul>
<li><strong>트랜잭션 A</strong>가 특정 Row를 수정하기 위해 <strong>IX + X Lock</strong>을 이미 보유 중인 상태  </li>
<li><strong>트랜잭션 B</strong>가 동일한 테이블에 대해 <strong>스키마 변경(ALTER TABLE 등)</strong> 작업을 시도할 경우, 테이블 단위에서 <strong>Exclusive Lock</strong>이 필요  </li>
<li>테이블에 이미 <strong>IX Lock</strong>이 존재하므로 충돌이 감지되어, B는 <strong>A가 끝날 때까지 대기</strong>  </li>
<li>이를 통해 <strong>불필요한 Lock 충돌</strong> 및 <strong>DeadLock</strong>을 방지</li>
</ul>
<h3 id="장점-및-주의사항">장점 및 주의사항</h3>
<ol>
<li><strong>Lock 충돌 사전 방지</strong>: 테이블 레벨에서 “의도”를 표시하므로, 큰 락이 필요한 작업(테이블 변경 등)과 Row 단위 잠금이 서로 충돌할 경우 빠르게 감지 및 대기 처리  </li>
<li><strong>동시성</strong>: Intention Lock은 Row 자체에 직접 영향을 주지 않으므로, 여러 트랜잭션이 동시에 <strong>IS/IX</strong>를 획득할 수 있음  </li>
<li><strong>테이블 구조 변경 시 주의</strong>: <code>ALTER TABLE</code>, <code>DROP TABLE</code> 등 테이블 레벨에서 배타적인 락이 필요한 작업과는 충돌 발생. 이 경우 여러 트랜잭션이 동시에 Intention Lock을 획득할 수 없고, <strong>Exclusive Lock</strong> 대기로 이어짐</li>
</ol>
<blockquote>
<p><strong>Intention Lock(IS, IX)</strong>은 MySQL InnoDB 엔진에서 <strong>Row 단위 Lock과 테이블 단위 Lock이 서로 어떻게 충돌하는지</strong>를 체계적으로 관리하기 위해 존재한다. 이를 통해 <strong>불필요한 교착 상태</strong>를 줄이고, 여러 트랜잭션이 동시에 안전하게 작업할 수 있도록 돕는 중요한 기능이다.</p>
</blockquote>
<ul>
<li>S락(Shared) / X락(Exclusive) → Row(레코드) 단위에서 걸린다.</li>
<li>IS락(Intention Shared) / IX락(Intention Exclusive) → Table(테이블) 단위에서 걸린다.</li>
</ul>
<blockquote>
<p>🔥 참고 : <strong>Intention Lock은 <code>테이블 전체</code>에 “어떤 행(Row)에 S/X락을 걸 의도가 있다”</strong>고 미리 표시하는 역할이고,
실제 <code>데이터(=Row) 자체</code>를 보호하는 잠금은 S락 또는 X락을 통해 이루어진다고 보면 된다.</p>
</blockquote>
<h2 id="4-s락과-x락-사이의-호환성compatibility">4) S락과 X락 사이의 호환성(Compatibility)</h2>
<blockquote>
<p><strong>“S락은 S락끼리 호환, X락은 아무것도 호환 안 됨.”</strong></p>
</blockquote>
<ol>
<li><p><strong>S락 ↔ S락 : 호환</strong> ✔  </p>
<ul>
<li>트랜잭션 A가 Row에 S락을 보유 중이라면, 트랜잭션 B도 S락을 얻을 수 있다.  </li>
<li>둘 다 “읽기 전용”인 상태이므로, 동시에 접근해도 데이터 정합성에 문제가 생기지 않는니다.</li>
</ul>
</li>
<li><p><strong>S락 ↔ X락 : 호환 안 됨</strong>  ✖</p>
<ul>
<li>트랜잭션 A가 Row에 S락을 보유 중일 때, 트랜잭션 B가 X락을 시도하면 대기 상태에 빠진다.  </li>
<li>반대로 트랜잭션 A가 X락을 보유 중일 때, B가 S락을 시도해도 대기 상태입니다.  </li>
<li>이유: X락은 배타적이므로 <strong>다른 어떤 락</strong>도 함께 걸 수 없음.</li>
</ul>
</li>
<li><p><strong>X락 ↔ X락 : 당연히 호환 안 됨</strong>  ✖</p>
<ul>
<li>어떤 Row에 이미 X락이 걸려 있으면, 그 Row에 또 다른 X락을 걸려고 시도해도 대기 상태로 들어단다.</li>
</ul>
</li>
</ol>
<h2 id="5-예시로-보는-흐름">5) 예시로 보는 흐름</h2>
<h3 id="예시-a-s락과-s락은-함께-보유-가능">예시 A: “S락과 S락은 함께 보유 가능”</h3>
<ol>
<li><strong>트랜잭션 A</strong>: 특정 Row(A레코드)에 대해 <code>SELECT ... LOCK IN SHARE MODE</code> 수행 → A레코드에 <strong>S락</strong> 획득  </li>
<li><strong>트랜잭션 B</strong>: 동일한 Row(A레코드)에 대해 <code>SELECT ... LOCK IN SHARE MODE</code> 수행 → <strong>S락</strong> 추가 획득 성공  </li>
<li>두 트랜잭션 A, B는 모두 <strong>읽기 잠금(Shared Lock)</strong> 이므로 서로 간섭하지 않고 동시에 데이터를 조회할 수 있음.</li>
</ol>
<h3 id="예시-b-s락과-x락은-충돌">예시 B: “S락과 X락은 충돌”</h3>
<ol>
<li><strong>트랜잭션 A</strong>: 특정 Row(A레코드)에 대해 <code>SELECT ... LOCK IN SHARE MODE</code> 수행 → A레코드에 <strong>S락</strong> 보유  </li>
<li><strong>트랜잭션 B</strong>: 같은 Row(A레코드)에 대해 <code>UPDATE ...</code> 또는 <code>SELECT ... FOR UPDATE</code> 수행 → <strong>X락</strong> 시도  </li>
<li>이미 A가 <strong>S락</strong>을 가지고 있으므로, B는 <strong>X락</strong>을 얻기 위해 A가 트랜잭션을 종료(커밋 또는 롤백)하거나 A의 S락을 해제할 때까지 <strong>대기 상태</strong>가 됨.</li>
</ol>
<h2 id="6-⛔-오해를-풀어보기-x락을-걸면-다른-트랜잭션이-읽을-수-없다">6) ⛔ 오해를 풀어보기: “X락을 걸면 다른 트랜잭션이 읽을 수 없다?”</h2>
<h3 id="⚠️-x락을-걸면-다른-트랜잭션이-읽을-수-없다">⚠️ &quot;X락을 걸면 다른 트랜잭션이 읽을 수 없다?”</h3>
<p>아무래도 “X락 = 쓰기 락”이라는 이름 때문에, “X락이 있으면 <strong>어떤 형태의 읽기(SELECT)도</strong> 불가능하다”고 단정하기 쉽다. </p>
<blockquote>
<p>하지만 실제 MySQL InnoDB(기본) 환경에서는 <strong>MVCC</strong>로 인해 <strong>단순 SELECT</strong>는 레코드의 “과거 버전”을 읽을 수도 있어서, X락을 갖고 있다고 해서 곧바로 모든 SELECT가 차단되는 것은 아니다.</p>
</blockquote>
<ul>
<li>단순 SELECT (락 요청 없음): <strong>X락 보유 중에도 조회 가능</strong> (InnoDB의 버전 관리)  </li>
<li>명시적 SELECT (락 요청 있음 → S락 시도): <strong>X락과 호환 불가</strong> → 대기 혹은 충돌</li>
</ul>
<p><strong>즉, “X락을 걸면 다른 트랜잭션이 읽지 못한다”라고 말하는 건 개념적으로 단순화된 표현</strong>이며, 더 정확하게는 <strong>“X락이 걸려 있는 레코드에 대해 새롭게 ‘S락(=읽기 락)’을 요청하면 충돌이 발생하여 대기한다.”</strong> 라고 볼 수 있다.</p>
<ul>
<li><strong>단순 <code>SELECT</code> (기본 READ)</strong>  <ul>
<li><strong>락을 얻지 않음</strong> (MVCC 버전 스냅샷을 조회)  </li>
<li>→ X락이 걸려 있어도 이 “과거 버전”을 읽을 수 있음  </li>
<li>→ <strong>충돌·대기 없음</strong></li>
</ul>
</li>
</ul>
<blockquote>
<p>출처 : <a href="https://velog.io/@soongjamm/Select-%EC%BF%BC%EB%A6%AC%EB%8A%94-S%EB%9D%BD%EC%9D%B4-%EC%95%84%EB%8B%88%EB%8B%A4.-X%EB%9D%BD%EA%B3%BC-S%EB%9D%BD%EC%9D%98-%EC%B0%A8%EC%9D%B4">Select 쿼리는 S락이 아니다. (X락과 S락의 차이)</a></p>
</blockquote>
<h3 id="⚠️-x락을-걸면-다른-트랜잭션이-읽을-수-없다-1">⚠️ &quot;X락을 걸면 다른 트랜잭션이 읽을 수 없다?”</h3>
<p>아래 내용을 핵심 포인트로 정리하자면, <strong>MySQL InnoDB에서는 “SELECT” 자체가 곧바로 S락(Shared Lock)을 획득하지 않는다</strong>는 점이 가장 중요하다. </p>
<h3 id="❓-s락과-x락은-호환되지-않다면서요">❓ “S락과 X락은 호환되지 않다면서요?”</h3>
<p>맞다. <strong>S락 ↔ X락</strong>은 호환되지 않는다. 즉, 한 트랜잭션이 <strong>X락</strong>을 보유 중이라면, 다른 트랜잭션이 <strong>S락</strong>을 걸려고 할 때 <strong>대기 상태</strong>가 된다(또는 반대).  </p>
<blockquote>
<p>하지만 “SELECT(단순 조회) = S락 획득”이 <strong>아니라는 점</strong>이 포인트이다. </p>
</blockquote>
<p>InnoDB에서 단순 SELECT는 <strong>락을 요청하지 않기 때문에</strong>, 사실상 S락이 아니라 “락 없이 과거 버전(MVCC)”을 읽는다고 보면 된다. 따라서 X락과 충돌이 발생하지 않아서 바로 읽기가 가능한 것임.</p>
<ul>
<li><strong><code>SELECT ... LOCK IN SHARE MODE</code> (S락 명시 요청)</strong>  <ul>
<li><strong>S락</strong> 획득 시도  </li>
<li>→ X락 보유 중인 트랜잭션과 <strong>충돌</strong>, 대기 발생  </li>
</ul>
</li>
<li><strong>단순 <code>SELECT ...</code> (락 명시 없음)</strong>  <ul>
<li><strong>S락 획득 X</strong>, MVCC 스냅샷 조회  </li>
<li>→ X락이 걸려 있어도 <strong>충돌 없음</strong>, 즉시 읽기 가능</li>
</ul>
</li>
</ul>
<h3 id="🧐-다른-dbms에서는-왜-다를-수-있나">🧐 다른 DBMS에서는 왜 다를 수 있나?</h3>
<p>DBMS마다 <strong>SELECT</strong> 시 기본적으로 S락을 획득하도록 설계된 경우가 있다. 그런 DB에서는 트랜잭션이 X락을 잡고 있을 때 <strong>SELECT가 대기</strong>하거나 <strong>실패</strong>하는 상황이 발생할 수 있다.  </p>
<ul>
<li>예: 일부 DBMS는 “Dirty Read를 허용하지 않기 위해” SELECT시 <strong>Shared Lock</strong>을 획득하는 경우가 있습니다. 그러면 X락을 가진 트랜잭션과 충돌이 발생해, SELECT도 대기하게 된다.</li>
</ul>
<p>MySQL InnoDB는 <strong>MVCC</strong> 기법을 통해 <strong>락 없이도</strong> 정합성 있는 데이터를 조회할 수 있는 구조이므로, “단순 SELECT가 S락을 요청하지 않는다”는 것이 특징이다.</p>
<h3 id="어떻게-하면-innodb에서-x락--select-충돌을-볼-수-있을까-😶">어떻게 하면 InnoDB에서 X락 &amp; SELECT 충돌을 볼 수 있을까? 😶</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ca504a16-40b9-41c6-9d2f-0982ee68737d/image.png" /></p>
<ol>
<li><strong>먼저 X락</strong>을 잡는다.  <ul>
<li>예: <code>SELECT ... FOR UPDATE;</code> 또는 <code>UPDATE ...</code> 로 특정 Row에 X락 획득  </li>
</ul>
</li>
<li><strong>다른 트랜잭션</strong>에서 <strong>S락 명시</strong>를 요청  <ul>
<li>예: <code>SELECT ... LOCK IN SHARE MODE;</code>  </li>
</ul>
</li>
</ol>
<p>이 경우 X락 ↔ S락은 호환되지 않으므로, 두 번째 트랜잭션은 <strong>X락이 해제될 때까지 대기</strong>하게 된다.</p>
<blockquote>
<p>만약 두 번째 트랜잭션이 단순 <code>SELECT ...</code>만 한다면, MySQL InnoDB는 S락을 걸지 않고 버전 스냅샷을 읽어 <strong>대기 없이</strong> 바로 조회를 완료한다.</p>
</blockquote>
<h3 id="결론-정리">결론 정리</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/88c821be-5528-4d5c-8333-4cb8a02da866/image.png" /></p>
<ol>
<li><strong>X락 ↔ S락 = 호환 불가</strong>가 맞지만, <strong>MySQL InnoDB에서 단순 SELECT는 “S락”을 잡지 않는다.</strong>  </li>
<li>따라서 “X락이 걸린 행을 다른 트랜잭션이 읽을 수 없는 것”이 아니라, InnoDB에서는 “<strong>락 없이도</strong> 과거 데이터를 읽을 수 있으므로” 실제로는 충돌 없이 읽는다.  </li>
<li>다만, “SELECT ... LOCK IN SHARE MODE”처럼 <strong>명시적으로 S락을 잡는</strong> SELECT라면 X락과 충돌하여 대기가 발생한다.  </li>
<li>DBMS마다 기본적으로 SELECT에 S락을 걸게 설계된 시스템도 있으므로, MySQL만의 MVCC 특성과 <strong>‘락 없는 읽기’</strong> 방식을 이해하는 것이 중요하다.</li>
</ol>
<h1 id="3-낙관적-락optimistic과-비관적-락pessimistic">3. 낙관적 락(Optimistic)과 비관적 락(Pessimistic)</h1>
<blockquote>
<p><strong>S락/X락</strong>은 DB가 <strong>Row</strong>를 물리적으로 잠그는 메커니즘<br /><strong>낙관적/비관적 락</strong>은 트랜잭션(또는 애플리케이션)에서 <strong>동시성 제어</strong>를 하는 <strong>전략</strong></p>
</blockquote>
<h2 id="1-비관적-락-pessimistic-lock">1) 비관적 락 (Pessimistic Lock)</h2>
<pre><code class="language-sql">START TRANSACTION;
SELECT * 
  FROM some_table 
 WHERE pk = 10 
 FOR UPDATE;  -- X락 획득
-- ... UPDATE 등 쓰기 작업 ...
COMMIT;       -- 락 해제</code></pre>
<h3 id="개념"><strong>개념</strong>:</h3>
<ul>
<li><strong>“충돌이 날 것”</strong>이라고 비관적으로 가정하여, 데이터를 수정하기 전에 미리 <strong>DB 락(주로 X락)</strong>을 잡고 시작</li>
<li>예) <code>SELECT ... FOR UPDATE</code> </li>
<li>Row-level Lock(행 단위 락)을 설정한다. 이 락은 트랜잭션이 완료될 때까지 유지된다.</li>
<li>충돌은 적지만, <strong>동시에 접근하는 트랜잭션이 많으면 병목</strong>과 <strong>데드락</strong> 위험 커짐</li>
</ul>
<h3 id="동작-방식"><strong>동작 방식</strong></h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/da0abb8a-a71c-45d6-b460-113e47bd6217/image.png" /></p>
<ol>
<li>데이터를 읽을 때, 동시에 해당 Row에 락을 설정하여 다른 트랜잭션의 접근을 차단한다. 이는 <strong>동시성을 제한</strong>하는 대가로 <code>안정성</code>을 확보하는 과정이다. 즉, *<em>트랜잭션이 시작될 때 Shared Lock 또는 Exclusive Lock을 걸고 시작하는 방법이다. *</em></li>
<li>다른 트랜잭션이 동일 데이터를 수정하려 할 경우, 대기하거나 차단된다.</li>
<li>트랜잭션이 정상적으로 종료되면 락이 해제되어 다른 트랜잭션이 접근할 수 있다.</li>
</ol>
<h3 id="사용-사례"><strong>사용 사례</strong>:</h3>
<ul>
<li><p>데이터 충돌 가능성이 높은 엔티티나 실시간 데이터 보호가 필요한 경우 적합하다.</p>
</li>
<li><p>예) 은행 계좌 잔액 관리, 재고 차감 등. 이러한 시스템에서는 <strong>안정성과 무결성이 최우선</strong></p>
<pre><code class="language-java">@Transactional
public void updateAccountBalance(Long accountId, BigDecimal amount) {
    // 계좌 정보를 읽으면서 PESSIMISTIC_WRITE 락을 설정합니다.
    Account account = entityManager.find(Account.class, accountId, LockModeType.PESSIMISTIC_WRITE);

    // 잔액을 업데이트합니다. 다른 트랜잭션은 대기 상태가 됩니다.
    account.setBalance(account.getBalance().add(amount));

    // 변경 사항을 저장합니다. 락은 트랜잭션 종료 시 해제됩니다.
    entityManager.merge(account);
}</code></pre>
</li>
</ul>
<h2 id="2-낙관적-락-optimistic-lock">2) 낙관적 락 (Optimistic Lock)</h2>
<pre><code class="language-sql">-- 1) SELECT pk, value, version FROM some_table WHERE pk=10;
-- 2) UPDATE some_table
--       SET value='newVal', version=version+1
--     WHERE pk=10 AND version=?
-- =&gt; 1 row affected 면 성공, 0이면 충돌(낙관적 락 실패)</code></pre>
<p>혹은 JPA/Hibernate에서 <code>@Version</code> 필드를 이용해 자동으로 체크.</p>
<h3 id="개념-1">개념</h3>
<ul>
<li><strong>“충돌이 별로 없을 것”</strong>이라고 낙관적으로 가정하여, 락을 잡지 않고 자유롭게 수정 후 - 커밋 직전에 버전(Version) 필드나 타임스탬프 등을 비교</li>
<li>예) <code>@Version</code>(JPA) 또는 <code>WHERE pk=? AND version=?</code>(SQL)  </li>
<li>병목과 데드락은 적지만, <strong>충돌 시 재시도</strong> 로직 필요 → 충돌이 잦으면 성능 저하</li>
<li>충돌 발생 시 애플리케이션에서 이를 처리(재시도, 롤백 등)해야 하므로 추가적인 구현이 필요하며, 이로 인해 개발 복잡도가 다소 증가할 수 있다.</li>
</ul>
<h3 id="동작-방식-1"><strong>동작 방식</strong>:</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/21466ffc-03f2-4032-be5d-132c6c2d338a/image.png" /></p>
<ol>
<li>데이터를 읽을 때 <code>version</code> 필드 값을 함께 가져옵니다. 이는 현재 데이터를 기준으로 비교할 기반값을 제공하는 단계입니다.</li>
<li>수정 시, 애플리케이션은 현재의 <code>version</code> 값과 DB의 <code>version</code> 값을 비교합니다.</li>
<li>두 값이 동일할 경우, 업데이트를 진행하고 <code>version</code> 값을 증가시킵니다. 이를 통해 데이터의 일관성을 보장합니다.</li>
<li>값이 다를 경우, 다른 트랜잭션에서 데이터를 수정한 것으로 간주하고 충돌 예외를 발생시킵니다. 이로 인해 데이터 손실을 방지합니다.</li>
</ol>
<h3 id="사용-사례-1"><strong>사용 사례</strong>:</h3>
<ul>
<li><p>충돌 가능성이 낮은 엔티티나 비즈니스 로직에서 적합</p>
</li>
<li><p>예) 게시판의 게시글 수정, 사용자 프로필 업데이트 등. 이러한 경우 동시성이 높아도 안정적으로 처리 가능</p>
<pre><code class="language-java:">@Entity
public class UserProfile {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @Version
    private int version;

    // Getters and Setters
}

@Transactional
public void updateProfile(Long userId, String newName) {
    // 데이터베이스에서 사용자 프로필을 조회합니다.
    UserProfile profile = entityManager.find(UserProfile.class, userId);

    // 조회한 사용자 이름을 변경합니다.
    profile.setName(newName);

    // 변경된 엔티티를 저장합니다. 만약 version이 맞지 않으면 예외가 발생합니다.
    entityManager.merge(profile);
}</code></pre>
</li>
</ul>
<h2 id="3-락-해제-방법-lock-release">3) 락 해제 방법 (Lock Release)</h2>
<p>1) <strong>트랜잭션 종료 시 해제</strong>  </p>
<ul>
<li>Commit/Rollback 시점에 Row 락(S/X) 자동 해제</li>
</ul>
<p>2) <strong>Autocommit 설정</strong>  </p>
<ul>
<li><code>autocommit=1</code>이면 단일 쿼리 후 자동 해제  </li>
<li><code>autocommit=0</code>+명시적 트랜잭션 중 Commit/Rollback 누락 시 락이 길게 유지 → 주의</li>
</ul>
<p>3) <strong>강제 해제</strong>  </p>
<ul>
<li>세션 종료(KILL 명령 등) 시 트랜잭션 롤백→락 해제  </li>
<li>운영 환경에서는 가급적 <strong>명시적 종료</strong> 권장</li>
</ul>
<h2 id="4-낙관적-vs-비관적-어느-쪽-동시성-성능이-더-좋나">4) 낙관적 vs 비관적, 어느 쪽 동시성 성능이 더 좋나?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/40782d51-4f1c-448e-96f8-2de797e1eb3c/image.png" /></p>
<table>
<thead>
<tr>
<th>특징</th>
<th>낙관적 락</th>
<th>비관적 락</th>
</tr>
</thead>
<tbody><tr>
<td><strong>충돌 가정</strong></td>
<td>드물다</td>
<td>잦다</td>
</tr>
<tr>
<td><strong>락 설정 위치</strong></td>
<td>애플리케이션 레벨</td>
<td>DB 레벨</td>
</tr>
<tr>
<td><strong>성능</strong></td>
<td>일반적으로 우수</td>
<td>동시성 처리 성능 저하 가능</td>
</tr>
<tr>
<td><strong>DeadLock 위험</strong></td>
<td>없음</td>
<td>존재</td>
</tr>
<tr>
<td><strong>롤백 처리</strong></td>
<td>애플리케이션에서 수동 처리 필요</td>
<td>DB 트랜잭션에서 자동 처리 가능</td>
</tr>
</tbody></table>
<ul>
<li><strong>낙관적 락</strong>:  <ul>
<li>DB 락 없이 진행 → <strong>대기 없음</strong>, <strong>DeadLock 위험↓</strong>  </li>
<li>단, 충돌 시 재시도 비용 발생  </li>
</ul>
</li>
<li><strong>비관적 락</strong>:  <ul>
<li>미리 락 선점 → 충돌은 적지만, 여러 트랜잭션이 몰리면 <strong>병목·DeadLock↑</strong>  </li>
</ul>
</li>
</ul>
<blockquote>
<p>결국 <strong>업데이트 충돌 빈도</strong>와 <strong>재시도 허용 가능성</strong> 등을 고려해 선택해야 한다. 가장 중요한 것은 트래픽 패턴, 충돌 빈도, 비즈니스 중요도에 맞춰 적절한 락 전략을 고르는 것이며, 필요하다면 여러 방식을 혼합하여 적용하는 것이 좋다.</p>
</blockquote>
<h2 id="5-혼합-사용-사례-✨">5) 혼합 사용 사례 ✨</h2>
<ul>
<li><p><strong>하이브리드 접근</strong>:</p>
<ul>
<li>동일한 테이블에서도 상황에 따라 낙관적 락과 비관적 락을 나누어 사용합니다.</li>
<li>예) 게시글 테이블:<ul>
<li>조회수 증가: 비관적 락을 사용하여 중복 증가 방지 (잦은 갱신).</li>
<li>내용 수정: 낙관적 락을 사용하여 충돌 발생 시 유연하게 처리 (드문 갱신).</li>
</ul>
</li>
</ul>
</li>
<li><p><strong>특정 시점에 비관적 락 사용</strong>:</p>
<ul>
<li>예) 결제 확정 시, <code>SELECT ... FOR UPDATE</code>를 사용하여 Row를 선점하고 중복 결제를 방지합니다. 이는 결제와 같은 중요한 트랜잭션에서 데이터 무결성을 유지하기 위한 방법입니다.</li>
</ul>
</li>
</ul>
<h2 id="6-결론">6) 결론</h2>
<ol>
<li><strong>충돌이 잦고, 재시도 비용이 크다면</strong> : <strong>비관적 락</strong>이 적합, 데이터 무결성을 최우선으로 고려하는 상황에 적합</li>
<li><strong>충돌이 드물고, 재시도가 가능하다면</strong>: <strong>낙관적 락</strong>이 적합, 성능과 동시성을 중요시하는 환경에서 유용합니다.</li>
<li><strong>복잡한 시스템</strong>: 필요에 따라 낙관적 락과 비관적 락을 혼합하여 사용하는 것이 가장 효과적이다. 각 상황에 맞는 전략을 선택해야 한다.</li>
</ol>
<h2 id="7-db-충돌-상황을-개선하는-방법">7) DB 충돌 상황을 개선하는 방법</h2>
<ol>
<li><p><strong>비관적 락 사용:</strong></p>
<ul>
<li>테이블 Row에 락을 걸어 다른 트랜잭션이 동일한 Row를 수정하지 못하게 한다.</li>
<li>트랜잭션이 종료될 때까지 락이 유지되므로 데이터 일관성이 보장된다.</li>
</ul>
</li>
<li><p><strong>낙관적 락 사용:</strong></p>
<ul>
<li>데이터를 수정할 때, 변경 전에 원래 데이터의 상태(version 등)를 확인하여 다른 작업의 충돌 여부를 판단한다.</li>
<li>충돌이 감지되면 예외를 발생시키고 애플리케이션에서 이를 처리한다.</li>
</ul>
</li>
</ol>
<h4 id="비관적-락-예제-상황">비관적 락 예제 상황</h4>
<ul>
<li>Transaction_1: 테이블의 ID 2번을 읽음 (name = Karol).</li>
<li>Transaction_2: 동일 ID를 읽고 업데이트 시도 → Transaction_1이 종료되기 전까지 대기.</li>
<li>Transaction_1이 종료(commit) 후, Transaction_2가 업데이트를 수행.</li>
</ul>
<h4 id="낙관적-락-예제-상황">낙관적 락 예제 상황</h4>
<ul>
<li>A가 ID 2번을 읽음 (version = 1).</li>
<li>B가 동일 Row를 읽고 업데이트 (version = 2로 변경).</li>
<li>A가 업데이트 시도 → version 불일치로 업데이트 실패.</li>
</ul>
<h2 id="8-롤백rollback-처리">8) 롤백(Rollback) 처리</h2>
<h3 id="비관적-락-롤백">비관적 락 롤백</h3>
<ul>
<li>단일 트랜잭션 내에서 여러 Row를 수정하는 경우, <strong>하나라도 실패하면 DB에서 전체 Rollback.</strong><pre><code class="language-sql">BEGIN TRANSACTION;
UPDATE table1 SET col = 'value1' WHERE id = 1;
UPDATE table2 SET col = 'value2' WHERE id = 2;
-- 오류 발생 시
ROLLBACK;</code></pre>
</li>
</ul>
<h3 id="낙관적-락-롤백">낙관적 락 롤백</h3>
<ul>
<li>애플리케이션 레벨에서 충돌 처리 및 재시도를 <code>수동</code>으로 구현해야 함.<pre><code class="language-sql">SELECT id, name, version FROM theTable WHERE id = 2;
UPDATE theTable SET name = 'newValue', version = version + 1 WHERE id = 2 AND version = 1;
-- AffectedRows == 0이면 충돌 발생</code></pre>
</li>
</ul>
<h1 id="4-deadlock교착-상태🤢의-발생-원리">4. DeadLock(교착 상태)🤢의 발생 원리</h1>
<h2 id="1-deadlock이란">1) DeadLock이란?</h2>
<ul>
<li>트랜잭션 경합 상태가 재귀적으로 반복되는 상황</li>
<li>구체적으로, 여러 개의 트랜잭션이 서로가 보유한 자원을 무한정 대기하며, 누구도 다음 단계로 진행하지 못하는 상태</li>
<li>실제 운영 환경(멀티 스레드, 여러 DB 세션)에서 한 번쯤은 겪게 되는 이슈</li>
</ul>
<p>DB 레벨에서 Timeout 설정과 애플리케이션 레벨에서 Retry 정책을 통해 방어 로직을 둘 수는 있지만, <strong>근본적으로 DeadLock 상황 자체를 방지하는 것이 가장 좋다.</strong></p>
<blockquote>
<p>물리적인 락(예: DB 내부에서 S락·X락 등을 서로 획득하고 놓지 않는 상황)이나 애플리케이션 차원에서 잘못 설계된 락 획득 순서 등이 서로 충돌할 때, 그 결과로 나타나는 교착 상태를 “데드락”</p>
</blockquote>
<p>즉, DeadLock은 특정 락(물리적/논리적)을 잘못 사용하여 “서로가 서로의 자원을 기다리는” 상황이 발생했을 때 나타나는 현상이다.</p>
<p>DB 내부의 물리적 락(Row Lock, Table Lock 등)이 서로 엇갈려 획득된 상황에서 주로 발생
또는 애플리케이션 트랜잭션 로직에서 서로 락을 잡는 순서가 꼬여 교착을 일으킬 수도 있음</p>
<h3 id="데드락은-락의-한-종류가-아니다-✔️">데드락은 “락의 한 종류”가 아니다 ✔️</h3>
<ul>
<li>데드락은 특정 락(물리적/논리적) 자체를 의미하지 않음</li>
<li>오히려 여러 트랜잭션이 락을 획득한 뒤 해제하지 못하고, 상대가 가진 락을 기다리는 상태를 말함</li>
</ul>
<h3 id="🤔-왜-데드락이-일어나는가">🤔 왜 데드락이 일어나는가?</h3>
<ul>
<li>DB 내부의 물리적 락(Row Lock, Table Lock 등)이 서로 엇갈려 획득된 상황</li>
<li>예) 트랜잭션 A가 Row1에 X락, 트랜잭션 B가 Row2에 X락을 가지고 있는 상태에서, A가 Row2를, </li>
</ul>
<p>B가 Row1을 필요로 하여 서로 대기</p>
<ul>
<li>애플리케이션 차원의 락 획득 순서가 꼬인 경우</li>
<li>예) 두 스레드가 각각 A 자원과 B 자원을 잡고, 반대편 자원도 필요로 할 때 서로 대기</li>
</ul>
<blockquote>
<p>즉, 물리적 락이든, <strong>애플리케이션 로직상의 논리적 락(전략)</strong>이든,
서로 자원을 점유한 상태에서 상대 자원을 기다리는 “교차 대기”가 발생하면 데드락이 형성된다.</p>
</blockquote>
<h2 id="2-예시-시나리오">2) 예시 시나리오</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/881a088b-db11-4591-8f98-09f1add39b8c/image.png" /></p>
<ol>
<li>트랜잭션 A: <code>pk=1</code> 행에 X-Lock을 걸고 업데이트 → 아직 커밋 안 함  </li>
<li>트랜잭션 B: <code>pk=2</code> 행에 X-Lock을 걸고 업데이트 → 아직 커밋 안 함  </li>
<li>트랜잭션 A가 이제 <code>pk=2</code> 행을 UPDATE하려고 함 → B가 X-Lock 보유 중이라 대기  </li>
<li>트랜잭션 B가 이제 <code>pk=1</code> 행을 UPDATE하려고 함 → A가 X-Lock 보유 중이라 대기  </li>
<li><strong>서로 락을 기다리면서</strong> 무한정 대기 상태 → DeadLock</li>
</ol>
<h2 id="3-deadlock-방지-방안">3) DeadLock 방지 방안</h2>
<ol>
<li><strong>복잡한 쿼리를 줄이기</strong>  <ul>
<li>한 번에 모든 일을 처리하는 “한 방 쿼리”는 Lock이 여러 곳에서 충돌하여 DeadLock이 쉽게 발생  </li>
<li>가능한 한 <strong>단순한 쿼리를 여러 번</strong> 호출하고, 트랜잭션 범위를 최소화</li>
</ul>
</li>
<li><strong>트랜잭션 내 Lock 순서 일관성 유지</strong>  <ul>
<li>여러 테이블이나 여러 Row를 수정할 때, <strong>항상 동일한 순서</strong>로 Lock을 획득하도록 구조화  </li>
<li>예: (A → B 순서)로 락을 잡기로 정했다면 모든 트랜잭션에서 동일하게</li>
</ul>
</li>
<li><strong>ON DUPLICATE KEY UPDATE 사용 시 주의</strong>  <ul>
<li>대규모 배치(Upsert) 환경에서 여러 트랜잭션이 동시에 같은 Row를 접근하면 DeadLock이 발생하기 쉬움  </li>
<li>배치 크기를 나누거나, 해당 로직을 단순화하여 락 충돌을 줄이는 것이 중요</li>
</ul>
</li>
</ol>
<h2 id="4-결론">4) 결론</h2>
<ul>
<li><strong>Lock</strong>은 동시성 이슈를 해결하는 강력한 방법이지만, 그만큼 <strong>DeadLock</strong>의 잠재적 위험도 함께 온다.  </li>
<li>특히 <strong>외래키</strong>를 사용하는 경우, <strong>부모 테이블까지 잠금 전파</strong>가 발생해 DeadLock이 빈번하게 발생할 수 있음.  </li>
<li>실무에서는 <strong>외래키를 제거</strong>하거나, <strong>트랜잭션 범위 최소화</strong>, <strong>쿼리 분리</strong>, <strong>Lock 획득 순서 일관화</strong>, <strong>재시도(Retry) 로직</strong> 적용 등으로 문제를 완화한다.  </li>
<li>궁극적으로 어떤 방식을 택하더라도, <strong>정합성과 운영 편의성의 균형</strong>을 찾는 것이 관건이다.</li>
</ul>
<blockquote>
<p>“잘 쓰면 좋은데, 못 쓰면 문제” — 락의 양면성</p>
</blockquote>
<p><strong>(1) 잘 쓰면?</strong></p>
<ul>
<li><strong>동시성 제어</strong>: 동시에 많은 요청이 와도 데이터가 꼬이지 않고 안전한 결과를 보장.  </li>
<li><strong>무결성 보장</strong>: 은행, 결제 시스템 등에서 돈이 잘못 계산되지 않도록 보호.</li>
</ul>
<p><strong>(2) 못 쓰면?</strong></p>
<ul>
<li><strong>교착상태</strong>: 트랜잭션이 서로의 락을 기다리며 멈춰버리는 데드락.  </li>
<li><strong>성능 하락</strong>: 불필요하게 긴 락 유지로 인해 다른 작업도 줄줄이 대기.</li>
</ul>
<h2 id="5-외래키foreign-key🔑와-deadlock🔓">5) 외래키(Foreign Key)🔑와 DeadLock🔓</h2>
<h3 id="✔️-외래키-제약의-특징">✔️ 외래키 제약의 특징</h3>
<ul>
<li>자식 테이블에 데이터를 삽입 혹은 수정할 때, <strong>부모 테이블</strong>에 해당 값이 <strong>실제로 있는지</strong> 검사  </li>
<li>무결성을 위해 부모 Row에 <strong>공유 잠금(Shared Lock)</strong> 이 걸릴 수 있음  </li>
<li>그 결과, 자식 테이블의 INSERT/UPDATE가 자주 일어나는 환경에서는 부모 테이블에도 빈번히 Lock이 전파됨</li>
</ul>
<h3 id="✔️-실제-서비스-예시">✔️ 실제 서비스 예시</h3>
<ul>
<li><strong>외래키 제거 후</strong>, 동일한 요청 상황에서 DeadLock 대신 “중복 키 에러”가 발생  </li>
<li>DeadLock은 트랜잭션 전체가 롤백되지만, 중복 키 에러는 특정 로직만 에러 처리하면 됨</li>
<li>높은 트래픽 환경에서 <strong>DB 구조의 복잡성을 낮추고</strong>, 오류 처리를 애플리케이션 레벨로 이동하는 전략</li>
</ul>
<h3 id="✔️-테이블-구조-및-기본-상황">✔️ 테이블 구조 및 기본 상황</h3>
<pre><code class="language-sql">CREATE TABLE parent
(
    id         bigint not null primary key,
    name       varchar(255) null,
    updated_at datetime(6)  null
);

CREATE TABLE child
(
    id         bigint       not null primary key,
    name       varchar(255) null,
    parent_id  bigint       null,
    CONSTRAINT parent_id_unique UNIQUE (parent_id),
    CONSTRAINT child_fk FOREIGN KEY (parent_id) REFERENCES parent (id)
);

CREATE TABLE child_index
(
    id         bigint       not null primary key,
    name       varchar(255) null,
    parent_id  bigint       null,
    CONSTRAINT child_index_fk FOREIGN KEY (parent_id) REFERENCES parent (id)
);
CREATE INDEX parent_id ON child_index (parent_id);

INSERT INTO parent VALUES (1, 'parent_1', NOW());</code></pre>
<ul>
<li><p><strong><code>child</code>와 <code>child_index</code></strong> 테이블은 모두 <strong><code>parent_id</code>를 외래키</strong>로 가지고 있다.  </p>
<blockquote>
<p> 즉, <code>parent_id</code> 값을 넣을 때마다, DB는 <strong>부모 테이블(<code>parent</code>)에 해당 값이 실제로 존재하는지</strong> 검사해야 한다.  </p>
</blockquote>
</li>
<li><p>InnoDB에서는 이러한 무결성 체크를 위해 부모 행을 <strong>Shared Lock(S락)</strong> 으로 잠그는 동작이 발생할 수 있다.</p>
</li>
</ul>
<h3 id="✔️각-트랜잭션에서-벌어지는-일-순서대로">✔️각 트랜잭션에서 벌어지는 일 (순서대로)</h3>
<h4 id="1-트랜잭션-tx1">(1) 트랜잭션 TX1</h4>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5f2229c8-a672-4785-83bc-1e88d3c2b7ba/image.png" /></p>
<ol>
<li><code>child</code> 테이블에 <code>(1, 'child1', 1)</code>을 <strong>INSERT</strong>  <ul>
<li><strong><code>child</code> 테이블의 해당 Row( id=1 )에 X-Lock</strong>(쓰기 락) 획득  </li>
<li>동시에 <code>parent_id = 1</code> 이 실제로 존재하는지 확인하기 위해, <strong><code>parent</code> 테이블의 <code>id=1</code> 행에 S-Lock</strong>(읽기 락) 획득  </li>
<li>트랜잭션 TX1은 아직 <code>COMMIT</code>하지 않고 대기 상태</li>
</ul>
</li>
</ol>
<p><strong>결과</strong>:  </p>
<ul>
<li><strong>child( id=1 )</strong>: X-Lock (TX1 보유)  </li>
<li><strong>parent( id=1 )</strong>: S-Lock (TX1 보유)</li>
</ul>
<h4 id="2-트랜잭션-tx2">(2) 트랜잭션 TX2</h4>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/15aa9476-8d0f-4492-b463-efb8a310fe3c/image.png" /></p>
<ol>
<li>똑같이 <code>child</code> 테이블에 <code>(1, 'child1', 1)</code>을 <strong>INSERT</strong> 시도  <ul>
<li><strong><code>child</code>의 같은 Row(id=1)</strong> 에 X-Lock을 얻으려 하지만, 이미 TX1이 X-Lock 보유 중이므로 이 부분에서 <strong>대기</strong>합니다.  </li>
<li>그러나, 외래키 검증을 위해 <code>parent</code>(id=1)에 대해서도 S-Lock을 또 시도 (또는 이미 획득)  </li>
<li>결국 <strong>child( id=1 )</strong>는 X-Lock 대기, <strong>parent( id=1 )</strong>는 TX2도 S-Lock 상태로 겹쳐 있을 수 있음</li>
</ul>
</li>
</ol>
<p><strong>결과</strong>:  </p>
<ul>
<li>TX2는 <strong>child( id=1 )</strong>에 대해서는 X-Lock을 <strong>대기</strong>하고 있음. (TX1이 끝나야 획득 가능)  </li>
<li>하지만 <strong>parent( id=1 )</strong> 행에 대해서는 <strong>TX2도 S-Lock</strong>을 가지고 있거나 잠금 확보 과정에서 충돌 대기 중</li>
</ul>
<h4 id="3-트랜잭션-tx1이-parentid1를-update">(3) 트랜잭션 TX1이 <code>parent</code>(id=1)를 UPDATE</h4>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5575a278-99d4-4cca-af80-f7c3d4cce13b/image.png" /></p>
<ul>
<li>이제 TX1이 부모 테이블 <code>parent( id=1 )</code>을 <strong>UPDATE</strong>하려고 합니다.  </li>
<li>UPDATE 시에는 <strong>Exclusive Lock(X-Lock)</strong> 이 필요합니다.  </li>
<li>그런데 이미 TX2가 <code>parent(id=1)</code>에 대해 <strong>S-Lock</strong>을 가지고 있거나(또는 대기 중) ⇒ <strong>S락 ↔ X락은 호환되지 않음</strong>  </li>
<li>따라서 TX1은 <strong><code>parent(id=1)</code>에 X-Lock을 얻지 못하고 대기</strong>에 빠집니다.</li>
</ul>
<p><strong>결과</strong>:  </p>
<ul>
<li>TX1: <strong>child( id=1 )</strong> X-Lock 보유, <strong>parent( id=1 )</strong> X-Lock 필요하지만 대기  </li>
<li>TX2: <strong>parent( id=1 )</strong> S-Lock 보유 (또는 획득 대기 중), <strong>child( id=1 )</strong> X-Lock 필요하지만 대기</li>
</ul>
<h4 id="4-서로-대기-→-deadlock">(4) 서로 대기 → DeadLock</h4>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/99c848e1-2920-46a5-8c69-1998277777c9/image.png" /></p>
<ul>
<li>TX1은 <code>parent( id=1 )</code>에 X-Lock을 얻어야 UPDATE를 마칠 수 있는데, TX2가 S-Lock을 잡고 있어서 불가능  </li>
<li>TX2는 <code>child( id=1 )</code>에 X-Lock을 얻어야 INSERT를 마칠 수 있는데, TX1이 이미 X-Lock을 갖고 있어서 불가능  </li>
<li><strong>둘 다 상대가 락을 풀어주길 기다리는 상태</strong> → <strong>교착 상태(DeadLock)</strong> 발생</li>
</ul>
<p>DB 엔진(InnoDB)은 일정 시간이 지나면 교착을 감지하여, 둘 중 한 트랜잭션을 강제로 롤백시킨다.</p>
<p><strong>전체 구조 간략 사진</strong>
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3bc5f633-350f-41b3-8098-083f3d26a24d/image.png" /></p>
<p>이후에 데드락이 생긴다.</p>
<h3 id="✔️-왜-이런-일이-벌어지는-걸까">✔️ 왜 이런 일이 벌어지는 걸까?</h3>
<ol>
<li><strong>외래키 제약</strong>  <ul>
<li>자식 테이블(<code>child</code>)에 데이터를 넣을 때, <strong>부모 테이블(<code>parent</code>)에 해당 값이 실제 존재하는지</strong> 무결성 체크를 수행  </li>
<li>이때 InnoDB가 부모 테이블의 해당 Row를 <strong>공유 잠금(S-Lock)</strong> 으로 확보하는 동작이 발생  </li>
</ul>
</li>
<li><strong>X-Lock &amp; S-Lock 호환성 문제</strong>  <ul>
<li>한 트랜잭션이 부모 Row에 <strong>S-Lock</strong>을 잡고 있고, 다른 트랜잭션이 같은 Row에 <strong>X-Lock</strong>을 시도하면, S↔X는 호환되지 않아 <strong>대기</strong>  </li>
</ul>
</li>
<li><strong>서로 다른 리소스 락을 먼저 잡아버림</strong>  <ul>
<li>TX1: <code>child(id=1)</code> X-Lock → <code>parent(id=1)</code> X-Lock 시도  </li>
<li>TX2: <code>parent(id=1)</code> S-Lock → <code>child(id=1)</code> X-Lock 시도  </li>
<li>락 획득 순서가 어긋나 <strong>교차 대기</strong>를 야기, 전형적인 DeadLock 구조가 만들어짐</li>
</ul>
</li>
</ol>
<h3 id="✔️-해결예방-방안">✔️ 해결/예방 방안</h3>
<ol>
<li><strong>쿼리 순서 재정의 or flush() 사용</strong>  </li>
</ol>
<ul>
<li>부모를 먼저 Update한 뒤, 즉시 flush()를 통해 쿼리를 DB에 반영 후, 자식 Insert</li>
<li>장점: 원하는 순서대로 락을 획득  </li>
<li>단점: flush() 사용 시점에 대한 <strong>추가 리스크</strong></li>
</ul>
<ol start="2">
<li><strong>외래키 제약 제거</strong>  </li>
</ol>
<ul>
<li>부모·자식 간 무결성 체크를 <strong>애플리케이션 레벨</strong>에서 해결(또는 DB Trigger, Batch 등 다른 방식으로 일관성 유지)  </li>
<li>장점: DeadLock 감소, 스키마 변경 용이  </li>
<li>단점: <strong>DB 스스로 무결성을 보장하지 못하므로</strong> 누락된 데이터 or 잘못된 참조가 발생할 수 있음  </li>
<li>실제로는 대규모 트래픽, 잦은 스키마 변경, 마이크로서비스 등에서 <strong>비교적 흔한 방식</strong></li>
</ul>
<ol start="3">
<li><strong>배치 크기 축소 &amp; 재시도(기동성) 전략</strong>  </li>
</ol>
<ul>
<li>DeadLock은 특정한 상황에서만 자주 발생하므로, <code>retry</code> 로직을 통해 해결 가능  </li>
<li>트랜잭션 단위를 줄이면(배치 크기 ↓) 충돌이 줄어 DeadLock 빈도가 낮아짐</li>
</ul>
<p><strong>4. 복잡한 쿼리 줄이기 &amp; 트랜잭션 범위 짧게</strong></p>
<ul>
<li>“한 방 쿼리”로 처리하면 락이 여러 테이블·Row에 확산되어 충돌 가능성 높아짐</li>
</ul>
<p><strong>5. Lock 획득 순서 일관성</strong></p>
<ul>
<li>여러 테이블을 동시에 수정해야 할 때, 항상 동일 순서(A→B→C)를 준수</li>
</ul>
<p><strong>6. ON DUPLICATE KEY UPDATE 주의</strong></p>
<ul>
<li>배치성 Upsert로 서로 다른 Row에 Lock을 건 뒤, 반대 Row에 접근 → 교착</li>
<li>배치 크기 줄이거나 로직 단순화</li>
</ul>
<p><strong>7. 재시도(Retry) 전략</strong></p>
<ul>
<li>교착 상태가 나는 순간, DB는 한 트랜잭션을 롤백시키므로, 애플리케이션 레벨에서 자동 재시도 로직을 둘 수 있음</li>
</ul>
<ol start="8">
<li><strong>트랜잭션 범위와 락 획득 순서를 일관</strong>되게 유지  </li>
</ol>
<ul>
<li>예: “부모 테이블을 먼저 UPDATE한 뒤, 자식 테이블 INSERT”  </li>
<li>쿼리 순서를 맞추면 교차 잠금이 줄어듦  </li>
</ul>
<h3 id="✔️-실무에서-외래키🔑를-자주-쓰지-않는-이유">✔️ 실무에서 외래키🔑를 자주 쓰지 않는 이유</h3>
<ol>
<li><strong>잠금이 여러 테이블로 전파</strong>되어 DeadLock 위험이 높아짐  </li>
<li><strong>테이블 변경(ALTER, DROP 등)</strong> 시 제약이 복잡해지고, 배포(마이그레이션) 로직이 까다로워짐  </li>
<li>대규모 트래픽 환경에서, <strong>부모·자식 테이블 간 제약 관계</strong>로 인해 의도치 않은 Lock 획득이 빈번히 발생  </li>
<li>특정 환경(분산 DB, 샤딩 등)에서는 외래키가 실효성이 없거나 적용하기 어려움  </li>
</ol>
<blockquote>
<p><strong>주의</strong>  </p>
<ul>
<li>외래키를 전혀 쓰지 않는 것이 무조건 옳다는 뜻은 아님  </li>
<li><strong>정합성을 유지하면서</strong> DeadLock 위험과 <strong>운영 편의성</strong> 사이에서 적절히 트레이드오프를 고려해야 함</li>
</ul>
</blockquote>
<h1 id="5-select으로-인해-lock이-걸렸던-상황은-이유가-뭘까-🤔">5. select으로 인해 lock이 걸렸던 상황은 이유가 뭘까? 🤔</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/07d3354c-8bfe-4a88-baf9-adb944fa49b7/image.png" /></p>
<h2 id="1-왜-commitrollback을-하지-않으면-락이-풀리지-않는가">1) 왜 Commit/Rollback을 하지 않으면 락이 풀리지 않는가?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/32dbff8b-d986-4360-a8ad-1aa31c0cee62/image.png" /></p>
<ul>
<li><p><strong>트랜잭션 내에서 획득한 락은 “트랜잭션 범위”</strong>를 갖는다.  </p>
<blockquote>
<p>즉, 트랜잭션이 “시작(START TRANSACTION)”된 뒤에 실행되는 DML(SELECT ... FOR UPDATE 등 포함)로 인해 획득된 잠금들은, <strong>그 트랜잭션이 명시적으로 끝나야(Commit/Rollback)</strong> 해제된다.  </p>
</blockquote>
</li>
<li><p>만약 <strong>autocommit=0</strong>(자동 커밋 비활성화) 상태에서 SELECT 문만 실행하고 <strong>Commit/Rollback을 생략</strong>하면, DB 입장에서는 트랜잭션이 계속 열려 있는 상태이므로 <strong>잠금도 계속 유지</strong>되는 것</p>
</li>
</ul>
<h2 id="2-왜-같은-테이블이라서-전체-lock이-걸렸나">2) 왜 “같은 테이블”이라서 전체 Lock이 걸렸나?</h2>
<ol>
<li><p><strong>Table-level Lock 사용 가능성</strong>  </p>
<ul>
<li><strong>MyISAM</strong>(또는 Aria) 엔진에서는 <code>UPDATE</code>가 발생하면 쓰기 락(Write Lock)이, <code>SELECT</code>가 발생하면 읽기 락(Read Lock)이 <strong>테이블 단위</strong>로 걸린다.  </li>
<li>이때 하나의 세션(개발자 B)이 <strong>SELECT</strong>로 <strong>Read Lock</strong>을 잡은 상태에서 트랜잭션을 종료하지 않으면, 다른 세션(개발자 A)의 Update(쓰기 락)와 <strong>충돌</strong>이 일어나 대기가 발생할 수 있음.</li>
</ul>
</li>
<li><p><strong>테이블 전체를 잠그는 방식</strong>(<code>LOCK TABLES</code> 등)  </p>
<ul>
<li>혹은 “<code>LOCK TABLES ...</code>” 로 테이블을 수동으로 잠가서 작업하는 경우, SELECT도 <strong>읽기 락</strong>을 테이블 단위로 확보 → 커밋/롤백(또는 <code>UNLOCK TABLES</code>) 없이는 해제되지 않음.</li>
</ul>
</li>
<li><p><strong>InnoDB라도 특정 설정(DDL·외래키 등)으로 인해 테이블 락 발생</strong>  </p>
<ul>
<li>보통 InnoDB는 Row-level Lock을 사용하지만, 스키마 변경(DDL)이나 외래키 점검 과정에서 <strong>테이블 레벨 락</strong>이 걸릴 수 있음.  </li>
<li>SELECT가 단순 조회 이상(예: <code>SELECT ... LOCK IN SHARE MODE</code>), 혹은 다른 이유로 테이블 전체 범위를 잠그는 상황도 가능.</li>
</ul>
</li>
</ol>
<h2 id="3-select-시-왜-read-lock이-오래-유지될까">3) SELECT 시 왜 “Read Lock”이 오래 유지될까?</h2>
<ol>
<li><p><strong>트랜잭션 범위</strong>(autocommit=0 상태)  </p>
<ul>
<li>MariaDB에서 <code>SELECT</code>가 끝나도, <strong>트랜잭션 종료(Commit/Rollback)를 안 하면</strong> 읽기 락이 해제되지 않는 경우가 있음.  </li>
<li>즉, <strong>SELECT로 얻은 Read Lock</strong>이 <strong>트랜잭션이 끝날 때까지</strong> 유지되므로, 다른 사람의 Update(Write Lock)와 충돌.</li>
</ul>
</li>
<li><p><strong>테이블 단위로 읽기 락을 보유</strong>  </p>
<ul>
<li>MyISAM/Aria 엔진일 때, “읽기 락”은 테이블 전체 범위에 적용 → <strong>또 다른 세션에서 Update 시도</strong>하면 대기.  </li>
<li>만약 SELECT한 쪽이 커밋/롤백(또는 세션 종료)을 하지 않으면 읽기 락이 계속 유지 → 결과적으로 “전체 테이블이 Lock 걸려 있다”는 현상.</li>
</ul>
</li>
</ol>
<h2 id="4-결국-select-후에도-commitrollback이-필요한-이유">4) 결국 “SELECT 후에도 Commit/Rollback”이 필요한 이유</h2>
<ol>
<li><p><strong>Lock 해제 시점 = 트랜잭션 종료</strong>  </p>
<ul>
<li>MariaDB(또는 MySQL 계열)에서 <strong>락은 트랜잭션 범위</strong>로 묶임  </li>
<li>Select가 끝나도 <code>COMMIT</code> 또는 <code>ROLLBACK</code>하지 않으면, <strong>읽기 락(READ LOCK)</strong> 상태가 그대로 유지</li>
</ul>
</li>
<li><p><strong>다른 세션(개발자 A)의 UPDATE</strong>와 충돌  </p>
<ul>
<li>읽기 락 ↔ 쓰기 락은 <strong>동시에 걸릴 수 없음</strong>(특히 테이블 단위 락의 경우 더욱).  </li>
<li>업데이트하려면 쓰기 락이 필요한데, 이미 누군가가 “읽기 락”을 들고 있으면 대기 상태 발생</li>
</ul>
</li>
<li><p><strong>동시성 저하 &amp; 병목</strong>  </p>
<ul>
<li>여러 개발자가 동시에 SELECT/UPDATE하는 환경이라면, 한 사람이라도 SELECT 락을 길게 유지하면 모두가 대기하게 됨  </li>
<li>결과적으로 “한 컬럼만 수정 중인데 왜 전체 테이블이 잠기지?” 같은 문제가 일어남</li>
</ul>
</li>
</ol>
<blockquote>
<p><strong>“왜 락이 걸렸고, 커밋/롤백을 해야 락이 풀리는가?”</strong>  </p>
<ul>
<li>이는 SELECT를 단순 조회 모드가 아닌, <strong>“락을 동반하거나, 특정 격리 수준에서 내부적으로 락이 필요한”</strong> 형태로 실행했기 때문이다. 그리고 이 락은 <strong>해당 트랜잭션이 종료될 때까지</strong> 유지된다.</li>
</ul>
</blockquote>
<h2 id="5-결론">5) 결론</h2>
<ul>
<li><strong>MariaDB</strong>에서 “같은 테이블”에 대해 한 명은 <code>UPDATE</code>, 다른 한 명은 <code>SELECT</code>를 했을 뿐인데 <strong>테이블 전체 Lock</strong>이 걸렸다?  <ul>
<li>이는 대개 <strong>테이블 레벨 락</strong>(MyISAM/Aria, <code>LOCK TABLES</code>, 혹은 인덱스/DDL 상황) + <strong>SELECT에 의한 Read Lock</strong> + <strong>트랜잭션 미종료</strong>가 겹친 결과.  </li>
</ul>
</li>
<li><strong>SELECT</strong> 쿼리가 끝나도, <strong>트랜잭션 종료(Commit/Rollback)를 안 하면</strong> 락이 계속 유지 → 다른 세션의 Update와 충돌.  </li>
<li>따라서 “SELECT 후에도 Commit/Rollback을 해달라”는 것은, <strong>불필요한 Read Lock이 오래 유지되어 전체 테이블이 막히는 사태</strong>를 방지하기 위함.</li>
</ul>
<blockquote>
<p><strong>정리</strong>:  </p>
<ul>
<li>테이블 단위로 락이 걸리는 엔진(또는 설정) 하에서, SELECT는 “읽기 락”을 잡음  </li>
<li>트랜잭션이 종료되지 않으면 락이 풀리지 않아, 다른 개발자의 UPDATE(쓰기 락)와 충돌  </li>
<li>이로 인해 테이블 전체가 락 걸린 것처럼 느껴지므로, <strong>SELECT 후에도 반드시 Commit/Rollback</strong>이 필요하다는 설명이 나온다. </li>
</ul>
</blockquote>
<ul>
<li><strong>SELECT로 인해 락이 걸렸고, 트랜잭션이 끝날 때까지 풀리지 않는다면</strong>, 이는 대부분<br />1) <code>SELECT ... FOR UPDATE</code>,  
2) <code>SELECT ... LOCK IN SHARE MODE</code>,  
3) 높은 격리 수준(Repeatable Read 이상),<br />4) 테이블 락(<code>LOCK TABLES</code>)  
중 하나로 인해 발생했을 가능성이 크다.</li>
</ul>
<blockquote>
<p>락이 풀리지 않고 계속 유지되는 이유는, 해당 쿼리를 실행한 <strong>트랜잭션이 아직 종료되지 않았기 때문</strong>이다.  </p>
</blockquote>
<ul>
<li><strong>autocommit 모드</strong>인지 확인하고,  </li>
<li>명시적으로 <strong>COMMIT 혹은 ROLLBACK</strong>을 해주는 습관을 들이면, 트랜잭션이 불필요하게 길어지면서 락이 묶이는 문제를 줄일 수 있다고 한다.</li>
</ul>
<ul>
<li>불필요하게 <strong>긴 트랜잭션</strong>은 다른 세션에서의 작업을 지연시키고 데드락 가능성을 높인다.  <ul>
<li>따라서, <strong>트랜잭션 범위를 최소화</strong>하고, 처리 후에는 <strong>바로 커밋/롤백</strong>하는 것이 좋다.</li>
</ul>
</li>
</ul>
<h2 id="6-확인-사항">6) 확인 사항</h2>
<ul>
<li><strong>어떤 SELECT 문을 사용했는지</strong>(FOR UPDATE / LOCK IN SHARE MODE / 테이블 락 등),  </li>
<li><strong>트랜잭션이 언제 시작되고 끝나는지</strong>,  </li>
<li><strong>autocommit 설정은 어떤지</strong><br />를 함께 점검하시면, 왜 “읽기만 했는데 락이 걸려 있고 트랜잭션 종료 전에는 해제되지 않는지”를 정확히 파악하실 수 있을 것</li>
</ul>
<blockquote>
<p><strong>SELECT로도 (Read Lock)</strong> 이 걸릴 수 있고, 이를 <strong>트랜잭션이 끝날 때까지</strong> 유지하기 때문에, <strong>Commit이나 Rollback</strong>을 꼭 해줘야 한다는 이야기</p>
</blockquote>
<p><strong>참고 및 출처</strong></p>
<ul>
<li><a href="https://nooblette.tistory.com/entry/MySQL-Lock-Type%EA%B3%BC-%EB%8D%B0%EB%93%9C%EB%9D%BDDeadLock-%EC%98%88%EB%B0%A9%ED%95%98%EA%B8%B0">[MySQL] Lock Type과 데드락(DeadLock) 예방하기</a></li>
<li><a href="https://velog.io/@soongjamm/Select-%EC%BF%BC%EB%A6%AC%EB%8A%94-S%EB%9D%BD%EC%9D%B4-%EC%95%84%EB%8B%88%EB%8B%A4.-X%EB%9D%BD%EA%B3%BC-S%EB%9D%BD%EC%9D%98-%EC%B0%A8%EC%9D%B4">Select 쿼리는 S락이 아니다. (X락과 S락의 차이)</a></li>
<li><a href="https://sabarada.tistory.com/175">[database] 낙관적 락(Optimistic Lock)과 비관적 락(Pessimistic Lock)</a></li>
</ul>