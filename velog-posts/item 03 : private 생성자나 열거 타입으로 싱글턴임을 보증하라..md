<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3d686d48-9e5b-4219-b916-4643e462aef6/image.png" /></p>
<h2 id="싱글턴임을-보증하라">싱글턴임을 보증하라</h2>
<h3 id="싱글턴singleton이란">싱글턴(singleton)이란?</h3>
<ul>
<li>인스턴스를 오직 하나만 생성할 수 있는 클래스를 말한다.</li>
<li>전형적인 예로는 함수와 같은 무상태(stateless) 객체나 설계상 유일해야 하는 시스템 컴포넌트</li>
</ul>
<blockquote>
<p>클래스를 싱글턴으로 만들면 <strong>이를 사용하는 클라이언트를 테스트하기가 어려워질 수 있다.</strong></p>
</blockquote>
<p>이유는 타입을 <code>인터페이스</code><strong>로 정의한 다음 그 인터페이스를 구현해서 만든 싱글턴이 아니라면</strong> 싱글턴 인스턴스를 <strong>가짜(MOCK) 구현으로 대체할 수 없기 때문</strong>이다.</p>
<h3 id="싱글턴을-만드는-방식"><strong>싱글턴을 만드는 방식</strong></h3>
<blockquote>
<p>두 방식 모두 <strong>생성자는 private</strong>으로 감춰두고, 유일한 인스턴스에 접근할 수 있는 수단으로 <code>public static 멤버</code>를 하나 마련</p>
</blockquote>
<h3 id="방식-1---publioc-static-멤버가-final-필드인-방식">방식 1 :  publioc static 멤버가 final 필드인 방식</h3>
<pre><code class="language-java">public class Elvis {
    // 유일한 인스턴스를 생성
    public static final Elvis INSTANCE = new Elvis();

    // 생성자를 private으로 설정하여 외부에서 인스턴스를 생성하지 못하게 함
    private Elvis() {
        // 초기화 코드 (필요한 경우)
    }

    // Elvis가 떠나는 행동을 정의하는 메서드
    public void leaveTheBuilding() {
        // 구현 코드
    }
}</code></pre>
<p>private 생성자는 public static final 필드인 <strong>Elvis.INSTANCE를 초기화할 때 딱 한 번만 호출</strong>된다. public이나 protected 생성자가 없으므로 Elvis 클래스가 초기화될 때 만들어진 인스턴스가 전체 시스템에서 하나뿐임이 보장된다.&#x20;</p>
<h4 id="클라이언트-생성자-호출-방법">클라이언트 생성자 호출 방법</h4>
<ul>
<li><strong>리플렉션 API</strong>: Java의 리플렉션 API는 런타임에 클래스, 메서드, 필드 등의 정보를 동적으로 조사하고 조작할 수 있는 기능을 제공</li>
<li><strong>AccessibleObject.setAccessible</strong>: 이 메서드는 <code>private</code> 또는 <code>protected</code>로 설정된 필드나 메서드에 접근할 수 있게 해준다. 즉, 일반적으로 접근이 제한된 요소에 접근할 수 있도록 허용한다.</li>
<li>권한이 있는 클라이언트(예: 특정 설정이나 보안 권한을 가진 코드)는 리플렉션을 사용하여 <code>private</code> 생성자를 호출할 수 있다. 이 경우, 싱글턴 패턴의 의도가 무시되고, 여러 개의 인스턴스가 생성될 수 있다.</li>
</ul>
<blockquote>
<p>이러한 공격을 방어하려면, 생성자를 수정하여 <strong>두 번째 객체가 생성되려 할 때 예외</strong>를 던지게 하면 됨</p>
</blockquote>
<h4 id="장점">장점</h4>
<ul>
<li>public 필드 방식의 큰 장점은 해당 클래스가 싱글턴임이 API에 명백히 드러난다는 것이다.</li>
<li>public static 필드가 final이니 절대로 다른 객체를 참조할 수 없다.</li>
<li>간결하다.</li>
</ul>
<h3 id="방식-2--정적-팩터리-메서드를-public-static-멤버로-제공">방식 2 : 정적 팩터리 메서드를 public static 멤버로 제공</h3>
<pre><code class="language-java">public class Elvis {
    // 유일한 인스턴스를 생성
    private static final Elvis INSTANCE = new Elvis();

    // private 생성자
    private Elvis() {
        // 초기화 코드 (필요한 경우)
    }

    // 인스턴스를 반환하는 메서드(새로)추가됨
    public static Elvis getInstance() {
        return INSTANCE;
    }

    // Elvis가 떠나는 행동을 정의하는 메서드
    public void leaveTheBuilding() {
        // 구현 코드
    }
}
</code></pre>
<p><code>Elvis.getInstance</code> 는 항상 같은 객체의 참조를 반환하므로 제2의 Elvis 인스턴스란 결코 만들어지지 않다（역시 리플렉션을 통한 예외는 똑같이 적용된다）</p>
<h4 id="장점-1">장점</h4>
<ul>
<li>(마음이 바뀌면) <strong>API를 바꾸지 않고도 싱글턴이 아니게 변경할 수 있다는 점 :</strong> 유일하게 인스턴스를 반환하던 팩터리 메서드가 호출하는 스레드별로 다른 인스턴스를 넘겨주게 할 수 있음</li>
</ul>
<pre><code class="language-java">import java.util.HashMap;
import java.util.Map;

