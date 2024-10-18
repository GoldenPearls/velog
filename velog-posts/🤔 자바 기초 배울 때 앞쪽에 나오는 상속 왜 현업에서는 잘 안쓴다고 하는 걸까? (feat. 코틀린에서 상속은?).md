<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b6bfd705-d2a9-48c3-be6e-6f8367b0554e/image.jpg" /></p>
<p>이펙티브 자바 스터디를 9월부터 하고 있는 중인데 저번주 주제 중에 <strong>상속을 아무때나 사용하지 말고 주의해서 사용하라</strong>라는 주제가 나왔었다.. 근데 주의점이 너무 많아서 그러면 상속을 안쓰면 되는 거 아닌가요? 하는 말이 나왔었음 스터디원이 정리한 것 중에 아래와 같은 글도 있었다.</p>
<blockquote>
<p>💬 Java의 창시자인 제임스 고슬링(James Arthur Gosling)이 한 인터뷰에서 &quot;<strong>내가 자바를 만들면서 가장 후회하는 일은 상속을 만든 점이다</strong>&quot;라고 말했다.</p>
</blockquote>
<p>조슈야 블로크의 Effective Java에서는 상속을 위한 설계와 문서를 갖추거나, 그럴 수 없다면 상속을 금지하라는 조언을 한다.
따라서 <strong>추상화가 필요하면</strong> <code>인터페이스</code>로 implements 하거나 객체 지향 설계를 할땐 <code>합성(composition)</code>을 이용하는 것이 추세이다.</p>
<p>하지만 우리가 기초를 배울 때는 항상 상속을 많이 배우기도 하고 해서 궁금해졌다! 그리고 <code>코틀린</code>이 자바에서의 불편한 점을 거의 많이 개선한 프로그래밍 언어인데 이러한 점도 개선되었는지 알아보고자 함</p>
<blockquote>
<p>좀 더 딥하게 상속을 쓰게 되면, </p>
</blockquote>
<ul>
<li>무엇이 문제인지 </li>
<li>왜 문제인지 </li>
<li>그렇다면 정확히 언제 사용해야 하는 건지 알아보자..</li>
<li>이펙티브 자바와 함께 그리고 코틀린에서 상속이 없는가도 알아보자 </li>
</ul>
<p>회사 코드가 정답은 아니지만 회사 코드 또한 살펴보았다! 일단 상속이 무엇인지와 이펙티브 자바에서 대안을 알아보자</p>
<h1 id="1-상속inheritance">1. 상속(Inheritance)</h1>
<p>일반적인 구체 클래스를 패키지 경계를 넘어, 즉 다른 패키지의 구체 클래스를 상속하는 일은 위험하다. 상기하자면, 이 책에서의 ‘상속’은 클래스가 다른 클래스를 확장하는  <strong>구현 상속</strong>을 말한다. 이번 아이템 에서 논하는 문제는 클래스가 인터페이스를 구현하거나 인터페이스가 다른 인터페이스를 확장하는 <strong>인터 페이스 상속</strong>과는 무관하다.</p>
<h2 id="1--상속이란">1)  상속이란</h2>
<p><code>상속</code>은 객체 지향 4가지 특징중 하나로서 클래스 기반의 프로그래밍에서 배우는 개념이다.</p>
<p>클래스 상속을 통해 자식 클래스는 부모 클래스의 자원을 물려 받게 되며, 부모 클래스와 다른 부분만 추가하거나 재정의함으로써 <strong>기존 코드를 쉽게 확장할 수 있다.</strong>
그래서 상속 관계를 <code>is-a</code> 관계라도 표현하기도 한다.</p>
<p>is-a는 일종의 ~이다라는 의미이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7f36a7c2-ee3b-4848-9b07-972336865984/image.png" /></p>
<blockquote>
<p>출처 : <a href="https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_ISA_%EA%B4%80%EA%B3%84">https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_ISA_%EA%B4%80%EA%B3%84</a></p>
</blockquote>
<pre><code class="language-java">class Mobile {
    // ...
}

class Apple extends Mobile {
    // ...
}</code></pre>
<h3 id="🔎-서브-클래싱과-서브-타이핑">🔎 서브 클래싱과 서브 타이핑</h3>
<p>상속의 방법에 대해 객체지향의 사실과 오해에서 다음과 같이 설명한다고 함. </p>
<p>💬 상속은 서브타이핑(subtyping)과 서브클래싱(subclassing)의 두 가지 용도로 사용될 수 있다. </p>
<p>서브클래스가 슈퍼클래스를 대체할 수 있는 경우 이를 서브타이핑이라고 한다. 서브클래스가 슈퍼클래스를 대체할 수 없는 경우에는 서브클래싱이라고 한다. <code>서브타이핑</code>은 설계의 유연성이 목표인 반면 <code>서브클래싱</code>은 <strong>코드의 중복 제거와 재사용이 목적</strong>이다. </p>
<h3 id="엄밀히-말하면-상속은-그저-코드-재사용을-위한-기법이-아니다">엄밀히 말하면 상속은 그저 코드 재사용을 위한 기법이 아니다?</h3>
<p><strong>[상속을 통한 코드 재사용]</strong>
<code>코드의 재사용</code>이란 무엇일까? 애초에 우리가 함수(function)을 만들어 쓰는 이유가 공통적으로 사용되는 코드를 묶어 재사용을 통해 <strong>코드 중복을 줄이기 위해서이다</strong>. 객체 지향 프로그래밍에서 공통적으로 사용되는 코드가 있다면, 부모 클래스에 메소드 하나 만들어놓고 상속을 통해 부모의 것을 가져와 사용한다는 기법으로 코드의 재사용이라고 말하는 것이다.</p>
<p>다만, 엄밀히 말하면 상속은 그저 코드 재사용을 위한 기법이 아니라고 한다.</p>
<blockquote>
<p>일반적인 클래스가 이미 구현이 되어 있는 상태에서 그보다 좀 더 구체적인 클래스를 구현하기 위해 사용되는 기법이며, 그로 인해 상위 클래스의 코드를 하위 클래스가 재사용 할 수 있을 뿐이다.
 
