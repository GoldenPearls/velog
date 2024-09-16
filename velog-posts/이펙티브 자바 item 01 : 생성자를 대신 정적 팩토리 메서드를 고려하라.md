<h1 id="tmi">TMI</h1>
<p>저번주부터 이펙티브 자바스터디를 시작했다. 정리해오고 발표는 그때 그때 랜덤으로 돌리는 형식이며, 6만원 예치금에서 빠지면 2만원씩 차감이닼ㅋㅋㅋㅋㅋ </p>
<p>그래서 그런지 쫄리지만 <code>도파민</code> 도는 느낌 ~ 
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2aa09507-0ab7-4ff2-9bae-f1f99e232d89/image.png" /></p>
<p>열심히 해볼 예정임</p>
<blockquote>
<p><a href="https://github.com/JAVACAFE-STUDY/2024-effective-java">깃허브 REPO</a></p>
</blockquote>
<h1 id="item-01-생성자를-대신-정적-팩토리-메서드를-고려하라">item 01. 생성자를 대신 정적 팩토리 메서드를 고려하라</h1>
<blockquote>
<p><a href="https://mellona-log.gitbook.io/log/programming-lanuage/java/effective-java/item-01.">gitbook 정리 버전</a></p>
</blockquote>
<h2 id="1장-들어가기">1장 들어가기</h2>
<blockquote>
<p>이 책은 성능에 집중하는 부분은 많지 않다. 대신 프로그램을 명확하고, 정확하고, 유용하고, 견고하고, 유연하고, 관리하기 쉽게 짜는데 집중한다.</p>
</blockquote>
<p>기술 용어는 대부분 자바8용  언어 명세를 따르며, 자바가 지원하는 타입은 인터페이스(interface), 클래스(class), 배열(array), 기본 타입(primitive) 총 네 가지다.</p>
<h3 id="애너테이션anntation">애너테이션(anntation)</h3>
<p>인터페이스의 일종</p>
<h3 id="열거-타입enum">열거 타입(enum)</h3>
<p>클래스의 일종</p>
<h3 id="참조-타입reference-type">참조 타입(Reference type)</h3>
<p>인터페이스, 클래스, 배열</p>
<blockquote>
<p>즉, 클래스의 인스턴스와 배열은 <code>객체(object)</code>인 반면, 기본 타입 값은 그렇지 않다.&#x20;</p>
</blockquote>
<h3 id="클래스의-멤버">클래스의 멤버</h3>
<ol>
<li>필드(field)</li>
<li>메서드(method)</li>
<li>멤버 클래스</li>
<li>멤버 인터페이스</li>
</ol>
<p><code>메서드 시그니처</code>는 메서드 이름과 입력 매개변수(parameter)의 타입들로 이뤄진다.(반환값의 타입은 시그니처에 포함되지 않는다)</p>
<blockquote>
<p><strong>단, 일부 용어는 자바 언어 명세와 다르게 사용한다.</strong> 자바 언어 명세와는 달리 이 책은 상속(inheritance)을 서브클래싱(subclassing)과 동의로 쓴다.</p>
</blockquote>
<p>인터페이스 상속 대신</p>
<p>✔️ 클래스가 인터페이스를 <strong>구현한다(implemetent)</strong>;</p>
<p>✔️ 인터페이스가 다른 인터페이스를 <strong>확장한다(extend)</strong></p>
<h3 id="apiapplication-programming-interface">API(application programming interface)</h3>
<p>프로그래머가 클래스, 인터페이스, 패키지를 통해 접근할 수 있는 모든 클래스, 인터페이스, 생성자, 멤버, 직렬화된 형태(serialiozed form)을 말한다.</p>
<h4 id="사용자-user">사용자 (user)</h4>
<p>API를 사용하는 프로그램 작성자(사람)을  그 API의 사용자라고 함</p>
<h4 id="클라이언트client">클라이언트(client)</h4>
<p>API를 사용하는 클래스(코드)는 그 API의 클라이언트</p>
<h2 id="2장-객체-생성과-파괴">2장 객체 생성과 파괴</h2>
<blockquote>
<p>객체의 생성과 파괴를 다룬 2장으로, 객체를 만들어야 할 때와 만들지 말아야 할 때를 구분하는 방법 등을 알아봄</p>
</blockquote>
<h2 id="아이템-1--생성자-대신-정적-팩터리-메서드를-고려하라">아이템 1 : 생성자 대신 정적 팩터리 메서드를 고려하라</h2>
<p>클라이언트가 클래스의 인스턴스를 얻는 전통적인 수단은 <code>public 생성자</code>다.;</p>
<blockquote>
<p>하지만 1가지 더 클래스는 생성자와 별도로 <strong>정적 팩터리 메서드(static factory method)를 제공</strong>할 수 있다.;</p>
</blockquote>
<p>그 클래스의 인스턴스를 반환하는 단순한 <strong>정적 메서드</strong> 말이다.</p>
<h4 id="boolean-기본-타입의-박싱클래스인--boolean-예">boolean 기본 타입의 박싱클래스인  boolean 예</h4>
<blockquote>
<p>이 메서드는 기본 타입인 boolean 값을 받아 <strong>Boolean 객체 참조로 변환</strong>해 준다.</p>
</blockquote>
<pre><code>public static Boolean valusOf(boolean b){
    return b ? Boolean.TRUE : Boolean.FALSE;
}</code></pre><p>✅ 여기서 얘기하는 정적 팩터리 메서드인 패턴에서의 <code>팩터리 메서드(Factory Method)</code><strong>와 다른다.</strong> 디자인 패턴 중에는 이와 일치하는 패턴은 없다.</p>
<h4 id="만약-public-생성자를-사용한다면">만약, PUBLIC 생성자를 사용한다면,</h4>
<pre><code>public static Boolean valueOf(boolean b) {
    return new Boolean(b);  // 직접 객체를 생성
}</code></pre><h3 id="정적-팩터리-메서드가-생성자-좋은-장점-5가지">정적 팩터리 메서드가 생성자 좋은 장점 5가지</h3>
<h4 id="✔️-이름을-가질-수-있다">✔️ <strong>이름을 가질 수 있다.</strong></h4>
<p>생성자에 넘기는 매개변수와 생성자 자체만으로는 반환될 객체의 특성을 제대로 설명 못하지만, <strong>정적 팩토리의 경우, 이름만 잘 지으면 쉽게 묘사 가능</strong>하다.</p>
<p>뿐만 아니라, 하나의 시그니처로는 생성자를 하나만 만들 수 있다. <strong>생성자가 어떤 역할을 하는 지 정확히 기억하기 어려워</strong> 엉뚱한 것을 호출하는 실수를 할 수 있다.</p>
<p>그렇기 떄문에 이름을 가질 수 있는 정적 팩터리 메서드를 쓰는 것이 좋다. 이런 제약이 없기 때문이다.;</p>
<blockquote>
<p>한 클래스 에 시그니처가 같은 생성자가 여러 개 필요할 것 같으면, 생성자를 정적 팩터리 메서드로 바꾸고 각각의 차이를 잘 드러내는 이름을 지어주자</p>
</blockquote>
<h4 id="✔️-호출될-때마다-인스턴스를-새로-생성하지는-않아도-된다"><strong>✔️ 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.</strong></h4>
<p>덕분에 <a href="https://mellona-log.gitbook.io/log/programming-lanuage/java/undefined/undefined">불변 클래스(immutable class</a>； 아이템 17는 인스턴스를 미리 만들어 놓거나 새로 생성한 인스턴스를 캐싱하여 <code>재활용</code>하는 식으로 <strong>불필요한 객체 생성을 피할 수 있다.</strong></p>
<p>따라서（특히 생성 비용이 큰) 같은 객체가 자주 요청되는 상황 이라면 <strong>성능을 끌어올려 준다.</strong> <a href="https://api.velog.io/rss/@prettylee620#user-content-fn-1">플라이웨이트 패턴(Flyweight pattern)</a>[^1]도 이와 비슷한 기법이라 할 수 있다.</p>
<p><strong>인스턴스 통제（instance-controlled) 클래스</strong></p>
<p>반복되는 요청에 같은 객체를 반환하는 식으로 정적 팩터리 방식의 클래스는 <strong>언제 어느 인스턴스를 살아 있게 할지를 통제</strong>할 수 있다.</p>
<blockquote>
<p><strong>인스턴스를 통제하는 이유는?</strong>;</p>
</blockquote>
<ol>
<li><strong>클래스를 싱글턴으로 만들수도, 인스턴스화 불가로 만들 수도 있다.</strong></li>
</ol>
<ul>
<li><code>싱글턴 패턴(Singleton Pattern)</code></li>
</ul>
<p><strong>싱글턴 패턴</strong>은 <strong>클래스의 인스턴스가 오직 하나만 생성</strong>되도록 보장하는 디자인 패턴입니다. 특정 클래스의 객체가 하나만 존재해야 하거나, 동일한 자원에 대해 여러 객체가 동시에 접근할 필요가 없을 때 사용됩니다.</p>
<p>싱글턴 패턴을 사용하는 클래스는 <strong>private 생성자</strong>를 사용하여 외부에서 새로운 객체를 생성할 수 없도록 하고, 내부에서 하나의 객체만 생성하여 공유하는 방식으로 동작합니다. 이를 통해 메모리 낭비를 줄이고, 모든 호출자들이 동일한 인스턴스를 사용하게 됩니다.</p>
<pre><code class="language-java">public class Singleton {
    // 유일한 인스턴스
    private static final Singleton INSTANCE = new Singleton();

    // private 생성자: 외부에서 인스턴스화 금지
    private Singleton() {}

    // 유일한 인스턴스를 반환하는 메서드
    public static Singleton getInstance() {
        return INSTANCE;
    }
}</code></pre>
<p>위 코드에서 <code>getInstance()</code> 메서드를 통해 객체가 오직 한 번만 생성되며, 동일한 객체가 모든 호출자에게 반환됩니다. 이 패턴은 메모리를 절약하고, 불필요한 객체 생성을 방지하여 성능을 최적화할 수 있습니다.</p>
<ul>
<li><code>인스턴스화 불가</code></li>
</ul>
<p>어떤 클래스를 <strong>인스턴스화 불가능하게</strong> 만들려면, <strong>생성자를 private으로 선언</strong>하여 외부에서 그 클래스를 생성할 수 없도록 할 수 있습니다. 이는 특정 클래스가 <strong>유틸리티 클래스</strong>이거나, 그 자체로는 인스턴스화되지 않고 오직 static 메서드나 필드만 사용하도록 하기 위해 사용됩니다.</p>
<pre><code class="language-java">public class UtilityClass {
    // private 생성자: 인스턴스화를 금지함
    private UtilityClass() {
        throw new AssertionError(&quot;Cannot instantiate this class.&quot;);
    }

    // static 메서드
    public static void utilityMethod() {
        // 유틸리티 기능을 제공
    }
}</code></pre>
<p>위와 같이 생성자를 <code>private</code>으로 선언하여, <code>UtilityClass</code>는 인스턴스화될 수 없습니다. 이 클래스는 오직 <code>utilityMethod()</code> 같은 <strong>정적 메서드</strong>를 제공하는 데 사용됩니다.</p>
<ol start="2">
<li><strong>불변 값 클래스에서 동치인 인스턴스가 단 하나뿐임을 보장할 수 있다.( a == b때만, a.equals(b)가 성립)</strong></li>
</ol>
<p>불변 클래스(Immutable Class)는 객체가 생성된 이후 그 상태가 절대 변경되지 않는 클래스입니다. 불변 클래스를 설계할 때, <strong>동치인 인스턴스가 단 하나만 존재</strong>하도록 보장하는 것이 가능합니다. 이를 인스턴스 통제(instance control)라고 하며, <strong>같은 값을 가진 인스턴스는 항상 동일한 인스턴스</strong>를 반환하는 방식으로 구현할 수 있습니다.</p>
<p>이를 통해 <code>a == b</code>일 때만 <code>a.equals(b)</code>가 성립하도록 보장할 수 있습니다. 즉, <strong>값이 동일한 객체는 동일한 인스턴스</strong>를 사용하게 만들어서 메모리 낭비를 줄이고 성능을 향상시킵니다.</p>
<pre><code class="language-java">public final class Boolean {
    public static final Boolean TRUE = new Boolean(true);
    public static final Boolean FALSE = new Boolean(false);

    private final boolean value;

    private Boolean(boolean value) {
        this.value = value;
    }

    public static Boolean valueOf(boolean value) {
        return value ? TRUE : FALSE; // 이미 생성된 객체를 반환
    }
}</code></pre>
<p>위 코드에서 <code>Boolean</code> 클래스는 불변 클래스이며, <code>valueOf()</code> 메서드를 통해 <code>true</code> 또는 <code>false</code> 값에 따라 미리 정의된 <code>TRUE</code> 또는 <code>FALSE</code> 객체를 반환합니다. 이 방식은 <strong>값이 같으면 항상 같은 객체를 사용</strong>하므로, <code>a == b</code>가 <code>a.equals(b)</code>와 동일한 결과를 보장합니다.</p>
<ol start="3">
<li>인스턴스 통제는 플라이웨이트 패턴의 근간이 되며, 열거 타입은 인스턴스가 하나만 만들어짐 보장</li>
</ol>
<ul>
<li>&#x20;<code>플라이웨이트 패턴과 인스턴스 통제</code></li>
</ul>
<p>플라이웨이트 패턴(Flyweight Pattern)은 <strong>동일한 객체를 여러 번 생성하지 않고, 동일한 상태를 공유</strong>함으로써 메모리와 성능을 최적화하는 디자인 패턴입니다. 플라이웨이트 패턴에서 <strong>인스턴스 통제</strong>가 중요한 이유는, 객체 생성이 비용이 많이 드는 경우에 <strong>동일한 값의 객체가 여러 개 생성되는 것을 방지</strong>하여 메모리 낭비를 줄이는 것이 목표이기 때문입니다.</p>
<p>예를 들어, 많은 문자를 출력하는 텍스트 편집기에서 각 문자를 객체로 표현한다면, <strong>동일한 문자에 대해 매번 객체를 새로 생성하지 않고</strong> 하나의 객체를 재사용하도록 하여 메모리를 절약할 수 있습니다. 이때, <strong>동일한 값을 가진 객체는 항상 같은 인스턴스를 재사용</strong>하게 됩니다.</p>
<p>플라이웨이트 패턴의 핵심은 <strong>객체를 가능한 한 많이 공유</strong>하여 메모리 낭비를 줄이는 것입니다. <strong>인스턴스 통제</strong>는 이 패턴의 근간을 이루며, 이를 통해 객체 생성과 메모리 사용을 최적화합니다.</p>
<ul>
<li><code>열거형(enum)과 인스턴스 하나만 생성 보장</code></li>
</ul>
<p>자바에서 열거형(enum)은 자동으로 <strong>인스턴스 하나만 생성</strong>되도록 보장하는 구조를 가지고 있습니다. 열거형은 자바에서 <strong>싱글턴 패턴을 구현하는 가장 안전하고 간단한 방법</strong> 중 하나입니다.</p>
<p>열거형은 <strong>JVM에 의해 인스턴스가 한 번만 생성</strong>되며, 프로그램 내에서 해당 인스턴스를 재사용합니다. 따라서 각 열거형 상수는 <strong>하나의 인스턴스만 유지</strong>하며, 동일한 열거형 값에 대해서는 항상 같은 인스턴스가 반환됩니다.</p>
<pre><code class="language-java">public enum SingletonEnum {
    INSTANCE;

    public void someMethod() {
        // 동작 정의
    }
}</code></pre>
<p>위의 <code>SingletonEnum</code> 클래스는 자바에서 <strong>열거형으로 구현된 싱글턴</strong>입니다. <code>INSTANCE</code>는 프로그램 실행 중에 오직 하나의 인스턴스만 생성되어 사용됩니다. 따라서 <strong>열거형을 사용하면 인스턴스가 하나만 생성됨</strong>이 보장됩니다.</p>
<h4 id="요약">요약</h4>
<ol>
<li><strong>싱글턴 패턴</strong>: 클래스의 인스턴스를 오직 하나만 만들도록 보장하는 패턴.</li>
<li><strong>인스턴스화 불가 클래스</strong>: 클래스의 객체 생성을 막고 정적 메서드로만 사용되도록 하는 설계.</li>
<li><strong>불변 값 클래스의 동치성 보장</strong>: 동일한 값을 가진 인스턴스는 하나만 생성하여 <code>==</code> 비교가 가능하게 만드는 방법.</li>
<li><strong>플라이웨이트 패턴</strong>: 동일한 객체를 여러 번 생성하지 않고 재사용하여 메모리와 성능을 최적화하는 패턴.</li>
<li><strong>열거형(enum)</strong>: 자바에서 인스턴스를 하나만 생성하는 것을 보장하는 구조로, 싱글턴 패턴을 안전하게 구현하는 방법.</li>
</ol>
<blockquote>
<p>이 안에 있는 내용들은 뒤에 자세히 나옴</p>
</blockquote>
<h4 id="✔️-반환-타입의-하위-타입-객체를-반환할-수-있는-능력이-있다"><strong>✔️ 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.</strong></h4>
<p>이 능력은 반환할 객체의 클래스를 자유롭게 선택할 수 있는 <code>엄청난 유연성</code>을 선물한다. API를 만들 때 이 유연성을 응용하면 <strong>구현 클래스를 공개하지 않고도 그 객체를 반환할 수 있어 API를 작게 유지할 수 있다.</strong></p>
<p>자바 8 이전에는 인터페이스에 정적 메서드 사용 불가였음 자바 8부터 제한이 풀렸기 때문에 인스턴스화 불가 동반 클래스를 둘 이유가 없다. <strong>동반 클래스에 두었던 public 정적 멤버들 상당수를 그냥 인터페이스 자체에 두면 됨</strong></p>
<ul>
<li><strong>자바 8 이전</strong>: 인터페이스에 정적 메서드를 정의할 수 없어서, 정적 메서드는 동반 클래스(Companion Class)에 정의</li>
<li><strong>자바 8 이후</strong>: 인터페이스 자체에 <code>public static</code> 메서드를 정의할 수 있어서 동반 클래스가 더 이상 필요하지 않게 되었다.</li>
<li><strong>자바 9 이후</strong>: 인터페이스에 <code>private static</code> 메서드를 정의할 수 있게 되어, 인터페이스 내부에서만 사용되는 유틸리티 메서드를 구현할 수 있다.</li>
</ul>
<p><strong>자바 8 이전 코드 예시:</strong></p>
<pre><code class="language-java">// 인터페이스 정의
public interface MyInterface {
    void doSomething();
}

