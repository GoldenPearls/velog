<h1 id="chater-12-연산자-오버로딩">Chater 12. 연산자 오버로딩</h1>
<h1 id="01-도입">01. 도입</h1>
<p>2장에서 살펴본 망델브로 집합 플로터에서는 복수평명 위의 수를 표현하기 위해 num 트레이트의 Complex 타입을 사용한 예시가 아래와 같음 </p>
<pre><code class="language-rust">#[derive(Clone, Copy, Debug)]
struct Complex&lt;T&gt; {
    /// 복소수의 실수 부분
    re: T,
    /// 복소수의 허수 부분
    im: T,
}</code></pre>
<p>보통 복소수의 형태는  a+bi 형식으로 나타낼 수 있으며, 여기서 a는 실수 부분이고 b는 허수 부분이다.  <code>T</code>는 제네릭 타입으로, 실수 부분과 허수 부분이 다양한 수치 타입을 가질 수 있도록 한다.</p>
<p>예를 들어, 복소수 <strong>3+4</strong>i를 표현하기 위해 <code>Complex</code> 구조체를 사용할 수 있다.</p>
<pre><code class="language-rust">let z = Complex { re: 3, im: 4 };</code></pre>
<p><code>Complex</code> 수는 기본 제공 수치 타입처럼 <strong>러스트의 +와 연산자로 더하고 곱할 수 있었다.</strong></p>
<h2 id="1-연산자-오버로딩operator-overloading이란">1. 연산자 오버로딩(operator overloading)이란?</h2>
<blockquote>
<p><strong>연산자 오버로딩</strong> : 사용자 정의 타입도 산술 연산자를 비롯한 여러 연산자를 지원 하는데 몇 가지 기본 트레이트를 구현하기만 되는 것을 말함</p>
</blockquote>
<p>참고로 C++, C#, 파이썬, 루비의 연산자 오버로딩과 효과가 매우 비슷하다는 것으로 연산자 오버로딩을 위한 트레이트는 <strong>언어의 어떤 부분을 지원하는지</strong>에 따라 몇 가지 <code>범주</code>로 나뉜다.</p>
<blockquote>
<p>이번 장의 목표는 이 장의 목표는 사용자 정의 타입을 언어에 잘 통합할 수 있도록 돕고, 이러한 연산자를 사용하는 타입에 가장 자연스럽게 작용하는 <code>제네릭 함수</code>를 작성하는 방법에 대해 이해를 돕는 것이다.</p>
</blockquote>
<h2 id="2-연산자-오버로딩을-위한-트레이트">2. 연산자 오버로딩을 위한 트레이트</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/bce18ffc-0f8a-4822-aaf8-b73d0d250b09/image.png" /></p>
<p>위의 표에 대한것들을 하나 하나 각자의 파트별로 조사해볼 예정!! </p>
<h1 id="02-산술-연산자와-비트별-연산자">02. 산술 연산자와 비트별 연산자</h1>
<blockquote>
<p>트레이트 <code>Add&lt;T&gt;</code> T 값을 자기 자신에게 더하는 능력</p>
</blockquote>
<h2 id="1-add의-표현식">1. add의 표현식</h2>
<h3 id="1-stdops--add">1) std::ops :: Add</h3>
<p>러스트 표현식 <strong>a + b</strong> 는 a.add(b)로, 표준 라이브러리의 트레이트 <code>std::ops::Add</code>가 가진 메서드 add에 대한 호출 축약 표시이다. 표현식 a + b가 <strong>Complex 값에도 통하는 이유</strong>는 num 크레이트가 Complex에 이 트레이트를 구현해 두었기 때문이다. </p>
<p>다른 연산자의 경우에도 비슷하다. 예시로 a* b는 트레이트 <code>std::ops: Mul</code>이 가진 메서드 a.mul(b)의 축약 표기이고, std::ops :: Neg는 앞에 붙는 부호 부정 연산자를 담당한다.</p>
<p>Rust에서 연산자 오버로딩을 사용하는 방법을 설명하는 예시 코드</p>
<pre><code class="language-rust">use std::ops::Add;
assert_eq!(4.125f32.add(5.75), 9.875);
assert_eq!(10.add(20), 30);</code></pre>
<p>여기서 <code>Add</code> 트레이트를 사용하여 <code>add</code> 메서드를 호출해 숫자를 더하는 예이다. <code>4.125f32.add(5.75)</code>는 <strong>4.125 + 5.75</strong>와 같은 결과를 가진다.</p>
<h3 id="2-stdopsadd-트레이트-정의">2) <code>std::ops::Add</code> 트레이트 정의</h3>
<pre><code class="language-rust">trait Add&lt;Rhs=Self&gt; {
    type Output;
    fn add(self, rhs: Rhs) -&gt; Self::Output;
}</code></pre>
<p>이 트레이트는 <code>Rhs</code>라는 타입 매개변수를 가지며 기본값은 <code>Self</code>이다. </p>
<ul>
<li><code>Output</code>은 덧셈의 결과 타입</li>
<li>이를 구현하면 <code>+</code> 연산자를 사용할 수 있게 된다.</li>
<li><code>add</code> 메서드는 <strong>self와 rhs</strong>라는 두 개의 매개변수를 가진다.<ul>
<li><code>self</code>는 메서드를 호출하는 값을 나타내며, <code>rhs</code>는 오른쪽 피연산자</li>
<li>이 메서드는 두 값을 더한 결과를 반환하며, 반환 타입은 <strong>Self::Output</strong></li>
<li>즉,  <code>add</code> 메서드는 <code>self</code>와 <code>rhs</code>를 더한 결과를 반환</li>
</ul>
</li>
</ul>
<h3 id="3-복소수-타입-complex의-add-트레이트-구현">3) 복소수 타입 Complex의 Add 트레이트 구현</h3>
<p>복소수 타입인 <strong>Complex</strong>에 대해 <strong>Add</strong> 트레이트를 구현한 예로 <code>Complex&lt;i32&gt;</code> 타입의 값을 더하기 위해 <code>Add&lt;Complex&lt;i32&gt;&gt;</code> 트레이트를 구현해야 한다. </p>
<pre><code class="language-rust">use std::ops::Add;

impl Add for Complex&lt;i32&gt; {
    type Output = Complex&lt;i32&gt;;

    fn add(self, rhs: Self) -&gt; Self::Output {
        Complex {
            re: self.re + rhs.re,
            im: self.im + rhs.im,
        }
    }
}
</code></pre>
<p>같은 타입(self와 rhs가 Complex로 같은 타임)을 더하는 것이므로 그냥 <code>Add</code>라고만 사용하면 된다.</p>
<h3 id="4-다양한-complex-타입에-대해-제네릭으로-add-트레이트-구현">4) 다양한 <code>Complex</code> 타입에 대해 제네릭으로 Add 트레이트 구현</h3>
<p>각각의 <strong>Complex, Complex, Complex</strong> 타입에 대해 <strong>Add 트레이트</strong>를 개별적으로 구현할 필요가 없다. 대신 <code>제네릭</code>을 사용하여 한 번에 모든 타입을 아우를 수 있다.</p>
<p><strong>여러 타입</strong>에 대해 일반적으로 사용할 수 있도록 제네릭을 사용하는 예</p>
<pre><code class="language-rust">use std::ops::Add;

impl&lt;T&gt; Add for Complex&lt;T&gt;
where
    T: Add&lt;Output = T&gt;,
{
    type Output = Self;

    fn add(self, rhs: Self) -&gt; Self {
        Complex {
            re: self.re + rhs.re,
            im: self.im + rhs.im,
        }
    }
}
</code></pre>
<p>여기서 <strong>where T: Add&lt;Output=T&gt;</strong>는 타입 <code>T</code>가 덧셈이 가능하며 그 결과로 또 다른 <code>T</code> 타입을 반환한다는 것을 나타낸다. 이는 합리적인 제한이지만, 더 일반적인 제네릭 구현을 위해 조금 더 느슨하게 가져갈 수 있다.</p>
<h3 id="5-더욱-일반적인-제네릭-구현">5) 더욱 일반적인 제네릭 구현</h3>
<p>왼쪽과 오른쪽 피연산자가 서로 다른 타입일 수 있도록 한 더 일반적인 제네릭 구현 예</p>
<pre><code class="language-rust">use std::ops::Add;