이처럼 '사람' 이라는 객체 주제는 같지만, 중학생, 고등학생 처럼** 서로 다른 속성이나 기능들을 가지고 있을때<strong>, 이러한 구조를 **상속 관계를 통해 논리적으로 개념적으로 연관 시키는 것을 상속</strong>이라 한다.</p>
</blockquote>
<h3 id="클래스-폭발-🔥-문제">클래스 폭발 🔥 문제</h3>
<p>상속 관계는 <code>컴파일 타임</code>에 결정되고 고정되기 때문에 코드를 실행하는 도중에 변경할 수 없다.  따라서 여러 기능을 조합해야 하는 설계에 상속을 이용하게 된다면 모든 조합별로 클래스를 하나하나 추가해주어야 한다.
이것을 <code>클래스 폭발 문제</code>라 한다.</p>
<p>더군다나 Java8부터는 인터페이스의 디폴트 메소드 기능이 나오면서 *<em>인터페이스내에서 로직 구현이 가능하여 상속의 장점이 약화되었다고 할 수 있다. *</em></p>
<h2 id="2-상속의-다사다난-문제점">2) 상속의 다사다난 문제점</h2>
<p>자바의 객체 지향 프로그래밍을 처음 배울때 클래스와 상속에 대해 배우기 때문에, 마치 상속이 코드 중복을 제거하고 클래스를 묶는 <code>다형성</code>도 이용할 수 있고 단점보다는 장점을 강조하다 보니 무분별하게 사용하는 경우가 많다.</p>
<blockquote>
<p>하지만 현업, 이펙티브 자바 등에서 <code>extends</code>를 지양하는 편이며 <strong>클래스 상속을 해야할때는 정말 개념적으로 연관 관계가 있을 때만 하는 상당히 제한적으로 선택적으로 다뤄진다.</strong></p>
</blockquote>
<h3 id="🔑-문제점-1--불필요한-기능-상속">🔑 문제점 1 : 불필요한 기능 상속</h3>
<blockquote>
<p> 서브 클래싱이란 관점에서 본 상속의 문제점으로 <code>서브클래싱</code>이란 코드 재사용 목적의 상속 </p>
</blockquote>
<p>다음은 이미 안정적으로 구현된 <code>CircularBuffer</code> 클래스를 상속하여 <code>CircularQueue</code>와 <code>CircularStack</code>을 구현하고자 하는 예시이다. 이 코드에서 상속을 통해 코드를 재사용할 수 있다. </p>
<p>다음은 Stack과 Queue 클래스가 <code>List</code> 클래스를 상속받을 때 발생할 수 있는 리스코프 치환 원칙(Liskov Substitution Principle, LSP) 위반 문제를 다룬 예시를 정리한 내용입니다.</p>
<blockquote>
<p>List 클래스 정의</p>
</blockquote>
<p>우리는 <code>List</code> 클래스를 사용하여 데이터를 배열처럼 저장하고, 왼쪽이나 오른쪽에 값을 추가하거나 제거할 수 있는 메서드들을 제공한다.</p>
<pre><code class="language-java">public class List {
    private int[] elements;

    // 맨 처음에 요소 추가
    public void pushLeft(int value) {
        // 구현 생략
    }

    // 맨 끝에 요소 추가
    public void push(int value) {
        // 구현 생략
    }

    // 첫 번째 요소 제거 후 반환
    public int popLeft() {
        // 구현 생략
        return 0; // 임시 반환값
    }

    // 마지막 요소 제거 후 반환
    public int pop() {
        // 구현 생략
        return 0; // 임시 반환값
    }
}</code></pre>
<p>이 <code>List</code> 클래스는 이미 안정적으로 구현된 상태로, 이제 이 클래스를 상속받아 스택과 큐 자료구조를 구현하려고 한다.</p>
<blockquote>
<p>Stack과 Queue 클래스 상속</p>
</blockquote>
<p><code>Stack</code>과 <code>Queue</code> 클래스는 <code>List</code> 클래스를 상속받아 각각 스택과 큐 자료구조로 동작하도록 구현</p>
<pre><code class="language-java">public class Stack extends List {}

public class Queue extends List {}</code></pre>
<p>이렇게 하면 <code>Stack</code>과 <code>Queue</code>는 <code>List</code>의 모든 메서드를 상속받아 재사용할 수 있다.</p>
<h4 id="stack-사용-예시">Stack 사용 예시</h4>
<p>스택은 <strong>후입선출(FILO)</strong> 특성을 가져야 한다. 이를 위해 <code>push</code>와 <code>pop</code> 메서드만을 사용하면 된다.</p>
<pre><code class="language-java">Stack stack = new Stack();
stack.push(1);  // [1]
stack.push(2);  // [1, 2]
stack.push(3);  // [1, 2, 3]
stack.pop();    // [1, 2] =&gt; 3 반환
stack.push(4);  // [1, 2, 4]
stack.pop();    // [1, 2] =&gt; 4 반환</code></pre>
<h4 id="queue-사용-예시">Queue 사용 예시</h4>
<p>큐는 <strong>선입선출(FIFO)</strong> 특성을 가져야 한다. 이를 위해 <code>push</code>와 <code>popLeft</code> 메서드만을 사용하면 된다.</p>
<pre><code class="language-java">Queue queue = new Queue();
queue.push(1);    // [1]
queue.push(2);    // [1, 2]
queue.push(3);    // [1, 2, 3]
queue.popLeft();  // [2, 3] =&gt; 1 반환
queue.push(4);    // [2, 3, 4]
queue.popLeft();  // [3, 4] =&gt; 2 반환</code></pre>
<blockquote>
<p>🚨 문제점:  상위 클래스(부모 클래스)를 상속받은 하위 클래스(자식 클래스)는 상위 클래스에서 기대하는 동작을 그대로 유지해야 한다는 원칙인 <code>리스코프 치환 원칙</code> 위배</p>
</blockquote>
<p><code>Stack</code>과 <code>Queue</code>는 <code>List</code>처럼 사용되더라도 문제가 없어야 한다. <code>Stack</code>과 <code>Queue</code>가 <code>List</code>를 상속받았으므로, 각 클래스는 문법적으로 <code>List</code> 타입으로 다뤄질 수 있다.</p>
<pre><code class="language-java">List stack = new Stack();
List queue = new Queue();</code></pre>
<p>그러나 <code>List</code>의 모든 메서드를 상속받은 <code>Stack</code>과 <code>Queue</code>는 본래 제공하지 않아야 할 메서드들 즉, <strong>불필요한 메서드들</strong>(<code>pushLeft</code>, <code>popLeft</code> 등)도 사용할 수 있게 된다. 이것은 각각의 자료구조의 기본 특성을 깨뜨릴 수 있다.</p>
<p><strong>스택 객체</strong>에서 <code>pushLeft</code>나 <code>popLeft</code>를 사용할 경우, 후입선출(FILO) 특성이 깨진다.</p>
<pre><code class="language-java">List stack = new Stack();
stack.push(1);    // [1]
stack.push(2);    // [1, 2]
stack.push(3);    // [1, 2, 3]
stack.pushLeft(4);  // [4, 1, 2, 3] - 순서가 깨짐
stack.pop();        // [4, 1, 2] =&gt; 3 반환
stack.popLeft();    // [1, 2] =&gt; 4 반환</code></pre>
<p><strong>큐 객체</strong>에서도 <code>pushLeft</code>나 <code>pop</code>을 사용할 경우, 선입선출(FIFO) 특성이 깨진다.</p>
<pre><code class="language-java">List queue = new Queue();
queue.push(1);    // [1]
queue.push(2);    // [1, 2]
queue.push(3);    // [1, 2, 3]
queue.pushLeft(4);  // [4, 1, 2, 3] - 순서가 깨짐
queue.pop();        // [4, 1, 2] =&gt; 3 반환
queue.popLeft();    // [1, 2] =&gt; 4 반환</code></pre>
<ul>
<li><strong>Stack</strong>은 후입선출(LIFO) 구조를 따르며, 마지막에 추가된 요소를 제거해야 한다.</li>
<li><strong>Queue</strong>는 선입선출(FIFO) 구조를 따르며, 먼저 추가된 요소를 먼저 제거해야 합한다.</li>
</ul>
<p>이는 리스코프 치환 원칙을 위배하는 사례로, 코드의 유지보수성과 가독성에 문제가 발생할 수 있다. </p>
<blockquote>
<p>📢 즉, <code>서브 클래싱 관점</code>의 상속은 <strong>타입들 사이의 관계에 대한 고려 없이</strong> 오로지 코드 재사용만을 목적으로 상속을 사용할 경우 발생할 수 있는 문제이다. </p>
</blockquote>
<p>상속으로 인해 Stack과 Queue에 호출되어서는 안되는 메서드들이 불필요하게 생겨났기 때문에, 정확히 말하면 Stack과 Queue 타입에 <strong>불필요한 퍼블릭 인터페이스들이 과하게 상속되었기 때문에 발생한 문제</strong>이다</p>
<p>이처럼 코드를 상속받아 <strong>Stack</strong>과 <strong>Queue</strong>를 구현하는 것은 잘못된 설계이다. Stack과 Queue의 동작은 다르기 때문에 상속보다는 각각의 동작을 구현한 별도의 클래스를 만들어야 한다. </p>
<h4 id="🔑-서브타이핑">🔑 서브타이핑</h4>
<blockquote>
<p><code>리스코프 치환원칙</code>이란 간단히 말해 &quot;상속을 할 때 서브클래싱은 나쁘고 서브타이핑을 해야 한다&quot;라는 원칙</p>
</blockquote>
<p>서브타이핑에 대해 조영호(2019)는 오브젝트에서 다음과 같이 설명한다. </p>
<p>💬 &quot;상속을 사용하는 일차적인 목표는 코드 재사용이 아니라 <strong>타입 계층을 구현하는 것이어야 한다...</strong> 동일한 메시지에 대해 서로 다르게 행동할 수 있는 다형적인 객체를 구현하기 위해서는 <strong>객체의 행동을 기반으로 타입 계층을 구성해야 한다.</strong> 상속의 가치는 이러한 타입 계층을 구현할 수 있는 쉽고 편안한 방법을 제공한다는 데 있다.&quot; </p>
<p><strong>즉, 서브 클래싱 관점으로 상속하면 문제가 생긴다는 점을 서브타이핑에서는 말하고 있는 것이다.</strong></p>
<h3 id="🌱-문제점-2--캡슐화-위반-메서드-오버라이딩-오작동">🌱 문제점 2 : 캡슐화 위반, 메서드 오버라이딩 오작동</h3>
<p>상위 클래스가 어떻게 구현되느냐에 따라 <strong>하위 클래스의 동작에 이상이 생길 수 있다.</strong></p>
<blockquote>
<p>여기서 캡슐화란, 단순히 private 변수로 Getter / Setter 를 얘기하는 것이 아니다. <code>캡슐화(정보 은닉)</code>은 <strong>객체가 내부적으로 기능을 어떻게 구현하는지를 감추는 것을 말한다.</strong> 그래서 우리는 클래스 자료형을 이용할때 내부 동작을 알필요없이 단순히 메소드만 갖다 쓰면 된다. 단, *<em>내부 동작을 알 필요가 없다는 말은 신뢰성이 보장되어야 한다는 말이기도 하다. *</em>캡슐화가 깨진건 이러한 <code>신뢰성이 깨진것</code>이라고 보면 된다.</p>
</blockquote>
<p>잘못된 상속의 예</p>
<pre><code class="language-java">public class InstrumentedHashSet&lt;E&gt; extends HashSet&lt;E&gt; {
    private int addCount = 0;

    public InstrumentedHashSet() { }

    @Override
    public boolean add(E e) {
        addCount++;
        return super.add(e);
    }

    @Override
    public boolean addAll(Collection&lt;? extends E&gt; c) {
        addCount += c.size();
        return super.addAll(c);
    }

    public int getAddCount() {
        return addCount;
    }
}
</code></pre>
<pre><code class="language-java">InstrumentedHashSet&lt;String&gt; s = new InstrumentedHashSet&lt;&gt;();
s.addAll(Arrays.asList(&quot;틱&quot;, &quot;탁탁&quot;, &quot;펑&quot;));