// 동반 클래스(Companion Class) - 정적 메서드 제공
public class MyInterfaceUtils {
    public static void printInfo() {
        System.out.println(&quot;MyInterface Utils method&quot;);
    }
}</code></pre>
<ul>
<li><code>MyInterface</code>에는 <code>doSomething()</code>이라는 추상 메서드가 정의되어 있지만, 정적 메서드는 정의할 수 없다.</li>
<li>정적 메서드를 사용하려면 별도의 유틸리티 클래스(<code>MyInterfaceUtils</code>)를 만들어 정적 메서드를 정의해야 했다.</li>
</ul>
<p><strong>사용 예시:</strong></p>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        // 동반 클래스의 정적 메서드 호출
        MyInterfaceUtils.printInfo();
    }
}</code></pre>
<p><strong>자바 8 이후 코드 예시:</strong></p>
<pre><code class="language-java">// 자바 8 이후 인터페이스에 정적 메서드 추가 가능
public interface MyInterface {
    void doSomething();

    // 정적 메서드 정의
    static void printInfo() {
        System.out.println(&quot;MyInterface static method&quot;);
    }
}</code></pre>
<ul>
<li>이제 <code>MyInterface</code> 안에 정적 메서드 <code>printInfo()</code>를 정의할 수 있다. 더 이상 동반 클래스를 만들어 정적 메서드를 관리할 필요가 없다.</li>
</ul>
<p><strong>사용 예시:</strong></p>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        // 인터페이스의 정적 메서드 호출
        MyInterface.printInfo();
    }
}</code></pre>
<h4 id="✔️-입력-매개변수에-따라-매번-다른-클래스의-객체를-반환할-수-있다"><strong>✔️ 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.</strong></h4>
<p>반환 타입의 하위 타입이기만 하면 어떤 클래스의 객체를 반환하든 상관없다. <strong>팩토리 메서드 패턴</strong>과 <strong>캡슐화</strong>를 활용하여 라이브러리의 내부 구현을 클라이언트(사용자)로부터 숨기고, 유연하게 클래스 설계를 변경할 수 있는 방법에 대한 예시로,&#x20;</p>
<blockquote>
<p><code>EnumSet</code> 클래스가 어떻게 작동하는지 설명하자면 아래와 같다. 참고로 <code>EnumSet</code> 클래스는 <strong>열거형(enum)</strong> 상수들을 집합으로 관리할 때 사용하는 <strong>고성능, 경량화된 Set 구현체</strong></p>
</blockquote>
<pre><code>public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