impl&lt;L, R&gt; Add&lt;Complex&lt;R&gt;&gt; for Complex&lt;L&gt;
where
    L: Add&lt;R&gt;,
{
    type Output = Complex&lt;L::Output&gt;;

    fn add(self, rhs: Complex&lt;R&gt;) -&gt; Self::Output {
        Complex {
            re: self.re + rhs.re,
            im: self.im + rhs.im,
        }
    }
}
</code></pre>
<h3 id="6-실제로-rust에서의-제약">6) 실제로 Rust에서의 제약</h3>
<p>Rust는 다양한 타입이 섞여 있는 연산을 지원하지 않으려는 경향이 있다. 앞의 제네릭 구현에서 <code>L</code>과 <code>R</code>이 다를 수 있지만, 실제로는 대부분 같은 타입이 된다. </p>
<p>다른 조합을 구현하고 있는 타입 중에는 <code>L</code>로 사용할 수 있는 것이 많지 않기 때문에, 이러한 일반적인 제네릭 구현이 간단한 제네릭 정의보다 크게 유용하지 않을 수 있다.</p>
<h3 id="7-결론">7) 결론</h3>
<p>Rust에서는 다양한 타입에 대해 연산자 오버로딩을 지원하여 사용자 정의 타입이 기본 제공 타입처럼 동작하도록 할 수 있다. 이를 통해 더 자연스럽고 읽기 쉬운 코드를 작성할 수 있으며, 제네릭을 사용하여 코드의 재사용성을 높일 수 있다.</p>
<ul>
<li><code>Add</code> 트레이트를 구현하면 사용자 정의 타입에서도 <code>+</code> 연산자를 사용할 수 있다.</li>
<li><code>Complex</code> 타입에 대해 여러 타입을 지원하도록 제네릭으로 <code>Add</code> 트레이트를 구현할 수 있다.</li>
<li>Rust는 여러 타입을 섞어서 연산하는 것을 지원하는 데 제약이 있기 때문에, 이러한 제네릭 구현이 항상 유용하지 않을 수 있다.</li>
</ul>
<h2 id="2-단항-연산자">2. 단항 연산자</h2>
<h3 id="1-단항-연산자를-위한-기본-제공-트레이트">1) 단항 연산자를 위한 기본 제공 트레이트</h3>
<table>
<thead>
<tr>
<th>트레이트 이름</th>
<th>표현식</th>
<th>동등한 표현식</th>
</tr>
</thead>
<tbody><tr>
<td>std::ops::Neg</td>
<td>-x</td>
<td>x.neg()</td>
</tr>
<tr>
<td>std::ops::Not</td>
<td>!x</td>
<td>x.not()</td>
</tr>
</tbody></table>
<p><strong>러스트의 부호 있는 수치 타입</strong>은 모두 단항 부호 부정 연산자 -를 위해서 <code>std::ops ::Neg</code>를 구현하
고 있고, <strong>정수 타입과 bool은 단항 보수 연산자</strong>를 위해서 <code>std::ops :: Not</code>을 구현하고 있다.</p>
<p><code>!</code>를 <strong>bool 값</strong>에 쓰면 값이 반대가 되지만, <strong>정수</strong>에 쓰면 비트별 반전(즉, 비트 뒤집기)이 일어난다. </p>
<h3 id="2-트레이트-정의">2) 트레이트 정의</h3>
<pre><code class="language-rust">trait Neg {
    type Output;
    fn neg(self) -&gt; Self::Output;
}
trait Not {
    type Output;
    fn not(self) → Self::Output;
}</code></pre>
<ul>
<li><strong>Neg 트레이트</strong>:<ul>
<li><code>type Output;</code>: neg 메서드의 결과 타입을 정의합</li>
<li><code>fn neg(self) -&gt; Self::Output;</code>: self의 부호를 부정한 결과를 반환</li>
</ul>
</li>
<li><strong>Not 트레이트</strong>:<ul>
<li><code>type Output</code>;: not 메서드의 결과 타입을 정의합니다.</li>
<li><code>fn not(self) -&gt; Self::Output</code>;: self의 논리 부정을 반환합니다.</li>
</ul>
</li>
</ul>
<h3 id="3-복소수의-부호-부정-구현">3) 복소수의 부호 부정 구현</h3>
<blockquote>
<p>복소수의 부호 부정은 <strong>실수 부분과 허수 부분 각각의 부호를 부정하는 방식</strong>으로 구현된다. 이를 제네릭하게 구현하여 다양한 타입의 복소수를 지원할 수 있다.</p>
</blockquote>
<pre><code class="language-rust">use std::ops::Neg;

