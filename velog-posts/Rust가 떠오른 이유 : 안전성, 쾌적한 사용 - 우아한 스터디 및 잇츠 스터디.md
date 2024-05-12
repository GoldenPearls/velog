<h1 id="tmi">TMI</h1>
<blockquote>
<p>프로그래밍 러스트 책에 있는 것을 정리</p>
</blockquote>
<h2 id="스터디">스터디</h2>
<p>잇츠 우먼 스터디 1기 Rust 스터디에 선발되어서 이번주부터 스터디 하게 됨
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/85b92868-c1f6-4adc-9a35-09151e151212/image.png" /></p>
<h2 id="현재-배달의-민족과-잇츠-2기-뽑는-중">현재 배달의 민족과 잇츠 2기 뽑는 중</h2>
<blockquote>
<p>난 1기라서 우아한 스터디만 신청 가능함</p>
</blockquote>
<h3 id="우아한-스터디">우아한 스터디</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/93ca11cd-70c3-4f15-a235-9814e8705a11/image.png" /></p>
<ul>
<li>링크 : <a href="https://techblog.woowahan.com/17328/">[모집] 우아한스터디 2024 여름시즌</a></li>
<li>모집 기간 : 5/8 ~ 5/14</li>
<li>활동 기간: 6/1 ~ 7/31 
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b5d68b3c-6436-4c1e-bb42-ef7a548e36ea/image.png" /></li>
</ul>
<h3 id="잇츠스터디">잇츠스터디</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/566c0379-5481-459d-b92e-b85ba2492089/image.png" /></p>
<ul>
<li>링크 : <a href="https://puffy-stick-fa1.notion.site/X-5936365761834b0d9b99722d71515fd8">서울 우먼잇츠 X 우아한스터디</a></li>
<li>모집 기간 : 5/8 ~ 5/14</li>
<li>활동 기간: 6/1 ~ 7/31
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/988bbbc9-dee6-42f0-9beb-8cfe8be0e0ca/image.png" /></li>
</ul>
<h1 id="rust를-쓰는-이유---chapter-1">Rust를 쓰는 이유 - chapter 1</h1>
<p><strong>텍스트</strong></p>
<h2 id="1-c언어-c언어의-문제점">1. C언어, C++언어의 문제점</h2>
<pre><code class="language-C언어">int main(int argc, char **argv){
    unnsigned long a[1];
    a[3] = 0x7ffff7b36cebUL;
    return 0;
}</code></pre>
<p>이 프로그램에는 결함이 있다. 배열 a는 요소가 하나뿐이므로 a[3]이라고 쓰는건 C 프로그래밍 언어 표준 상 <code>미정의 동작</code>이라고 한다.</p>
<h3 id="미정의-동작이란">미정의 동작이란</h3>
<blockquote>
<p>본 국제 표준이 요건을 부과하지 않는, 이식할 수 없거나 잘못된 프로그램구문 요소 또는 잘못된 데이터를 사용할 때의 동작</p>
</blockquote>
<p>미정의 동작은 단순히 예측할 수 없는 결과를 내는 것으로 끝이 아닌, 표준은 노골적으로 프로그램이 <strong>무엇이든</strong> 할 수 있게 허락한다.</p>
<h3 id="c-c는-미정의-동작을-회피하기-위한-책임이-프로그래머에게-있음">C, C++는 미정의 동작을 회피하기 위한 책임이 프로그래머에게 있음</h3>
<p>C, C++의 미정의 동작을 회피하기 위한 규칙이 수 백 개로 결과 책임이 프로그래머에게 있는 것임 이는 <strong>품질 문제</strong>와 더 나아가 <strong>보안 결함</strong>으로 주된 원인이 됨 </p>
<h2 id="2-안전성">2. 안전성</h2>
<blockquote>
<p>Rust의 약속 : 컴파일러의여러 검사를 통과한 프로그램에는 미정의 동작이 없게 하겠다는 것 </p>
</blockquote>
<p>즉, 러스트는 대상을 잃은 포인터, 중복 해제, 널 포인터 역참조를 전부 <strong>컴파일러 시점</strong>에서 잡는다. 또한 배열 참조를 컴파일 
시점 검사와 실행 시점 검사로 보호하기 때문에 버퍼 오버런이 없다고 한다. 즉, 앞 선 c언어의 문제를 오류메세지와 함께 안전하게 종료시킨다. </p>
<p>아직, 러스트가 탐지할 수 있는 버그의 양에는 한계가 있지만, 코드에서 미정의 동작만 사라져도 개발 특성이 크게 좋아진다고 함</p>
<h2 id="3-병렬-프로그래밍">3. 병렬 프로그래밍</h2>
<p>C언어와 C++은 <code>동시성</code>을 제대로 이용하기 어려워, 싱글 스레드 코드로 도저히 성능을 낼 수 없을 때만 <code>동시성</code>에 의존한다.</p>
<p>러스트는 <strong>데이터가 변경되지 않는 한 스레드 간에 자유롭게 공유</strong>할 수 있고, 변경되는 데이터는 동기화 기본 요소를 써야만 접근 가능하다. </p>
<blockquote>
<p>즉, 러스트는 최신 멀티 코어 기기의 성능을 제대로 활용하기 위한 최적의 언어로 만들어 준다. </p>
</blockquote>
<p>러스트 생태계는 복잡한 작업 부하를 프로세서 풀에 고루 분배할 수 있게 도와주고 Read-Copy-Update 같은 무잠금 동기화 기법을 쓸 수 있게 해주는 등, <strong>일반적인 동시성 기본 요소의 역할을 뛰어넘는 다양한 라이브러리 제공</strong>한다.</p>
<h2 id="4-빠른-속도">4. 빠른 속도</h2>
<h3 id="rust의-빠르다의-의미">Rust의 빠르다의 의미</h3>
<p>프로그램 설계 시 Rust의 경우, 밑바닥에 있는 머신의 성능을 최대한 활용하는데 기꺼이 도와준다.</p>
<blockquote>
<p>효율적인 기본 값을 가지고 설계된 언어로서, 메모리의 사용 방식과 프로세서의 관심이 할애되는 방식을 제어할 수 있게 도와준다.</p>
</blockquote>
<h3 id="범용-프로그래밍-언어">범용 프로그래밍 언어</h3>
<p>범용 언어를 사용하면 누구나 성능이 좋지 않은 코드를 작성할 수 있다.</p>
<p>범용 언어는 프로그래머의 편의성을 중시하기 때문에 하드웨어 자원 관리를 직접적으로 제어하기 어렵다. 따라서 <strong>메모리 관리나 프로세서 활용 측면에서 비효율적인 코드가 작성</strong>될 수 있다.</p>
<h3 id="rust">Rust</h3>
<blockquote>
<p>범용 언어는 프로그래머의 편의성 위주로 설계되어 하드웨어 자원 관리가 어렵지만, Rust는 시스템 자원 활용을 최적화하도록 저수준 제어를 허용하는 언어로 <strong>하드웨어 자원을 최대한 활용</strong> 할 수 있다.</p>
</blockquote>
<p>Rust는 메모리 사용 방식과 프로세서 활용 방식을 프로그래머가 직접 제어할 수 있게 한다. 효율적인 기본 값(default)을 제공하여 저수준 하드웨어 제어를 용이하게 해준다.</p>
<p>이를 통해 Rust는 시스템 자원을 최적화된 방식으로 활용할 수 있다. 메모리 사용량을 최소화하고, 프로세서 연산을 효율적으로 배분할 수 있다. 결과적으로 높은 성능과 효율성을 가진 프로그램을 작성할 수 있다.</p>