System.out.println(s.getAddCount()); // 예상: 3, 실제: 6</code></pre>
<p>일반적으로 위 코드 실행 후 <code>addCount</code>가 3이 될 것이라 예상할 것이다. 하지만 실제로는 6이다. 이유는 부모 클래스인 <code>HashSet</code>의 <code>addAll</code> 메서드 안에서 <code>add</code>메서드를 호출하기 때문이다. </p>
<pre><code class="language-java">public boolean addAll(@NotNull Collection&lt;? extends E&gt; c) {
    boolean modified = false;
    for (E e : c) {
        if (add(e)) { // 내부에서 자체적으로 add()를 계속 호출한거임
            modified = true;
        }
    }
    return modified;
}</code></pre>
<blockquote>
<p><code>addAll</code>을 호출하면 내부에서 <code>add</code>를 호출하는데 <code>add</code>가 상위 클래스의 add를 호출할줄 알았지만 <code>InstrumentedHashSet</code>의 <code>add</code>를 호출했다.</p>
</blockquote>
<p>위에서의  문제는 메서드 재정의 시 당장은 해결할 수 있으나,   HashSet의 <code>addAll</code>이 add 메서드를 이용해 구현했음을 가정한 해법이라는 한계를 지닌다. 이처럼 자신의 다른 부분을 사용하는 <code>자기사용(self-use)</code> 여부는 해당 클래스의 내부 구현 방식 에 해당하며, 자바 플랫폼 전반적인 정책인지, 그래서 <strong>다음 릴리스에서도 유지될지는 알 수 없다.</strong> 따라서 이런 가정에 기댄 <code>InstrumentedHashSet</code>도 깨지기 쉽다.</p>
<p><code>addAll</code> 메서드를 다른 식으로 재정의할 수도 있다. 주어진 컬렉션을 순회하며 원소 하나당 <code>add</code> 메서드를 하나만 호출하는 것이다. 조금 나은 방법이지만 상위 클래스의 메서드 동작을 다시 구현하는 것은 어렵고, 비용이 든다. 또한 하위 클래스에서 접근할 수 없는 private 필드를 써야 한다면 이 방식으로는 구현 자체가 불가능하다.</p>
<ul>
<li><strong>상위 클래스의 구현에 의존</strong>: <code>HashSet</code>의 내부 구현이 <code>addAll()</code>에서 <code>add()</code>를 호출한다는 사실에 의존하고 있다.</li>
<li><strong>메서드 오버라이딩의 위험성</strong>: 상위 클래스의 메서드를 재정의하면, 상위 클래스의 내부 구현이 변경될 때 하위 클래스의 동작이 예기치 않게 변할 수 있다.</li>
</ul>
<blockquote>
<p>그렇다면 위에서의 문제는 다 메서드 재정의 시니까 새로운 메서드를 추가한다면?</p>
</blockquote>
<p>이 방식이 훨씬 안전한 것은 맞지만, 위험이 전혀 없는 것은 아니다. 다음 릴리스에서 상위 클래스에 새 메서드가 추가됐는데, 하필 하위 클래스에 추가한 메서드와 시그니처가 같고 반환 타입은 다르다면 여러분의 클래스는 컴파일조차 되지 않을 수 있다.</p>
<h3 id="🌱-문제점-3--강한-결합도">🌱 문제점 3 : 강한 결합도</h3>
<blockquote>
<p>상속은 코드를 재사용하는 강력한 수단이지만, 항상 최선은 아니다</p>
</blockquote>
<p>부모 클래스의 내부 변경이 자식 클래스에 영향을 줄 수 있어 유연성이 저하된다. 상속을 하게 되면 부모 클래스와 자식 클래스의 관계가 <code>컴파일 시점</code>에 관계가 결정되어 결합도가 당연히 높아질수 밖에 없다.</p>
<p>예를 들어 클래스 B가 클래스 A를 상속(extends) 한다고 하면, 코드 실행(런타임) 중간에 클래스 C를 상속하도록 바꿀수 없다. 처음 실행되기 전에 미리 그렇게 결정되었기 때문이다.</p>
<ul>
<li>캡슐화 위반 : 자식 클래스가 부모 클래스의 구현 세부 사항에 의존하게되면, 캡슐화가 약화된다.</li>
<li>재사용성 저하 : 특정 구현에 강하게 결합된 상속 구조는 새로운 상황에 재사용하기 어렵다.</li>
</ul>
<h3 id="🌱-문제점-4--자식은-부모의-거울-안-좋은-점까지-그리고-동시-수정">🌱 문제점 4 : 자식은 부모의 거울, 안 좋은 점까지? 그리고 동시 수정</h3>
<blockquote>
<p>마치 자식은 부모의 거울이라는 말처럼 부모의 안 좋은 점을 자식클래스들이 다 닮게 된다.</p>
</blockquote>
<p><strong>[결함 상속]</strong>
부모 클래스에 결함이 있을 때 자식 클래스도 그 결함을 그대로 상속받게 되는 상황입니다.</p>
<pre><code class="language-java">class Vehicle {
    private int speed;

    public Vehicle(int speed) {
        this.speed = speed;
    }

    // 결함이 있는 메서드: 속도가 음수일 때도 허용
    public void accelerate(int increment) {
        speed += increment;
    }

    public int getSpeed() {
        return speed;
    }
}

class Car extends Vehicle {
    public Car(int speed) {
        super(speed);
    }