impl&lt;T&gt; Neg for Complex&lt;T&gt;
where
    T: Neg&lt;Output = T&gt;,
{
    type Output = Complex&lt;T&gt;;

    fn neg(self) -&gt; Complex&lt;T&gt; {
        Complex {
            re: -self.re,
            im: -self.im,
        }
    }
}</code></pre>
<h3 id="4-결론">4) 결론</h3>
<ul>
<li>Rust에서 연산자 오버로딩을 위해 <code>Neg</code>와 <code>Not</code> 트레이트를 사용한다.</li>
<li><code>Neg</code> 트레이트는 부호 부정(<code>-</code>), <code>Not</code> 트레이트는 논리 부정(<code>!</code>) 연산자를 정의한다.</li>
<li>복소수(<code>Complex&lt;T&gt;</code>) 타입에 대해 <code>Neg</code> 트레이트를 제네릭하게 구현하여, 실수 부분과 허수 부분 각각의 부호를 부정할 수 있다.</li>
<li>이러한 구현을 통해 <code>Complex</code> 타입이 기본 제공 수치 타입처럼 부호 부정 연산을 지원하도록 할 수 있다.</li>
</ul>
<h2 id="3-이항-연산자">3. 이항 연산자</h2>
<h3 id="1-이항-연산자를-위한-기본-제공-트레이트--산술-연산자">1) 이항 연산자를 위한 기본 제공 트레이트 : 산술 연산자</h3>
<table>
<thead>
<tr>
<th>범주</th>
<th>트레이트 이름</th>
<th>표현식</th>
<th>동등한 표현식</th>
</tr>
</thead>
<tbody><tr>
<td>산술 연산자</td>
<td>std::ops::Add</td>
<td>x + y</td>
<td>x.add(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::Sub</td>
<td>x - y</td>
<td>x.sub(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::Mul</td>
<td>x * y</td>
<td>x.mul(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::Div</td>
<td>x / y</td>
<td>x.div(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::Rem</td>
<td>x % y</td>
<td>x.rem(y)</td>
</tr>
</tbody></table>
<h3 id="2-이항-연산자를-위한-기본-제공-트레이트--비트별-연산자">2) 이항 연산자를 위한 기본 제공 트레이트 : 비트별 연산자</h3>
<table>
<thead>
<tr>
<th>범주</th>
<th>트레이트 이름</th>
<th>표현식</th>
<th>동등한 표현식</th>
</tr>
</thead>
<tbody><tr>
<td>비트별 연산자</td>
<td>std::ops::BitAnd</td>
<td>x &amp; y</td>
<td>x.bitand(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::BitOr</td>
<td>`x</td>
<td>y`</td>
</tr>
<tr>
<td></td>
<td>std::ops::BitXor</td>
<td>x ^ y</td>
<td>x.bitxor(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::Shl</td>
<td>x &lt;&lt; y</td>
<td>x.shl(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::Shr</td>
<td>x &gt;&gt; y</td>
<td>x.shr(y)</td>
</tr>
</tbody></table>
<h3 id="3-기본-제공-트레이트의-일반적인-형태">3) 기본 제공 트레이트의 일반적인 형태</h3>
<p>이항 연산자를 지원하는 트레이트들은 모두 동일한 일반적인 형태를 갖는다. 예를 들어, <code>std::ops::BitXor</code> 트레이트의 정의</p>
<pre><code class="language-rust">trait BitXor&lt;Rhs = Self&gt; {
    type Output;
    fn bitxor(self, rhs: Rhs) -&gt; Self::Output;
}
</code></pre>
<ul>
<li><strong><code>Rhs</code></strong>: 오른쪽 피연산자의 타입을 나타내며, 기본값은 <code>Self</code>이다.</li>
<li><strong><code>Output</code></strong>: 연산의 결과 타입을 정의한다.</li>
<li><strong><code>bitxor</code> 메서드</strong>: <code>self</code>와 <code>rhs</code>를 받아서 <code>Self::Output</code> 타입의 결과를 반환한다.</li>
</ul>
<h3 id="4-rust의-수치-및-비트-연산자">4) Rust의 수치 및 비트 연산자</h3>
<ul>
<li>Rust의 수치 타입들은 모두 산술 연산자를 구현하고 있다.</li>
<li>정수 타입과 <code>bool</code>은 비트별 연산자를 구현하고 있다.</li>
<li>이러한 타입들의 레퍼런스를 한쪽 또는 양쪽 피연산자로 사용할 수 있게 하는 구현도 있다.</li>
</ul>
<h3 id="5-문자열-연결에-대한-특이-사항">5) 문자열 연결에 대한 특이 사항</h3>
<ul>
<li><code>+</code> 연산자를 사용하여 <code>String</code>을 <code>&amp;str</code> 슬라이스나 다른 <code>String</code>과 연결할 수 있다.</li>
<li>그러나 <code>&amp;str</code>을 <code>+</code>의 왼쪽 피연산자로 사용할 수 없게 러스트가 막고 있기에, 짧은 문자열을 왼쪽에 거듭 연결하는 방식으로 긴 문자열을 쓸 수 없다.</li>
<li>여러 문자열을 하나로 합칠 때는 <code>write!</code> 매크로를 사용하는 것이 더 효율적이다. 이는 17장의 '텍스트 추가와 삽입' 절에서 자세히 다룬다.</li>
</ul>
<h2 id="4-복합-배정-연산자">4. 복합 배정 연산자</h2>
<h3 id="1-복합-배정-연산자란">1) 복합 배정 연산자란?</h3>
<blockquote>
<p>복합 배정 표현식은 <code>x += y나 x&amp;= y</code>와 같은 것을 말하며, 두 피연산자를 가지고 덧셈이나 비트별 논리곱 같은 연산을 수행한 뒤 결과를 다시 <strong>왼쪽 피연산자에 저장</strong>한다.</p>
</blockquote>
<p> 러스트에서 복합 배정 표현식의 값은 저장된 값이 아니라 항상 <code>()</code>이다.</p>
<p>러스트는 접근법이 다르다. x += y는 그런 뜻이 아니라 <strong>메서드 호출 x.add_assign(y)</strong>의 <strong>축약 표기</strong>다. 여기서 <code>add_assign</code>은 std::ops :: AddAssign 트레이트가 가진 유일한 메서드다.</p>
<pre><code class="language-rust">trait AddAssign&lt;Rhs=Self&gt;{
    fn add_assign(&amp;mut self, rhs: Rhs);
}</code></pre>
<h3 id="2-복합-배정-연산자를-위한-기본-제공-트레이트">2) 복합 배정 연산자를 위한 기본 제공 트레이트</h3>
<table>
<thead>
<tr>
<th>범주</th>
<th>트레이트 이름</th>
<th>표현식</th>
<th>동등한 표현식</th>
</tr>
</thead>
<tbody><tr>
<td>산술 연산자</td>
<td>std::ops::AddAssign</td>
<td>x += y</td>
<td>x.add_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::SubAssign</td>
<td>x -= y</td>
<td>x.sub_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::MulAssign</td>
<td>x *= y</td>
<td>x.mul_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::DivAssign</td>
<td>x /= y</td>
<td>x.div_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::RemAssign</td>
<td>x %= y</td>
<td>x.rem_assign(y)</td>
</tr>
<tr>
<td>비트별 연산자</td>
<td>std::ops::BitAndAssign</td>
<td>x &amp;= y</td>
<td>x.bitand_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::BitOrAssign</td>
<td>`x</td>
<td>= y`</td>
</tr>
<tr>
<td></td>
<td>std::ops::BitXorAssign</td>
<td>x ^= y</td>
<td>x.bitxor_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::ShlAssign</td>
<td>x &lt;&lt;= y</td>
<td>x.shl_assign(y)</td>
</tr>
<tr>
<td></td>
<td>std::ops::ShrAssign</td>
<td>x &gt;&gt;= y</td>
<td>x.shr_assign(y)</td>
</tr>
</tbody></table>
<h3 id="3-rust의-수치-타입과-정수-타입">3) Rust의 수치 타입과 정수 타입</h3>
<ul>
<li>Rust의 수치 타입들은 모두 산술 복합 배정 연산자를 구현하고 있다.</li>
<li>정수 타입과 <code>bool</code> 타입은 비트별 복합 배정 연산자를 구현하고 있다.</li>
</ul>
<h3 id="4-complex-타입에-대한-addassign-트레이트-구현">4) <code>Complex</code> 타입에 대한 <code>AddAssign</code> 트레이트 구현</h3>
<pre><code class="language-rust">use std::ops::AddAssign;

