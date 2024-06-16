<blockquote>
<p><a href="https://swits.notion.site/WEEK-6-ec11487900754d42828b2b978359cb02?pvs=4">노션 정리</a> : 좀 더 색깔이나 덧글로 모르는 단어까지 걸어두고 조금 더 정갈하게 정리해뒀다. 발표를 위한 발제글 올리기</p>
</blockquote>
<p>This chapter covers the two different kinds of error handling in Rust: panic and Results.</p>
<blockquote>
<p>Rust에서의 두 가지 에러 처리 방법인 <code>패닉(panic)</code>과 <code>결과(Result)</code>를 다룬다.</p>
</blockquote>
<p>Ordinary errors are handled using the Result type. Results typically represent problems caused by things outside the program, like erroneous input, a network outage,
or a permissions problem. That such situations occur is not up to us; even a bug-free
program will encounter them from time to tim</p>
<p>일반적인 에러는 <strong>Result 타입</strong>을 사용하여 처리한다. <code>Result</code>는 보통 프로그램 외부의 요인, 예를 들어 잘못된 입력, 네트워크 장애, 또는 권한 문제로 인해 발생하는 문제를 나타낸다. 이러한 상황은 우리가 통제할 수 없으며, 버그가 없는 프로그램이라도 가끔은 이런 문제를 마주하게 된다. </p>
<p>Panic is for the other kind of error, the kind that should never happen.</p>
<blockquote>
<p><strong>패닉</strong>은 다른 종류의 오류, 즉 절대 발생해서는 안 되는 에러입니다.</p>
</blockquote>
<h2 id="01-panic패닉">01. Panic(패닉)</h2>
<p>A program panics when it encounters something so messed up that there must be a
bug in the program itself. </p>
<p>프로그램 자체에 있는 버그로 인해 문제가 생기면 프로그램은 패닉에 빠진다. </p>
<ul>
<li><p>Out-of-bounds array access</p>
</li>
<li><p>Integer division by zero</p>
</li>
<li><p>Calling .expect() on a Result that happens to be Err</p>
</li>
<li><p>Assertion failure</p>
</li>
<li><p>배열의 범위 밖에 있는 요소에 접근하는 행위</p>
</li>
<li><p>정수를 0으로 나누는 행위</p>
</li>
<li><p>Err이 되어버린 Result에 대고 .expect()를 호출하는 행위</p>
</li>
<li><p>단언문 실패</p>
</li>
</ul>
<p>What these conditions have in common is that they are all-not to put too fine a
point on it--the programmer's fault. A good rule of thumb is: &quot;Don't panic.&quot;</p>
<p>위의 조건들의 <strong>공통점</strong>은 모두 프로그래머가 저지르는 실수라는 것으로 당황스럽다고 해도 패닉에 빠지지는  말자.</p>
<h3 id="패닉-매크로">패닉 매크로</h3>
<p>(There's also the macro panic! (), for cases where your own code discovers that it has
gone wrong, and you therefore need to trigger a panic directly. panic!() accepts
optional println! ()-style arguments, for building an error message.)</p>
<p>내가 작성한 코드가 잘못된 길로 들어서서 스스로 패닉에 빠져나가야 할 때 쓸 수 있는 <code>panic!()</code>이란 매크로도 있다. panic!()은 오류 메세지를 작성을 위한 println!() 스타일의인수를 옵션으로 받는다. </p>
<blockquote>
<p>위의 뜻에 경우, 즉, 코드를 작성하다 예상치 못한 오류가 발생하면, 프로그램이 계속해서 실행되면 안 되는 상황이 있는데 이럴 때는 프로그램이 스스로 중단되도록 하는 것이 안전하다. 이를 <strong>패닉에 빠져나간다고 표현</strong>한다.</p>
</blockquote>
<ol>
<li><strong>panic!() 매크로</strong></li>
</ol>
<ul>
<li>그때 rust에서는 이런 치명적인 오류가 발생시 panic!() 매크로 사용 가능, 이 매크로를 호출하면 프로그램 즉시 중단</li>
<li>즉, <code>panic!()</code>은 코드가 &quot;더 이상 진행할 수 없는 상황&quot;에 도달했을 때 사용</li>
</ul>
<ol start="2">
<li><strong>오류 메세지 작성</strong></li>
</ol>
<ul>
<li><code>panic!()</code> 매크로는 오류가 발생했을 때, 왜 프로그램이 중단되었는지를 알려주는 메시지를 출력할 수 있다.</li>
<li>이 메시지는 <code>println!()</code> 매크로와 비슷하게 작성할 수 있습니다. 예를 들어, 변수의 값을 포함하는 형태로 메시지를 구성할 수 있다.</li>
</ul>
<pre><code class="language-rust">fn main() {
    let value = -1;
    if value &lt; 0 {
        panic!(&quot;Value {} is negative, which is not allowed!&quot;, value);
    }
}
</code></pre>
<ul>
<li>여기서 <code>value</code>가 음수인지 확인</li>
<li>만약 <code>value</code>가 음수라면, <code>panic!()</code>을 호출하여 프로그램을 중단</li>
<li><code>panic!()</code>은 &quot;Value -1 is negative, which is not allowed!&quot;와 같은 오류 메시지를 출력</li>
<li>이 메시지는 <code>println!()</code> 매크로처럼, <code>{}</code>를 사용하여 <code>value</code>의 값을 포함할 수 있다.</li>
</ul>
<p>But we all make mistakes. When these errors that shouldn't happen do happen-what
then? Remarkably, Rust gives you a choice. Rust can either unwind the stack when a
panic happens or abort the process. Unwinding is the default.
하지만 우리 모두는 실수를 하고 발생해서 안되는 오류들이 발생하면, 러스트는 우리에게 선택의 기회를준다. 러스트는 패닉이 발생하면 스택을 해제하거나 프로세스를 중단할 수 있다. 기본 동작은 <strong>해제</strong>이다.  </p>
<h2 id="02-unwinding해제">02. Unwinding(해제)</h2>
<p>hen pirates divvy up the booty from a raid, the captain gets half of the loot. Ordinary crew members earn equal shares of the other half. (Pirates hate fractions, so if
either division does not come out even, the result is rounded down, with the remainder going to the ship's parrot.)</p>
<p>해적들이 약탈한 전리품을 나눌 때, 선장은 전리품의 절반을 가져가고, 일반 선원들은 나머지 절반을 동등하게 나눈다. (해적들은 분수를 싫어하기 때문에 나눗셈이 딱 맞지 않으면 결과는 내림하고 나머지는 선박의 앵무새에게 돌아간다.)</p>
<pre><code class="language-rust">fn pirate_share(total: u64, crew_size: usize) -&gt; u64 {
    let half = total / 2;
    half / crew_size as u64
}</code></pre>
<p>This may workfine for centuries until one day it transpires that the captain is the sole
survivor of a raid. If we pass a crew_size of zero to this function, it will divide by
zero. In C++, this would be undefined behavior. In Rust, it triggers a panic, which
typically proceeds as follows:</p>
<p>이 코드는 몇 세기 동안 잘 작동하다가 어느 날 선장이 유일한 생존자라는 사실이 밝혀질 수 있습니다. 이 함수에 <code>crew_size</code>를 0으로 전달하면 0으로 나누게 됩니다. C++에서는 이것이 미정의 동작을, <strong>Rust</strong>에서는 <code>패닉</code>을 발생시킵니다.</p>
<h3 id="러스트가-패닉에-빠지고-unwinding하는-과정">러스트가 패닉에 빠지고 Unwinding하는 과정</h3>
<ol>
<li>오류 메세지</li>
</ol>
<p>If you set the RUST_BACKTRACE environment variable, as the messages suggests, Rust will also dump the stack at this point</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/19f10624-a2b4-4a81-be44-7dccde5ed0a0/image.png" /></p>
<p>이 메세지는 제안하는 대로 RUST_BACKTRACE 환경 변수를 설정하면 러스트가 해당 지점의 스택을 같이 덤프해준다. </p>
<p>덤프(dump) = 메모리의 내용을 자세히 보여주는 것을 의미 </p>
<p>오류 메세지 대로 <code>RUST_BACKTRACE</code> 환경 변수를 설정하면, Rust 프로그램이 오류로 인해 중단될 때, <strong>어디서 어떻게 중단되었는지 자세한 정보를 제공하는 스택 트레이스를</strong> 출력한다. 이는 오류를 추적하고 디버깅하는 데 유용하다.</p>
<p>The stack is unwound. This is a lot like C++ exception handling.</p>
<ol start="2">
<li>스택이 해제된다. 이는 C++의 <strong>예외 처리</strong>와 매우 유사하다.</li>
</ol>
<p>The stack is unwound. This is a lot like C++ exception handling.
Any temporary values, local variables, or arguments that the current function
was using are dropped, in the reverse of the order they were created. Dropping a
value simply means cleaning up after it: any Strings or Vecs the program was
using are freed, any open Files are closed, and so on. User-defined drop methods
are called too; see &quot;Drop&quot; on page 302. </p>
<ul>
<li>현재 함수가 쓰던 임시 값, 지역 변수, 인수는 모두 <strong>생성된 순서와 반대로 드롭</strong>된다.</li>
</ul>
<p>= 프로그램이 <code>panic!</code>이나 오류로 인해 중단될 때, 프로그램의 각 함수 호출을 역순으로 정리하는 </p>
<ul>
<li>드롭 = 뒷정리 한다는 뜻</li>
<li>프로그램이 쓰던 String이나 Vec은 모두 해제되고 열린 File은 모두 닫힌다.</li>
</ul>
<p>Once the current function call is cleaned up, we move on to its caller, dropping its variables and arguments the same way. Then we move to that function's caller,
and so on up the stack</p>
<ul>
<li>현재 함수 호출이 정리되면, 호출부로 이동해서 같은 방법으로 변수와 인수를 드롭한다. 그리고 스택 끝에 닾을 때까지 이런식으로 계속해서 그 함수의 호출부로 이동해 정리한다.</li>
</ul>
<p>즉, 위의 것을 풀어 설명하면,</p>
<ol>
<li>현재 함수호출이 정리되면,</li>
</ol>
<ul>
<li>프로그램이 중단이 되었을때, 먼저 중단된 시점에 실행 중이던 현재 함수가 있다.</li>
<li>rust는 이 함수에서 사용 중인 모든 변수와 리소스를 정리(메모리 해제, 파일닫기 등 )한다.</li>
</ul>
<ol start="2">
<li><strong>호출부로 이동해서 같은 방법으로 변수와 인수를 드롭한다</strong>:</li>
</ol>
<ul>
<li>현재 함수가 정리된 후, Rust는 이 함수를 호출한 <strong>상위 함수</strong>로 이동</li>
<li>그리고 상위 함수에서도 동일하게 변수와 리소스를 정리</li>
</ul>
<ol start="3">
<li><strong>스택 끝에 닿을 때까지</strong>:<ul>
<li>Rust는 이러한 과정을 계속해서 반복하여 함수 호출 스택의 끝, 즉 프로그램이 시작된 지점까지 이동하며 모든 함수를 정리</li>
<li>프로그램이 처음 시작된 <code>main</code> 함수까지 모든 함수가 역순으로 정리될 때까지 이 작업 수행</li>
</ul>
</li>
</ol>
<p>Perhaps panic is a misleading name for this orderly process. A panic is not a crash. It's
not undefined behavior. It's more like a RuntimeException in Java or a
std::logic_error in C++. The behavior is well-defined; it just shouldn't be
happening</p>
<p>패닉은 이 규칙적인 과정에 어울리지 않는 이름일지 모른다. 미정의 동작보다는 자바의 <code>RuntimeException</code>과 가깝다. 단지 발생하면 안 될 뿐이다. </p>
<p>Finally, the thread exits. If the panicking thread was the main thread, then the
whole process exits (with a nonzero exit code).</p>
<ol start="4">
<li>끝으로 스레드가 종료된다. 만일 패닉에 빠진 스레드가 메인스레드였다면 (0이 아닌 종료 코드를 가지고) 전체 프로세스가 종료된다. </li>
</ol>
<h3 id="패닉이라는-것">패닉이라는 것..</h3>
<p>The idea is that Rust catches the invalid array access,
or whatever it is, before anything bad happens. It would be unsafe to proceed, so Rust
unwinds the stack. But the rest of the process can continue running</p>
<p>러스트는 잘못된 배열 접근이든 뭐든 안 좋은 일이 <strong>벌어지기 전</strong>에 잡아낸다. = 안전성 패닉에 빠지면 계속 진행하는것이 위험하므로 러스트는 스택을 해제한다. 그러나 프로세스의 나머지 부분은 계속 실행을 이어갈 수 있다.     </p>
<p>Panic is per thread. One thread can be panicking while other threads are going on
about their normal business</p>
<p>패닉은 <strong>스레드 별로 발생</strong>한다. 한 스레드가 패닉에 빠져도 다른 스레는 정상적으로 일을 수행할 수 있다. </p>
<p>There is also a way to catch stack unwinding, allowing the thread to survive and continue running. The standard library function std::panic:: catch_unwind() does
this. We won't cover how to use it, but this is the mechanism used by Rust's test harness to recover when an assertion fails in a test</p>
<p><strong>스택 해제를 잡아서</strong> 스레드를 죽지 않고 계속 실행되게 만드는 방법도 있다. 표준 라이브러리 함수 <code>std::panic::catch_unwind()</code>가하는 일이 바로 그것이다. 이 함수의 사용법은 다루지 않고 러스트의 테스트 도구가 <strong>테스트에 있는 단언문 실패 시</strong> 이 매커니즘을 써서 <strong>원상 복구한다는 것</strong>은 알아두기! </p>
<p>이 부분은 22장에서 자세히 다룬다고 함 </p>
<p>Ideally, we would all have bug-free code that never panics. But nobody's perfect. You
can use threads and catch_unwind() to handle panic, making your program more
robust.</p>
<p>절대로 패닉을 빠지지 않는 코드를 짤 수 있는 사람은 거의 없을 것 하지만,  스<strong>레드와 catch_unwind()로 패닉을 잘 다루면</strong> 프로그램을 보다 견고하게 만들 수 있다.</p>
<p>One important caveat is that these tools only catch panics that unwind the
stack. Not every panic proceeds this way.</p>
<blockquote>
<p>꼭 알아둬야 할 점은 <strong>스택을 해제하는 패닉만</strong> 이런 식으로 잡을 수 있다는 것이다.</p>
</blockquote>
<h3 id="자바의-try-catch와-다른-점">자바의 try catch와 다른 점</h3>
<ul>
<li>Rust에서 패닉은 일반적으로 <strong>복구 불가능한 오류</strong>로 간주됩니다. 따라서 패닉 후의 복구를 시도하는 대신 프로그램을 종료하는 것이 일반적입니다. <code>catch_unwind</code>을 사용해 패닉을 포착하는 것은 비상 상황에만 권장됩니다.</li>
<li>Java의 예외는 <strong>복구 가능한 오류</strong>로 간주되며, 예외 처리 구문을 통해 정상적인 프로그램 흐름으로 복귀할 수 있습니다. 이는 Java가 예외를 프로그램 로직의 일부로 사용할 수 있게 합니다.</li>
</ul>
<h2 id="03-aborting중단">03. Aborting(중단)</h2>
<p>Stack unwinding is the default panic behavior, but there are two circumstances in which Rust does not try to unwind the stack.</p>
<p>스택 해제는 패닉의 기본 동작이지만, 다음 두 가지 상황에서는 러스트가 <strong>스택 해제를 시도하지 않는다.</strong>  </p>
<h3 id="첫-번째-상환">첫 번째 상환</h3>
<p>If a .drop() method triggers a second panic while Rust is still trying to clean up after the first, this is considered fatal. Rust stops unwinding and aborts the whole process.</p>
<p>만일 러스트가 첫 번째 패닉을 정리하고 있는 상황에서 <code>.drop()</code> 메서드가 <strong>두 번째 패닉을 유발하면 이는 치명적인 상황으로 간주</strong>하고, 러스트는 해제를 멈추고 전체 프로세스를 중단한다.</p>
<h3 id="두-번째-상황">두 번째 상황</h3>
<p>Also, Rust's panic behavior is customizable. If you compile with -C panic-abort, the first panic in your program immediately aborts the process. (With this option, Rust does not need to know how to unwind the stack, so this can reduce the size of your compiled code.)</p>
<p>또한 러스트의 패닉 동작은 변경이 가능하다.  프로그램을 <code>-C panic=abort</code> 옵션으로 컴파일하면 <strong>첫
번째</strong> 패닉이 발생하는 즉시 프로세스가 중단된다(이 옵션을 쓰면 러스트가 스택 해제 방법을 몰라도 되기 때문에 컴파일된 코드의 크기가 줄어들 수 있다.)</p>
<p>It's unreasonable to expect every function in a program to anticipate and cope with bugs in its own code. Errors caused by other factors are another kettle of fish</p>
<p>프로그램에 있는 모든함수가자기 코드에 있는 버그를 예견해 대처할 수 있기를 기대하는 건 무리가  있다. 하지만 다른 요인에 의해 유발되는 오류는 전혀 다른 문제다.  </p>
<h2 id="04-result">04. Result</h2>
<p>Rust doesn't have exceptions. Instead, functions that can fail have a return type that says so:</p>
<p><strong>러스트는 예외가 없다.</strong> 대신 실패할 수 있는 함수가 다음과 같은 반환 타입을 갖는다.</p>
<pre><code class="language-rust">fn get weather (location: LatLng) -&gt; Result&lt;Weather Report, io::Error&gt;</code></pre>
<p>The Result type in Rust indicates potential failure in functions. 
Rust에서 <code>Result</code> 타입은 함수 실행 시 발생할 수 있는 실패를 나타낸다.</p>
<p>When calling a function like get_weather(), it returns either Ok(weather) for success or Err(error_value) for an error, such as an io::Error. Rust requires handling these results to avoid compiler warnings. 
예를 들어, <code>get_weather()</code> 함수를 호출하면 성공 시 <strong>Ok(weather)</strong>, 실패 시 <strong>Err(error_value)</strong>를 반환하며, 이때 <strong>error_value</strong>는 io::Error로 어떤 문제가 발생했는지 설명한다. Rust는 이러한 결과를 처리하도록 강제하며, <code>Result</code> 값을 사용하지 않으면 컴파일러 경고가 발생한다.</p>
<h2 id="05-catching-errors오류-잡기">05. Catching Errors(오류 잡기)</h2>
<pre><code class="language-rust">match get weather (hometown) {
    Ok(report) =&gt; {
        display_weather (hometown, &amp;report);
    }
    Err(err) =&gt; {
        println(&quot;error querying the weather: {}&quot;, err);
        schedule_weather_retry();
    }
}</code></pre>
<blockquote>
<p>다른 언어의 <strong>try/catch</strong>에 해당한다. 오류를 호출부에 넘기지 않고 직접 처리하고자 할 때 이 방법을 쓴다.</p>
</blockquote>
<p>match is a bit verbose, so Result&lt;T, E&gt; offers a variety of methods that are useful in particular common cases. Each of these methods has a match expression in its implementation. (For the full list of Result methods, consult the online documentation. The methods listed here are the ones we use the most.)</p>
<p>하지만, <code>match</code>는 코드를 구구절절 늘어놓는 경향이 있어 <code>Result&lt;T, E&gt;</code>는 <strong>자주 겪는 몇 가지 상황에서 유용하게 쓸 수 있는 메서드들</strong>을 모아 제공한다. 이 메서드들은 각자 자신의 구현안에 match 표현식을 가지고 있다.    </p>
<h3 id="메서드-소개">메서드 소개</h3>
<ol>
<li><strong>result.is_ok(), result.is_err() :</strong> result가 성공 결과인지 오류 결과인지 말해 주는 bool을 반환한다.</li>
<li><strong>result.ok() :</strong> 성공값이 있을 경우 그것을 Option로 반환한다. result가 <code>성공</code> 결과이면 Some (success_value)를 반환하고, <code>그렇지 않으면</code> None을 반환하며 오륫값은 버린다.</li>
<li><strong>result.err() :</strong> 오륫값이 있을 경우 그것을 Option로 반환한다.</li>
<li><strong>result.unwrap_or(fallback) :</strong> result가 <strong>성공</strong> 결과일 경우 성공값을 반환하고, <strong>그렇지 않으면</strong> fallback을 반환하며 오릇값은 버린다.</li>
</ol>
<pre><code class="language-rust">// 남부 캘리포니아의 평상시 예측치.
const THE_USUAL: WeatherReport= WeatherReport::Sunny (72);

// 실제 날씨 정보를 받아온다.
// 받아올 수 없으면 평상시 예측치를 대신 쓴다.
let report = get_weather(los_angeles).unwrap_or(THE_USUAL);
display_weather(los_angeles, &amp;report);</code></pre>
<p>이 메서드는 반환 타입이 Option가 아니라 이기 때문에<strong>.ok() 대신 쓰면 편리하다.</strong> 물론 적
절한 대체값이 있을 때만 쓸 수 있다.</p>
<ol>
<li><strong>result.unwrap_or_else(fallback_fn) :</strong> 앞과 동일하지만 대체값을 직접 받는 게 아니라 <strong>함수나 클로저를 받는다는 점이 다르다.</strong> 쓰지도 않을 대체값을 계산하기 아까울 때 쓴다. <code>fallback_fn</code>은 오류 결과를 가질 때만 호출된다.</li>
</ol>
<pre><code class="language-rust">let report =
get_weather(hometown)
.unwrap_or_else(i_err! vague_prediction(hometown));
</code></pre>
<ol start="2">
<li><strong>result.unwrap() :</strong> 마찬가지로 result가 성공 결과일 경우 성공값을 반환한다. <strong>하지만 result가 오류 결과일 경우에는 패닉에 빠진다.</strong> 이 메서드는 용도가 따로 있는데 그 부분은 잠시 뒤에 살펴본다.</li>
<li><strong>result.expect(message) :</strong> unwrap()과 동일하지만 패닉에 빠졌을 때 출력할 메시지를 지정할 수 있다.</li>
</ol>
<h3 id="끝으로-다음-메서드들은-result에-있는-레퍼런스를-다룰-때-사용한다">끝으로 다음 메서드들은 Result에 있는 레퍼런스를 다룰 때 사용한다.</h3>
<ol start="4">
<li>result.as_ref() : Result&lt;T, E&gt;를 Result&lt;&amp;T, &amp;E&gt;로 변환한다.</li>
<li>result.as_mut() : 앞과 동일하지만 변경할 수 있는 레퍼런스를 빌려 온다는 점이 다르다. 반환 타입은 Result&lt;&amp;mutT, &amp;mut E&gt;다.</li>
</ol>
<p>One reason these last two methods are useful is that all of the other methods listed
here, except.is_ok() and .is_err(), consume the result they operate on. </p>
<p>마지막 두 메서드가 유용한 이유 중 하나는 .is_ok() .is_err()을 제외한 여기 나열된 다른 모든
메서드들이 작업 대상인 result를 소비(consume)한다는 것이다. </p>
<p>That is,
they take the self argument by value. Sometimes it's quite handy to access data inside
a result without destroying it, and this is what .as_ref() and .as_mut() do for us.</p>
<blockquote>
<p>즉, 이들은 <code>self 인수</code>를 값으로 받는다. 경우에 따라서는 <strong>result에 있는 데이터를 소멸시키지 않고 접근하는 것이 아주 유용할 때가 있는데,</strong> 이렇게 할 수 있도록 해주는 것이 바로 <code>.as_ref()</code>와 <code>.as_mut()</code>다.</p>
</blockquote>
<h3 id="as_ref와-as_mut의-역할">.as_ref()와 .as_mut()의 역할</h3>
<ul>
<li><code>.as_ref()</code>와 <code>.as_mut()</code> 메서드는 <code>Result</code> 타입에서 값을 참조로 접근하거나 가변 참조로 접근할 수 있도록 해주는 메서드</li>
<li><code>.as_ref()</code>는 값을 소멸시키지 않고, <strong>참조로 접근</strong>할 수 있게 한다. 이를 통해 값에 접근하되, 소유권을 넘기지 않으므로 원래 값은 여전히 유효하다.</li>
<li><code>.as_mut()</code>는 값을 소멸시키지 않고, <strong>가변 참조로 접근</strong>하여 값을 수정할 수 있게 한다.</li>
<li>이 메서드들은 원래 <code>Result</code> 값을 소유권을 넘기지 않고도 필요한 작업을 수행할 수 있게 해주는 유용한 도구디다.</li>
</ul>
<pre><code class="language-rust">fn main() {
    let result: Result&lt;String, String&gt; = Ok(String::from(&quot;Hello&quot;));

    // result를 소멸시키지 않고, 내부의 값을 참조로 접근
    match result.as_ref() {
        Ok(value) =&gt; println!(&quot;Got a reference to: {}&quot;, value),
        Err(e) =&gt; println!(&quot;Got an error reference: {}&quot;, e),
    }

    // result는 여전히 사용할 수 있습니다.
    println!(&quot;Original result: {:?}&quot;, result);
}</code></pre>
<p>For example, suppose you'd like to call result.ok(), but you need result to be left
intact. You can write result.as_ref().ok(), which merely borrows result, returning an Option&lt;&amp;T&gt; rather than an Option</p>
<p>예를 들어, result.ok()를 호출하더라도 <strong>result가 그대로 남아 있길 원한다면</strong> result.as_ref().ok()라고 쓰면 된다. 이렇게하면 result를 빌려 오게 되므로 Option가 아니라 <code>Option&lt;&amp;T&gt;</code>가 반환된다</p>
<h2 id="06-result-type-aliasesresult-타입-별칭">06. Result Type Aliases(Result 타입 별칭)</h2>
<p>Sometimes you'll see Rust documentation that seems to omit the error type of a Result:</p>
<p>러스트 문서를 보다 보면 가끔 오류 타입이 생략된 Result를 만날 때가 있다.</p>
<pre><code class="language-rust">fn remove_file(path: &amp;Path) -&gt; Result&lt;()&gt;</code></pre>
<p>이는 Result 타입 별칭을 쓰고 있다는 뜻이다.   </p>
<p>A type alias is a kind of shorthand for type names. Modules often define a Result
type alias to avoid having to repeat an error type that's used consistently by almost
every function in the module. For example, the standard library's std::io module
includes this line of code:</p>
<p>일종의 축약 표시로, 모듈은 보통 Result 타입 별칭을 정의해서 <strong>그 모듈에 있는 함수들 대부분이 공통으로 사용하는 오류 타입을 반복해 적지 않아도 되게끔 만든다.</strong></p>
<p>This defines a public type std::io::Result. It's an alias for Result&lt;T, E&gt;, but
hardcodes std::io:: Error as the error type. In practical terms, this means that if
you write use std::io;, then Rust will understand io::Result as shorthand for Result&lt;String, io::Error&gt;</p>
<p><code>use std::io;</code>라고 써 두면 러스트가 io::Result을 <strong>Result&lt;String, io::Error&gt;의 축약 표기</strong>로 이해한다는 뜻이다. </p>
<p>이는 표준 라이브러리 모듈 안에 들어 있기 때문</p>
<h2 id="07-printing-errors오류-출력하기">07. Printing Errors(오류 출력하기)</h2>
<blockquote>
<p>Rust에서 <code>std::error::Error</code> 트레이트는 다양한 오류 타입을 처리하기 위한 공통 인터페이스를 제공합니다. 이를 통해 오류를 출력하고, 근본 원인을 추적하며, 적절한 오류 메시지를 얻을 수 있다. <code>println!</code>과 <code>writeln!</code> 매크로를 사용하여 오류를 콘솔에 출력하거나 특정 스트림에 기록할 수 있다. <code>anyhow</code> 크레이트는 표준 라이브러리 이상의 강력한 오류 관리 기능을 제공한다.</p>
</blockquote>
<p>Sometimes the only way to handle an error is by dumping it to the terminal and moving on.</p>
<p>경우에 따라서는 오류를 터미널에 덤프하고 다음으로 넘어가는 게 유일한 방법일 때가 있다.</p>
<pre><code class="language-rust">println(&quot;error querying the weather: {}&quot;, err);</code></pre>
<p>The standard library defines several error types with boring names: std::io:: Error,
std::fmt:: Error, std::str::Utf8Error, and so on</p>
<p>표준 라이브러리는 std::io::Error, std::fmt::Error, std::str::Utf8Error 등 지루한 이름으로 된 오류 타입 몇 가지를 정의해 두고 있다. </p>
<p>All of them implement a
common interface, the std::error:: Error trait, which means they share the following features and methods:</p>
<p>이들은 모두 공통 인터페이스인 <code>std::error:Error</code> 트레이트를 구현하고 있는데, 그 말인 즉슨 이들이 <strong>아래의 기능과 메서드를 공유하고 있다는 뜻</strong>이다.</p>
<ol>
<li><strong>println!()</strong></li>
</ol>
<p>All error types are printable using this. Printing an error with the {} format
specifier typically displays only a brief error message. Alternatively, you can print
with the {:?} format specifier, to get a Debug view of the error. This is less userfriendly, but includes extra technical information.</p>
<p><strong>모든 오류 타입은 이 메서드로 출력할 수 있다.</strong> {} 형식 지정자로 오류를 출력하면 보통 간단한 오류만 표시된다. 이것 말고 <code>{:?}</code> 형식 지정자를 써서 해당 오류의 Debug 뷰를 보는 방법도 있는데 내용은 좀 딱딱해도 <strong>추가적인 기술 정보를 같이 볼 수 있어서 좋다.</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2971e93c-dc2b-43c5-826d-0b89aea42cee/image.png" /></p>
<ol start="2">
<li>err.to_string() : 오류 메세지를 String으로 반환한다.</li>
<li><strong>err.source()</strong> </li>
</ol>
<blockquote>
<p><code>source()</code> 메서드는 현재 오류의 근본 원인이 되는 이전 오류를 반환</p>
</blockquote>
<p>Returns an option of the underlying error, if any, that caused err</p>
<ul>
<li>err의 원인이 되는 오류가 있을 경우, 그것을 Option으로 반환한다.</li>
</ul>
<p>For example, a network error might cause a banking transaction to fail, leading to your boat being repossessed.  Here, err.to_string() might be &quot;boat was repossessed&quot;, and err.source() would return the error related to the failed transaction. This transaction error’s to_string() could be &quot;failed to transfer $300 to United Yacht Supply&quot;, and its source() might return a detailed io::Error about the specific network outage.</p>
<ul>
<li>예를 들어, 네트워크 오류로 인해 은행 거래가 실패하고, 그로 인해 보트가 압류되었다고 가정합시다. 이 경우, <code>err.to_string()</code>은 &quot;boat was repossessed&quot;(보트가 압류됨)일 수 있으며, <code>err.source()</code>는 거래 실패와 관련된 오류를 반환할 것이다. 이 거래 오류의 <code>to_string()</code>은 <code>&quot;failed to transfer $300 to United Yacht Supply&quot;</code>(United Yacht Supply에 $300 이체 실패)일 수 있고, 이 오류의 <code>source()</code>는 네트워크 중단에 관한 <strong>상세한 내용을 담은 io::Error를 반환</strong>할 수 있다.</li>
</ul>
<p>Since this third error is the root cause, its <code>.source()</code> method returns <code>None</code>. Standard library errors often return <code>None</code> for their source because they usually operate at a lower level. To print all available error information, use a function like the one provided.</p>
<ul>
<li>이때 세 번째 오류는 문제의 근본 원인이므로, <code>.source(</code>)메서드는 None을 반환할 것이다. 표준 라이브러리의 오류는 보통 낮은 수준에서 작동하기 때문에, 원인을 반환하는 경우가 드물다. 오류에 관한 모든 정보를 출력하려면 제공된 함수를 사용해야 함</li>
</ul>
<pre><code class="language-rust">std::error::Error;
use std::io::{Write, stderr};
/// 오류 메시지를 'stderr`에 덤프한다.

/// 오류 메시지를 생성하는 도중이나 'stderr'에 기록하는 도중에 
/// 또 다른 오류가 발생하면 무시한다.
fn print_error(mut err: &amp;dyn Error) {
    let_ = writeln!(stderr(), &quot;error: {}&quot;, err);
    while let Some(source) = err.source() {
    let_ = writeln!(stderr(), &quot;caused by: {}&quot;, source); 
    err = source;
    }
}</code></pre>
<p>The writeln! macro works like println!, except that it writes the data to a stream of
your choice. Here, we write the error messages to the standard error stream,
std::io::stderr. We could use the eprintln! macro to do the same thing, but
eprintln! panics if an error occurs. In print_error, we want to ignore errors that
arise while writing the message; we explain why in &quot;Ignoring Errors&quot; on page 169,
later in the chapter.</p>
<p>rust의 <strong>writeln!</strong> 매크로는 <strong>println!</strong>과 유사하게 동작하지만, 데이터를 특정 스트림에 쓸 수 있게 해준다. 여기서는 오류 메시지를 <code>표준 오류 스트림(std::io::stderr)</code>에 쓰기 위해 <strong>writeln!</strong>을 사용한다. <strong>eprintln!</strong> 매크로도 stderr에 메시지를 쓸 수 있지만, 쓰는 도중 오류가 발생하면 패닉을 일으킨다. print_error 함수에서는 메시지를 쓰는 동안 발생하는 오류를 무시하고 싶었는데, 이유는 오류 무시하기에서 나옴</p>
<h3 id="writeln-매크로">writeln! 매크로</h3>
<ul>
<li><strong>기능</strong>: <code>writeln!</code> 매크로는 <code>println!</code>과 비슷하게 동작하지만, 주어진 스트림에 데이터를 씁니다. 이 스트림은 파일, 네트워크 소켓, 또는 표준 출력/오류 스트림일 수 있습니다.</li>
<li><strong>사용 방법</strong>: <code>writeln!</code>의 첫 번째 인수는 데이터를 쓸 대상 스트림입니다. 예를 들어, <code>stderr</code> 스트림에 쓰려면 <code>writeln!(std::io::stderr(), &quot;error: {}&quot;, err)</code>와 같이 사용합니다.</li>
<li><strong>유연성</strong>: 이는 데이터를 표준 출력 대신 다른 위치로 보내고자 할 때 유용합니다.</li>
</ul>
<pre><code class="language-rust">use std::io::{self, Write};

fn main() {
    let mut handle = io::stdout(); // 표준 출력에 쓰기
    writeln!(handle, &quot;Hello, world!&quot;).unwrap();

    let mut handle = io::stderr(); // 표준 오류 스트림에 쓰기
    writeln!(handle, &quot;An error occurred!&quot;).unwrap();
}
</code></pre>
<h3 id="eprintln-매크로">eprintln! 매크로</h3>
<ul>
<li><strong>기능</strong>: <code>eprintln!</code> 매크로는 <code>println!</code>과 유사하게 작동하지만, 메시지를 표준 오류 스트림(<code>stderr</code>)에 씁니다.</li>
<li><strong>패닉 발생</strong>: <code>eprintln!</code>은 메시지를 쓰는 도중 오류가 발생하면 패닉을 일으킵니다. 이는 추가적인 오류 처리를 필요로 할 수 있습니다.</li>
</ul>
<pre><code class="language-rust">fn main() {
    eprintln!(&quot;This is an error message!&quot;);
}
</code></pre>
<h3 id="print_error-함수에서-writeln을-사용하는-이유"><code>print_error</code> 함수에서 <code>writeln!</code>을 사용하는 이유</h3>
<ul>
<li><strong>오류 무시</strong>: <code>print_error</code> 함수에서는 오류 메시지를 쓰는 도중에 발생하는 오류를 무시하고자 합니다. 이는 추가적인 복잡성을 피하기 위해서입니다.</li>
<li><strong>안정성</strong>: <code>writeln!</code>을 사용하면, 쓰기 작업 중 발생하는 오류를 <code>Result</code>로 반환하고, 이를 무시할 수 있는 유연성을 제공합니다. 반면 <code>eprintln!</code>은 패닉을 발생시켜 프로그램의 흐름을 방해할 수 있습니다.</li>
<li><strong>의도된 동작</strong>: <code>print_error</code> 함수는 이미 발생한 오류를 보고하는 도중에 또 다른 오류가 발생하더라도 프로그램의 주 실행 흐름을 방해하지 않도록 설계되었습니다.</li>
</ul>
<pre><code class="language-rust">use std::error::Error;
use std::io::{self, Write};

fn print_error(mut err: &amp;dyn Error) {
    let _ = writeln!(io::stderr(), &quot;error: {}&quot;, err);
    while let Some(source) = err.source() {
        let _ = writeln!(io::stderr(), &quot;caused by: {}&quot;, source);
        err = source;
    }
}</code></pre>
<ul>
<li>이 함수에서는 <code>writeln!</code>을 사용하여 <code>stderr</code>에 오류 메시지를 씁니다.</li>
<li>쓰기 작업 중 발생할 수 있는 오류를 무시하기 위해 <code>Result</code>를 처리하지 않고, 단순히 <code>_</code>로 무시합니다.</li>
</ul>
<p>The standard library's error types do not include a stack trace, but the popular anyhow
crate provides a ready-made error type that does, when used with an unstable version
of the Rust compiler</p>
<p><strong>표준 라이브러리의 오류 타입은 스택 트레이스를 포함하지 않는다.</strong> 스택 트레이스를 포함하는 오류
타입이 필요할 때는 <code>anyhow</code> 크레이트의 도움을 받으면 되는데, 단 이 경우에는 정식으로 릴리스되지
않은 불안정한 버전의 러스트 컴파일러를 써야 한다.</p>
<h3 id="anyhow">anyhow</h3>
<ul>
<li><code>anyhow</code>는 Rust의 오류 처리에 강력한 기능을 추가하는 크레이트입니다. 복잡한 오류 체인과 상세한 스택 트레이스를 관리할 수 있는 기능을 제공합니다. Rust의 불안정(Unstable) 버전에서 제공되는 특정 기능을 활용하여, 더 많은 디버깅 정보를 제공합니다.</li>
<li><strong>불안정한 Rust 컴파일러(Unstable Rust Compiler)</strong>:<ul>
<li>Rust는 주기적으로 새로운 기능을 실험하기 위해 &quot;불안정한&quot; 버전을 출시합니다.</li>
<li><code>anyhow</code> 크레이트는 이러한 불안정 버전에서만 사용 가능한 특정 기능을 활용하여, 스택 트레이스와 같은 추가적인 오류 정보를 제공합니다.</li>
</ul>
</li>
</ul>
<h3 id="anyhow-사용-예시"><code>anyhow</code> 사용 예시</h3>
<pre><code class="language-rust">use anyhow::{Result, Context};

fn main() -&gt; Result&lt;()&gt; {
    let file_content = std::fs::read_to_string(&quot;non_existent_file.txt&quot;)
        .context(&quot;Failed to read the file&quot;)?;
    println!(&quot;{}&quot;, file_content);
    Ok(())
}
</code></pre>
<ul>
<li><code>anyhow::Context</code> 트레이트를 사용하여 오류 메시지에 추가적인 정보를 제공할 수 있습니다.</li>
<li><code>context(&quot;Failed to read the file&quot;)</code>는 기본 오류 메시지에 더 자세한 문맥을 추가하여, 디버깅을 쉽게 합니다.</li>
</ul>
<h2 id="08-propagating-errors오류-전파하기">08. Propagating Errors(오류 전파하기)</h2>
<p>It is simply too much code to use a 10-line match statement every place where something could go wrong.</p>
<p>문제가 생길 수 있는 곳마다 10줄짜리 match문으로 코드를 도배하다시피 하는 건 너무 과하다.</p>
<p>Instead, if an error occurs, we usually want to let our caller deal with it. We want errors to propagate up the call stack</p>
<p>오류가 발생하면 보통은 호출부에 처리를 맡기고 싶어 한다. 오류가 호출 스택을 타고 <strong>전파(propagation)</strong>되길 원하는 것이다. </p>
<p>Rust has a ? operator that does this. You can add a ? to any expression that produces a Result, such as the result of a function call:</p>
<p>러스트에는 이런 일을 하는 <code>?</code>연산자가 있다. <code>?</code>는 <strong>함수 호출 결과와 같이 Result를 산출하는 모든 표현식에 붙여 쓸 수 있다.</strong>   </p>
<pre><code class="language-rust">let weather = get_weather(hometown)?;
</code></pre>
<p>The behavior of? depends on whether this function returns a success result or an error result:</p>
<p>앞의 코드에서 <code>?</code>의 동작은 <strong>함수가 성공 결과를 반환하는지, 오류 결과를 반환하는지</strong>에 따라 달라진다.</p>
<blockquote>
<p>Rust에서 <code>?</code> 연산자는 <code>Result</code> 또는 <code>Option</code>을 반환하는 함수에서 오류 처리를 간소화합니다.</p>
</blockquote>
<ul>
<li><p>On success, it unwraps the Result to get the success value inside. The type of weather here is not Result&lt;Weather Report, io::Error&gt; but simply WeatherReport.</p>
</li>
<li><p><code>성공</code>한 경우에는 Result를 풀어서 그 안에 있는 <strong>성공값을 꺼낸다.</strong> 여기서 <strong>weather</strong>의 타입은
Result&lt;WeatherReport, io::Error&gt;가 아니라 그냥 <code>WeatherReport</code>다.</p>
</li>
<li><p>On error, it immediately returns from the enclosing function, passing the error result up the call chain. To ensure that this works, ? can only be used on a Result in functions that have a Result return type.</p>
</li>
<li><p><code>오류</code>가 발생한 경우에는 즉시 바깥쪽 함수에서 복귀하고 오류 결과를 호출 체인 위로 전달한다. 이 때문에 <code>?</code>는 <strong>반환 타입이 Result인 함수에서만</strong> 쓸 수 있다.</p>
</li>
</ul>
<p>There's nothing magical about the ? operator. You can express the same thing using a
match expression, although it's much wordier:</p>
<p>match 표현식으로 가능하지만, ?으로 하면 간편하게 처리 가능하다는 것이다.</p>
<p>The only differences between this and the ? operator are some fine points involving
types and conversions. We'll cover those details in the next section.
In older code, you may see the try! () macro, which was the usual way to propagate
errors until the? operator was introduced in Rust 1.13</p>
<p>다만, 이 둘은 타입과 변환이 개입되는 부분에서 약간의 미묘한 차이점이 있다.  오래된 코드를 읽다 보면 try!() 매크로를 보게 될 수도 있다. <code>?</code> 연산자가 도입되기 전까지는 대부분 <strong>이 매크로를 써서 오류를 전파</strong>했다.</p>
<pre><code class="language-rust"> let weather try! (get_weather (hometown));</code></pre>
<p>The macro expands to a match expression, like the one earlier.
It's easy to forget just how pervasive the possibility of errors is in a program, particularly in code that interfaces with the operating system. The ? operator sometimes shows up on almost every line of a function:</p>
<p>이 매크로는 이전 예시처럼 <code>match</code> 표현식으로 확장된다. 프로그램에서 오류가 발생할 가능성을 쉽게 잊을 수 있지만, 특히 운영 체제와 인터페이스하는 코드에서는 그렇다. <code>?</code> 연산자는 때로 함수의 <strong>거의 모든 줄에서 등장할 수 있다:</strong></p>
<pre><code class="language-rust">use std::fs;
use std::io;
use std::path::Path;

fn move_all(src: &amp;Path, dst: &amp;Path) -&gt; io::Result&lt;()&gt; {
    for entry_result in src.read_dir()? { // 디렉터리를 여는 도중 오류가 발생할 수 있습니다.
        let entry = entry_result?; // 디렉터리를 읽는 도중 오류가 발생할 수 있습니다.
        let dst_file = dst.join(entry.file_name());
        fs::rename(entry.path(), dst_file)?; // 파일 이름 변경 중에 오류가 발생할 수 있습니다.
    }
    Ok(()) // 휴!
}
</code></pre>
<p><code>?</code> 연산자는 <code>Option</code> 타입에서도 비슷하게 작동한다. <code>Option</code>을 반환하는 함수에서는, <code>?</code>를 사용하여 값을 언랩하고 <code>None</code>인 경우(값이 존재하지 않는 경우) 조기에 반환할 수 있다:</p>
<pre><code class="language-rust">let weather = get_weather(hometown).ok()?;</code></pre>
<p>이 코드는 두 가지 주요 작업을 수행합니다:</p>
<ol>
<li><code>get_weather(hometown)</code> 함수 호출의 결과를 <code>ok()</code> 메서드로 변환합니다.</li>
<li><code>ok()</code> 메서드의 결과에 <code>?</code> 연산자를 사용합니다.</li>
</ol>
<h3 id="각-부분의-역할">각 부분의 역할</h3>
<p><strong>1. get_weather(hometown)</strong></p>
<ul>
<li>get_weather는 <code>hometown</code>이라는 인자를 받아 호출되는 함수입니다.</li>
<li>이 함수가 반환하는 타입은 <code>Result&lt;T, E&gt;</code>입니다. 여기서 <code>T</code>는 <strong>성공적으로 반환되는 값의 타입</strong>이고, <code>E</code>는 <strong>오류가 발생했을 때 반환되는 오류 타입</strong>입니다.</li>
</ul>
<p><strong>2. .ok()</strong></p>
<ul>
<li>ok() 메서드는 Result&lt;T, E&gt; 타입에서 사용됩니다.</li>
<li>ok() 메서드는 Result를 Option으로 변환합니다:<ul>
<li>만약 Result가 Ok(value)라면, Some(value)를 반환합니다.</li>
<li>만약 Result가 Err(error)라면, None을 반환합니다.</li>
</ul>
</li>
</ul>
<p>즉, get_weather(hometown).ok()는 Result&lt;T, E&gt;를 Option로 변환합니다.</p>
<p><strong>3. ? 연산자</strong></p>
<ul>
<li>? 연산자는 Option 타입이나 Result 타입에서 사용되어, 값이 있으면 그 값을 반환하고, 없으면 함수 전체를 조기에 종료합니다.</li>
<li>Option에서 ?를 사용하면:<ul>
<li>값이 <strong>Some(value)</strong>이면 값을 반환합니다.</li>
<li>값이 <code>None</code>이면, 호출한 함수가 즉시 None을 반환합니다. 즉시. 종료한다.</li>
</ul>
</li>
</ul>
<p><strong>Option 타입으로 변환된 이유</strong></p>
<p>위의 과정을 통해, get_weather(hometown)가 반환하는 <strong>Result 타입의 값을 Option 타입으로 변환한 후 ? 연산자를 사용하고 있습니다</strong>. 따라서 최종적으로 weather는 Option 타입이 됩니다.</p>
<p>즉, <code>let weather = get_weather(hometown).ok()?;</code>는 <code>weather</code>를 <code>Option</code> 타입으로 변환하고, 값이 없으면 조기에 반환하여 함수의 흐름을 제어합니다.</p>
<h2 id="09-working-with-multiple-error-types여러-오류-타입-다루기">09. Working with Multiple Error Types(여러 오류 타입 다루기)</h2>
<pre><code class="language-rust">use std::io::{self, BufRead};
        /// 텍스트 파일에서 정수들을 읽어 온다.
        /// 파일에는 숫자가 한 줄에 하나씩 있다고 가정한다.
        fn read_numbers(file: &amp;mut dyn BufRead) → Result&lt;Vec&lt;i64&gt;, io::Error&gt;{
            let mut numbers = vec![];
            for line_result in file. lines() {
                // 줄을 읽을 때 실패할 수 있다.
                numbers.push(line.parse()?); // 정수를 파싱할 때 실패할 수 있다.
                let line = line_result?;
        }
        Ok(numbers)
}</code></pre>
<p>Rust gives us a compiler error:</p>
<p>러스트는 앞의 코드에 대해 다음과 같은 컴파일러 오류를 낸다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/50ddfa32-9319-46d7-9fd5-dce616768466/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/23887057-22df-471a-bc4d-bbf2f9049fe4/image.png" /></p>
<p>The terms in this error message will make more sense when we reach Chapter 11,</p>
<p>여기 나오는 오류 메세지의 용어들은 트레이트를 다루는 11장을 읽고 나면 이해가 될 것이라고 함</p>
<p>which covers traits. For now, just note that Rust is complaining that the ? operator
can't convert a std::num:: ParseIntError value to the type std::io::Error</p>
<p><code>?</code>는 오류를 자동으로 전파하기 위해 변환이 필요한데, 현재 코드에서는 ? 연산자가 std::num::ParseIntError 값을 std::io::Error 타입으로 변환할 수 없어서 오류를 낸 것</p>
<p>참고로 </p>
<p><strong><code>std::convert::From</code> 트레이트</strong>:</p>
<ul>
<li>Rust에서 한 타입을 다른 타입으로 변환하기 위해 사용하는 트레이트이다. <code>From</code> 트레이트가 구현된 두 타입 사이에서는 안전하게 변환할 수 있다.</li>
</ul>
<p>There are several ways of dealing with this. For example, the image crate that we used
in Chapter 2 to create image files of the Mandelbrot set defines its own error type,
ImageError, and implements conversions from io:: Error and several other error
types to ImageError. If you'd like to go this route, try the thiserror crate, which is
designed to help you define good error types with just a few lines ofcode.</p>
<p>문제를 해결하는 방법은 여러가지가 있음</p>
<ol>
<li>2장에서 망델브로 집합에서 나온 <strong>image 크레이트 사용</strong></li>
</ol>
<p>A simpler approach is to use what's built into Rust. All of the standard library error
types can be converted to the type Box&lt;dyn std::error:: Error + Send + Sync +
'static&gt;. This is a bit of a mouthful, but dyn std::error:: </p>
<ol>
<li>좀 더 간단한 방법은 <strong>러스트의 내장된 기능</strong> 이용 </li>
</ol>
<ul>
<li>표준 라이브러리의 모든 오류 타입은 <code>Box&lt;dyn std::error:: Error + Send + Sync+ 'static&gt;</code> 타입으로 변환될 수 있다.</li>
</ul>
<p>Error represents &quot;any error,&quot; and Send + Sync + 'static makes it safe to pass between threads, which you'll often want. For convenience, you can define type aliases</p>
<ul>
<li>dyn std::error::Error는 '모든 오류'를 표현 하고, Send+ Sync+ 'static은 이를 스레드 간에 전달해도 안전하게 만들어 준다. 다음처럼 타입 별칭을 정의해 쓰면 편리하다.</li>
</ul>
<pre><code class="language-rust">type GenericError = Box&lt;dyn std::error:: Error + Send + Sync + 'static&gt;;
type GenericResult&lt;T&gt; Result&lt;T, GenericError&gt;;</code></pre>
<p>Then, change the return type of read_numbers() to GenericResult&lt;Vec&gt;. With
this change, the function compiles. The ? operator automatically converts either type
oferror into a GenericError as needed.</p>
<p>그런 다음 <strong>read_numbers()</strong>의 반환 타입을 <strong>GenericResult&lt;Vec&gt;</strong>로 바꾼다. 이렇게 하고 나면 함수가 문제없이 컴파일된다. 이제? 연산자는 필요에 따라 두 오류 타입을 GenericError로 자동 변환한다.</p>
<p>Incidentally, the ? operator does this automatic conversion using a standard method
that you can use yourself. To convert any error to the GenericError type, call
GenericError::from():</p>
<p>여담이지만 연산자는 누구나 쓸 수 있는 표준 메서드를 써서 이 <code>자동 변환을 수행</code>한다. 임의의 오류를 GenericError 타입으로 변환하려면 <strong>GenericError: :from()을 호출</strong>하면 된다</p>
<pre><code class="language-rust">let io_error = io::Error::new(
    io::ErrorKind::Other, &quot;timed out&quot;);
    // io::Error를 만든다.
return Err(GenericError: :from(io_error)); // 직접 GenericError로 변환한다</code></pre>
<p>The downside ofthe GenericError approach is that the return type no longer communicates precisely what kinds of errors the caller can expect. The caller must be
ready for anything</p>
<p><code>GenericError</code> 방식의 단점은 반환 타입이 이 이상 발생할 수 있는 <strong>오류의 종류를 콕 찍어 알려 주지 않는다는 것</strong>이다. 호출부는 만반의 준비가 되어 있어야 한다.</p>
<p><strong>GenericResult를 반환하는 함수를 호출할 때</strong> 특정 유형으로 된 오류만 처리하고 나머지는 <strong>그냥 전파하길 원한다면 제네릭 메서</strong>드 <code>error.downcast_ref:: &lt;ErrorType&gt;()</code>을 쓰면 된다. 이 메서드는 만일 어떤 오류가 여러분이 찾는 그 특정 유형의 것일 경우 그 오류의 레퍼런스를 빌려 온다.</p>
<p>많은 언어가 이를 위한 문법을 내장하고 있지만, 실제로 쓰이는 일은 거의 드물다. 따라서 러스트는 이를 <code>메서드</code>로 처리한다.</p>
<h2 id="10-발생할-리-없는-오류-다루기dealing-with-errors-that-cant-happen">10. '발생할 리 없는 오류 다루기’(Dealing with Errors That &quot;Can't Happen”)</h2>
<p>Example: Parsing a Configuration File</p>
<p>예시: 구성 파일 파싱</p>
<pre><code class="language-rust">if next_char.is_digit(10) {
    let start = current_index;
    current_index = skip_digits(&amp;line, current_index);
    let digits = &amp;line[start..current_index];
    let num = digits.parse::&lt;u64&gt;();
}
</code></pre>
<p><strong>The Problem: str.parse::() Returns a Result</strong></p>
<p>문제: <code>str.parse::&lt;u64&gt;()</code>는 <code>Result</code>를 반환한다</p>
<pre><code class="language-rust">&quot;bleen&quot;.parse::&lt;u64&gt;() // ParseIntError: invalid digi</code></pre>
<p><strong>Solution: Use <code>.unwrap()</code> When Confident</strong></p>
<p>해결책: 확실할 때는 <code>.unwrap()</code> 사용하기</p>
<pre><code class="language-rust">let num = digits.parse::&lt;u64&gt;().unwrap();</code></pre>
<p>Beware: Overflow Can Happen</p>
<p>주의: 오버플로가 발생할 수 있다</p>
<pre><code class="language-rust">&quot;99999999999999999999&quot;.parse::&lt;u64&gt;() // overflow error</code></pre>
<p>Use <code>.unwrap()</code> or <code>.expect()</code> for Impossible Errors</p>
<p>불가능한 오류에 대해 <code>.unwrap()</code>이나 <code>.expect()</code> 사용하기</p>
<pre><code class="language-rust">fn print_file_age(filename: &amp;Path, last_modified: SystemTime) {
    let age = last_modified.elapsed().expect(&quot;system clock drift&quot;);
}</code></pre>
<p>Error Handling with GenericError</p>
<p><code>GenericError</code>를 사용한 오류 처리</p>
<p>The downside of the GenericError approach is that the return type no longer communicates precisely what kinds of errors the caller can expect. The caller must be ready for anything.</p>
<ol>
<li><strong>Use .unwrap() and .expect() When Sure</strong>:<ul>
<li>If you are certain that a Result can only be Ok, use .unwrap() to get the value or .expect(message) to provide a custom panic message.</li>
<li>Result가 반드시 Ok일 것이라고 확신한다면, <code>.unwrap()</code>을 사용하여 값을 얻거나 <code>.expect(message)</code>를 사용하여 사용자 지정 패닉 메시지를 제공하세요.</li>
</ul>
</li>
<li><strong>Drawbacks of GenericError</strong>:<ul>
<li>Using GenericError does not convey specific error types, requiring the caller to handle a wide range of potential errors.</li>
<li>GenericError를 사용하면 특정 오류 유형을 전달하지 않으므로, <strong>호출부에서 다양한 잠재적 오류를 처리해야 합니다.</strong></li>
</ul>
</li>
<li><strong>When to Use .unwrap() or .expect()</strong>:<ul>
<li>Use these methods when dealing with impossible errors or in scenarios where failing indicates a severe issue, and panic is appropriate.</li>
<li>불가능한 오류를 처리하거나 실패가 심각한 문제를 나타내는 경우, 패닉이 적절한 상황에서는 이러한 <code>메서드</code>를 사용하세요.</li>
</ul>
</li>
<li><strong>Handle Overflows and Unexpected Input</strong>:<ul>
<li>Even when confident, always consider edge cases like overflows or unexpected input, as these can lead to bugs if not properly handled.</li>
<li>확실할 때에도 오버플로우나 예기치 않은 입력과 같은 엣지 케이스를 항상 고려하세요. 이를 제대로 처리하지 않으면 버그로 이어질 수 있습니다.</li>
</ul>
</li>
</ol>
<p>By understanding and appropriately using these techniques, you can handle errors efficiently in Rust, maintaining both code simplicity and robustness.
이러한 기술들을 이해하고 적절히 사용함으로써, Rust에서 오류를 효율적으로 처리하고, 코드의 간결성과 견고함을 유지할 수 있습니다.</p>
<p>GenericError 방식의 단점은 반환 타입이 이 이상 발생할 수 있는 오류의 종류를 콕 찍어 알려 주지 않는다는 것이다. 호출부는 만반의 준비가 되어 있어야 한다.</p>
<h2 id="11--오류-무시하기ignoring-error">11.  오류 무시하기(Ignoring Error)</h2>
<p>Sometimes we just want to ignore an error altogether.</p>
<p>가끔은 오류를 완전히 무시하고 싶을 때도 있다</p>
<pre><code class="language-rust">writeln!(stderr(), &quot;error: {}&quot;, err); // 경고: 사용하지 않은 결과</code></pre>
<p>The idiom <code>let _ = ...</code> is used to silence this warning.</p>
<p>이럴 때는 <code>let _ = ...</code> 관용구를 쓰면 경고를 잠재울 수 있다.</p>
<pre><code class="language-rust">let _ = writeln!(stderr(), &quot;error: {}&quot;, err); // OK. 결과를 무시한다.</code></pre>
<h2 id="12--main에서-오류-처리하기handling-errors-in-main">12.  main()에서 오류 처리하기(Handling Errors in main())</h2>
<p>However, you can also change the type signature so you can use ?:</p>
<p>오류 전파 단계가 너무 길어지면 결국 main()까지 오게 되므로 뭔가 조치를 취해야 한다. 보통 main()은 반환 타입이 Result가 아니라서 <code>?</code>를 쓸 수 없다.</p>
<pre><code class="language-rust">fn main() {
    calculate_tides()?; // 오류: 더 이상 책임을 전가할 수 없다.
}</code></pre>
<p>The simplest way to handle errors in <code>main()</code> is to use <code>.expect()</code>.</p>
<p>main()에서 오류를 처리하는 가장 간단한 방법은 <code>.expect()</code>를 쓰는 것이다.</p>
<pre><code class="language-rust">calculate_tides().expect(&quot;error&quot;); // 여기서 최종 책임을 진다.</code></pre>
<p>The error message is a little intimidating, though:</p>
<p>단, 오류 메시지가 다소 난감하다</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/37c39580-d38d-4aa9-9eb4-b601e00ba6f3/image.png" /></p>
<p>However, you can also change the type signature of main() to return a Result type,
so you can use ?:</p>
<p>하지만 main()의 타입 시그니처를 바꿔서 <strong>Result 타입을 반환하게 만들면</strong> <code>?</code>를 쓸 수 있다.</p>
<pre><code class="language-rust">fn main()&gt; Result&lt;(), TideCalcError&gt;{
        let tides = calculate_tides();
        print_tides(tides);
        ok(())
    }</code></pre>