// 주중만 포함하는 EnumSet
EnumSet&lt;Day&gt; weekdays = EnumSet.of(Day.MONDAY, Day.TUESDAY, Day.WEDNESDAY, Day.THURSDAY, Day.FRIDAY);
</code></pre><ul>
<li><code>EnumSet</code> 클래스는 <strong>public 생성자 없이 정적 팩토리 메서드</strong>로만 인스턴스를 생성한다.</li>
<li><code>EnumSet</code>은 원소의 개수에 따라 두 가지 하위 클래스를 사용하여 성능을 최적화한다.<ul>
<li>원소가 <strong>64개 이하</strong>면, <code>RegularEnumSet</code>을 사용하여 <strong>long</strong> 변수를 하나만 사용해 원소를 관리한다.</li>
<li>원소가 <strong>65개 이상</strong>이면, <code>JumboEnumSet</code>을 사용해 <strong>long 배열</strong>로 원소를 관리한다.</li>
</ul>
</li>
<li><strong>클라이언트는</strong> 이 두 클래스(<code>RegularEnumSet</code>과 <code>JumboEnumSet</code>)의 존재를 <strong>모른다</strong>. 단지 <code>EnumSet</code> 인스턴스만 받는다.</li>
<li>만약 다음 릴리스에서 <code>RegularEnumSet</code>이 필요 없어진다면, 이를 <strong>삭제</strong>해도 클라이언트 코드에는 영향이 없다.</li>
<li>나아가, 성능을 더 개선한 새로운 클래스를 추가할 수도 있는데, 역시 클라이언트는 이를 <strong>알거나 고려할 필요가 없다</strong>.</li>
<li>중요한 점은, 클라이언트가 사용하는 객체가 어떤 구체적인 하위 클래스인지 <strong>알 필요가 없고</strong>, <strong>알지 않아도 제대로 작동</strong>한다는 것이다.</li>
</ul>
<blockquote>
<p>💬  풀어서 설명하자면,&#x20;</p>
</blockquote>
<ol>
<li><p><strong>정적 팩토리 메서드</strong>:</p>
<ul>
<li><code>EnumSet</code> 클래스는 <strong>public 생성자</strong>를 제공하지 않고, 대신 <strong>정적 팩토리 메서드</strong>만을 통해 객체를 생성합니다. 정적 팩토리 메서드는 객체를 생성하는 유연한 방법으로, 생성자와 달리 여러 가지 반환 타입을 제공하거나 캐싱을 통해 객체 생성을 제어할 수 있습니다.</li>
</ul>
<p>예를 들어, <code>EnumSet.of()</code> 같은 메서드를 사용해 <code>EnumSet</code>의 인스턴스를 생성할 수 있습니다. 여기서 중요한 점은 클라이언트가 객체를 생성할 때 어떤 특정 하위 클래스의 생성자를 호출하지 않는다는 것입니다. 그저 팩토리 메서드(<code>of()</code>)만 호출하여 <code>EnumSet</code>을 받을 뿐입니다.</p>
</li>
<li><p><strong>내부 구현의 캡슐화</strong>:</p>
<ul>
<li><code>EnumSet</code> 클래스는 내부적으로 <strong>두 가지 하위 클래스</strong>를 사용합니다. 이는 성능을 최적화하기 위해 사용되는 방법입니다.<ul>
<li><strong><code>RegularEnumSet</code></strong>: 원소의 개수가 <strong>64개 이하</strong>일 때 사용됩니다. 이 경우, 단일 <code>long</code> 변수를 사용해 64비트 내에서 원소들을 관리할 수 있으므로 메모리와 성능이 매우 효율적입니다.</li>
<li><strong><code>JumboEnumSet</code></strong>: 원소의 개수가 <strong>65개 이상</strong>일 때 사용됩니다. 이 경우, 단일 <code>long</code> 변수로는 모든 원소를 관리할 수 없으므로 <strong>long 배열</strong>을 사용하여 원소들을 관리합니다.</li>
</ul>
</li>
</ul>
<p>이 구조는 성능을 극대화하려는 목적에서 만들어졌지만, 클라이언트는 이 두 가지 하위 클래스의 존재를 전혀 알 필요가 없습니다. 클라이언트는 <code>EnumSet</code> 팩토리 메서드로 객체를 생성하지만, 실제로 어떤 구체적인 클래스(<code>RegularEnumSet</code> 또는 <code>JumboEnumSet</code>)가 반환되는지는 몰라도 괜찮습니다. 이것이 <strong>캡슐화</strong>의 핵심입니다.</p>
</li>
<li><p><strong>미래의 유연성</strong>:</p>
<ul>
<li>만약 추후 릴리스에서 <code>RegularEnumSet</code>을 더 이상 사용하지 않는다고 결정하면, 이를 삭제하더라도 클라이언트의 코드에는 영향을 주지 않습니다. 클라이언트는 <code>EnumSet</code> 팩토리 메서드를 사용해 객체를 생성하고, 반환된 객체가 구체적으로 어떤 하위 클래스인지는 중요하지 않기 때문입니다. 이처럼 내부 구현을 자유롭게 변경할 수 있는 유연성을 확보할 수 있습니다.</li>
<li>반대로, 새로운 성능 개선 기법을 적용한 세 번째, 네 번째 클래스를 추가하여도 클라이언트는 알 필요가 없습니다. 이는 라이브러리의 내부 구현이 클라이언트에게 <strong>투명하게</strong> 처리되기 때문에 가능합니다.</li>
</ul>
</li>
<li><p><strong>다형성의 활용</strong>:</p>
<ul>
<li><code>EnumSet</code>의 팩토리 메서드는 두 하위 클래스 중 하나를 반환하는데, 클라이언트는 그저 <strong>상위 타입인 <code>EnumSet</code>만 사용</strong>하게 됩니다. 이로 인해, 구체적인 하위 클래스의 존재를 몰라도 프로그램은 정상적으로 작동합니다. 다형성을 사용함으로써, 구체적인 구현에 대한 의존성을 제거하고, 내부 구현을 자유롭게 변경할 수 있게 됩니다.</li>
</ul>
</li>
</ol>
<p><strong>자바 8 이전 스타일: 동반 클래스가 없는 경우 (이 설명과 연관 없음)</strong></p>
<pre><code class="language-java">public enum Color {
    RED, GREEN, BLUE;
}