impl&lt;T&gt; AddAssign for Complex&lt;T&gt;
where
    T: AddAssign&lt;T&gt;,
{
    fn add_assign(&amp;mut self, rhs: Complex&lt;T&gt;) {
        self.re += rhs.re;
        self.im += rhs.im;
    }
}
</code></pre>
<h3 id="설명">설명:</h3>
<ul>
<li>use std::ops::AddAssign; : 이 트레이트는 <code>+=</code> 연산자를 정의한다.</li>
<li>impl AddAssign for Complex where T: AddAssign<ul>
<li>제네릭 타입 T에 대해 <strong>Complex 타입의 AddAssign 트레이트</strong>를 구현한다.</li>
<li><code>where T: AddAssign&lt;T&gt;</code>는 타입 T가 AddAssign 트레이트를 구현해야 한다는 조건을 의미</li>
</ul>
</li>
<li>fn add_assign(&amp;mut self, rhs: Complex)<ul>
<li><code>add_assign</code> 메서드는 <strong>&amp;mut self와 rhs</strong>를 받아, <strong>Complex 값을 더한 결과를 self에 반영</strong>합니다.</li>
</ul>
</li>
<li>self.re += rhs.re; self.im += rhs.im;<ul>
<li><strong>self</strong>의 실수 부분(<strong>re</strong>)과 허수 부분(<strong>im</strong>)에 각각 <strong>rhs</strong>의 실수 부분과 허수 부분을 더한다.</li>
</ul>
</li>
</ul>
<h3 id="5-복합-배정-연산자-트레이트와-이항-연산자-트레이트의-관계">5) 복합 배정 연산자 트레이트와 이항 연산자 트레이트의 관계</h3>
<p>복합 배정 연산자를 위한 기본 제공 트레이트는 그에 상응하는 이항 연산자를 위한 트레이트와 완전히 별개이다.</p>
<ul>
<li>예를 들어, <code>std::ops::Add</code>를 구현한다고 해서 <code>std::ops::AddAssign</code>이 자동으로 구현되지는 않는다.</li>
<li>만약 특정 타입을 <code>+=</code> 연산자의 왼쪽 피연산자로 사용하고 싶다면, 해당 타입에 대해 직접 <code>AddAssign</code>을 구현해야 한다.</li>
</ul>
<h3 id="6-결론">6) 결론</h3>
<ul>
<li><code>Complex</code> 타입에 대해 제네릭으로 <strong>AddAssign 트레이트를 구현</strong>하여, 실수 부분과 허수 부분 각각에 대해 <code>+=</code> 연산을 지원할 수 있다.</li>
<li>복합 배정 연산자 트레이트는 이항 연산자 트레이트와는 별개로 구현되어야 하며, 필요에 따라 각각을 명시적으로 구현해야 한다.</li>
</ul>
<h1 id="03-동치비교">03. 동치비교</h1>
<blockquote>
<p>Rust에서 상등(<code>==</code>) 연산자와 같지 않음(<code>!=</code>) 연산자는 <code>std::cmp::PartialEq</code> 트레이트를 통해 정의된 <code>eq</code>와 <code>ne</code> 메서드를 호출하는 축약 표기</p>
</blockquote>
<pre><code class="language-rust">assert_eq!(x == y, x.eq(&amp;y));
assert_eq!(x != y, x.ne(&amp;y));</code></pre>
<h2 id="1-partialeq">1. PartialEq</h2>
<h3 id="1-stdcmppartialeq의-정의">1) std::cmp::PartialEq의 정의</h3>
<pre><code class="language-rust">trait PartialEq&lt;Rhs = Self&gt;
where
    Rhs: ?Sized,
{
    fn eq(&amp;self, other: &amp;Rhs) -&gt; bool;
    fn ne(&amp;self, other: &amp;Rhs) -&gt; bool {
        !self.eq(other)
    }
}</code></pre>
<ul>
<li><code>eq</code> 메서드는 두 값을 비교하여 같으면 <code>true</code>, 다르면 <code>false</code>를 반환</li>
<li><code>ne</code> 메서드는 기본적으로 eq 메서드를 반대로 사용하여 정의된다. 즉, <code>ne</code>는 <code>eq</code>의 결과를 부정</li>
<li>즉, ne 메서드는 기본 정의가 있기 때문에 PartialEq 트레이트를 구현할 때는 eq만 정의하면 된다.</li>
</ul>
<h3 id="2-partialeq-구현-예시--complex을-위한-완전한-구현">2) PartialEq 구현 예시 : Complex을 위한 완전한 구현</h3>
<p><code>Complex</code> 타입에 대한 <code>PartialEq</code> 트레이트를 구현하는 예시</p>
<pre><code class="language-rust">impl&lt;T: PartialEq&gt; PartialEq for Complex&lt;T&gt; {
    fn eq(&amp;self, other: &amp;Complex&lt;T&gt;) -&gt; bool {
        self.re == other.re &amp;&amp; self.im == other.im
    }
}</code></pre>
<ul>
<li>이 구현은 임의의 구성 요소 타입 <code>T</code>에 대해 상등 비교가 가능한 <code>Complex&lt;T&gt;</code>를 위한 비교를 정의한다.</li>
<li>실수 부분(<code>re</code>)과 허수 부분(<code>im</code>)을 각각 비교하여 두 <code>Complex</code> 값이 같은지 확인한다.</li>
</ul>
<h3 id="3-partialeq-구현의-자동-생성">3) PartialEq 구현의 자동 생성</h3>
<p>PartialEq의 구현은 왼쪽 피연산자의 각 필드를 그에 대응하는 오른쪽 피연산자의 필드와 비교하는 게 전부라서 자주 쓰이는 연산임에도 이기에 <code>PartialEq</code> 자동 생성이 있다.</p>
<blockquote>
<p>Rust는 요청이 있을 경우 <code>PartialEq</code>의 구현을 자동으로 생성해 준다. 다음과 같이 타입 정의에 <code>derive</code> 어트리뷰트를 추가하면 됨</p>
</blockquote>
<pre><code class="language-rust">#[derive(Clone, Copy, Debug, PartialEq)]
struct Complex&lt;T&gt; {
    re: T,
    im: T,
}</code></pre>
<ul>
<li>자동으로 생성되는 구현은 수작업으로 작성한 코드와 본질적으로 동일</li>
<li>모든 필드나 요소를 차례로 비교하여 상등성을 판단한다.</li>
</ul>
<h3 id="4-partialeq와-eq의-관계">4) PartialEq와 Eq의 관계</h3>
<ul>
<li><code>PartialEq</code>는 부분 동치 관계를 나타내며, 완전 동치 관계는 아니다.</li>
<li>완전 동치 관계를 나타내는 <strong>std::cmp::Eq</strong> 트레이트가 있으며, 이는 <code>PartialEq</code>의 확장의 의미</li>
</ul>
<pre><code class="language-rust">trait Eq: PartialEq&lt;Self&gt; {}</code></pre>
<ul>
<li><strong>Eq</strong>를 구현하는 타입은 <code>PartialEq</code>를 구현해야 하며, <strong>x == x가 항상 true</strong>여야 합니다.</li>
<li>대부분의 타입은 <strong>PartialEq와 Eq</strong>를 모두 <strong>구현</strong>합니다. f32와 f64는 예외입니다.</li>
</ul>
<h2 id="2-산술과-비트별-트레이트와-partialeq">2. 산술과 비트별 트레이트와 PartialEq</h2>
<h3 id="1-산술과-비트별-트레이트와-partialeq의-차이">1) 산술과 비트별 트레이트와 PartialEq의 차이</h3>
<ul>
<li><strong>산술 연산자와 비트 연산자</strong>:<ul>
<li>피연산자를 값으로 받는다.</li>
<li>예: x + y, x &amp; y</li>
</ul>
</li>
<li><strong><code>PartialEq</code> 트레이트</strong>:<ul>
<li>피연산자를 레퍼런스로 받습니다.</li>
<li>예: x == y, x != y</li>
<li>이는 <strong><code>String, Vec, HashMap</code></strong> 같은 비Copy 값을 비교할 때 <strong>이동이 발생하지 않음을 의미</strong></li>
<li>비교만 했을 뿐인데 값이 이동된다면 예상치 못한 동작이 발생할 수 있다.</li>
</ul>
</li>
</ul>
<h3 id="2-산술과-비트별-트레이트와-partialeq의-차이-예제-코드">2) 산술과 비트별 트레이트와 PartialEq의 차이 예제 코드</h3>
<pre><code class="language-rust">let s = &quot;d\x6fv\x65t\x61i\x6c&quot;.to_string();
let t = &quot;\x640\x76e\x74a\x69l&quot;.to_string();
assert!(s == t); // s와 t는 차용될 뿐이다.
// 따라서 여기서도 값을 계속 사용할 수 있다.
assert_eq!(format!(&quot;{} {}&quot;, s, t), &quot;dovetail dovetail&quot;);
</code></pre>
<ul>
<li>이 예제에서 s와 t는 PartialEq 트레이트를 사용하여 비교됩</li>
<li>s와 t는 <code>차용(borrow)</code>되었으므로 값이 이동하지 않는다.</li>
</ul>
<p><a href="https://www.notion.so/borrow-move-54d377c84016470a83243dbe57ad824b?pvs=21">차용(borrow)와 값의 이동(move)의 차이</a></p>
<ul>
<li>따라서 비교 후에도 s와 t를 계속 사용할 수 있다.</li>
</ul>
<h3 id="3-partialeq-트레이트의-rhs-타입-매개변수--rhs-타입-매개변수의-트레이트-바운드">3) PartialEq 트레이트의 Rhs 타입 매개변수 : Rhs 타입 매개변수의 트레이트 바운드</h3>
<pre><code class="language-rust">where
    Rhs: ?Sized</code></pre>