<p>This works for any error type that can be printed with the {:?} formatter, which all
standard error types, like std::io:: Error, can be. This technique is easy to use and
gives a somewhat nicer error message, but it's not ideal</p>
<p>이 기법은 <code>{:?} 형식 지정자</code>로 출력할 수 있는 <strong>모든 오류 타입에 대해 작동</strong>한다. <code>std::io::Error</code>와 같은 표준 <strong>오류 타입이 전부 여기에 해당</strong>한다. 사용법이 간단하고 오류 메시지가 단순하다는 장점이 있지만, <strong>그렇다고 완벽한 해결책이라고 할 수는 없다.</strong></p>
<p>If have more complex error types or want to include more details in your message, it pays to print the error message yourself:</p>
<p>다루어야 할 오류 타입이 복잡하거나 오류 메시지에 추가 정보를 넣고 싶을 때는 <strong>차라리 직접 오류 메시지를 출력하는 게 더 낫다</strong></p>
<h2 id="13-declaring-a-custom-error-type사용자-정의-오류-타입-선언하기">13. Declaring a Custom Error Type(사용자 정의 오류 타입 선언하기)</h2>
<p>As with many aspects of the Rust language, crates exist to make error handling much
easier and more concise. There is quite a variety, but one of the most used is
thiserror, which does all of the previous work for you, allowing you to write errors
like this:</p>
<p>러스트 언어의 많은 측면이 그렇듯 오류 처리도 외부 크레이트의 도움을 받으면 일이 훨씬 더 쉽고 간단해진다. </p>
<h2 id="14-왜-result일까">14. 왜 Result일까?</h2>
<p>Rust requires the programmer to make some sort of decision, and record it in the
code, at every point where an error could occur. This is good because otherwise
it's easy to get error handling wrong through neglect.</p>
<ul>
<li>러스트는 오류가 발생할 수 있는 모든위치에서 프로그래머가 모종의 결정을 내린 뒤 그것을 코드에 기록할 것을 요구한다. 이렇게 하면 오<strong>류가 방치되어 잘못 처리되는 일이 줄기 때문에 좋다.</strong></li>
</ul>
<p>The most common decision is to allow errors to propagate, and that's written
with a single character, ?. Thus, error plumbing does not clutter up your codethe
way it does in C and Go. Yet it's still visible: you can look at a chunk of code and
see at a glance all places where errors are propagated</p>
<ul>
<li>가장 일반적인 결정은 <strong>오류가 전파</strong>되도록 만드는 것인데, 여기에 필요한 코드는 <code>?</code> 한 문자뿐이다. 따라서 C와 고처럼 오류 배관작업으로 인해 코드가 어수선해지는 일이 없다. 게다다 가독성이 좋아서 코드를 조금를 봐도 오류가 전파되는 모든 것을 한눈에 파악할 수 있다.</li>
</ul>
<p>Since the possibility of errors is part of every function's return type, it's clear
which functions can fail and which can't. If you change a function to be fallible,
you're changing its return type, so the compiler will make you update that function's downstream users.</p>
<ul>
<li>오류의 가능성이 <strong>모든 함수의 반환 타입에 명시</strong>되기 때문에 실패할 수 없는 함수와 실패할 수 없는 함수를 명확히 구분할 수 있다. 실패할 수 없는 함수를 실패할 수 있는 함수로 바꾸는 일은 곧 <code>반환 타입</code>을 바꾸는 일이므로, 컴파일러가 함수의 사용처를 모두 업데이트할 수 있도록 도와 줄 것이다</li>
</ul>
<p>Rust checks that Result values are used, so you can't accidentally let an error pass
silently (a common mistake in C)</p>
<ul>
<li>러스트는 Result 값의 사용 여부를 확인하기 때문에 <strong>실수로 오류를 무시하고 넘어가는 일이 생길 수 없다</strong>(C에서는 흔히 있는 실수다).</li>
</ul>
<p>Since Result is a data type like any other, it's easy to store success and error
results in the same collection. This makes it easy to model partial success. For
example, ifyou're writing a program that loads millions of records from a textfile
and you need a way to cope with the likely outcome that most will succeed, but
some will fail, you can represent that situation in memory using a vector of
Results</p>
<ul>
<li>Result는 평범한 데이터 타입이므로 성공 결과와 오류 결과를 같은 <code>컬렉션 안</code>에 담을 수 있는데, 이렇게 하면 부분적인 성공을 쉽게 모델링할 수 있다. 예를 들어, 텍스트 파일에서 수백만 개의 레코드를 읽어오는 프로그램을 작성 중이라고 하자. 이때 대부분은 성공하겠지만 간혹 실패할 수도 있는 상황에 대비할 방법이 필요하다면 Result 벡터로 해당 상황을 메모리에 표현할 수 있다.</li>
</ul>