public class Elvis {
    // 인스턴스를 저장할 맵
    private static final Map&lt;Long, Elvis&gt; instances = new HashMap&lt;&gt;();

    // private 생성자
    private Elvis() {
        // 초기화 코드
    }

    // 정적 메서드: 스레드 ID를 기준으로 인스턴스를 반환
    public static Elvis getInstance() {
        long threadId = Thread.currentThread().getId();
        return instances.computeIfAbsent(threadId, id -&gt; new Elvis());
    }

    public void leaveTheBuilding() {
        // 행동 구현
    }
}</code></pre>
<ol>
<li><strong>인스턴스 저장소</strong>: <code>instances</code>라는 <code>Map</code>을 사용하여 각 스레드에 대한 인스턴스를 저장한다. 스레드 ID를 키로 사용한다.</li>
<li><strong>정적 메서드</strong>: <code>getInstance()</code> 메서드는 현재 스레드의 ID를 가져와서, 해당 스레드에 대한 인스턴스가 이미 존재하는지 확인한다. 존재하지 않으면 새 인스턴스를 생성하고 저장</li>
<li><strong>유연성</strong>: 이 구현은 API를 변경하지 않고도, 사용자가 원할 경우 스레드마다 다른 인스턴스를 반환할 수 있게 한다. 즉, 각 스레드는 독립적으로 <code>Elvis</code> 인스턴스를 가질 수 있다.</li>
</ol>
<ul>
<li>원한다면 정적 팩터리를 <code>제네릭 싱글턴 팩터리</code>로 만들 수 있다. : 정적 팩터리의 메서드 참조를 <code>공급자(supplier)</code>로 사용할 수 있다는 점이다.</li>
</ul>
<pre><code class="language-java">import java.util.function.Supplier;

public class Elvis {
    private static final Map&lt;Long, Elvis&gt; instances = new HashMap&lt;&gt;();

    private Elvis() {
        // 초기화 코드
    }

    public static Elvis getInstance(Supplier&lt;Elvis&gt; supplier) {
        long threadId = Thread.currentThread().getId();
        return instances.computeIfAbsent(threadId, id -&gt; supplier.get());
    }

    public void leaveTheBuilding() {
        // 행동 구현
    }
}