<ul>
<li><code>PartialEq</code> 트레이트의 정의</li>
</ul>
<pre><code class="language-rust">trait PartialEq&lt;Rhs = Self&gt;
where
    Rhs: ?Sized,
{
    fn eq(&amp;self, other: &amp;Rhs) -&gt; bool;
    fn ne(&amp;self, other: &amp;Rhs) -&gt; bool {
        !self.eq(other)
    }
}
</code></pre>
<ul>
<li><code>Rhs: ?Sized</code>:<ul>
<li>Rust는 보통 타입 매개변수가 균일 크기 타입이어야 한다고 요구한다.</li>
<li>그러나 <code>?Sized</code>를 사용하면 비균일 크기 타입을 지원할 수 있다.</li>
<li>이를 통해 요건이 완화되어 <strong>PartialEq나 PartialEq&lt;[T]&gt;</strong> 같은 트레이트를 작성할 수 있다.</li>
</ul>
</li>
</ul>
<h3 id="4-partialeq의-사용-예">4) PartialEq의 사용 예</h3>
<pre><code class="language-rust">assert!(&quot;ungula&quot; != &quot;ungulate&quot;);
assert!(&quot;ungula&quot;.ne(&quot;ungulate&quot;));</code></pre>
<ul>
<li><code>PartialEq</code> 트레이트를 사용하여 문자열 비교를 수행합니다.</li>
<li>eq와 ne 메서드는 &amp;Rhs 타입의 매개변수를 받으므로, &amp;str나 &amp;[T]와 비교해도 전혀 문제없다.</li>
<li>두 단언문은 동일한 의미를 가진다.</li>
</ul>
<p>여기서 Self Rhs는 모두 비균일 크기 타입인 str이므로 ne의 self와 rhs 매개변수는 모두 &amp;str값이 된다. 균일 크기 타입, 비균일 크기 타입. Sized 트레이트는 13장의 'Sized' 절에서 자세히 살펴본다.</p>
<h2 id="3-동치-관계와-부분-동치-관계">3. 동치 관계와 부분 동치 관계</h2>
<h3 id="1-동치-관계의-수학적-정의">1) 동치 관계의 수학적 정의</h3>
<p>동치 관계(equivalence relation)의 세 가지 요구 사항:</p>
<ol>
<li><strong>대칭성</strong>: <code>x == y</code>가 참이면 <code>y == x</code>도 참</li>
<li><strong>전이성</strong>: <code>x == y</code>이고 <code>y == z</code>이면 <code>x == z</code>여야 한다.</li>
</ol>
<ul>
<li>일련의 값이 주어졌을 때, 각 값이 옆에 있는 값과 같다면 각 값은 나머지 모든 값과 같다. 상등성은 전염성이 있다.</li>
</ul>
<ol>
<li><strong>반사성</strong>: <code>x == x</code>는 항상 참이어야 한다.</li>
</ol>
<h3 id="2-ieee-표준-부동소수점-값과-nan">2) IEEE 표준 부동소수점 값과 NaN</h3>
<ul>
<li>Rust의 <code>f32</code>와 <code>f64</code>는 IEEE 표준 부동소수점 값을 사용한다.</li>
<li>이 표준에 따르면 NaN(특별한 수가 아님) 값은 자기 자신을 포함한 어떤 값과도 같지 않다고 취급</li>
</ul>
<pre><code class="language-rust">assert!(f64::is_nan(0.0/0.0));
assert_eq!(0.0/0.0 == 0.0/0.0, false);
assert_eq!(0.0/0.0 != 0.0/0.0, true);
assert_eq!(0.0/0.0 &lt; 0.0/0.0, false);
assert_eq!(0.0/0.0 &gt; 0.0/0.0, false);
assert_eq!(0.0/0.0 &lt;= 0.0/0.0, false);
assert_eq!(0.0/0.0 &gt;= 0.0/0.0, false);
</code></pre>
<ul>
<li>NaN 값의 상등 및 순서 비교는 항상 거짓을 반환해야 한다.</li>
</ul>
<p>Rust에서 동치 관계를 만족시키기 위해 <code>PartialEq</code>와 <code>Eq</code> 트레이트가 사용된다. 그러나, 이들 트레이트는 각각 부분 동치 관계와 완전 동치 관계를 나타낸다.</p>
<h3 id="3-부분-동치-관계-partial-equivalence-relation">3) 부분 동치 관계 (Partial Equivalence Relation)</h3>
<ul>
<li>Rust의 <code>==</code> 연산자는 일반적으로 동치 관계의 세 가지 요구 사항 중 <strong>첫 번째와 두 번째</strong>를 만족한다.</li>
<li>첫 번째 요구 사항: <strong>대칭성</strong> - <code>x == y</code>가 참이면 <code>y == x</code>도 참이어야 한다.</li>
<li>두 번째 요구 사항: <strong>전이성</strong> - <code>x == y</code>이고 <code>y == z</code>이면 <code>x == z</code>여야 한다.</li>
<li>세 번째 요구 사항: <strong>반사성</strong> - <code>x == x</code>는 항상 참이어야 한다.</li>
</ul>
<p>그러나, IEEE 부동소수점 값(예: <code>f32</code>와 <code>f64</code>)에 대해서는 세 번째 요구 사항인 반사성을 만족하지 못한다. 예를 들어, NaN 값은 자기 자신과도 같지 않다고 취급된다.</p>
<pre><code class="language-rust">assert!(f64::is_nan(0.0/0.0));
assert_eq!(0.0/0.0 == 0.0/0.0, false);
assert_eq!(0.0/0.0 != 0.0/0.0, true);
</code></pre>
<ul>
<li>이러한 이유로 <code>PartialEq</code>는 부분 동치 관계를 나타낸다.</li>
<li><code>PartialEq</code> 트레이트는 두 값이 같은지 비교하기 위해 사용된다.</li>
</ul>
<pre><code class="language-rust">trait PartialEq&lt;Rhs = Self&gt;
where
    Rhs: ?Sized,
{
    fn eq(&amp;self, other: &amp;Rhs) -&gt; bool;
    fn ne(&amp;self, other: &amp;Rhs) -&gt; bool {
        !self.eq(other)
    }
}
</code></pre>
<ul>
<li><code>eq</code> 메서드는 두 값을 비교하여 같으면 <code>true</code>, 다르면 <code>false</code>를 반환한다.</li>
<li><code>ne</code> 메서드는 기본적으로 <code>eq</code> 메서드를 반대로 사용하여 정의된다.</li>
</ul>
<h3 id="4-완전-동치-관계-full-equivalence-relation">4) 완전 동치 관계 (Full Equivalence Relation)</h3>
<ul>
<li>완전 동치 관계는 세 가지 요구 사항을 모두 만족해야 한다.</li>
<li><code>Eq</code> 트레이트는 완전 동치 관계를 나타내며, <code>PartialEq</code>의 확장으로 정의된다.</li>
</ul>
<pre><code class="language-rust">trait Eq: PartialEq&lt;Self&gt; {}
</code></pre>
<ul>
<li>Eq를 구현하는 타입은 PartialEq도 구현해야 하며, <strong>x == x가 항상 true</strong>여야 한다.</li>
<li>대부분의 타입은 PartialEq와 Eq를 모두 구현한다. 예외적으로, <strong>f32와 f64는 PartialEq</strong>만 구현하고 <code>Eq</code>는 구현하지 않는다.</li>
</ul>
<h3 id="5-partialeq의-구현-예">5) PartialEq의 구현 예</h3>
<pre><code class="language-rust">impl&lt;T: PartialEq&gt; PartialEq for Complex&lt;T&gt; {
    fn eq(&amp;self, other: &amp;Complex&lt;T&gt;) -&gt; bool {
        self.re == other.re &amp;&amp; self.im == other.im
    }
}
</code></pre>
<ul>
<li>이 구현은 임의의 구성 요소 타입 <code>T</code>에 대해 상등 비교가 가능한 <code>Complex&lt;T&gt;</code>를 위한 비교를 한다고 함</li>
</ul>
<h3 id="5-eq의-구현-예">5) Eq의 구현 예</h3>
<pre><code class="language-rust">impl&lt;T: Eq&gt; Eq for Complex&lt;T&gt; {}</code></pre>
<ul>
<li><code>Complex</code> 타입에 대해 <code>Eq</code>를 구현하는 예입니다. 매우 간단하게 구현할 수 있다.</li>
</ul>
<h3 id="6-자동-생성">6) 자동 생성</h3>
<p>Rust는 <strong>PartialEq와 Eq</strong> 트레이트의 구현을 자동으로 생성할 수 있다.</p>
<pre><code class="language-rust">#[derive(Clone, Copy, Debug, Eq, PartialEq)]
struct Complex&lt;T&gt; {
    re: T,
    im: T,
}</code></pre>
<ul>
<li><code>derive</code> 어트리뷰트를 사용하면, 필드나 요소를 차례로 비교하는 방식으로 상등성을 판단하는 구현이 자동으로 생성된다.</li>
<li>이 경우, <code>Complex&lt;i32&gt;</code>는 i32가 Eq를 구현하므로 <strong>Eq를 구현하지만</strong>, <code>Complex&lt;f32&gt;</code>는 f32가 Eq를 구현하지 않으므로 <strong>PartialEq만 구현합니다.</strong></li>
</ul>
<h3 id="7-제네릭-코드와-동치-관계">7) 제네릭 코드와 동치 관계</h3>
<ul>
<li>타입 매개변수로 <code>PartialEq</code>만 받는 제네릭 코드를 작성할 때는 첫 번째와 두 번째 요구 조건이 지켜진다고 가정할 수 있다.</li>
<li>그러나 값이 그 자신과 항상 같을 거라고 가정해서는 안 된다.</li>
<li>만일 제네릭 코드가 완전 동치 관계를 필요로 한다면 <code>std::cmp::Eq</code> 트레이트를 바운드로 사용해야 한다.</li>
</ul>
<h3 id="8-결론">8) 결론</h3>
<ul>
<li>Rust의 <code>PartialEq</code> 트레이트는 부분 동치 관계를 나타내며, <code>Eq</code> 트레이트는 완전 동치 관계를 나타낸다.</li>
<li><code>PartialEq</code>를 구현하면 <code>==</code>와 <code>!=</code> 연산자를 사용할 수 있으며, <code>Eq</code>를 구현하면 완전 동치 관계를 보장할 수 있다.</li>
<li>Rust는 <code>PartialEq</code>와 <code>Eq</code>의 구현을 자동으로 생성할 수 있으며, 이를 통해 사용자 정의 타입에서도 상등 비교 연산을 지원할 수 있다.</li>
</ul>
<h1 id="04-순서비교">04. 순서비교</h1>
<p>Rust의 <code>PartialOrd</code> 트레이트는 값들 간의 부분적인 순서 비교를 가능하게 한다. 이 트레이트는 두 값이 비교 가능한 경우에만 순서 관계를 정의하며, 순서를 매길 수 없는 경우도 허용한다. </p>
<h2 id="1-순서-비교-연산자와-partialord-트레이트">1. 순서 비교 연산자와 PartialOrd 트레이트</h2>
<p>Rust에서 순서 비교 연산자 (<code>&lt;</code>, <code>&gt;</code>, <code>&lt;=</code>, <code>&gt;=</code>)는 <code>std::cmp::PartialOrd</code> 트레이트를 통해 구현된다. 이 트레이트는 상등 비교가 가능한 타입에 대해서만 순서 비교를 정의한다.</p>
<h3 id="1-partialord-트레이트-정의">1) PartialOrd 트레이트 정의</h3>
<pre><code class="language-rust">trait PartialOrd&lt;Rhs = Self&gt;: PartialEq&lt;Rhs&gt;
where
    Rhs: ?Sized,
{
    fn partial_cmp(&amp;self, other: &amp;Rhs) -&gt; Option&lt;Ordering&gt;;
    fn lt(&amp;self, other: &amp;Rhs) -&gt; bool {
        self.partial_cmp(other) == Some(Ordering::Less)
    }
    fn le(&amp;self, other: &amp;Rhs) -&gt; bool {
        matches!(self.partial_cmp(other), Some(Ordering::Less | Ordering::Equal))
    }
    fn gt(&amp;self, other: &amp;Rhs) -&gt; bool {
        self.partial_cmp(other) == Some(Ordering::Greater)
    }
    fn ge(&amp;self, other: &amp;Rhs) -&gt; bool {
        matches!(self.partial_cmp(other), Some(Ordering::Greater | Ordering::Equal))
    }
}
</code></pre>
<ul>
<li><strong>PartialOrd</strong>: 상등 비교가 가능한 타입(<code>PartialEq</code>)이어야 순서 비교도 가능함.</li>
<li><strong>partial_cmp</strong>: 두 값을 비교하여 <code>Option&lt;Ordering&gt;</code>을 반환. 순서를 매길 수 없으면 <code>None</code>을 반환.</li>
<li><strong>lt, le, gt, ge</strong>: <code>partial_cmp</code>를 사용하여 각각 <code>&lt;</code>, <code>&lt;=</code>, <code>&gt;</code>, <code>&gt;=</code> 연산자를 정의함.</li>
</ul>
<p>PartialOrd가 Partial Eq를 확장하고 있다. <strong>즉, 상등 비교가 가능한 타입이어야 순서 비교도 가능하다.</strong>
PartialOrd에서 직접 구현해야 하는 메서드는 partial_cmp뿐이다. partial_cmp가 Some(o)를 반환하면, o는 <strong>self와 other의 관계를 나타낸다.</strong></p>
<h3 id="2-ordering-enum">2) Ordering Enum</h3>
<pre><code class="language-rust">enum Ordering {
    Less,       // self &lt; other
    Equal,      // self == other
    Greater,    // self &gt; other
}</code></pre>
<h3 id="3-partialord-구현-예제-interval">3) PartialOrd 구현 예제: Interval</h3>
<p><code>Interval</code> 타입에 대해 <code>PartialOrd</code>를 구현하여 순서 비교를 가능하게 함.</p>
<pre><code class="language-rust">use std::cmp::{Ordering, PartialOrd};