EnumSet&lt;Color&gt; set = EnumSet.of(Color.RED, Color.GREEN);</code></pre>
<p><strong>자바 8 이후 스타일: 내부적으로 두 하위 클래스를 사용하지만 클라이언트는 모름</strong></p>
<pre><code class="language-java">// 정적 팩토리 메서드 사용
EnumSet&lt;Color&gt; set = EnumSet.of(Color.RED, Color.GREEN);

// 내부에서의 구현 예시 (OpenJDK 내부적 처리)
if (enumConstants.length &lt;= 64) {
    return new RegularEnumSet&lt;&gt;(...);  // long으로 처리
} else {
    return new JumboEnumSet&lt;&gt;(...);    // long 배열로 처리
}</code></pre>
<ul>
<li>클라이언트는 <code>RegularEnumSet</code> 또는 <code>JumboEnumSet</code> 중 어떤 것을 사용하는지 알지 못합니다. 팩토리 메서드는 내부에서 가장 효율적인 구현체를 선택해 제공한다.</li>
</ul>
<h4 id="✔️-정적-팩터리-메서드를-작성하는-시점에는-반환할-객체의-클래스가-존재하지-않아도-된다"><strong>✔️</strong> 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.</h4>
<blockquote>
<p><strong>이런 유연함이 서비스 제공자 프레임워크를 만드는 근간이 되며, 서비스 제공자 프레임워크</strong>는 여러 종류의 서비스(또는 기능)를 다양한 방식으로 제공할 수 있도록 설계된 시스템이다. 이 프레임워크는 <strong>동적인 유연성</strong>을 제공하여, 특정한 구현체에 고정되지 않고 다양한 구현체를 선택하거나 교체할 수 있다. 자바에서 이 패턴은 <code>JDBC</code>와 같은 시스템에서 사용</p>
</blockquote>
<p>패턴의 <strong>세 가지 핵심 컴포넌트</strong></p>
<ol>
<li><strong>서비스 인터페이스 (Service Interface)</strong>:<ul>
<li>서비스 제공자가 구현해야 할 <strong>기능과 동작</strong>을 정의하는 인터페이스</li>
<li>예를 들어, JDBC에서 <strong>Connection</strong>이 서비스 인터페이스 역할을 한다. 모든 데이터베이스 드라이버는 이 인터페이스를 구현하여 <code>데이터베이스 연결</code>을 처리한다.</li>
</ul>
</li>
<li><strong>제공자 등록 API (Provider Registration API)</strong>:<ul>
<li>서비스 제공자가 자신의 구현체를 <strong>등록</strong>하는 데 사용하는 API</li>
<li>예를 들어, JDBC에서 <code>DriverManager.registerDriver()</code>가 <strong>제공자 등록 API 역할을 한다.</strong> 각 데이터베이스 드라이버는 자신을 이 API에 등록하여 클라이언트가 사용할 수 있게 만든다.</li>
</ul>
</li>
<li><strong>서비스 접근 API (Service Access API)</strong>:<ul>
<li>클라이언트가 서비스의 <strong>인스턴스를</strong> <strong>얻을 때 사용하는 API</strong>입</li>
<li>예를 들어, JDBC에서는 <code>DriverManager.getConnection()</code>이 서비스 접근 API로, 이 메서드를 통해 클라이언트는 특정 조건에 맞는 데이터베이스 연결 객체를 얻을 수 있다.</li>
<li>클라이언트는 이 API를 사용하여 특정한 조건에 맞는 구현체를 명시할 수도 있고, 그렇지 않으면 기본 구현체를 얻거나, 여러 구현체를 순차적으로 반환받을 수 있다.</li>
</ul>
</li>
</ol>
<p>이 패턴에는 <code>서비스 제공자 인터페이스(Service Provider Interface)</code>라는 <strong>네 번째 컴포넌트</strong>가 추가될 수 있다. 이 인터페이스는 각 서비스의 구현체를 생성하는 <strong>팩토리 객체</strong>로 사용된다. 이 컴포넌트가 없으면 구현체를 인스턴스화할 때 리플렉션(Reflection)을 사용해야 한다. 예를 들어, JDBC에서는 <code>Driver</code>가 서비스 제공자 인터페이스 역할을 한다. 이는 데이터베이스 연결 객체(<code>Connection</code>)을 생성하는 팩토리 역할을 수행한다.</p>
<p><strong>💬 자바의 예시 (JDBC)</strong></p>
<ul>
<li><strong>서비스 인터페이스</strong>: <code>Connection</code></li>
<li><strong>제공자 등록 API</strong>: <code>DriverManager.registerDriver()</code></li>
<li><strong>서비스 접근 API</strong>: <code>DriverManager.getConnection()</code></li>
<li><strong>서비스 제공자 인터페이스</strong>: <code>Driver</code></li>
</ul>
<p>JDBC는 자바에서 데이터베이스와 상호작용할 수 있는 표준 API입니다. 데이터베이스마다 다른 드라이버가 필요하지만, 이들은 모두 같은 <code>Connection</code> 인터페이스를 구현한다. 각 데이터베이스 드라이버는 <code>DriverManager</code>에 자신을 등록하여 클라이언트가 사용할 수 있게 된다.</p>
<p><strong>💬 변형 및 확장</strong></p>
<ol>
<li><strong>브리지 패턴(Bridge Pattern)</strong>: 서비스 접근 API는 서비스 제공자가 제공하는 것보다 더 많은 기능을 포함할 수 있으며, 이를 통해 더 풍부한 인터페이스를 클라이언트에 제공할 수 있다.</li>
<li><strong>의존성 주입(Dependency Injection)</strong>: 의존성 주입 프레임워크 또한 <strong>강력한 서비스 제공자 프레임워크</strong>의 변형으로 간주할 수 있다. 이 프레임워크는 객체 간의 의존성을 관리하고 주입해주는 시스템으로, 서비스 제공자의 역할을 수행한다.</li>
<li><strong><code>ServiceLoader</code> (자바 6부터 제공)</strong>: 자바 6부터는 <code>java.util.ServiceLoader</code>라는 범용 서비스 제공자 프레임워크가 제공된다. 이를 통해 직접 서비스 제공자 프레임워크를 만들 필요 없이 간편하게 구현체를 로드하고 사용할 수 있다.<ul>
<li><code>ServiceLoader</code>는 자바 애플리케이션에서 구현체를 찾고 로드하는 범용 메커니즘을 제공한다. 이를 통해 다양한 서비스 제공자가 존재하더라도 손쉽게 서비스를 사용하고 관리할 수 있다.</li>
</ul>
</li>
</ol>
<h4 id="장점">장점</h4>
<ul>
<li><strong>유연성</strong>: 특정 구현체에 의존하지 않고 다양한 구현체를 교체하거나 추가할 수 있어 유연한 설계가 가능</li>
<li><strong>확장성</strong>: 새로운 구현체를 추가하거나 기존 구현체를 변경해도 클라이언트 코드에 영향을 주지 않기 때문에 시스템 확장에 유리</li>
<li><strong>재사용성</strong>: 동일한 서비스 인터페이스를 구현한 여러 제공자를 재사용할 수 있어 코드 중복을 줄이고 유지보수를 쉽게 할 수 있다.</li>
</ul>
<blockquote>
<p>서비스 제공자 인터페이스(Service Provider Interface)는 종종 추가되는 네 번째 컴포넌트로, 서비스 인터페이스의 인스턴스를 생성하는 팩토리 역할을 한다. 자바에서는 <code>java.util.ServiceLoader</code>라는 범용 서비스 제공자 프레임워크가 제공됨</p>
</blockquote>
<h3 id="단점-2가지">단점 2가지</h3>
<h4 id="❌-상속을-하려면-public이나-protected-생성자가-필요하니-정적-팩터리-메서드만-제공하면-하위클래스를-만들-수-없다">❌ 상속을 하려면, public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위클래스를 만들 수 없다.</h4>
<blockquote>
<p>앞서 이야기한 컬렉션 프레임워크의 유틸리티 구현 클래스들은 상속할 수 없다는 이야기다</p>
</blockquote>
<p>어찌 보면 이 제약은 상속보다 <code>컴포지션</code>을 사용(아이템 18하도록 유도하고 불변 타입(아이템 17으로 만들려면 이 제약을 지켜야 한다는 점에서 오히려 장점으로 받아들일 수도 있다.</p>
<h4 id="❌-정적-팩터리-메서드는-프로그래머가-찾기-어렵다">❌ 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.</h4>
<p>API 문서를 잘 써놓고 메서드 이름도 널리 알려진 규약을 따라 짓는 식으로 문제를 완화해줘야 한다.</p>
<blockquote>
<p>이<strong>정적 메서드로 미리 정의</strong>되어 있는 것들</p>
</blockquote>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>예시</th>
</tr>
</thead>
<tbody><tr>
<td>from</td>
<td>매개변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형 변환 메서드.</td>
<td>Date d = Date.from(instant);</td>
</tr>
<tr>
<td>of</td>
<td>여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드.</td>
<td>Set faceCards = EnumSet.of(JACK, QUEEN, KING);</td>
</tr>
<tr>
<td>valueOf</td>
<td>from과 of의 더 자세한 버전.</td>
<td>BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);</td>
</tr>
<tr>
<td>instance / getInstance</td>
<td>매개변수로 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지 않음.</td>
<td>StackWalker luke = StackWalker.getInstance(options);</td>
</tr>
<tr>
<td>create / newInstance</td>
<td>instance 혹은 getInstance와 같지만, 매번 새로운 인스턴스를 생성해 반환함을 보장함.</td>
<td>Object newArray = Array.newInstance(classObject, arrayLen);</td>
</tr>
<tr>
<td>getType</td>
<td>getInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 사용. 'Type'은 반환할 객체의 타입.</td>
<td>FileStore fs = Files.getFileStore(path);</td>
</tr>
<tr>
<td>newType</td>
<td>newInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 사용. 'Type'은 반환할 객체의 타입.</td>
<td>BufferedReader br = Files.newBufferedReader(path);</td>
</tr>
<tr>
<td>type</td>
<td>getType과 newType의 간결한 버전.</td>
<td>List litany = Collections.list(legacyLitany);</td>
</tr>
</tbody></table>
<blockquote>
<p><strong>❗ 핵심 정리</strong></p>
<p>정적 팩터리 메서드와 public 생성자는 각자의 쓰임새가 있으니 상대적인 장단점을 이해하고 사용하는 것이 좋다. 그렇다고 하더라도 정적 팩터리를 사용하는 게 유리한 경우 가 더 많으므로 무작정 public 생성자를 제공하던 습관이 있다면 고치자.</p>
</blockquote>