    // Car는 별도의 결함이 없으나 부모 클래스의 accelerate 메서드 결함을 그대로 상속
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car(50);
        car.accelerate(-100);  // 속도가 음수가 될 수 있는 문제 발생
        System.out.println(&quot;Car speed: &quot; + car.getSpeed());  // 출력 결과가 음수
    }
}</code></pre>
<p>위 코드에서 Vehicle 클래스의 accelerate 메서드에 결함이 있어 음수 속도가 허용되지만, 이 결함이 자식 클래스 Car에도 그대로 영향을 미친다.</p>
<p><strong>[부모 클래스와 자식 클래스의 동시 수정 문제]</strong>
부모 클래스가 변경될 때 자식 클래스와 호출부도 모두 수정해야 해야 함</p>
<h3 id="🌱-문제점-6--클래스-폭발class-explosion">🌱 문제점 6 : 클래스 폭발(class explosion)</h3>
<blockquote>
<p>상속을 남용할 경우 클래스 폭발(class explosion) 문제가 발생할 수 있다. </p>
</blockquote>
<p>즉, 기능을 추가하기 위해 상속을 계속하다 보면 클래스가 급격히 늘어나고, 서로 복잡하게 얽히게 되어 관리가 어려워진다. 이를 <strong>조합의 폭발(combinational explosion)</strong>이라고도 부른다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9991afe6-a0e4-4c7d-96d4-7f57c771f46d/image.png" /></p>
<p><code>상속</code>은 <strong>컴파일 타임에 결정되므로, 실행 중에 변경할 수 없다.</strong> 기능을 추가하거나 수정할 때마다 새로운 클래스를 상속받아 추가해야 한다.
이러한 문제를 피하기 위해서는 상속 대신 <strong>합성(Composition)</strong>을 사용하는 것이 좋습니다. 합성은 기존 객체를 포함하고, 그 객체에 기능을 추가하는 방식으로 상속의 문제를 피할 수 있습니다.</p>
<h3 id="🌱-문제점-7--단일-상속의-한계">🌱 문제점 7 : 단일 상속의 한계</h3>
<p>자바는 다중 상속을 지원하지 않기 때문에 하나의 클래스는 오직 하나의 부모 클래스만 상속받을 수 있다. </p>
<blockquote>
<p>다중 상속이 불가능하기 때문에 상속 계층을 복잡하게 나눠야 하는 상황이 발생할 수 있다.</p>
</blockquote>
<p>이로 인해 클래스 폭발 문제가 더욱 심화될 수 있다. 따라서, 자바에서는 이런 단일 상속의 문제를 해결하기 위해 <strong>인터페이스를 사용</strong>하여 <strong>다중 구현</strong>을 지원하고 있다.</p>
<h1 id="2-상속의-대안-컴포지션composition">2. 상속의 대안 컴포지션(composition)</h1>
<blockquote>
<p>하나의 클래스가 다른 클래스의 인스턴스를 포함하여, 그 인스턴스의 메서드를 활용하는 방식</p>
</blockquote>
<h2 id="1-합성이란">1) 합성이란?</h2>
<blockquote>
<p><code>합성</code>은 객체 간의 관계가 수직관계가 아닌 수평 관계가 된다.</p>
</blockquote>
<p>합성은 기존 클래스를 상속을 통한 확장하는 대신에, <strong>필드로 클래스의 인스턴스를 참조하게 만드는 설계</strong>이다. 예를 들어 서로 관련없는 이질적인 클래스의 관계에서, 한 클래스가 다른 클래스의 기능을 사용하여 구현해야 한다면 합성의 방식을 사용한다고 보면 된다.</p>
<h3 id="2-합성-예시">2) 합성 예시</h3>
<p>컴퓨터(Computer)와 모니터(Monitor)의 관계를 예로 들어보겠다. 컴퓨터는 모니터가 필요하지만, 모니터를 상속받을 필요는 없다. 대신 모니터를 합성하여 사용하는 것이 더 적합하다.</p>
<pre><code class="language-java">// Computer 클래스
class Computer {
    Monitor monitor; // 필드로 Monitor 클래스 변수를 갖는다 (Has-A 관계)

    Computer(Monitor monitor) {
        this.monitor = monitor; // 생성자 초기화 시 Monitor 인스턴스를 받음
    }

    void display() {
        System.out.printf(&quot;%s 모니터로 화면 출력 중...\n&quot;, monitor.getMonitorType());
    }

    void turnOff() {
        System.out.printf(&quot;%s 모니터를 끕니다...\n&quot;, monitor.getMonitorType());
    }
}

// Monitor 클래스
class Monitor {
    String monitorType; // 모니터 종류 (예: LCD, LED)

    Monitor(String type) {
        this.monitorType = type;
    }

    String getMonitorType() {
        return this.monitorType;
    }
}

// Main 클래스
public class Main {
    public static void main(String[] args) {
        // LCD 모니터가 연결된 컴퓨터
        Computer lcdComputer = new Computer(new Monitor(&quot;LCD&quot;));
        lcdComputer.display(); // LCD 모니터로 화면 출력 중...

        // LED 모니터가 연결된 컴퓨터
        Computer ledComputer = new Computer(new Monitor(&quot;LED&quot;));
        ledComputer.display(); // LED 모니터로 화면 출력 중...

        lcdComputer.turnOff(); // LCD 모니터를 끕니다...
        ledComputer.turnOff(); // LED 모니터를 끕니다...
    }
}</code></pre>
<ul>
<li>Computer 클래스는 Monitor <strong>클래스를 필드로 가진다.</strong> 이것이 바로 <code>합성</code>의 예로 컴퓨터는 모니터를 필요로 하지만, 모니터를 상속하지 않고 인스턴스로 참조하여 기능을 사용한다.</li>
<li>Computer 클래스의 생성자는 Monitor 객체를 받아서, 그 객체의 monitorType을 통해 모니터 종류에 따른 동작을 수행한다.</li>
<li>Monitor 클래스는 모니터의 종류(monitorType)를 나타내는 필드를 가지고 있으며, 이를 Computer 클래스가 호출하여 사용한다.</li>
</ul>
<p>위의 초기화 코드에서 볼수 있듯이, 기존 클래스를 확장하는 대신, <strong>새로운 클래스를 만들고 private 필드로 기존 클래스의 인스턴스를 참조하게 한 것이다.</strong> </p>
<blockquote>
<p>상속의 문제의 대안법인 합성은 기능이 필요하다고 해서 무조건 상속하지말고, 따로 클래스 인스턴스 변수에 저장하여 가져다 쓴다는 원리이다.</p>
</blockquote>
<p>새 클래스의 인스턴스 메서드들은 (private 필드로 참조하는) 기존 클래스의 대응하는 메서드를 호출 해 그 결과를 반환한다. 이 방식을 <strong>전달(forwarding)</strong>이라 하며, 새 클래스의 메서드들을 <strong>전달 메서드(forwarding method)</strong>라 부른다.</p>
<p>그 결과 새로운 클래스는 기존 클래스의 내부 구현 방식의 영향에서 벗어나며, 심지어 기존 클래스에 새로운 메서드가 추가되더라도 전혀 영향받지 않는다.&#x20;</p>
<h3 id="3-컴포지션-사용하기">3) 컴포지션 사용하기</h3>
<p>상속 대신 컴포지션(Composition)을 사용하여 기존 <code>Set</code> 인스턴스를 감싸는 래퍼 클래스(Wrapper Class)를 만들어가자.</p>
<pre><code class="language-java">public class InstrumentedSet&lt;E&gt; implements Set&lt;E&gt; {
    private final Set&lt;E&gt; set;
    private int addCount = 0;

    public InstrumentedSet(Set&lt;E&gt; set) {
        this.set = set;
    }

    @Override
    public boolean add(E e) {
        addCount++;
        return set.add(e);
    }

    @Override
    public boolean addAll(Collection&lt;? extends E&gt; c) {
        addCount += c.size();
        return set.addAll(c);
    }

    public int getAddCount() {
        return addCount;
    }

    // 나머지 Set 인터페이스 메서드들은 set 인스턴스에 위임
    @Override
    public int size() {
        return set.size();
    }

    @Override
    public boolean isEmpty() {
        return set.isEmpty();
    }

    // ... 기타 메서드들도 동일하게 위임
}</code></pre>
<p><strong>설명</strong>:</p>
<ul>
<li><code>InstrumentedSet</code>은 <code>Set</code> 인터페이스를 구현하고, 내부에 실제 작업을 수행할 <code>Set</code> 인스턴스를 가진다.</li>
<li>모든 메서드는 내부 <code>set</code> 객체에 작업을 위임한다.</li>
<li><code>add()</code>와 <code>addAll()</code> 메서드에서 <code>addCount</code>를 정확하게 증가시킬 수 있다.</li>
<li>상속이 아닌 컴포지션을 사용함으로써 상위 클래스의 내부 구현에 의존하지 않는다.</li>
</ul>
<p><strong>사용 예시</strong>:</p>
<pre><code class="language-java">Set&lt;String&gt; s = new InstrumentedSet&lt;&gt;(new HashSet&lt;&gt;());
s.addAll(Arrays.asList(&quot;틱&quot;, &quot;탁탁&quot;, &quot;펑&quot;));