#[derive(Debug, PartialEq)]
struct Interval&lt;T&gt; {
    lower: T, // 포함
    upper: T, // 미포함
}

impl&lt;T: PartialOrd&gt; PartialOrd for Interval&lt;T&gt; {
    fn partial_cmp(&amp;self, other: &amp;Interval&lt;T&gt;) -&gt; Option&lt;Ordering&gt; {
        if self == other {
            Some(Ordering::Equal)
        } else if self.lower &gt;= other.upper {
            Some(Ordering::Greater)
        } else if self.upper &lt;= other.lower {
            Some(Ordering::Less)
        } else {
            None
        }
    }
}
</code></pre>
<ul>
<li><strong>impl&lt;T: PartialOrd&gt; PartialOrd for Interval</strong>:<ul>
<li>PartialOrd 트레이트를 Interval 타입에 대해 구현.</li>
<li>T는 PartialOrd 트레이트를 구현해야 함.</li>
</ul>
</li>
<li><strong>fn partial_cmp(&amp;self, other: &amp;Interval) -&gt; Option</strong>:<ul>
<li>두 Interval 값을 비교하여 순서를 반환.</li>
<li>순서를 매길 수 없는 경우(self와 other가 겹칠 경우) None을 반환.</li>
</ul>
</li>
</ul>
<h3 id="4-partialord-예제-사용">4) PartialOrd 예제 사용</h3>
<pre><code class="language-rust">fn main() {
    let interval1 = Interval { lower: 10, upper: 20 };
    let interval2 = Interval { lower: 20, upper: 40 };
    let interval3 = Interval { lower: 7, upper: 8 };
    let interval4 = Interval { lower: 0, upper: 8 };
    let interval5 = Interval { lower: 7, upper: 1 };

    assert!(interval1 &lt; interval2);
    assert!(interval3 &gt; interval4);
    assert!(interval3 &lt;= interval5);

    let left = Interval { lower: 18, upper: 30 };
    let right = Interval { lower: 28, upper: 40 };

    assert!(!(left &lt; right));
    assert!(!(left &gt;= right));
}</code></pre>
<h3 id="5-순서-비교-연산자와-partialord-메서드">5) 순서 비교 연산자와 PartialOrd 메서드</h3>
<table>
<thead>
<tr>
<th>표현식</th>
<th>동등한 메서드 호출</th>
<th>기본 정의</th>
</tr>
</thead>
<tbody><tr>
<td>x &lt; y</td>
<td>x.lt(y)</td>
<td>x.partial_cmp(&amp;y) == Some(Ordering::Less)</td>
</tr>
<tr>
<td>x &gt; y</td>
<td>x.gt(y)</td>
<td>x.partial_cmp(&amp;y) == Some(Ordering::Greater)</td>
</tr>
<tr>
<td>x &lt;= y</td>
<td>x.le(y)</td>
<td>matches!(x.partial_cmp(&amp;y), Some(Ordering::Less</td>
</tr>
<tr>
<td>x &gt;= y</td>
<td>x.ge(y)</td>
<td>matches!(x.partial_cmp(&amp;y), Some(Ordering::Greater</td>
</tr>
</tbody></table>
<h3 id="6-완전한-순서-비교를-위한-ord-트레이트">6) 완전한 순서 비교를 위한 Ord 트레이트</h3>
<p>Rust에서 <code>PartialOrd</code> 트레이트 외에도 완전한 순서 비교를 제공하는 <code>Ord</code> 트레이트가 있다.</p>
<h3 id="7-ord-트레이트-정의">7) Ord 트레이트 정의</h3>
<pre><code class="language-rust">trait Ord: Eq + PartialOrd&lt;Self&gt; {
    fn cmp(&amp;self, other: &amp;Self) -&gt; Ordering;
}</code></pre>
<ul>
<li><strong>Ord</strong>: <code>PartialOrd</code>를 확장하며, <code>PartialOrd</code>와 <code>Eq</code> 트레이트를 구현해야 함.</li>
<li><strong>cmp</strong>: 두 값을 비교하여 항상 <code>Ordering</code>을 반환. 순서를 매길 수 없는 경우가 없음.</li>
</ul>
<pre><code class="language-rust">use std::cmp::Reverse;

fn main() {
    let mut intervals = vec![
        Interval { lower: 10, upper: 20 },
        Interval { lower: 5, upper: 15 },
        Interval { lower: 1, upper: 5 },
    ];

    intervals.sort_by_key(|i| i.upper);
    println!(&quot;{:?}&quot;, intervals);

    intervals.sort_by_key(|i| Reverse(i.lower));
    println!(&quot;{:?}&quot;, intervals);
}
</code></pre>
<h3 id="8-결론-1">8) 결론</h3>
<ul>
<li><code>PartialOrd</code> 트레이트는 부분적인 순서 비교를 가능하게 하며, 순서를 매길 수 없는 경우를 허용한다.</li>
<li><code>Ord</code> 트레이트는 완전한 순서 비교를 제공하며, 모든 값을 비교할 수 있다.</li>
<li><code>Interval</code> 타입에 대해 <code>PartialOrd</code>와 <code>Ord</code>를 적절히 구현하여 순서 비교와 정렬을 지원할 수 있다.</li>
</ul>
<h1 id="05-index와-indexmut">05. Index와 IndexMut</h1>
<blockquote>
<p>Rust에서는 <code>std::ops::Index</code>와 <code>std::ops::IndexMut</code> 트레이트를 구현하여 <code>a[i]</code> 같은 색인 표현식의 동작 방식을 정의할 수 있다. 배열은 <code>[]</code> 연산자를 직접 지원하지만, 다른 타입에 대해서는 색인 표현식을 사용할 때 <code>Index</code>와 <code>IndexMut</code> 트레이트를 통해 메서드를 호출한다.</p>
</blockquote>
<h2 id="1-index와-indexmut-트레이트-정의">1. Index와 IndexMut 트레이트 정의</h2>
<h3 id="1-index-트레이트">1) Index 트레이트</h3>
<pre><code class="language-rust">trait Index&lt;Idx&gt; {
    type Output: ?Sized;
    fn index(&amp;self, index: Idx) -&gt; &amp;Self::Output;
}
</code></pre>
<ul>
<li><strong>Index</strong>: 타입 <code>Idx</code>를 매개변수로 받아 색인 연산을 수행하는 트레이트</li>
<li><strong><code>t</code>ype Output</strong>: 색인 연산의 결과 타입을 나타낸다.</li>
<li><strong>fn index(&amp;self, index: Idx) -&gt; &amp;Self::Output</strong>: 주어진 인덱스에 대한 참조를 반환하는 메서드이다.</li>
</ul>
<h3 id="2-indexmut-트레이트">2) IndexMut 트레이트</h3>
<pre><code class="language-rust">trait IndexMut&lt;Idx&gt;: Index&lt;Idx&gt; {
    fn index_mut(&amp;mut self, index: Idx) -&gt; &amp;mut Self::Output;
}
</code></pre>
<ul>
<li><strong>IndexMut</strong>: <code>Index</code> 트레이트를 확장하여 변경 가능한 색인 연산을 지원한다.</li>
<li><strong>fn index_mut(&amp;mut self, index: Idx) -&gt; &amp;mut Self::Output</strong>: 주어진 인덱스에 대한 변경 가능한 참조를 반환하는 메서드이다.</li>
</ul>
<h2 id="2-예제-hashmap에서의-색인-사용">2. 예제: HashMap에서의 색인 사용</h2>
<pre><code class="language-rust">use std::collections::HashMap;