// 사용 예시
public class Main {
    public static void main(String[] args) {
        Elvis elvis = Elvis.getInstance(Elvis::new); // 공급자로서의 메서드 참조
        elvis.leaveTheBuilding();
    }
}</code></pre>
<blockquote>
<p>🧐  참고로 왜 API를 바꾸지 않고도 싱글턴을 변경하는 방법, API를 바꾸지 않고도 여러 인스턴스를 반환할 수 있도록 변경하는 것은 결국 <strong>코드를 바꾸는 건데 의미가 있어?</strong></p>
</blockquote>
<p><strong>AI  답변</strong></p>
<p>좋은 질문입니다. &quot;API를 바꾸지 않고도&quot;라는 표현은 기존 인터페이스(메서드 시그니처 등)를 유지하면서 내부 구현을 변경할 수 있다는 의미입니다. 즉, 외부에서 사용하는 코드에 영향을 주지 않고, 클래스의 동작 방식을 바꿀 수 있다는 점에서 의미가 있습니다.</p>
<h4 id="의미와-장점">의미와 장점</h4>
<ol>
<li><strong>호환성 유지</strong>: 기존 코드를 사용하는 다른 부분은 변경할 필요가 없으므로, 시스템의 안정성을 유지할 수 있습니다. 즉, 외부에서 <code>getInstance()</code> 호출 방식은 그대로 유지됩니다.</li>
<li><strong>유연성</strong>: 내부적으로 스레드별 인스턴스를 반환하는 방식으로 변경함으로써, 필요에 따라 여러 인스턴스를 제공할 수 있습니다. 이는 새로운 요구사항이 생길 때 유용합니다.</li>
<li><strong>확장성</strong>: 나중에 더 복잡한 로직이나 상태 관리가 필요할 때, API를 변경하지 않고도 기능을 추가하거나 수정할 수 있습니다.</li>
<li></li>
</ol>
<h4 id="예시">예시</h4>
<p>예를 들어, 기존에 <code>Elvis.getInstance()</code>를 사용하던 코드가 있다고 가정해 보겠습니다. 이 코드는 변경하지 않고도, 내부 구현을 통해 스레드별로 다른 인스턴스를 관리하게 할 수 있습니다.</p>
<pre><code class="language-java">Elvis elvis1 = Elvis.getInstance();
Elvis elvis2 = Elvis.getInstance();</code></pre>
<p>위 코드는 여전히 동일하게 작동하지만, 내부 구현에서는 이제 각 스레드에 대해 다른 <code>Elvis</code> 인스턴스를 제공하게 됩니다. 외부 코드는 전혀 변경되지 않지만, 내부 동작은 훨씬 더 유연해진 것입니다.</p>
<h4 id="결론">결론</h4>
<p>결론적으로, API를 변경하지 않고도 내부 구현을 수정하는 것은 코드의 유연성과 유지보수성을 높이는 좋은 방법입니다. 이는 장기적으로 시스템의 확장성과 안정성을 보장하는 데 큰 도움이 됩니다.</p>
<h3 id="싱글턴singleton-패턴을-구현하는-방법과-직렬화serialization-문제">싱글턴(Singleton) 패턴을 구현하는 방법과 직렬화(Serialization) 문제</h3>
<h4 id="1-직렬화와-싱글턴">1. 직렬화와 싱글턴</h4>
<ul>
<li><p>메모리 주소가 똑같은 한 개의 인스턴스만 있어야 하는데 직렬화 후 역직렬화를 하게 되면, 완전 다른 인스턴스가 생성되게 되버리는 거임</p>
</li>
<li><p><strong>Serializable 구현</strong>: 싱글턴 클래스를 직렬화하려면 <code>Serializable</code> 인터페이스를 구현해야 한다. 그러나 이 인터페이스를 구현하는 것만으로는 충분하지 않다.</p>
</li>
<li><p><strong>transient 필드</strong>: 모든 인스턴스 필드를 <code>transient</code>로 선언해야 하며, 이는 직렬화 시 해당 필드가 저장되지 않도록 한다.</p>
</li>
<li><p><strong>readResolve 메서드</strong>: 직렬화된 객체를 역직렬화할 때마다 새로운 인스턴스가 생성되는 것을 방지하기 위해 <code>readResolve</code> 메서드를 제공한다. 이 메서드는 역직렬화 과정에서 호출되어, 진짜 싱글턴 인스턴스를 반환하게 된다.</p>
<pre><code class="language-java">//싱글턴임을 보장해주는 readResolve 메서드
private Object readResolve() {    
    return INSTANCE; // 진짜 Elvis 인스턴스를 반환 가짜 Elvis는 가비지 컬렉터에게 
}</code></pre>
<p>이 메서드는 가짜 <code>Elvis</code> 인스턴스가 생성되는 것을 방지하고, 기존의 <code>INSTANCE</code>를 반환하여 원래의 싱글턴을 유지한다. 특정 클래스에서 사용할 수 있으며, 직렬화와 역직렬화를 지원하는 클래스에서 <code>readResolve</code> 메서드를 정의하면, 해당 클래스의 인스턴스가 역직렬화될 때 호출된다.</p>
</li>
</ul>
<blockquote>
<p>✔️  &quot;진짜 Elvis 인스턴스를 반환하고 가짜 Elvis는 가비지 컬렉터에게&quot;라는 표현</p>
<p>주로 싱글턴 패턴을 설명할 때 사용된다. 여기서 &quot;진짜 Elvis&quot;는 실제로 사용해야 하는 유일한 인스턴스를 의미하고, &quot;가짜 Elvis&quot;는 불필요하게 생성된 인스턴스를 의미합</p>
<p>이 문구는 <code>readResolve</code> 메서드의 역할을 강조한다. 역직렬화 과정에서 <code>readResolve</code> 메서드가 호출되면, 가짜 인스턴스가 아닌 진짜 인스턴스를 반환하여, 불필요한 인스턴스가 생성되는 것을 방지한다. 가짜 인스턴스는 더 이상 필요 없게 되어 가비지 컬렉터에 의해 수거될 수 있다. <strong>즉, 메모리 관리 측면에서 불필요한 객체를 제거하여 자원을 효율적으로 사용할 수 있게 된다.</strong></p>
</blockquote>
<h4 id="2-열거-타입을-이용한-싱글턴">2. 열거 타입을 이용한 싱글턴</h4>
<ul>
<li><p><strong>열거 타입</strong>: 싱글턴을 구현하는 세 번째 방법으로, 원소가 하나인 열거 타입을 사용하는 것입니다. 아래와 같이 선언할 수 있습니다.</p>
<pre><code class="language-java">public enum Elvis {    
    INSTANCE;  

    public void leaveTheBuilding() {        
    // 메서드 구현    
}}</code></pre>
</li>
<li><p><strong>장점</strong>:</p>
<ul>
<li><strong>간결함</strong>: 코드가 더 간단하고 이해하기 쉬워짐</li>
<li><strong>직렬화</strong>: 추가적인 노력 없이 자동으로 직렬화가 가능하며, 복잡한 직렬화 상황에서도 안전</li>
<li><strong>리플렉션 공격 방지</strong>: 리플렉션을 통해 새로운 인스턴스가 생성되는 것을 방지하며, 열거 타입은 자바에서 싱글턴 패턴을 안전하게 구현하는 방법으로 널리 권된다.</li>
</ul>
</li>
<li><p><strong>제한사항</strong>: 열거 타입은 다른 클래스를 상속할 수 없기 때문에, 싱글턴이 다른 클래스를 상속해야 할 경우에는 사용할 수 없다. 그러나 열거 타입은 다른 인터페이스를 구현할 수 있다.</p>
</li>
</ul>
<h4 id="결론-1">결론</h4>
<p>결론적으로, <code>readResolve</code> 메서드를 사용하여 직렬화 시 진짜 인스턴스를 반환함으로써 싱글턴을 보장하고, 원소가 하나인 열거 타입을 사용하여 간결하고 안전하게 싱글턴을 구현하는 방법이 있다. 이 두 가지 방법은 각각의 상황에 맞게 사용할 수 있으며, <strong>특히 열거 타입은 복잡한 직렬화와 리플렉션 공격에 대한 안전성을 제공하는 최선의 선택으로 여겨진다.</strong></p>
<p><strong>++ 스터디에 추가</strong></p>
<pre><code class="language-java">class Singleton {
    // 싱글톤 클래스 객체를 담을 인스턴스 변수
    private static Singleton instance;

    // 생성자를 private로 선언 (외부에서 new 사용 X)
    private Singleton() {}

    // 외부에서 정적 메서드를 호출하면 그제서야 초기화 진행 (lazy)
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton(); // 오직 1개의 객체만 생성
        }
        return instance;
    }
}</code></pre>
<p>제공하신 <code>Singleton</code> 클래스는 기본적인 싱글톤 패턴을 구현하고 있지만, 멀티스레드 환경에서 안전하지 않은 문제가 있다. 여러 스레드가 동시에 <code>getInstance()</code> 메서드를 호출할 경우, <code>instance</code>가 여러 번 초기화될 수 있는 위험이 있다.</p>
<p><strong>저 코드에서 문제</strong></p>
<ol>
<li>스레드는 없다고 판단을 하게 됨...결국 싱글톤을 만들기 위해 만들어진 코드인데. .싱글톤이 깨지게 된다는 것</li>
<li>getInstance에서 인스턴스가 없는데 인스턴스가 생성되는 걸 수도 있다.</li>
</ol>
<blockquote>
<p>해결방법</p>
</blockquote>
<h4 id="1-동기화synchronized-사용">1. 동기화(Synchronized) 사용</h4>
<p>가장 간단한 방법은 <code>getInstance()</code> 메서드에 <code>synchronized</code> 키워드를 추가하여 동기화하는 것입니다. 이렇게 하면 한 번에 하나의 스레드만 메서드에 접근할 수 있습니다.</p>
<pre><code class="language-java">public static synchronized Singleton getInstance() {
    if (instance == null) {
        instance = new Singleton();
    }
    return instance;
}</code></pre>
<pre><code class="language-java">class Singleton {
    // 싱글톤 클래스 객체를 담을 인스턴스 변수
    private static Singleton instance;

    // 생성자를 private로 선언 (외부에서 new 사용 X)
    private Singleton() {}

    // 외부에서 정적 메서드를 호출하면 그제서야 초기화 진행 (lazy)
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton(); // 오직 1개의 객체만 생성
        }
        return instance;
    }
}</code></pre>
<p>매번 동기화하면... 성능 문제가 생길 수 있음 모든 스레드가 동기화를 하게 됨..</p>
<h4 id="2-이중-검사-잠금double-checked-locking">2. 이중 검사 잠금(Double-Checked Locking)</h4>
<p>성능을 개선하기 위해 이중 검사 잠금을 사용할 수 있습니다. 이 방법은 <code>synchronized</code> 블록을 최소화하여 성능을 향상시킵니다</p>
<p><strong>여기서 질문?</strong></p>
<ul>
<li>if가 두 번 걸린 이유? <code>동기화</code>를 선택적으로 하기 위해? 처음 instance는 여러 스레드가 대기상태에 걸릴 수 있는데... 그 다음 부터 들어오는 스레드들은 대기 상태가 아니고 빠르게 넘어갈 수 있어서..?</li>
</ul>
<pre><code class="language-java">public static Singleton getInstance() {
    if (instance == null) {
        synchronized (Singleton.class) { //최신 값으로 동기화가 가능 
            if (instance == null) {
                instance = new Singleton();
            }
        }
    }
    return instance;
}</code></pre>
<pre><code class="language-java">class Singleton {
    private static volatile Singleton instance; // volatile 키워드 적용

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            // 메서드에 동기화 거는게 아닌, Singleton 클래스 자체를 동기화 걸어버림
            synchronized (Singleton.class) { 
                if(instance == null) { 
                    instance = new Singleton(); // 최초 초기화만 동기화 작업이 일어나서 리소스 낭비를 최소화
                }
            }
        }
        return instance; // 최초 초기화가 되면 앞으로 생성된 인스턴스만 반환
    }
}</code></pre>
<h4 id="3-정적-초기화static-initialization">3. 정적 초기화(Static Initialization)</h4>
<p>정적 초기화 블록을 사용하여 클래스가 로드될 때 인스턴스를 생성하는 방법도 있습니다. 이 방법은 스레드 안전하며, 간단하게 구현할 수 있습니다.</p>
<pre><code class="language-java">public class Singleton {
    private static final Singleton instance = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return instance;
    }
}</code></pre>
<pre><code class="language-java">class Singleton {

    private Singleton() {}

    // static 내부 클래스를 이용
    // Holder로 만들어, 클래스가 메모리에 로드되지 않고 getInstance 메서드가 호출되어야 로드됨
    private static class SingleInstanceHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingleInstanceHolder.INSTANCE;
    }
}</code></pre>
<ul>
<li>성능 이슈가 없어서 많이 사용함</li>
<li>동기화도 없기 때문에 대신 직렬화나 리플렉션 공격이 들어올 수 있다.</li>
</ul>
<h4 id="4-enum을-사용한-싱글톤">4. Enum을 사용한 싱글톤</h4>
<p>Java에서는 <code>enum</code>을 사용하여 싱글톤을 구현하는 방법도 있습니다. 이 방법은 직렬화와 리플렉션 공격에 대해 안전합니다.</p>
<pre><code class="language-java">public enum Singleton {
    INSTANCE;

    // 필요한 메서드 추가
    public void someMethod() {
        // ...
    }
}</code></pre>
<p>리플렉션까지 방어한 것</p>
<pre><code class="language-java">import java.io.ObjectStreamException;
import java.io.Serializable;

public class Singleton implements Serializable {

    // 직렬화 방지를 위해 serialVersionUID를 명시적으로 선언
    private static final long serialVersionUID = 1L;

    // 생성자에서 이미 객체가 생성된 경우 예외를 던져 Reflection을 통한 추가 인스턴스 생성을 방지
    private Singleton() {
        if (SingleInstanceHolder.INSTANCE != null) {
            throw new IllegalStateException(&quot;Singleton instance already created.&quot;);
        }
    }

    // static 내부 클래스를 이용한 Singleton 구현
    private static class SingleInstanceHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingleInstanceHolder.INSTANCE;
    }

    // 역직렬화 시 Singleton 보장 (기존 인스턴스를 반환)
    private Object readResolve() throws ObjectStreamException {
        return SingleInstanceHolder.INSTANCE;
    }
}</code></pre>
<p>####</p>