System.out.println(((InstrumentedSet&lt;String&gt;) s).getAddCount()); // 출력: 3</code></pre>
<ul>
<li><strong>안전성</strong>: 상위 클래스의 내부 구현 변화에 영향을 받지 않는다.</li>
<li><strong>유연성</strong>: 기존 클래스의 기능을 확장하거나 변경할 때 더 안전하게 구현할 수 있다.</li>
<li><strong>재사용성</strong>: 다양한 클래스와 함께 사용할 수 있으며, 기능을 추가하거나 변경하기 쉽다.</li>
</ul>
<blockquote>
<p>위임 메서드를 일일이 작성하는 대신, 재사용 가능한 포워딩 클래스를 만들어서 중복 코드를 줄일 수 있다.</p>
</blockquote>
<pre><code class="language-java">public class ForwardingSet&lt;E&gt; implements Set&lt;E&gt; {
    protected final Set&lt;E&gt; s;

    public ForwardingSet(Set&lt;E&gt; s) {
        this.s = s;
    }

    @Override
    public boolean add(E e) { return s.add(e); }

    @Override
    public boolean addAll(Collection&lt;? extends E&gt; c) { return s.addAll(c); }

    // 나머지 메서드들도 동일하게 s에 위임
    @Override
    public int size() { return s.size(); }

    @Override
    public boolean isEmpty() { return s.isEmpty(); }

    // ... 기타 메서드들도 동일하게 위임
}</code></pre>
<p>이제 <code>InstrumentedSet</code>은 <code>ForwardingSet</code>을 상속받아 필요한 기능만 추가하면 됨</p>
<pre><code class="language-java">public class InstrumentedSet&lt;E&gt; extends ForwardingSet&lt;E&gt; {
    private int addCount = 0;

    public InstrumentedSet(Set&lt;E&gt; s) {
        super(s);
    }

    @Override
    public boolean add(E e) {
        addCount++;
        return super.add(e);
    }

    @Override
    public boolean addAll(Collection&lt;? extends E&gt; c) {
        addCount += c.size();
        return super.addAll(c);
    }

    public int getAddCount() {
        return addCount;
    }
}</code></pre>
<p><code>InstrumentedSet</code>은 <code>HashSet</code>의 모든 기능을 정의한 <code>Set</code> 인터페이스를 활용해 설계되어 견고하고 아주 유연하다. 구체적으로는 Set 인터페이스를 구현했고, Set의 인스턴스를 인수로 받는 생성자를 하나 제공한다. 임의의 Set에 계측 기능을 덧씌어 새로운 Set으로 만드는 것이 이 클래스의 핵심이다. 이 컴포지션 방식은 한 번만 구현해두면 어떠한 Set 구현체라도 계측할 수 있으며, 기존 생성자들도 함께 사용할 수 있다.</p>
<pre><code class="language-java">Set&lt;Instant&gt; times = new InstrumentedSet&lt;&gt;(new TreeSet&lt;&gt;(cmp));
Set&lt;E&gt; s = new InstrumentedSet&lt;&gt;(new HashSet&lt;&gt;(INIT_CAPACITY));</code></pre>
<p>다른 Set 인스턴스를 감싸고 있다는 뜻에서 <code>InstrumentedSet</code> 같은 클래스를 래퍼 클래스라 하며, 다른 Set에 계측 기능을 덧씌운다는 뜻에서 데코레이터 패턴이라고 한다. 컴포지션과 전달의 조합은 넓은 의미로 <strong>위임</strong>(delegation)이라고 부른다.</p>
<blockquote>
<p>상속은 반드시 하위 클래스가 상위 클래스의 '진짜' 하위 타입인 상황에서만 쓰여야 한다. 다르게 말하면, 클래스 B가 클래스 A와 <code>is-a</code> 관계일 때만 클래스 A를 상속해야 한다.</p>
</blockquote>
<p>컴포지션을 써야 할 상황에서 상속을 사용하는 건 내부 구현을 불필요하게 노출하는 꼴이다. 그 결과 API가 내부 구현에 묶이고 그 클래스의 성능도 영원히 제한된다. 더 심각한 문제는 클라이언트가 노출된 내부에 직접 접근할 수 있다는 점이다.</p>
<blockquote>
<p>래퍼 클래스는 단점이 거의 없다. 한 가지, 래퍼 클래스가 콜백(callback) 프레임워크와는 어울리지 않는다는 점만 주의하면 된다.</p>
</blockquote>
<p>콜백 프레임워크에서 는 자기 자신의 참조를 다른 객체에 넘겨서 다음 호출(콜백) 때 사용하도록 한다. 내부 객체는 자신을 감싸고 있는 래퍼의 존재를 모르니 대신 자신(this)의 참조를 넘기고, 콜백 때는 래퍼가 아닌 내부 객체를 호출하게 된다. 이를 <code>SELF 문제</code>라고 한다.</p>
<p>전달 메서드가 성능에 주는 영향이나 래퍼 객체가 <strong>메모리 사용량에 주는 영향</strong>을 걱정하는 사람도 있지만, 실전에서는 둘 다 별다른 영향이 없다고 밝혀졌다. 전달 메서드들을 작성하는 게 재사용할 수 있는 전달 클래스를 인터 페이스당 하나씩만 만들어두 면 원하는 기능을 덧씌우는 전달 클래스들을 아주 손쉽게 구현할 수 있다.</p>
<h3 id="4-컴포지션의-장점">4) 컴포지션의 장점</h3>
<blockquote>
<p>합성(Composition)을 사용하는 이유는 <strong>유연성</strong>과 <strong>재사용성</strong>을 높이기 위해서입니다. 상속에 비해 합성은 다음과 같은 이점이 있다.</p>
</blockquote>
<ol>
<li><strong>유연한 객체 관계 관리</strong><blockquote>
<p>상속에서는 객체 간의 관계가 고정되지만, 합성에서는 더 유연하게 객체를 구성할 수 있다.</p>
</blockquote>
</li>
</ol>
<p><strong>❌ 상속 예시 (상속으로 고정된 관계)</strong></p>
<pre><code class="language-java">// 부모 클래스: Animal
class Animal {
    public void eat() {
        System.out.println(&quot;This animal is eating.&quot;);
    }
}