let mut m = HashMap::new();
m.insert(&quot;+&quot;, 10);
m.insert(&quot;百&quot;, 100);
m.insert(&quot;千&quot;, 1000);
m.insert(&quot;万&quot;, 10_000);
m.insert(&quot;亿&quot;, 1_0000_0000);

assert_eq!(m[&quot;+&quot;], 10);
assert_eq!(m[&quot;亿&quot;], 1_0000_0000);
</code></pre>
<ul>
<li><code>HashMap&lt;&amp;str, i32&gt;</code>는 <strong>Index&lt;&amp;str&gt;</strong>를 구현하므로, <strong>m[&quot;+&quot;]</strong>와 같은 표현식을 사용할 수 있다.</li>
<li>이 색인 표현식은 <code>m.index(&quot;+&quot;)</code>와 동등하다.</li>
</ul>
<h2 id="3-index와-indexmut의-구현-예제">3. Index와 IndexMut의 구현 예제</h2>
<pre><code class="language-rust">use std::ops::{Index, IndexMut};

struct Image&lt;P&gt; {
    width: usize,
    pixels: Vec&lt;P&gt;,
}

impl&lt;P: Default + Copy&gt; Image&lt;P&gt; {
    fn new(width: usize, height: usize) -&gt; Image&lt;P&gt; {
        Image {
            width,
            pixels: vec![P::default(); width * height],
        }
    }
}

impl&lt;P&gt; Index&lt;usize&gt; for Image&lt;P&gt; {
    type Output = [P];
    fn index(&amp;self, row: usize) -&gt; &amp;[P] {
        let start = row * self.width;
        &amp;self.pixels[start..start + self.width]
    }
}