// 자식 클래스: Dog
class Dog extends Animal {
    public void bark() {
        System.out.println(&quot;The dog is barking.&quot;);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // 상속된 메서드: Dog가 Animal의 eat 메서드를 사용
        dog.bark(); // Dog 클래스의 메서드
    }
}</code></pre>
<p>위 코드는 Dog 클래스가 Animal 클래스를 상속하므로, Dog 객체는 Animal의 모든 메서드를 자동으로 상속받는다. 하지만 관계가 고정되어 변경하기 어렵다.</p>
<p><strong>⭕합성 예시 (유연한 관계)</strong></p>
<pre><code class="language-java">// 독립적인 기능 클래스: SoundMaker
class SoundMaker {
    public void makeSound(String sound) {
        System.out.println(sound);
    }
}

// 합성을 이용한 Dog 클래스
class Dog {
    private SoundMaker soundMaker;  // Dog 클래스는 SoundMaker를 사용 (has-a 관계)

    public Dog() {
        this.soundMaker = new SoundMaker();
    }

    public void bark() {
        soundMaker.makeSound(&quot;The dog is barking.&quot;);
    }

    public void eat() {
        System.out.println(&quot;The dog is eating.&quot;);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.bark();  // 합성을 이용하여 소리를 만듦
        dog.eat();   // 독립적인 Dog의 메서드
    }
}</code></pre>
<p>여기서는 Dog 클래스가 SoundMaker 객체를 <strong>조립(합성)</strong>하여 더 유연하게 동작을 정의</p>
<ol start="2">
<li><strong>다중 상속 문제 해결</strong><blockquote>
<p>자바는 다중 상속을 지원하지 않지만, 합성을 사용하면 여러 객체를 합성하여 다중 상속과 유사한 효과를 얻을 수 있다.</p>
</blockquote>
</li>
</ol>
<p><strong>⭕ 합성 예시 (다중 상속 대체)</strong></p>
<pre><code class="language-java">// 독립적인 기능 클래스: Engine
class Engine {
    public void start() {
        System.out.println(&quot;Engine is starting...&quot;);
    }
}

// 독립적인 기능 클래스: GPS
class GPS {
    public void activate() {
        System.out.println(&quot;GPS is activated.&quot;);
    }
}

// Car 클래스가 Engine과 GPS를 합성
class Car {
    private Engine engine; // Car는 Engine을 가짐 (has-a)
    private GPS gps;       // Car는 GPS를 가짐 (has-a)

    public Car() {
        this.engine = new Engine();
        this.gps = new GPS();
    }

    public void drive() {
        engine.start();
        gps.activate();
        System.out.println(&quot;Car is driving.&quot;);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.drive();  // Car는 Engine과 GPS 기능을 모두 사용할 수 있음
    }
}</code></pre>
<p>위 코드에서는 Car가 Engine과 GPS 두 객체를 합성하여 <strong>다중 상속 없이</strong> 두 객체의 기능을 모두 사용할 수 있습니다.</p>
<ol start="3">
<li><strong>상속의 문제 해결</strong><blockquote>
<p>상속은 부모 클래스의 세부 구현에 의존하지만, <code>합성</code>은 <strong>객체의 행동을 위임함으로써 더 독립적인 관계를 제공한다.</strong></p>
</blockquote>
</li>
</ol>
<p><strong>❌상속의 문제 예시</strong></p>
<pre><code class="language-java">// 부모 클래스: Beverage (음료)
class Beverage {
    public void drink() {
        System.out.println(&quot;Drinking a beverage.&quot;);
    }
}

// 자식 클래스: Juice
class Juice extends Beverage {
    public void addIce() {
        System.out.println(&quot;Adding ice to the juice.&quot;);
    }
}

public class Main {
    public static void main(String[] args) {
        Juice juice = new Juice();
        juice.drink();  // 상속된 메서드: Juice가 Beverage의 drink 메서드를 사용
        juice.addIce();
    }
}</code></pre>
<p>이 코드에서 만약 <code>Beverage</code> 클래스에 변경이 생기면 <code>Juice</code> 클래스에도 영향을 미칩니다. 이는 부모 클래스에 의존하는 문제를 야기할 수 있다.</p>
<p><strong>⭕ 합성으로 해결</strong></p>
<pre><code class="language-java">// 독립적인 기능 클래스: IceMaker
class IceMaker {
    public void addIce() {
        System.out.println(&quot;Ice is added.&quot;);
    }
}

// Juice 클래스가 IceMaker를 합성하여 사용
class Juice {
    private IceMaker iceMaker;  // Juice는 IceMaker를 합성 (has-a)

    public Juice() {
        this.iceMaker = new IceMaker();
    }

    public void drink() {
        System.out.println(&quot;Drinking juice.&quot;);
    }

    public void addIce() {
        iceMaker.addIce();  // IceMaker 객체에 기능을 위임
    }
}

public class Main {
    public static void main(String[] args) {
        Juice juice = new Juice();
        juice.drink();
        juice.addIce();  // Juice는 IceMaker 객체의 메서드를 호출함
    }
}</code></pre>
<p>이 방식은 Juice가 IceMaker의 내부 동작에 의존하지 않기 때문에 더 독립적이고 유연하게 설계할 수 있다.</p>
<ol start="4">
<li><strong>캡슐화 보장</strong> <blockquote>
<p><code>상속</code>은 부모 클래스의 모든 public 메서드를 자식 클래스에 공개하는 반면, 합성은** 필요한 메서드만 노출할 수 있다.**</p>
</blockquote>
</li>
</ol>
<p><strong>❌ 상속에서의 문제</strong></p>
<pre><code class="language-java">class Vector {
    public void addElement(String element) {
        System.out.println(&quot;Element added to vector: &quot; + element);
    }
}

class Stack extends Vector {
    public void push(String element) {
        addElement(element);
    }

    public void pop() {
        System.out.println(&quot;Element removed from stack.&quot;);
    }
}

public class Main {
    public static void main(String[] args) {
        Stack stack = new Stack();
        stack.push(&quot;item&quot;);
        stack.addElement(&quot;another item&quot;);  // 불필요한 부모 클래스 메서드가 노출됨
        stack.pop();
    }
}</code></pre>
<p>이 코드에서는 <code>Stack</code> 클래스에서 <strong>불필요한</strong> <code>addElement</code> 메서드가 노출되어 잘못된 사용을 허용하게 된다.</p>
<p><strong>⭕ 합성으로 캡슐화</strong></p>
<pre><code class="language-java">// Vector와 동일한 기능을 가진 클래스: ListManager
class ListManager {
    public void addElement(String element) {
        System.out.println(&quot;Element added to list: &quot; + element);
    }
}

// Stack은 ListManager를 합성하여 필요한 메서드만 노출
class Stack {
    private ListManager listManager;  // Stack은 ListManager를 합성 (has-a)

    public Stack() {
        this.listManager = new ListManager();
    }

    public void push(String element) {
        listManager.addElement(element);  // 필요한 기능만 사용
    }

    public void pop() {
        System.out.println(&quot;Element removed from stack.&quot;);
    }
}

public class Main {
    public static void main(String[] args) {
        Stack stack = new Stack();
        stack.push(&quot;item&quot;);
        stack.pop();
        // stack.addElement()는 호출할 수 없음
    }
}</code></pre>
<p>여기서 <code>Stack</code>은 <code>ListManager</code>의 내부 동작 중 <strong>필요한 메서드만 노출</strong>하여 사용하며, 불필요한 세부 사항을 숨긴다.</p>
<ul>
<li><code>합성</code>을 사용하면 각 객체는 독립적으로 관리되며, 변경에 더 강한 설계를 할 수 있다.</li>
</ul>
<h3 id="5-엄밀히-보면-합성이랑-컴포지션도-다르다">5) 엄밀히 보면 합성이랑 컴포지션도 다르다?</h3>
<blockquote>
<p>혼용해서 쓰는 경우가 대부분이라고 함.. 합성이라고 하면 컴포지션이라고 생각해도 무방할 듯 하다.</p>
</blockquote>
<p>컴포지션(Composition)과 합성(Aggregation)은 객체지향 프로그래밍에서 객체 간의 관계를 나타낼 때 사용하는 중요한 개념들이다. 두 개념은 서로 유사하지만 중요한 차이점이 있으며, 각각의 경우에 맞는 적절한 사용 방법이 있다.</p>
<h4 id="컴포지션composition"><strong>컴포지션(Composition)</strong></h4>
<ul>
<li><strong>의미</strong>: 컴포지션은 <strong>강한 관계</strong>를 뜻한다. 한 객체가 다른 객체를 <strong>포함하고</strong>, 포함된 객체는 <strong>독립적으로 존재할 수 없는</strong> 관계이다.</li>
<li><strong>예시</strong>: 자동차(전체)는 엔진(부분)을 포함한다. 엔진은 자동차의 일부로, 자동차가 없으면 엔진은 의미가 없다. 즉, <strong>컴포지션에서는 전체 객체가 소멸하면 부분 객체도 함께 소멸</strong>된다.</li>
</ul>
<p><strong>예시 코드:</strong></p>
<pre><code class="language-java">class Car {
    private Engine engine;

    Car() {
        this.engine = new Engine(); // 엔진을 직접 초기화
    }

    void start() {
        engine.run();
    }
}