impl&lt;P&gt; IndexMut&lt;usize&gt; for Image&lt;P&gt; {
    fn index_mut(&amp;mut self, row: usize) -&gt; &amp;mut [P] {
        let start = row * self.width;
        &amp;mut self.pixels[start..start + self.width]
    }
}
</code></pre>
<ul>
<li><strong>struct Image<p></strong>: Image 구조체는 제네릭 타입 P를 가지며, width와 pixels 필드를 포함한다.<ul>
<li>width: 이미지의 너비를 나타낸다.</li>
<li>pixels: 이미지의 픽셀 데이터를 저장하는 벡터이다.</li>
</ul>
</li>
<li><strong>impl&lt;P: Default + Copy&gt; Image<p></strong>: new 메서드는 주어진 크기로 새 이미지를 생성한다.</li>
<li><strong>impl<p> Index for Image<p></strong>:<ul>
<li>Index 트레이트를 구현하여 <strong>행(row) 색인을 지원</strong>한다.</li>
<li>index 메서드는 주어진 행의 <strong>픽셀 슬라이스를 반환</strong>한다.</li>
</ul>
</li>
<li><strong>impl<p> IndexMut for Image<p></strong>:<ul>
<li>IndexMut 트레이트를 구현하여 <strong>변경 가능한 행 색인을 지원</strong>한다.</li>
<li>index_mut 메서드는 주어진 행의 변경 가능한 <strong>픽셀 슬라이스를 반환</strong>한다.</li>
</ul>
</li>
</ul>
<h2 id="4-index와-indexmut의-사용-예">4. Index와 IndexMut의 사용 예</h2>
<pre><code class="language-rust">fn main() {
    let mut desserts = vec![&quot;Howalon&quot;.to_string(), &quot;Soan papdi&quot;.to_string()];
    desserts[0].push_str(&quot; (fictional)&quot;);
    desserts[1].push_str(&quot; (real)&quot;);

    println!(&quot;{:?}&quot;, desserts);

    use std::ops::IndexMut;
    (*desserts.index_mut(0)).push_str(&quot; (fictional)&quot;);
    (*desserts.index_mut(1)).push_str(&quot; (real)&quot;);

    println!(&quot;{:?}&quot;, desserts);
}
</code></pre>
<ul>
<li><strong>desserts</strong>: 문자열 벡터입니다.</li>
<li><strong>desserts[0].push_str(&quot; (fictional)&quot;);</strong>와 <strong>desserts[1].push_str(&quot; (real)&quot;);</strong><ul>
<li><code>push_str</code> 메서드는 <strong>&amp;mut self</strong>에 작용하므로, 이 표현식들은 <strong>IndexMut</strong> 트레이트의 <strong>index_mut</strong> 메서드를 사용하여 동등한 표현으로 변환된다.</li>
</ul>
</li>
</ul>
<h3 id="1-주의-사항">1) 주의 사항</h3>
<ul>
<li>색인 표현식이 배열, 슬라이스, 벡터 등의 범위 밖에 있는 요소에 접근하려 하면 패닉이 발생한다.</li>
<li><code>Image</code> 예제에서 <code>row</code>가 범위 밖에 있으면 <strong>.index()</strong> 메서드가 <strong>self.pixels</strong>의 범위 밖을 색인하게 되어 패닉이 발생할 수 있다.</li>
</ul>
<h3 id="2-결론">2) 결론</h3>
<ul>
<li><code>Index</code>와 <code>IndexMut</code> 트레이트를 구현하면 사용자 정의 타입에서도 배열처럼 <code>[]</code> 색인 연산을 사용할 수 있다.</li>
<li><strong>Index</strong>는 불변 참조를, <strong>IndexMut</strong>는 변경 가능한 참조를 반환한다.</li>
<li>Rust의 컬렉션 타입들은 이들 트레이트를 구현하여 색인 연산을 지원한다.</li>
<li>색인 연산 시 범위 밖의 요소에 접근하지 않도록 주의해야 한다.</li>
</ul>
<h1 id="06-기타연산자">06. 기타연산자</h1>
<p>Rust에서 모든 연산자를 오버로딩할 수 있는 것은 아니다. 특정 연산자는 현재 오버로딩할 수 없으며, 일부는 특정 타입에만 사용할 수 있다. </p>
<h2 id="1-오버로딩이-불가능한-연산자">1. 오버로딩이 불가능한 연산자</h2>
<h3 id="1-오류-검사-연산자-">1) 오류 검사 연산자 <code>?</code></h3>
<ul>
<li><strong>설명</strong>: <code>?</code> 연산자는 <code>Result</code>와 <code>Option</code> 값에만 사용할 수 있다.</li>
<li><strong>현황</strong>: 사용자 정의 타입으로의 확장 작업이 진행 중</li>
</ul>
<h3 id="2-논리-연산자-와-">2) 논리 연산자 <code>&amp;&amp;</code>와 <code>||</code></h3>
<ul>
<li><strong>설명</strong>: 이 논리 연산자는 불(<code>bool</code>) 값에만 사용할 수 있다.</li>
<li><strong>오버로딩 불가능</strong>: 현재는 불 값 외의 타입에 대해서는 오버로딩할 수 없다.</li>
</ul>
<h3 id="3-점-연산자-와-">3) 점 연산자 <code>.</code>와 <code>..</code></h3>
<ul>
<li><strong>설명</strong>: <code>.</code> 연산자는 항상 범위의 경계를 나타내는 구조체를 생성하며, <code>..</code> 연산자는 레퍼런스를 빌려오거나 값을 이동하거나 복사한다.</li>
<li><strong>오버로딩 불가능</strong>: 이 연산자들은 오버로딩할 수 없다.</li>
</ul>
<h2 id="2-특정-트레이트로-오버로딩-가능한-연산자">2. 특정 트레이트로 오버로딩 가능한 연산자</h2>
<h3 id="1-역참조-연산자">1) 역참조 연산자``</h3>
<ul>
<li><strong>설명</strong>: <code>val</code>처럼 사용하는 역참조 연산자는 오버로딩할 수 있다.</li>
<li><strong>사용 트레이트</strong>: <code>Deref</code>와 <code>DerefMut</code> 트레이트를 사용하여 오버로딩할 수 있다.</li>
</ul>
<h3 id="2-필드-접근-및-메서드-호출-연산자-">2) 필드 접근 및 메서드 호출 연산자 <code>.</code></h3>
<ul>
<li><strong>설명</strong>: <code>val.field</code>와 <code>val.method()</code>처럼 필드에 접근하고 메서드를 호출할 때 사용하는 점(<code>.</code>) 연산자는 오버로딩할 수 있다.</li>
<li><strong>사용 트레이트</strong>: <code>Deref</code>와 <code>DerefMut</code> 트레이트를 사용하여 오버로딩할 수 있다.</li>
</ul>
<h2 id="3-함수-호출-연산자-fx">3. 함수 호출 연산자 <code>f(x)</code></h2>
<ul>
<li><strong>설명</strong>: Rust는 함수 호출 연산자 <code>f(x)</code>의 오버로딩을 지원하지 않는다.</li>
<li><strong>대안</strong>: 호출 가능한 값을 필요로 할 때는 클로저를 작성하면 된다.</li>
<li><strong>특수 트레이트</strong>: 클로저의 동작 방식과 특수 트레이트 <code>Fn</code>, <code>FnMut</code>, <code>FnOnce</code>에 대해서는 14장에서 설명한다.</li>
</ul>
<h3 id="1-요약">1) 요약</h3>
<ul>
<li>Rust에서는 모든 연산자를 오버로딩할 수 있는 것은 아니다.</li>
<li><code>?</code> 연산자, 논리 연산자 <code>&amp;&amp;</code>와 <code>||</code>, 점(<code>.</code>) 연산자, 그리고 <code>&amp;</code> 연산자는 현재 오버로딩할 수 없다.</li>
<li>역참조 연산자 ``와 필드 접근 및 메서드 호출 연산자 <code>.</code>는 <code>Deref</code>와 <code>DerefMut</code> 트레이트를 사용하여 오버로딩할 수 있다.</li>
<li>함수 호출 연산자 <code>f(x)</code>는 오버로딩할 수 없지만, 클로저를 사용하여 대체할 수 있다.</li>
</ul>