class Engine {
    void run() {
        System.out.println(&quot;Engine is running...&quot;);
    }
}</code></pre>
<ul>
<li><code>Car</code>는 <code>Engine</code>을 <strong>포함</strong>하고 있으며, <code>Car</code>가 없어지면 <code>Engine</code>도 의미를 잃습니다. 이는 <strong>컴포지션</strong>의 전형적인 예</li>
</ul>
<h3 id="합성aggregation"><strong>합성(Aggregation)</strong></h3>
<ul>
<li><strong>의미</strong>: 합성은 <strong>약한 관계</strong>를 나타낸다. 하나의 객체가 다른 객체를 포함하고 있지만, 그 포함된 객체는 <strong>독립적으로 존재</strong>할 수 있다. 즉, <strong>전체 객체가 없어져도 부분 객체는 여전히 존재할 수 있는</strong> 관계이다.</li>
<li><strong>예시</strong>: 학교(전체)는 학생(부분)을 포함한다. 하지만 학교가 없어져도 학생은 여전히 존재할 수 있다.</li>
</ul>
<p><strong>예시 코드:</strong></p>
<pre><code class="language-java">class School {
    private Student student;

    School(Student student) {
        this.student = student; // 외부에서 객체를 주입받음
    }

    void educate() {
        student.study();
    }
}

class Student {
    void study() {
        System.out.println(&quot;Student is studying...&quot;);
    }
}</code></pre>
<ul>
<li><code>School</code>은 <code>Student</code>를 <strong>참조</strong>하고 있지만, <code>Student</code> 객체는 <code>School</code>이 없어져도 독립적으로 존재할 수 있습니다. 이는 <strong>합성</strong>의 전형적인 예</li>
</ul>
<h3 id="컴포지션과-합성의-차이점-요약"><strong>컴포지션과 합성의 차이점 요약</strong></h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>컴포지션(Composition)</th>
<th>합성(Aggregation)</th>
</tr>
</thead>
<tbody><tr>
<td><strong>관계</strong></td>
<td>강한 관계 (전체와 부분이 강하게 결합됨)</td>
<td>약한 관계 (전체와 부분이 독립적)</td>
</tr>
<tr>
<td><strong>생명 주기</strong></td>
<td>전체가 없어지면 부분도 없어짐</td>
<td>전체가 없어져도 부분은 존재할 수 있음</td>
</tr>
<tr>
<td><strong>객체 생성 방식</strong></td>
<td>포함하는 객체가 직접 부분 객체를 생성함</td>
<td>포함하는 객체가 외부에서 부분 객체를 받아옴</td>
</tr>
<tr>
<td><strong>의존성</strong></td>
<td>전체 객체에 강하게 의존 (독립적으로 존재 불가)</td>
<td>약한 의존성 (부분 객체는 독립적으로 존재 가능)</td>
</tr>
<tr>
<td><strong>예시</strong></td>
<td>자동차와 엔진</td>
<td>학교와 학생</td>
</tr>
</tbody></table>
<blockquote>
<p>합성은 객체지향 설계에서 상속에 비해 더 <strong>유연하고, 유지보수가 용이</strong>한 방법이다. 특히 객체 간의 관계를 더 자유롭게 설계하고, 변경이 용이하며, 불필요한 의존성을 줄일 수 있다.</p>
</blockquote>
<h1 id="3-정리해보면">3. 정리해보면,</h1>
<h3 id="1-현업에서는-보통-상속을-어떻게-쓰냐">1) 현업에서는 보통 상속을 어떻게 쓰냐..</h3>
<p>보통 보니까 예를 들어 WebController - WebBaseController처럼 클래스 이름부터 is-a 관계인 애들만 상속에서 쓰더라</p>
<h3 id="2-정리-🐾">2) 정리 🐾</h3>
<ul>
<li><strong>상속은 is-a 관계일 때만 사용</strong>해야 한다. 클래스 간의 계층 구조를 형성할 때  말이다.  즉, 하위 클래스가 상위 클래스의 진짜 하위 타입인 경우에만 상속을 사용해야 한다. 내부 구현에 의존하거나 강한 결합이 발생할 수 있으므로 주의해야 한다.</li>
<li><strong>컴포지션</strong>은 <strong>Has-a 관계</strong>를 나타내며, 클래스의 기능을 유연하게 확장하고 재사용할 수 있다.  <strong>컴포지션과 위임</strong>을 사용하면 상속의 단점을 피하면서 유연하고 안전하게 기능을 확장할 수 있다. 하지만결합도가 낮아 유지보수가 용이하지만, 다형성 활용이 제한적일 수 있다.</li>
<li><strong>래퍼 클래스</strong>를 사용하면 기존 클래스의 내부 구현에 의존하지 않고도 기능을 추가하거나 변경할 수 있다.</li>
<li>특히, 상위 클래스에 새로운 메서드가 추가되더라도 하위 클래스의 동작에 영향을 주지 않는다.</li>
</ul>
<blockquote>
<p>상속을 지양하고 합성을 지향하라는 말은, 상속은 반드시 어떠한 특정한 관계 일 때만 사용하라고 엄격하게 제한하라는 말이며, 그 관계가 IS-A 관계 인 것이다.</p>
</blockquote>
<h3 id="3-상속과-합성-비교">3) 상속과 합성 비교</h3>
<table>
<thead>
<tr>
<th><strong>항목</strong></th>
<th><strong>상속 (Inheritance)</strong></th>
<th><strong>합성 (Composition)</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>의존성 해결</strong></td>
<td>부모 클래스와 자식 클래스 사이의 의존성은 컴파일 타임에 해결됨</td>
<td>두 객체 사이의 의존성은 런타임에 해결됨</td>
</tr>
<tr>
<td><strong>관계 유형</strong></td>
<td>&quot;is-a&quot; 관계를 나타냄</td>
<td>&quot;has-a&quot; 관계를 나타냄</td>
</tr>
<tr>
<td><strong>결합도</strong></td>
<td>부모 클래스와 자식 클래스 간의 결합도가 높음</td>
<td>포함된 객체 또는 인터페이스에 의존하므로 결합도가 낮음</td>
</tr>
<tr>
<td><strong>코드 재사용</strong></td>
<td>자식 클래스가 부모 클래스의 구현을 재사용함</td>
<td>포함된 객체나 인터페이스에 작업을 위임하여 재사용함</td>
</tr>
<tr>
<td><strong>유연성</strong></td>
<td>클래스 간의 결합이 강해 유연성이 떨어짐</td>
<td>객체 간 결합이 약하고 유연성이 높음</td>
</tr>
<tr>
<td><strong>수정 시 영향</strong></td>
<td>부모 클래스의 수정이 자식 클래스에 영향을 줄 수 있음</td>
<td>내부적으로 수정하기 용이하며, 종속성도 적음</td>
</tr>
</tbody></table>
<blockquote>
<p><code>합성</code>은 보통 더 유연하고 모듈화가 잘 되어 있으며, <code>상속</code>은 잘못 사용하면 결합도가 높아져 예기치 않은 문제가 발생할 수 있다.</p>
</blockquote>
<blockquote>
<p>✔️ OOP적 관점에서 봤을 때도 상속보다는 컴포지션이 객체의 자율성을 인정하면서도 안정적이고, 캡슐화를 더 좋게 이용할 수 있는 것 같다.</p>
</blockquote>
<h1 id="4-코틀린에서는-상속을-어떤식으로-해결해줬을까">4. 코틀린에서는 상속을 어떤식으로 해결해줬을까?</h1>
<h2 id="🍀-코틀린이란">🍀 코틀린이란</h2>
<p>JetBrains에서 개발한 프로그래밍 언어로, 주로 자바를 대체하거나 함께 사용할 수 있도록 설계되었다. 코틀린은 JVM(자바 가상 머신)에서 실행되며, 자바와 100% 호환되기 때문에 기존 자바 프로젝트에서 무리 없이 사용이 가능하다. 코틀린은 자바에서 불편한 점이나 한계점을 해결하는 데 중점을 두었으며, 자바보다 더 간결하고 안전한 코드를 작성할 수 있게 해준다.</p>
<p>코틀린의 널 안전성, 간결한 문법, 함수형 프로그래밍 지원, 스마트 캐스트, 위임, 코루틴 등의 기능은 자바보다 더 안전하고 효율적인 코드를 작성하는 데 큰 도움을 준다.</p>
<blockquote>
<p>그렇기에 자바에서 상속 문제를 어느 정도 해결해줄 거라 생각해서 찾아보게 됨</p>
</blockquote>
<h2 id="🍀-코틀린의-자바에서-상속-문제-해결-방법">🍀 코틀린의 자바에서 상속 문제 해결 방법</h2>
<p>코틀린(Kotlin)에서도 자바와 마찬가지로 상속을 지원하지만, 상속에 따른 문제를 줄이기 위해 몇 가지 언어적 특성을 제공한다. *<em>특히, 상속과 관련된 문제를 예방하거나 완화하기 위한 코틀린의 설계 철학은 자바보다 엄격하고 더 안전한 방향으로 나아가 있다. *</em>이런 특징들이 자바에서 발생할 수 있는 상속 문제들을 일부 해결해준다.</p>
<h3 id="1-기본적으로-클래스가-final">1) <strong>기본적으로 클래스가 <code>final</code></strong></h3>
<ul>
<li><p>코틀린에서는 모든 클래스가 <strong>기본적으로 <code>final</code></strong>로 선언된다. 즉, <strong>명시적으로 <code>open</code> 키워드를 사용하지 않는 한 클래스는 상속이 불가능</strong>하다.</p>
<p><strong>자바 예시</strong>:</p>
<pre><code class="language-java">class Animal {
    public void makeSound() {
        System.out.println(&quot;Animal makes a sound&quot;);
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println(&quot;Dog barks&quot;);
    }
}</code></pre>
<p><strong>코틀린 예시</strong>:</p>
<pre><code class="language-kotlin">open class Animal {
    open fun makeSound() {
        println(&quot;Animal makes a sound&quot;)
    }
}

class Dog : Animal() {
    override fun makeSound() {
        println(&quot;Dog barks&quot;)
    }
}</code></pre>
<p>코틀린에서는 상속을 사용하고 싶으면 <code>open</code> 키워드를 명시적으로 선언해야 한다. 이는 상속의 남용을 줄이고, 불필요한 상속을 통한 문제를 방지하는 데 도움을 준다.</p>
</li>
</ul>
<h3 id="2-sealed-클래스">2) <strong><code>sealed</code> 클래스</strong></h3>
<ul>
<li><p>코틀린의 <code>sealed</code> 클래스는 상속을 제한하는 또 다른 방법이다. <strong><code>sealed</code> 클래스는 같은 파일 내에서만 하위 클래스를 정의할 수 있게 제한</strong>하므로, 계층 구조를 명확히 정의하고 외부에서 임의로 확장하지 못하게 막는다.</p>
<p><strong>코틀린 예시</strong>:</p>
<pre><code class="language-kotlin">sealed class Animal {
    class Dog : Animal()
    class Cat : Animal()
}</code></pre>
<p>이 방식은 클래스 계층이 제한적이고, 의도된 사용에 따라만 하위 클래스를 만들 수 있도록 설계되어 상속 문제를 방지하는 데 도움을 준다. 이를 통해 클래스 계층의 예측 가능성을 높이고, 의도하지 않은 확장을 막을 수 있다.</p>
</li>
</ul>
<h3 id="3-data-클래스">3) <strong><code>data</code> 클래스</strong></h3>
<ul>
<li><p><strong><code>data</code> 클래스</strong>는 불변 객체를 쉽게 만들 수 있는 기능을 제공한다. 이는 상속보다 <strong>조합(Composition)</strong>을 사용하는 방향을 장려하며, 불필요한 상속 없이도 객체의 기능을 쉽게 관리할 수 있게 해준다.</p>
<p><strong>코틀린 예시</strong>:</p>
<pre><code class="language-kotlin">data class Person(val name: String, val age: Int)</code></pre>
</li>
</ul>
<p><code>data</code> 클래스를 통해 불변 객체를 만들고, 상속 대신 조합을 사용해 객체 간의 관계를 설계하도록 유도할 수 있다. 이는 상속으로 인한 리스코프 치환 원칙(LSP) 위반 문제를 방지할 수 있는 좋은 대안이다.</p>
<h3 id="4-인터페이스와-default-메서드-문제-해결">4) <strong>인터페이스와 <code>default</code> 메서드 문제 해결</strong></h3>
<ul>
<li>코틀린은 자바 8 이후 등장한 <strong>인터페이스의 <code>default</code> 메서드</strong>와 유사한 기능을 제공한다. 하지만 코틀린에서는 인터페이스의 메서드 충돌 문제가 더 명확하게 처리되며, 메서드 구현이 명시적이므로 상속 구조에서 발생할 수 있는 혼란을 줄인다.</li>
</ul>
<h3 id="5-코틀린의-by-키워드로-위임delegation">5) <strong>코틀린의 <code>by</code> 키워드로 위임(Delegation)</strong></h3>
<ul>
<li><p>코틀린에서는 상속을 사용하지 않고 <strong>위임(Delegation)</strong>을 통해 코드 재사용성을 높이는 기능을 제공한다. 이를 통해 <strong>상속 대신 객체의 기능을 다른 객체에 위임하는 방식으로 구조를 설계</strong>할 수 있다. 이 방식은 상속의 문제점인 리스코프 치환 원칙 위반을 피하는 데 도움을 준다.</p>
<p><strong>코틀린 예시</strong>:</p>
<pre><code class="language-kotlin">interface Sound {
    fun makeSound()
}

class Dog : Sound {
    override fun makeSound() {
        println(&quot;Dog barks&quot;)
    }
}

class Cat : Sound {
    override fun makeSound() {
        println(&quot;Cat meows&quot;)
    }
}

class Animal(sound: Sound) : Sound by sound</code></pre>
</li>
</ul>
<p>이래서 다들.. 코틀린 코틀린 하는 건가 싶음...</p>
<blockquote>
<p>📎 참고 글 </p>
</blockquote>
<ul>
<li><a href="https://inpa.tistory.com/entry/OOP-%F0%9F%92%A0-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5%EC%9D%98-%EC%83%81%EC%86%8D-%EB%AC%B8%EC%A0%9C%EC%A0%90%EA%B3%BC-%ED%95%A9%EC%84%B1Composition-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0">상속을 자제하고 합성을 이용하자</a></li>
<li><a href="https://bugoverdose.github.io/development/composition-over-inheritance/">상속 대신 조합</a></li>
<li>이펙티브 자바 </li>
</ul>