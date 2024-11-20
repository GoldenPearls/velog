<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7e4a0766-f55c-41ba-86e8-666becf8897f/image.png" /></p>
<p>이펙티브 자바 스터디를 하고 있는데, 2주전까지의 파트는 <code>제네릭</code>이었음 보통 <strong>Controller 짤 때 Map에 때려 넣는 곳이 진짜 많은데 Map이랑 같이 제네릭</strong>을 많이 쓰는 것 같음 </p>
<p>그래서 한 번 공부하면 머리에 남지도 않으니 <strong>제네릭</strong>에 대한 것 전부 다 정리해보자 그리고 코틀린에서는 겸사겸사 제네릭 어떻게 쓰는지, 있는지도 알아보자.</p>
<h1 id="1-제네릭을-알아보기-전-공변과-불공변에-대해-알아보자">1. 제네릭을 알아보기 전, 공변과 불공변에 대해 알아보자.</h1>
<blockquote>
<p>배열은 공변이고, 제네릭은 불공변이다.공변은 자기 자신과 자식 객체로 타입 변환을 허용해주는 것이다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/dcc0dff9-b7a1-4a74-9ba5-73715bd97aa5/image.png" /></p>
<h2 id="🍂-먼저-java-타입-계층-구조-알아보기">🍂 먼저, Java 타입 계층 구조 알아보기</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/29e697a8-cbd4-48f1-8a50-e7f7707faa61/image.png" /></p>
<ol>
<li><strong>Object가 최상위 클래스</strong>  <blockquote>
<p>Java의 모든 클래스는 <code>Object</code>를 직접 또는 간접적으로 상속받는다. 이는 모든 참조 타입이 <code>Object</code> 타입으로 취급될 수 있음을 의미한다. </p>
</blockquote>
</li>
</ol>
<ul>
<li><code>String</code>, <code>Integer</code>, <code>Double</code>, <code>List</code>, <code>Map</code> 등 모든 참조 타입은 <code>Object</code> 타입의 변수에 할당 가능하다.</li>
<li>예:</li>
</ul>
<pre><code class="language-java">     Object obj = &quot;Hello&quot;;  // String -&gt; Object
     Object obj2 = 10;      // Integer -&gt; Object</code></pre>
<ol start="2">
<li><strong>기본 타입 (Primitive Types)</strong><br />Java에는 <code>int</code>, <code>double</code>, <code>boolean</code> 등 <strong>기본 타입</strong>이 있다. 이들은 <code>Object</code>를 직접 상속받지 않으며, <strong>래퍼 클래스</strong>(Wrapper Class)를 통해 간접적으로 <code>Object</code> 계층 구조에 참여한다.</li>
</ol>
<ul>
<li>예: <code>int</code> -&gt; <code>Integer</code>, <code>double</code> -&gt; <code>Double</code>.</li>
<li>래퍼 클래스는 기본 타입을 <code>Object</code> 타입으로 사용할 수 있도록 지원한다. 이를 <strong>오토박싱(Auto-boxing)</strong>이라고 한다.</li>
</ul>
<pre><code class="language-java">Object obj = 42;  // int는 Integer로 오토박싱되어 Object에 할당</code></pre>
<h2 id="🍂-공변이란convariant">🍂 공변이란(convariant)?</h2>
<p>A가 B의 하위 타입일 때, <code>T&lt;A&gt;</code>가 <code>T&lt;B&gt;</code>의 하위 타입이면 T는 공변이라고 한다. 타입 A가 B의 하위 타입(subtype)이라면, A[]는 B[]의 하위 타입이 될 수 있는 성질이다.</p>
<p>공변성은 <strong>서브타입 관계가 제네릭 타입에도 적용되는 것</strong>을 의미한다. 즉, <code>Integer</code>는 <code>Number</code>의 서브타입이므로, 공변성을 지원하는 경우 <code>List&lt;Integer&gt;</code>는 <code>List&lt;Number&gt;</code>로 처리될 수 있다.</p>
<pre><code class="language-java">List&lt;Number&gt; numbers = new ArrayList&lt;Integer&gt;(); // 컴파일 오류</code></pre>
<blockquote>
<p>하지만 결론만 먼저 말하면 제네릭은 서브타입을 지원하지 않기 때문에 이렇게 쓰면 안됨</p>
</blockquote>
<h3 id="배열의-공변성-예제">배열의 공변성 예제</h3>
<blockquote>
<p>배열은 공변성이 있으므로, 하위 타입의 배열을 상위 타입의 배열로 사용할 수 있다.</p>
</blockquote>
<pre><code class="language-java">@Test
void arrayCovarianceTest() {
    Integer[] integers = new Integer[]{1, 2, 3}; // Integer 배열 생성
    printArray(integers); // Integer[]를 Object[]로 전달 가능
}

void printArray(Object[] arr) {
    for (Object e : arr) {
        System.out.println(e); // 배열 요소 출력
    }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/79438a6d-ffa2-415c-855b-18b979699db0/image.png" /></p>
<p>위의 코드에서 <code>Integer[]</code>는 <code>Object[]</code>의 하위 타입으로 간주된다. 따라서 <code>printArray(Object[] arr)</code> 메서드에 <code>Integer[]</code>를 인자로 전달해도 문제가 발생하지 않는다.</p>
<h2 id="🍂-불공변이란invariant">🍂 불공변이란(invariant)?</h2>
<p>A가 B의 하위 타입일 때, <code>T&lt;A&gt;</code>가 <code>T&lt;B&gt;</code>의 하위 타입이 아니면, T는 불공변이라고 한다. 제네릭 타입 <code>List&lt;Object&gt;</code>와 <code>List&lt;Integer&gt;</code>가 있을 때, Integer가 Object의 하위 타입이더라도 <code>List&lt;Object&gt;</code>는 <code>List&lt;Integer&gt;</code>의 하위 타입이 아니다. </p>
<blockquote>
<p>불공변성은 <strong>제네릭 타입의 상속 관계가 명시적으로 정의되지 않는 한 유지되지 않는 것</strong>을 의미한다.</p>
</blockquote>
<p>즉, 제네릭 타입은 불공변성을 가진다고 말할 수 있다.</p>
<pre><code class="language-java">import org.junit.jupiter.api.Test;
import java.util.Arrays;
import java.util.Collection;
import java.util.List;

public class GenericInvarianceExample {

    @Test
    void genericInvarianceTest() {
        List&lt;Integer&gt; list = Arrays.asList(1, 2, 3); // List&lt;Integer&gt; 생성
        printCollection(list); // 컴파일 오류 발생
    }

    void printCollection(Collection&lt;Object&gt; c) { // Collection&lt;Object&gt; 파라미터
        for (Object e : c) {
            System.out.println(e); // 컬렉션 요소 출력
        }
    }
}
</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/27cbc863-8aa8-4319-9e7f-9bf0837efb47/image.png" /></p>
<h3 id="제네릭의-불공변성-예제">제네릭의 불공변성 예제</h3>
<blockquote>
<p>제네릭 타입은 불공변성을 가지므로, <code>List&lt;Integer&gt;</code>를 <code>List&lt;Object&gt;</code>로 사용할 수 없다.</p>
</blockquote>
<pre><code class="language-java">@Test
void genericInvarianceTest() {
    List&lt;Integer&gt; list = Arrays.asList(1, 2, 3); // List&lt;Integer&gt; 생성
    printCollection(list); // 와일드카드 타입으로 인해 호출 가능
}

void printCollection(Collection&lt;?&gt; c) {
    for (Object e : c) {
        System.out.println(e); // 컬렉션 요소 출력
    }
}</code></pre>
<p>위의 코드에서 <code>List&lt;Integer&gt;</code>는 <code>List&lt;Object&gt;</code>의 하위 타입이 아니기 때문에, <code>printCollection(Collection&lt;Object&gt; c)</code> 메서드에 <code>List&lt;Integer&gt;</code>를 전달하면 컴파일 오류가 발생한다.;</p>
<blockquote>
<p>제네릭 타입은 불공변성이기 때문에, <code>List&lt;Integer&gt;</code>와 <code>List&lt;Object&gt;</code>는 아무런 관계가 없다.</p>
</blockquote>
<p>이러한 제네릭의 불공변 때문에 와일드카드(제네릭의 ?타입)가 등장할 수 밖에 없었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6d706b49-d496-4e9b-bfee-fc3d08936973/image.png" /></p>
<h1 id="2-제네릭">2. 제네릭</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1a589092-6340-4dcd-ab3b-1b8584c6444d/image.png" /></p>
<h2 id="1-제네릭이란">1) 제네릭이란?</h2>
<p>자바에서 <strong>제네릭(Generics)은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미</strong>한다. 제네릭은 런타임 형변환 오류를 방지하기 위해, 자바 5(JDK 1.5)부터 도입되었다. 컴파일러가 안전하게 자동으로 형변환을 추가해줄 수 있게 되었다.</p>
<blockquote>
<p>객체별로 다른 타입의 자료가 저장될 수 있도록 한다.</p>
</blockquote>
<p>자바에서 배열과 함께 자주 쓰이는 자료형이 리스트(List)인데, 다음과 같이 클래스 선언 문법에 꺾쇠 괄호 <code>&lt;&gt;</code>로 되어있는 코드 형태가 있다.</p>
<pre><code class="language-java">ArrayList&lt;String&gt; list = new ArrayList&lt;&gt;();</code></pre>
<p><strong>꺾쇠 괄호가 바로 제네릭이다.</strong> 괄호 안에는 타입명을 기재한다. </p>
<blockquote>
<p>제네릭 형식: <code>클래스/인터페이스 이름&lt;실제 타입 매개변수&gt;</code></p>
</blockquote>
<p>그렇게 되면 저 리스트 클래스 자료형의 타입은 String 타입으로 지정되어 문자열 데이터만 리스트에 적재할 수 있게 된다.</p>
<p>아래 그림과 같이 배열과 리스트의 선언문 형태를 비교해보면 이해하기 쉬울 것이다. 선언하는 키워드나 문법 순서가 다를뿐, 결국 자료형명을 선언하고 자료형의 타입을 지정한다는 점은 같다고 볼 수 있다.</p>
<blockquote>
<p>이처럼 제네릭은 배열의 타입을 지정하듯이 리스트 자료형 같은 컬렉션 클래스나 메소드에서 사용할 내부 데이터 타입(type)을 파라미터(parameter) 주듯이 외부에서 지정하는 이른바 타입을 변수화 한 기능이라고 이해하면 된다.</p>
</blockquote>
<p>제네릭 타입을 하나 정의하면, 그에 딸린 로 타입(Raw Type)도 함께 정의된다.</p>
<h3 id="☄️-제네릭-타입-매개변수">☄️ 제네릭 타입 매개변수</h3>
<p>제네릭은 <code>&lt;&gt;</code> 를 사용하는데 이를 다이아몬드 연산자라고 한다. 그리고 이 꺾쇠 괄호 안에 <code>식별자 기호</code>를 지정함으로써 <strong>파라미터화 할 수 있다.</strong> 이것을 마치 메소드가 매개변수를 받아 사용하는 것과 비슷하여 <strong>제네릭의 타입 매개변수(parameter) / 타입 변수</strong> 라고 부른다.</p>
<pre><code class="language-JAVA">List&lt;T&gt; 타입 매개변수
List&lt;String&gt; stringList = new Array&lt;String&gt;(); //매개변수화된 타입
</code></pre>
<h4 id="☄️-타입-파라미터-정의">☄️ 타입 파라미터 정의</h4>
<p>타입 매개변수는 제네릭 클래스를 설계할 때 사용된다. 제네릭을 통해 코드의 타입 안정성을 높이고 반복적인 코드를 줄일 수 있다.</p>
<p><strong>예제: 제네릭을 사용한 클래스 정의</strong></p>
<pre><code class="language-java">class FruitBox&lt;T&gt; {
    List&lt;T&gt; fruits = new ArrayList&lt;&gt;();

    public void add(T fruit) {
        fruits.add(fruit);
    }
}</code></pre>
<ul>
<li><code>&lt;T&gt;</code>는 타입 매개변수이다. 클래스 내부에서 <code>T</code>를 타입처럼 사용할 수 있다.</li>
</ul>
<h4 id="타입-파라미터-사용-예시">타입 파라미터 사용 예시</h4>
<p>제네릭 클래스를 만들었다면, 실제 인스턴스를 생성할 때 타입을 지정해야 한다. 이때 타입 매개변수가 지정되면 해당 타입으로 모든 <code>T</code>가 대체된다. 이를 <code>구체화</code>라고 한다.</p>
<h4 id="예제-타입-매개변수-할당">예제: 타입 매개변수 할당</h4>
<pre><code class="language-java">// 정수 타입 할당
FruitBox&lt;Integer&gt; intBox = new FruitBox&lt;&gt;();

// 실수 타입 할당
FruitBox&lt;Double&gt; doubleBox = new FruitBox&lt;&gt;();

// 문자열 타입 할당
FruitBox&lt;String&gt; stringBox = new FruitBox&lt;&gt;();

// 클래스 타입 할당 (예: Apple 클래스)
FruitBox&lt;Apple&gt; appleBox = new FruitBox&lt;&gt;();</code></pre>
<ul>
<li>이런 방식으로 제네릭을 사용하면 타입 안정성이 확보된다.</li>
</ul>
<h4 id="타입-추론">타입 추론</h4>
<p>JDK 1.7 이후부터는 <strong>제네릭 객체를 생성할 때 오른쪽에 있는 타입 매개변수를 생략할 수 있다.</strong> 컴파일러가 타입을 추론하기 때문이다.</p>
<pre><code class="language-java">// 타입 매개변수 생략 전
FruitBox&lt;Apple&gt; appleBox = new FruitBox&lt;Apple&gt;();

// 타입 매개변수 생략 후
FruitBox&lt;Apple&gt; appleBox = new FruitBox&lt;&gt;();</code></pre>
<ul>
<li>컴파일러가 앞에서 지정된 타입을 보고 알아서 추론해준다.</li>
</ul>
<h4 id="제네릭에서-할당-가능한-타입">제네릭에서 할당 가능한 타입</h4>
<p>제네릭에서 할당할 수 있는 타입은 <strong>참조 타입(Reference Type)</strong>만 가능하다. </p>
<blockquote>
<p>즉, <code>int</code>, <code>double</code> 같은 <strong>기본 타입(Primitive Type)</strong>은 사용할 수 없다. 대신 <strong>래퍼 클래스(Wrapper Class)</strong>를 사용하면 된다.</p>
</blockquote>
<pre><code class="language-java">// Primitive 타입은 사용 불가
// List&lt;int&gt; intList = new ArrayList&lt;&gt;(); // 오류 발생

// Wrapper 클래스를 사용해야 함
List&lt;Integer&gt; integerList = new ArrayList&lt;&gt;();</code></pre>
<ul>
<li>기본 타입을 사용하려면 래퍼 클래스를 이용해야 한다.</li>
</ul>
<h4 id="제네릭과-다형성">제네릭과 다형성</h4>
<p>제네릭 타입도 객체 지향의 다형성 원리를 그대로 적용받는다. 부모 타입을 사용한 제네릭이라면, 그 자식 클래스 객체도 타입으로 넣을 수 있다.</p>
<p><strong>예제: 다형성 적용</strong></p>
<pre><code class="language-java">class Fruit {}
class Apple extends Fruit {}
class Banana extends Fruit {}

class FruitBox&lt;T&gt; {
    List&lt;T&gt; fruits = new ArrayList&lt;&gt;();

    public void add(T fruit) {
        fruits.add(fruit);
    }
}

public class Main {
    public static void main(String[] args) {
        FruitBox&lt;Fruit&gt; box = new FruitBox&lt;&gt;();

        // 다형성 적용: 부모 타입으로 자식 객체도 추가 가능
        box.add(new Fruit());
        box.add(new Apple());
        box.add(new Banana());
    }
}</code></pre>
<ul>
<li>이렇게 하면 다양한 타입의 객체를 한 번에 다룰 수 있다.</li>
</ul>
<h4 id="복수-타입-파라미터">복수 타입 파라미터</h4>
<p>제네릭 타입은 한 개만 쓰라는 법은 없다. </p>
<blockquote>
<p>여러 개의 타입이 필요하다면 <code>&lt;T, U&gt;</code> 같은 형식으로 여러 개를 쓸 수 있다.</p>
</blockquote>
<p><strong>예제: 복수 타입 파라미터</strong></p>
<pre><code class="language-java">class Apple {}
class Banana {}

class FruitBox&lt;T, U&gt; {
    List&lt;T&gt; apples = new ArrayList&lt;&gt;();
    List&lt;U&gt; bananas = new ArrayList&lt;&gt;();

    public void add(T apple, U banana) {
        apples.add(apple);
        bananas.add(banana);
    }
}

public class Main {
    public static void main(String[] args) {
        // 복수 제네릭 타입 사용
        FruitBox&lt;Apple, Banana&gt; box = new FruitBox&lt;&gt;();
        box.add(new Apple(), new Banana());
    }
}</code></pre>
<ul>
<li>여러 타입의 데이터를 동시에 다룰 수 있어 유용하다.</li>
</ul>
<h4 id="중첩-타입-파라미터">중첩 타입 파라미터</h4>
<p>제네릭 객체를 또 다른 제네릭 타입으로 쓸 수도 있다. 예를 들어, <code>ArrayList&lt;LinkedList&lt;String&gt;&gt;</code>처럼 말이다.</p>
<p><strong>예제: 중첩 타입 파라미터</strong></p>
<pre><code class="language-java">import java.util.ArrayList;
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        // LinkedList&lt;String&gt;을 원소로 저장하는 ArrayList
        ArrayList&lt;LinkedList&lt;String&gt;&gt; list = new ArrayList&lt;&gt;();

        LinkedList&lt;String&gt; node1 = new LinkedList&lt;&gt;();
        node1.add(&quot;aa&quot;);
        node1.add(&quot;bb&quot;);

        LinkedList&lt;String&gt; node2 = new LinkedList&lt;&gt;();
        node2.add(&quot;11&quot;);
        node2.add(&quot;22&quot;);

        list.add(node1);
        list.add(node2);

        System.out.println(list);
    }
}</code></pre>
<ul>
<li>이런 식으로 복잡한 자료 구조도 다룰 수 있다.</li>
</ul>
<p>ArrayList&lt;LinkedList&gt;는 중첩된 제네릭 타입으로, 이를 풀어서 설명하면 다음과 같은 뜻이다.</p>
<p><strong>ArrayList&lt;LinkedList&gt;</strong>는 <strong>ArrayList</strong>라는 타입의 객체이며, 그 안에 들어가는 원소들이 LinkedList 타입이다. 각 <strong>LinkedList</strong>는 String 타입의 요소들을 저장할 수 있는 연결 리스트이다.</p>
<p>이를 좀 더 구체적으로 설명하자면:</p>
<ul>
<li><strong>ArrayList&lt;LinkedList&gt;</strong>는 여러 개의 <strong>LinkedList</strong>를 담는 <strong>ArrayList</strong>이다.</li>
<li>각 <strong>LinkedList</strong>는 <strong>문자열(String)</strong>을 저장할 수 있다.</li>
</ul>
<p><strong>큰 상자(ArrayList)</strong>에 여러 개의 <strong>작은 상자(LinkedList)</strong>가 들어있고,
각 작은 상자에는 <strong>문자열(String)</strong>이 담겨 있다.</p>
<h4 id="타입-파라미터-네이밍-규칙">타입 파라미터 네이밍 규칙</h4>
<p>타입 파라미터의 기호는 정해진 게 없다. 하지만 보통 약속된 대로 사용하는 게 좋다. 예를 들어 <code>&lt;T&gt;</code>는 타입, <code>&lt;E&gt;</code>는 요소(Element)를 의미한다. 아래는 자주 쓰는 기호이다:</p>
<table>
<thead>
<tr>
<th>타입 기호</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>&lt;T&gt;</code></td>
<td>타입 (Type)</td>
</tr>
<tr>
<td><code>&lt;E&gt;</code></td>
<td>요소 (Element), 주로 컬렉션에서 사용</td>
</tr>
<tr>
<td><code>&lt;K&gt;</code></td>
<td>키 (Key), <code>Map&lt;K, V&gt;</code>에서 사용</td>
</tr>
<tr>
<td><code>&lt;V&gt;</code></td>
<td>값 (Value)</td>
</tr>
<tr>
<td><code>&lt;N&gt;</code></td>
<td>숫자 (Number)</td>
</tr>
<tr>
<td><code>&lt;S, U, V&gt;</code></td>
<td>여러 타입 매개변수를 사용할 때</td>
</tr>
</tbody></table>
<ul>
<li><code>&lt;T&gt;</code>는 타입을 의미하고, <code>&lt;E&gt;</code>는 컬렉션의 요소를 의미하는 등 상황에 맞게 네이밍을 사용하면 된다.</li>
</ul>
<p>위의 내용을 그림으로 정리하면 아래와 같다.
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3aa87833-c500-443d-bda5-4850a3e47c66/image.png" /></p>
<h2 id="2-제네릭의-등장-이전-및-도입-배경">2) 제네릭의 등장 이전 및 도입 배경</h2>
<p>제네릭(generic)은 자바 5부터 사용할 수 있다. 제네릭을 지원하기 전에는 컬렉션에서 <strong>객체를 꺼낼 때마다 형변환을 해야 했다.</strong> 그래서 누군가 실수로 엉뚱한 타입의 객체를 넣어두면 런타임에 형변환 오류가 나곤 했다. </p>
<blockquote>
<p>반면, *<em>제네릭을 사용하면 컬렉션이 담을 수 있는 타입을 컴파일러에 알려주게 된다. *</em></p>
</blockquote>
<p>그래서 컴파일러는 알아서 형변환 코드를 추가할 수 있게 되고, 엉뚱한 타입의 객체를 넣으려는 시도를 컴파일 과정에서 차단하여 더 안전하고 명확한 프로그램을 만들어 준다. *<em>꼭 컬렉션이 아니더라도 이러한 이점을 누릴 수 있으나, 코드가 복잡해진다는 단점이 따라온다. *</em></p>
<blockquote>
<p>제네릭이 도입되기 전에는 컬렉션의 요소를 다루는 <code>메서드(= 로 타입)</code>는 타입 안전성을 보장하지 못했다. </p>
</blockquote>
<p>컬렉션의 타입 매개변수를 명시할 수 없기 때문에, 모든 요소는 <code>Object</code> 타입으로 처리되었고, 타입 캐스팅이 필요한 상황에서 문제가 발생할 수 있었다.</p>
<p><strong>예시 1: 컬렉션 요소 출력</strong></p>
<pre><code class="language-java">void printCollection(Collection c) {
    Iterator i = c.iterator(); // 타입 지정 없이 Iterator 사용
    while (i.hasNext()) {
        System.out.println(i.next()); // 모든 요소는 Object 타입으로 간주
    }
}</code></pre>
<p>위 코드에서 컬렉션의 요소들은 <code>Object</code> 타입으로 취급되기 때문에, 특정 타입으로 다루려면 타입 캐스팅이 필요하다. 이는 런타임에 타입 에러를 발생시킬 수 있는 잠재적인 위험을 내포하고 있다.</p>
<p><strong>예시 2: 컬렉션 요소 합 구하기</strong></p>
<pre><code class="language-java">int sum(Collection c) {
    int sum = 0;
    Iterator i = c.iterator();
    while (i.hasNext()) {
        // 문제: 컬렉션의 요소가 Integer가 아닐 수도 있음
        sum += Integer.parseInt(i.next().toString()); // 런타임 오류 가능성
    }
    return sum;
}</code></pre>
<p>위 메서드는 <code>Collection</code>에 있는 요소들이 <code>Integer</code> 타입이라고 가정하고 작성된 것이다. 하지만 만약 <code>String</code>과 같은 다른 타입의 요소를 가진 컬렉션을 전달하면, 컴파일 시에는 문제가 없지만 런타임에 <code>ClassCastException</code>이 발생할 수 있다.</p>
<p>위와 같은 문제를 해결하기 위해 Java 개발자들은 타입을 지정하여 컴파일 시점에 타입 안전성을 보장할 수 있는 방법을 고안하였고, 그 결과 제네릭이 등장하게 되었다. </p>
<blockquote>
<p>제네릭을 사용하면, <strong>컬렉션이나 메서드에 타입 매개변수를 지정할 수 있어 컴파일 시점에 타입을 검사할 수 있다.</strong> 이렇게 하면 런타임 오류의 가능성을 줄이고, 코드의 안정성과 가독성을 높일 수 있다.</p>
</blockquote>
<h2 id="3-와일드카드의-등장-이유">3) 와일드카드의 등장 이유</h2>
<p>제네릭을 사용하면 컬렉션에 타입을 지정할 수 있어 컴파일 시점에 타입 안전성을 보장할 수 있다. 예를 들어, <code>Collection&lt;Integer&gt;</code> 타입을 사용하여 숫자들의 합을 구하는 메서드를 작성할 수 있다.</p>
<p><strong>수정된 코드 예제</strong></p>
<pre><code class="language-java">int sum(Collection&lt;Integer&gt; c) {
    int sum = 0;
    for (Integer e : c) { // Collection의 요소 타입을 Integer로 제한
        sum += e;
    }
    return sum;
}</code></pre>
<p>위 코드에서는 <code>Collection&lt;Integer&gt;</code> 타입을 사용하여, 컬렉션이 <code>Integer</code> 타입의 요소만 포함하도록 제한했다. <strong>컴파일 시점</strong>에 타입 검사가 이루어져, 다른 타입의 컬렉션이 전달되면 컴파일 오류가 발생한다. 이로써 <strong>타입 안전성을 보장</strong>할 수 있다.</p>
<p>제네릭 타입은 <code>불공변성</code>을 가진다. 즉, <code>Collection&lt;Integer&gt;</code>와 <code>Collection&lt;Object&gt;</code>는 아무런 관계가 없다. <strong>제네릭이 도입되기 전에는 가능했던 작업이 이제는 불가능해진 경우가 발생할 수 있다.</strong></p>
<p>아래와 같이 <code>printCollection</code> 메서드를 작성하고 <code>List&lt;Integer&gt;</code>를 전달하려고 하면, 컴파일 오류가 발생한다.</p>
<pre><code class="language-java">@Test
void genericTest() {
    List&lt;Integer&gt; list = Arrays.asList(1, 2, 3);
    printCollection(list); // 컴파일 오류: Collection&lt;Object&gt;는 Collection&lt;Integer&gt;와 호환되지 않음
}

void printCollection(Collection&lt;Object&gt; c) {
    for (Object e : c) {
        System.out.println(e);
    }
}</code></pre>
<blockquote>
<p><code>Collection&lt;Object&gt;</code>는 <code>Collection&lt;Integer&gt;</code>의 상위 타입이 아니기 때문에, 제네릭 타입에서는 서로 호환되지 않는다. </p>
</blockquote>
<p>이로 인해 <code>printCollection</code> 메서드에 <code>List&lt;Integer&gt;</code>를 전달하려고 하면 컴파일 오류가 발생한다. 이는 제네릭의 불공변성으로 인한 문제이다.</p>
<h3 id="☄️-와일드카드의-도입">☄️ <strong>와일드카드의 도입</strong></h3>
<p>위와 같은 문제를 해결하기 위해 와일드카드(<code>?</code>)가 도입되었다. 와일드카드를 사용하면 제네릭 타입을 보다 유연하게 사용할 수 있으며, 모든 타입의 컬렉션에서 공통으로 사용할 수 있는 메서드를 작성할 수 있다.</p>
<h3 id="☄️-와일드카드-타입-사용-예제">☄️ <strong>와일드카드 타입 사용 예제</strong></h3>
<pre><code class="language-java">void printCollection(Collection&lt;?&gt; c) {
    for (Object e : c) { // 와일드카드 타입으로 컬렉션의 요소를 다룸
        System.out.println(e);
    }
}

@Test
void genericTest() {
    List&lt;Integer&gt; list = Arrays.asList(1, 2, 3);
    printCollection(list); // 이제 컴파일 오류 없이 호출 가능
}</code></pre>
<blockquote>
<p><code>Collection&lt;?&gt;</code>는 비한정적 와일드카드 타입으로, 어떤 타입의 컬렉션이라도 인자로 받을 수 있다. </p>
</blockquote>
<p><code>List&lt;Integer&gt;</code>, <code>List&lt;String&gt;</code>, <code>List&lt;Object&gt;</code> 등 다양한 타입의 컬렉션을 모두 전달할 수 있어, 보다 유연한 메서드를 작성할 수 있다. 단, 와일드카드 타입에서는 컬렉션에 새로운 요소를 추가할 수 없고, <code>null</code>만 허용된다. 이는 타입 안전성을 유지하기 위함이다.</p>
<ul>
<li><code>Collection&lt;Object&gt;</code>는 <code>Collection&lt;Integer&gt;</code>의 상위 타입이 아니기 때문에, 제네릭 타입에서는 서로 호환되지 않는다. 이로 인해 <code>printCollection</code> 메서드에 <code>List&lt;Integer&gt;</code>를 전달하려고 하면 컴파일 오류가 발생한다.</li>
<li>이는 <strong>제네릭의 불공변성</strong>으로 인한 문제이다.</li>
</ul>
<blockquote>
<p>와일드 카드에 대한 설명 블로그 : <a href="https://mangkyu.tistory.com/241">https://mangkyu.tistory.com/241</a></p>
</blockquote>
<h1 id="3-로raw-타입이란">3. 로(raw) 타입이란?</h1>
<ul>
<li>제네릭 타입을 하나 정의하면, 그에 딸린 로 타입(Raw Type)도 함께 정의된다</li>
<li>제네릭이 도입되기 전에는 컬렉션의 요소를 다루는 메서드(= 로 타입)는 타입 안전성을 보장하지 못했다.</li>
</ul>
<p>위에서 저렇게 언급된 로 타입이란 뭘까?</p>
<h2 id="1-로-타입의-정의">1) 로 타입의 정의</h2>
<blockquote>
<p><strong>로 타입</strong>은 제네릭(Generic) 타입에서 타입 매개변수를 전혀 사용하지 않은 때를 말한다.   (ex)<code>List</code>). 또한 타입 선언에서 제네릭 타입 정보가 전부 지워진 것처럼 동작한다.</p>
</blockquote>
<h2 id="2-로-타입을-사용하면-문제가-뭘까">2) 로 타입을 사용하면 문제가 뭘까?</h2>
<p>로 타입의 단점을 나타내주는 몇 가지 예시를 들어보자.</p>
<pre><code class="language-java">// Stamp 인스턴스만 취급한다.
private final Collection stamps = ...;
stamps.add(new Coin(...));</code></pre>
<p>실수로 도장 대신 동전을 넣어도 오류 없이 컴파일 되고 실행되는 문제가 발생한다.</p>
<pre><code class="language-java">for(Iterator i = stamps.iterator(); i.hasNext(); ){
    Stamp stamp = (Stamp) i.next();  //ClassCastException
    stamp.cancle();
 }</code></pre>
<blockquote>
<p>오류는 이상적으로 <strong>컴파일할때 발견</strong>하는 것이 좋지만, 로 타입을 사용한다면 <strong>런타임에나 오류를 발견할 수 있다.</strong></p>
</blockquote>
<h2 id="3-제네릭-지원-이후에는">3) 제네릭 지원 이후에는?</h2>
<p>제네릭을 지원한 이후에는 매개변수화된 컬렉션 타입으로 타입 안전성을 확보한다. 제네릭을 사용하면 타입 선언 자체에 <strong>Stamp 인스턴스만 취급한다</strong>라는 것이 녹아든다.</p>
<pre><code class="language-java">private final Collection&lt;Stamp&gt; stamps = ...;
stamps.add(new Coin()); // 컴파일 오류 발생</code></pre>
<p><strong>컴파일 오류</strong>가 바로 발생한다. 컴파일러는 컬렉션에서 원소를 꺼내는 모든 곳에 보이지 않는 <code>형변환</code>을 <strong>추가</strong> 하여 절대 실패하지 않음을 보장한다.</p>
<blockquote>
<p>제네릭을 사용하여 컬렉션의 타입을 지정함으로써, 컴파일러가 타입 안전성을 보장할 수 있다.</p>
</blockquote>
<h2 id="4-로-타입raw-type과-제네릭-코드의-비교">4) 로 타입(Raw Type)과 제네릭 코드의 비교</h2>
<p><strong>로 타입을 사용한 코드</strong></p>
<pre><code class="language-java">import java.util.ArrayList;
import java.util.List;

public class RawTypeExample {
    public static void main(String[] args) {
        // 로 타입 사용
        List list = new ArrayList(); // 타입 매개변수를 지정하지 않음
        list.add(&quot;Hello&quot;);
        list.add(123); // 문자열과 숫자를 모두 추가할 수 있음

        // 컬렉션의 요소를 가져올 때마다 타입 캐스팅이 필요함
        String str = (String) list.get(0);
        Integer num = (Integer) list.get(1);

        System.out.println(str); // 출력: Hello
        System.out.println(num); // 출력: 123
    }
}</code></pre>
<p>위 예제에서 <code>List</code>는 로 타입으로 사용되었다. 이 경우, 리스트에 어떤 타입의 객체든 추가할 수 있기 때문에, 각 요소를 꺼낼 때 타입 캐스팅이 필요하다. 만약 잘못된 타입으로 캐스팅하려고 하면 <code>ClassCastException</code>이 발생할 수 있다.</p>
<p><strong>제네릭을 사용한 코드</strong></p>
<pre><code class="language-java">import java.util.ArrayList;
import java.util.List;

public class GenericTypeExample {
    public static void main(String[] args) {
        // 제네릭을 사용하여 List&lt;String&gt;으로 선언
        List&lt;String&gt; list = new ArrayList&lt;&gt;();
        list.add(&quot;Hello&quot;);
        // list.add(123); // 컴파일 오류: 정수는 추가할 수 없음

        // 타입 캐스팅이 필요 없음
        String str = list.get(0);

        System.out.println(str); // 출력: Hello
    }
}</code></pre>
<p>위 코드에서 <code>List&lt;String&gt;</code>은 제네릭 타입을 사용하여 선언되었다.&#x20;</p>
<blockquote>
<p>이제 이 리스트에는 <code>String</code> 타입만 저장할 수 있으며, 컴파일 시점에 타입 오류가 발생할 가능성을 줄일 수 있다. 요소를 가져올 때도 타입 캐스팅이 필요하지 않다.</p>
</blockquote>
<h3 id="5--왜-로-타입보다-제네릭을-사용해야-할까">5)  왜 로 타입보다 제네릭을 사용해야 할까?</h3>
<p>먼저 하나의 그림으로 정리해보면 사진과 같음</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0842a4e9-ba65-4a63-8ff5-d486d16cefb5/image.png" /></p>
<ol>
<li><strong>타입 안전성이 확보된다.</strong></li>
</ol>
<pre><code class="language-java">private final Collection&lt;Stamp&gt; stamps = ...;</code></pre>
<p>위 예제처럼 컴파일러가 <code>stamps</code> 에는 <code>Stamp</code> 의 인스턴스만 넣어야 함을 인지하기 때문에, 다른 엉뚱한 타입의 인스턴스는 컴파일 에러를 내뱉게 된다.</p>
<p>올바른 인스턴스라면 컴파일러는 컬렉션에서 원소를 꺼내는 모든 곳에 <strong>보이지 않는 형변환을 추가</strong>하기 때문에 그 이후부터는 정상적으로 작동할 것이다.</p>
<ol start="2">
<li><strong>로 타입은 제네릭이 안겨주는 안전성과 표현력이 없다.</strong></li>
</ol>
<p>하지만 그럼에도 로 타입이 존재하고 있는 것은, 로 타입을 사용하는 메서드에 매개변수화 타입의 인스턴스를 넘겨도 동작해야 했기 때문이다.</p>
<p>따라서 이러한 <strong>마이그레이션 호환성</strong>을 위해 로 타입을 지원하고 제네릭 구현에는 소거방식을 도입하게 된다. 소거 방식이란, 런타임에 타입 정보가 사라지는 것을 의미한다.</p>
<p>6) 로 타입은 권장되지 않는다(<code>List</code>와 <code>List&lt;Object&gt;</code>의 차이)</p>
<blockquote>
<p>로 타입을 쓰면 제네릭이 안겨주는 안전성과 표현력을 모두 잃게 된다. 제네릭이 등장하기 이전의 코드와의 <strong>호환성</strong>을 위해서 로 타입이 남겨져 있다.</p>
</blockquote>
<p><code>List</code>와 같은 로 타입은 권장하지 않지만 <code>List&lt;Object&gt;</code>는 괜찮다. 모든 타입을 허용한다는 의사를 컴파일러에게 명확하게 전달한 것이기 때문이다</p>
<blockquote>
<p>그렇다면 <code>List와 List&lt;Object&gt;의 차이</code>는 무엇일까?</p>
</blockquote>
<p><code>List</code>는 제네릭 타입과 무관한 것이고 <code>List&lt;Object&gt;</code>는 모든 타입을 허용한다는 것입니다.</p>
<p>다시 말해서 매개변수로 <code>List</code>를 받는 메서드에 <code>List&lt;String&gt;</code>을 넘길 수 있지만, 제네릭의 하위 규칙 때문에 <code>List&lt;Object&gt;</code>를 받는 메서드에는 매개변수로 넘길 수 없다.</p>
<p><code>List&lt;String&gt;</code>은 로 타입인 <code>List</code>의 하위 타입이지만 <code>List&lt;Object&gt;</code>의 하위 타입은 아니기 때문이다. 위의  공변  설명에서 함 그래서 <code>List&lt;Object&gt;</code>와 같은 매개변수화 타입을 사용할 때와 달리 <code>List</code>같은 로 타입을 사용하면 타입 안전성을 잃게 된다.</p>
<pre><code class="language-java">public static void main(String[] args) {
    List&lt;String&gt; strings = new ArrayList&lt;&gt;();

    unsafeAdd(strings, Integer.valueOf(42));
    String s = strings.get(0);
}

// 로 타입
private static void unsafeAdd(List list, Object o) {
    list.add(o);
}</code></pre>
<p>위의 코드는 컴파일은 성공하지만 로 타입인 <code>List</code>를 사용하여 <code>unchecked call to add(E) as a member of raw type List...</code> 라는 <strong>경고 메시지</strong>가 발생된다. 그런데 실행을 하게 되면 <code>strings.get(0)</code>의 결과를 형변환하려 할 때 <code>ClassCastException</code>이 발생한다. <strong>Integer를 String으로 변환하려고 시도했기 때문이다.</strong></p>
<blockquote>
<p>위 코드를 <code>List&lt;Object&gt;</code>로 변경하면?</p>
</blockquote>
<pre><code class="language-java">public static void main(String[] args) {
    List&lt;String&gt; strings = new ArrayList&lt;&gt;();

    unsafeAdd(strings, Integer.valueOf(42));
    String s = strings.get(0);
}

// List&lt;Object&gt;
private static void unsafeAdd(List&lt;Object&gt; list, Object o) {
    list.add(o);
}</code></pre>
<p>컴파일 오류가 발생하며 <code>incompatible types: List&lt;String&gt; cannot be converted to List&lt;Object&gt;...</code> 라는 메시지가 출력된다. 실행 시점이 아닌 컴파일 시점에 오류를 확인할 수 있어 보다 안전하다.</p>
<h1 id="4-제네릭의-한계-극복--와일드-카드">4. 제네릭의 한계 극복 : 와일드 카드</h1>
<p><strong>제네릭을 사용하는 이유</strong>는 타입 안전성을 보장하고, 코드의 가독성과 유지보수성을 높이기 위함이다.</p>
<blockquote>
<p>하지만 모든 상황에서 특정 타입을 명시할 수 없는 경우가 있기 때문에 비한정적 와일드카드(<code>?</code>)와 로 타입(Raw Type)이 존재한다.</p>
</blockquote>
<p>와일드카드는 Java의 제네릭 타입에서 유연성을 높이기 위해 도입된 기능으로, 제네릭 타입 매개변수를 특정하지 않고 사용할 수 있게 해준다. 주로 세 가지 형태로 사용되며, 각각의 의미와 사용법이 조금씩 다르다.</p>
<blockquote>
<p>사실 들어가기 전 한마디를 하자면, <strong>우리가 직접 코드를 짤 때 쓰는 것보다는 라이브러리나 클래스 열어보면 많이 정의되어 있는 것을 볼 수 있음.</strong> 즉 분석할 때 알고 있으면 도움이 많이 됨</p>
</blockquote>
<p>Java에서는 다음 세 가지 형태의 와일드카드를 사용할 수 있다.</p>
<ol>
<li><p>비한정적 와일드카드 (<code>?</code>)</p>
</li>
<li><p>상한 경계 와일드카드 (<code>? extends T</code>)</p>
</li>
<li><p>하한 경계 와일드카드 (<code>? super T</code>)</p>
</li>
</ol>
<p>이 세 가지 와일드카드는 서로 다른 상황에서 제네릭 타입의 유연성을 높이기 위해 사용된다.</p>
<h2 id="1-원소의-타입을-모른채-쓰고-싶다면-비한정적-와일드-카드-타입-set">1) 원소의 타입을 모른채 쓰고 싶다면? 비한정적 와일드 카드 타입 (<code>Set&lt;?&gt;</code>)</h2>
<ul>
<li>표기법: &lt;?&gt;</li>
<li><strong>비한정적 와일드카드 타입</strong>은 &quot;아무 타입이나&quot; 허용한다는 의미로, 제네릭 타입 매개변수가 무엇이든 상관없이 사용할 수 있도록 한다.</li>
<li>제네릭 타입의 안전성을 유지하면서도, 실제 타입 매개변수에 의존하지 않는 메서드를 작성할 수 있다.</li>
<li><code>Set&lt;?&gt;</code>와 같은 비한정적 와일드카드 타입은 <code>Set&lt;String&gt;</code>, <code>Set&lt;Integer&gt;</code> 등 어떤 타입의 <code>Set</code>이라도 사용할 수 있다.</li>
<li>사용 사례: 컬렉션의 원소 타입이 무엇인지 신경 쓰지 않고, 모든 타입의 컬렉션을 처리하고자 할 때 사용한다. 예를 들어, List&lt;?&gt;는 어떤 타입의 리스트든 받을 수 있다.</li>
<li>제약사항: 비한정적 와일드카드를 사용하는 컬렉션에는 null 외의 다른 값을 추가할 수 없다.</li>
</ul>
<pre><code class="language-java">public class TypeTest {
    private static void addToWildList(final List&lt;?&gt; list, final Object o) {
        // 컴파일 오류: 제네릭 타입에 의존성이 있음
        // list.add(o);

        // null은 허용됨
        list.add(null);
    }

    public static void main(String[] args) {
        List&lt;String&gt; list = new ArrayList&lt;&gt;();
        String s = &quot;kimtaeng&quot;;

        addToWildList(list, s); // Okay! 메서드 호출 자체는 문제없음
    }
}</code></pre>
<h2 id="2-불변성을-강조하며-안전한-읽기-작업에-적합한-상한-경계-와일드카드--extends-t">2) 불변성을 강조하며, 안전한 읽기 작업에 적합한 상한 경계 와일드카드 (<code>? extends T</code>)</h2>
<ul>
<li>표기법: &lt;? extends T&gt;</li>
<li>의미: 특정 타입 T와 그 하위 타입만을 허용한다.</li>
<li>사용 사례: 주로 읽기 전용 작업에 사용된다. 예를 들어, 특정 클래스의 하위 클래스 타입을 다룰 때 유용하다.</li>
<li>제약사항: 와일드카드 타입으로 컬렉션에 추가할 수 있는 요소의 타입이 불명확하므로, 컬렉션에 요소를 추가할 수 없다.</li>
</ul>
<pre><code class="language-java">
void printNumbers(List&lt;? extends Number&gt; list) {

    for (Number n : list) {

        System.out.println(n);

    }

}
</code></pre>
<p>위 코드에서 List&lt;? extends Number&gt;는 List, List 등 Number의 하위 타입을 인자로 받을 수 있다.</p>
<pre><code class="language-java">
public void read(Collection&lt;?&gt; list) {

        list.add(null);

    }
</code></pre>
<blockquote>
<p>읽기 전용이라는 게 파라미터로 와일드카드 타입인 컬렉션 받으면 add 가 Null 밖에 안되고 읽기만 가능해서 그렇다는 것 </p>
</blockquote>
<p><strong>?가 들어가면 결국 타입을 알수 없다는 건데 **<code>List&lt;? extends Number&gt; list = new ArrayList();</code>라는 정의가 있을 때 컴파일러는 list가 적어도 Number라는 건 알지만</strong> 실제로 어떤 타입인지 모르니까 그 다음에 list.add(1.0); 으로 Integer 아닌 값을 넣어도 타입을 몰라서 이부분까지 체크를 못해준다고 함** 타입이 다를 수 있는데 컴파일러가 체크해줄수 없어서 막아둔 듯 하다. 반대로 <code>하한제한</code>은 컴파일러가 타입 체크를 해줄 수 있어서 쓰기 작업도 허용해준다고 함</p>
<p>다시 말하면, 상한 제한인 한정적 와일드카드가 읽기 전용인 건 타입 안정성 때문인데 읽을 때는 상위 타입으로 처리하면 되지만 <code>?</code>는 *<em>실제로 어떤 타입이 들어가는지 알 수 없다는 거라서 그렇다고 함 *</em>List라고 해도 실제로 Double이 들어갈지 어떤 타입이 들어가는지 모르니까 타입 불일치가 있을수 있고 이건 컴파일타임에 체크할 수 없어서 막아두었다고 함</p>
<h2 id="3-가변성을-강조하며-안전한-추가-작업에-적합한-하한-경계-와일드카드--super-t">3) 가변성을 강조하며, 안전한 추가 작업에 적합한 하한 경계 와일드카드 (<code>? super T</code>)</h2>
<ul>
<li>표기법: &lt;? super T&gt;</li>
<li>의미: 특정 타입 T와 그 상위 타입만을 허용한다.</li>
<li>사용 사례: 컬렉션에 안전하게 요소를 추가할 수 있도록 보장한다. T와 그 상위 타입만을 허용하므로, 예를 들어 List&lt;? super Integer&gt;는 Integer, Number, Object 타입의 요소를 추가할 수 있다.</li>
<li>제약사항: <strong>요소를 읽을 때는 Object 타입으로 반환된다.</strong></li>
</ul>
<pre><code class="language-java">
void addIntegers(List&lt;? super Integer&gt; list) {

    list.add(10);

    list.add(20);

}
</code></pre>
<p>위 코드에서 List&lt;? super Integer&gt;는 List, List, List와 같은 상위 타입의 리스트를 인자로 받을 수 있으며, Integer 타입의 값을 추가할 수 있다.</p>
<h2 id="4-로-타입-set">4) 로 타입 (<code>Set</code>)</h2>
<ul>
<li><strong>로 타입</strong>은 제네릭 도입 이전의 컬렉션 타입으로, 타입 안전성을 보장하지 않는다.</li>
<li>로 타입을 사용할 경우, 어떤 타입의 객체든 추가할 수 있으며, 컴파일 시점에 타입 검사가 이루어지지 않아 런타임 오류의 가능성이 높다.</li>
<li>제네릭 타입의 타입 정보가 런타임에 지워지기 때문에 <code>Set&lt;String&gt;</code>과 <code>Set</code>은 동일하게 취급된다.</li>
</ul>
<pre><code class="language-java">public class TypeTest2 {
    public static void main(String[] args) {
        List raw = new ArrayList&lt;String&gt;(); // Okay! 로 타입은 타입 안전성을 제공하지 않음
        List&lt;?&gt; wildcard = new ArrayList&lt;String&gt;(); // Okay! 비한정적 와일드카드

        raw.add(&quot;Hello&quot;); // Okay! 로 타입은 어떤 타입의 원소도 추가 가능
        raw.add(1); // 컴파일러가 타입 검사를 하지 않기 때문에 가능
        // wildcard.add(&quot;Hello&quot;); // 컴파일 오류: 비한정적 와일드카드 타입은 null 외에 추가할 수 없음

        List&lt;String&gt; list = new ArrayList&lt;&gt;(); // 제네릭 타입 사용
        list.add(&quot;Hello&quot;); // String 타입의 원소만 추가 가능
        // list.add(1); // 컴파일 오류: 정수는 추가할 수 없음

        // 메서드 호출은 가능
        wildcard.size(); // Okay!
        wildcard.clear(); // Okay!
    }
}</code></pre>
<h2 id="5-와일드카드-사용-시-주의사항">5) 와일드카드 사용 시 주의사항</h2>
<ol>
<li><p>비한정적 와일드카드 (<code>?</code>)는 컬렉션의 타입 매개변수를 알 수 없으므로, 안전한 타입을 보장하기 위해 null 외의 값을 추가할 수 없다.</p>
</li>
<li><p>상한 경계 와일드카드 (<code>? extends T</code>)는 주로 읽기 전용 작업에 사용되며, 컬렉션에 <strong>요소를 추가하는 것은 불가능</strong>하다.</p>
</li>
<li><p>하한 경계 와일드카드 (<code>? super T</code>)는 안전하게 요소를 추가할 수 있지만, 요소를 읽을 때는** Object로 반환되므로 타입 캐스팅이 필요할 수 있다.**</p>
</li>
</ol>
<h2 id="6-로-타입과의-차이">6) 로 타입과의 차이</h2>
<ul>
<li><p>로 타입 (<code>List</code>)은 타입 안전성이 보장되지 않으며, 제네릭의 장점을 활용할 수 없다. 타입을 지정하지 않으면 컴파일 시점에 타입 오류를 검출할 수 없고, 런타임 오류가 발생할 수 있다.</p>
</li>
<li><p>와일드카드 (<code>List&lt;?&gt;</code>, <code>List&lt;? extends T&gt;</code>, <code>List&lt;? super T&gt;</code>)를 사용하면 제네릭의 타입 안전성을 유지하면서도, 유연한 타입 처리가 가능하다.</p>
</li>
</ul>
<h2 id="7-와일드카드-사용-시-유의점">7) 와일드카드 사용 시 유의점</h2>
<ul>
<li><p>와일드카드는 제네릭 메서드 작성 시 유용하며, 특히 라이브러리 설계에서 API의 유연성을 높이는 데 큰 도움이 된다.</p>
</li>
<li><p>클래스 리터럴에서는 로 타입을 사용해야 하며, List&lt;?&gt;.class나 List.class는 허용되지 않다.</p>
</li>
<li><p>instanceof 연산자와 함께 사용할 때도 로 타입을 사용해야 합니다. 제네릭 타입 정보는 런타임에 지워지기 때문ㅇ이다.</p>
</li>
</ul>
<pre><code class="language-java">
// 로 타입을 사용하여 instanceof 연산자 적용

if (o instanceof Set) {

    Set&lt;?&gt; set = (Set&lt;?&gt;) o;

}
</code></pre>
<h2 id="8-pecsproducer-extends-consumer-super-공식">8) PECS(Producer-Extends, Consumer-Super) 공식</h2>
<p>그렇다면 도대체 언제 super를 사용해야 하고, 언제 extends를 사용해야 하는지 헷갈릴 수 있다. 그래서 이펙티브 자바에서는 PECS라는 공식을 만들었는데, 이는 Producer-Extends, Consumer-Super의 줄임말이다. 즉, 컬렉션으로부터 와일드카드 타입의 객체를 꺼내서 생성하면(produce) extends를, 갖고 있는 객체를 컬렉션에 사용(consumer)하여 더하면 super를 사용하라는 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/68065ccf-b1c5-4f4b-acc0-f8ea368846d2/image.png" /></p>
<pre><code class="language-java">
void printCollection(Collection&lt;? extends MyParent&gt; c) {

    for (MyParent e : c) {

        System.out.println(e);

    }

}



void addElement(Collection&lt;? super MyParent&gt; c) {

    c.add(new MyParent());

}
</code></pre>
<p>printCollection 같은 경우에는 컬렉션으로부터 원소들을 꺼내면서 와일드카드 타입 객체를 생성(produce)하고 있다. 반대로 addElement의 경우에는 컬렉션에 해당 타입의 원소를 추가함으로써 객체를 사용(consume)하고 있다. 그러므로 와일드카드 타입의 객체를 <strong>produce하는 printCollection은 extends</strong>가, 객체를 <strong>consume하는 addElement에는 super가 적합한 것</strong>이다.</p>
<h2 id="9-로-타입과-비한정적-와일드카드-타입의-차이">9) 로 타입과 비한정적 와일드카드 타입의 차이</h2>
<table>
<thead>
<tr>
<th>특성</th>
<th>로 타입 (<code>Set</code>)</th>
<th>비한정적 와일드카드 (<code>Set&lt;?&gt;</code>)</th>
</tr>
</thead>
<tbody><tr>
<td><strong>타입 안전성</strong></td>
<td>보장되지 않음</td>
<td>보장됨</td>
</tr>
<tr>
<td><strong>타입 불변식 유지</strong></td>
<td>위반하기 쉬움</td>
<td>타입 불변식 유지</td>
</tr>
<tr>
<td><strong>원소 추가</strong></td>
<td>어떤 타입의 원소도 추가 가능</td>
<td><code>null</code> 외에는 추가할 수 없음</td>
</tr>
<tr>
<td><strong>메서드 호출</strong></td>
<td>타입에 관계없이 사용 가능</td>
<td>제네릭 타입에 의존하지 않는 메서드만 사용 가능</td>
</tr>
<tr>
<td><strong>사용 가능 상황</strong></td>
<td>하위 버전과의 호환성 필요 시, 클래스 리터럴, <code>instanceof</code></td>
<td>제네릭 타입에 의존하지 않는 메서드 작성 시</td>
</tr>
</tbody></table>
<h2 id="10-로-타입이-필요한-예외적인-상황">10) 로 타입이 필요한 예외적인 상황</h2>
<h3 id="☄️-클래스-리터럴">☄️ 클래스 리터럴</h3>
<p>제네릭 타입은 <strong>클래스 리터럴</strong>에서 사용할 수 없다. <code>List.class</code>와 같은 로 타입만 사용할 수 있으며, <code>List&lt;String&gt;.class</code>나 <code>List&lt;?&gt;.class</code>는 허용되지 않는다.</p>
<pre><code class="language-java">Class&lt;List&gt; listClass = List.class; // Okay!</code></pre>
<h3 id="☄️-instanceof-연산자">☄️ <code>instanceof</code> 연산자</h3>
<p>제네릭 타입 정보는 런타임에 제거되므로, <code>instanceof</code> 연산자는 로 타입이나 비한정적 와일드카드 타입에서만 사용할 수 있다. <code>Set&lt;?&gt;</code>을 사용해 타입 캐스팅을 할 수 있다.</p>
<pre><code class="language-java">if (o instanceof Set) {
    Set&lt;?&gt; s = (Set&lt;?&gt;) o; // 로 타입 대신 비한정적 와일드카드 타입으로 형변환
}</code></pre>
<h2 id="⭐-결론">⭐ 결론</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/12988b19-4cfd-4bd9-a0c6-d019b45744e9/image.png" />  </p>
<ul>
<li><p>비한정적 와일드카드 (<code>?</code>): 모든 타입을 허용하지만, 읽기 전용 작업에 적합하며 null 외에는 값을 추가할 수 없다.</p>
</li>
<li><p>상한 경계 와일드카드 (<code>? extends T</code>): 특정 타입의 하위 타입만 허용하며, 주로 읽기 전용 작업에 사용된다.</p>
</li>
<li><p>하한 경계 와일드카드 (<code>? super T</code>): 특정 타입의 상위 타입만 허용하며, 컬렉션에 안전하게 요소를 추가할 때 사용된다.</p>
</li>
</ul>
<p>와일드카드는 제네릭 타입의 유연성을 높이기 위한 중요한 도구이며, 각각의 와일드카드 타입을 적절히 사용하면 코드의 재사용성과 안전성을 동시에 확보할 수 있다. API의 확장느낌으로 클래스 등에서 자주 쓰임으로 알아두면 좋음</p>
<h1 id="⭐-전체-용어-정리--및-사용-코드">⭐ 전체 용어 정리  및 사용 코드</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1963a35d-d0f9-4651-a18d-2f7926c443a8/image.png" /></p>
<h2 id="1-매개변수화-타입-parameterized-type">1) 매개변수화 타입 (Parameterized Type)</h2>
<blockquote>
<p>타입 매개변수를 사용해 실제 타입으로 지정된 제네릭 타입</p>
</blockquote>
<pre><code class="language-java">List&lt;String&gt; list = new ArrayList&lt;&gt;(); // List의 타입 매개변수로 String을 지정
list.add(&quot;Hello&quot;); // String 타입의 요소를 추가</code></pre>
<h2 id="2-실제-타입-매개변수-actual-type-parameter">2) 실제 타입 매개변수 (Actual Type Parameter)</h2>
<blockquote>
<p>매개변수화 타입에서 구체적으로 지정된 타입 <code>List&lt;E&gt;</code></p>
</blockquote>
<pre><code class="language-java">// 매개변수화 타입에서 String이 실제 타입 매개변수
List&lt;String&gt; list = new ArrayList&lt;&gt;(); // 여기서 String이 실제 타입 매개변수로 사용됨</code></pre>
<h2 id="3-제네릭-타입-generic-type">3) 제네릭 타입 (Generic Type)</h2>
<blockquote>
<p>타입 매개변수를 가지는 클래스나 인터페이스 <code>E</code></p>
</blockquote>
<pre><code class="language-java">// 제네릭 클래스를 정의할 때 타입 매개변수 T를 사용
public class Box&lt;T&gt; {
    private T content; // T 타입의 변수를 선언

    public void setContent(T content) {
        this.content = content; // T 타입의 값을 설정
    }

    public T getContent() {
        return content; // T 타입의 값을 반환
    }
}

// Box 클래스를 사용하는 예제
Box&lt;Integer&gt; intBox = new Box&lt;&gt;(); // Integer 타입의 Box 생성
intBox.setContent(123); // Integer 값 설정
System.out.println(intBox.getContent()); // 출력: 123

Box&lt;String&gt; strBox = new Box&lt;&gt;(); // String 타입의 Box 생성
strBox.setContent(&quot;Hello, Generics&quot;); // String 값 설정
System.out.println(strBox.getContent()); // 출력: Hello, Generics</code></pre>
<h2 id="4-정규-타입-매개변수-formal-type-parameter">4) 정규 타입 매개변수 (Formal Type Parameter)</h2>
<blockquote>
<p>제네릭 타입 또는 제네릭 메서드에서 사용되는 타입 매개변수</p>
</blockquote>
<pre><code class="language-java">// 제네릭 클래스 Box의 정의에서 E가 정규 타입 매개변수
public class Box&lt;E&gt; {
    private E content; // E 타입의 변수를 선언

    public void setContent(E content) {
        this.content = content; // E 타입의 값을 설정
    }

    public E getContent() {
        return content; // E 타입의 값을 반환
    }
}</code></pre>
<h2 id="5-비한정적-와일드카드-타입-unbounded-wildcard-type">5) 비한정적 와일드카드 타입 (Unbounded Wildcard Type)</h2>
<blockquote>
<p>타입 매개변수를 <code>?</code>로 지정하여 어떤 타입이든 허용함 <code>List&lt;?&gt;</code></p>
</blockquote>
<pre><code class="language-java">// 와일드카드 타입을 사용한 메서드 정의
public void printList(List&lt;?&gt; list) {
    // List&lt;?&gt;는 어떤 타입의 리스트든 받을 수 있음
    for (Object elem : list) {
        // 와일드카드 타입이므로 요소를 Object로 취급
        System.out.println(elem);
    }
}

// 사용 예제
List&lt;String&gt; stringList = Arrays.asList(&quot;Apple&quot;, &quot;Banana&quot;, &quot;Orange&quot;);
List&lt;Integer&gt; intList = Arrays.asList(1, 2, 3);

printList(stringList); // 출력: Apple, Banana, Orange
printList(intList);    // 출력: 1, 2, 3</code></pre>
<h2 id="6-로-타입-raw-type">6) 로 타입 (Raw Type)</h2>
<blockquote>
<p>제네릭 타입에서 타입 매개변수를 사용하지 않은 형태 <code>List</code></p>
</blockquote>
<pre><code class="language-java">// 제네릭 타입의 타입 매개변수를 사용하지 않은 경우
List rawList = new ArrayList(); // 로 타입으로 정의
rawList.add(&quot;Hello&quot;); // String 타입의 값 추가
rawList.add(123);     // Integer 타입의 값 추가

// 로 타입 사용 시 컴파일러가 타입 안전성을 보장하지 않음
for (Object obj : rawList) {
    System.out.println(obj); // 출력: Hello, 123
}</code></pre>
<h2 id="7-한정적-타입-매개변수-bounded-type-parameter">7) 한정적 타입 매개변수 (Bounded Type Parameter)</h2>
<blockquote>
<p>특정 타입 또는 그 하위 타입으로 제한된 타입 매개변수  <code>&lt;E extends Number&gt;</code></p>
</blockquote>
<pre><code class="language-java">// 타입 매개변수 E가 Number 또는 그 하위 타입이어야 함
public &lt;E extends Number&gt; void printNumber(E number) {
    System.out.println(number); // Number 타입의 값을 출력
}

// 사용 예제
printNumber(123);     // 출력: 123 (Integer)
printNumber(45.67);   // 출력: 45.67 (Double)
// printNumber(&quot;Hello&quot;); // 컴파일 에러: String은 Number의 하위 타입이 아님</code></pre>
<h2 id="8-재귀적-타입-한정-recursive-type-bound">8) 재귀적 타입 한정 (Recursive Type Bound)</h2>
<blockquote>
<p>자기 자신을 타입 매개변수로 참조하는 타입 한정  <code>&lt;T extends Comparable&lt;T&gt;&gt;</code></p>
</blockquote>
<pre><code class="language-java">// T가 Comparable&lt;T&gt; 인터페이스를 구현해야 함
public class Node&lt;T extends Comparable&lt;T&gt;&gt; {
    private T value; // T 타입의 값을 저장
    private Node&lt;T&gt; next; // 다음 노드를 가리키는 포인터

    public Node(T value) {
        this.value = value; // 노드의 값을 설정
    }

    public T getValue() {
        return value; // 노드의 값을 반환
    }
}

// 사용 예제
Node&lt;Integer&gt; node = new Node&lt;&gt;(10); // Integer 타입의 노드 생성
System.out.println(node.getValue()); // 출력: 10</code></pre>
<h2 id="9-한정적-와일드카드-타입-bounded-wildcard-type">9) 한정적 와일드카드 타입 (Bounded Wildcard Type)</h2>
<blockquote>
<p>와일드카드 타입이 특정 타입 또는 그 하위/상위 타입으로 제한됨 <code>List&lt;? extends Number&gt;</code></p>
</blockquote>
<pre><code class="language-java">// Number 또는 그 하위 타입을 요소로 갖는 리스트를 인자로 받음
public void printNumbers(List&lt;? extends Number&gt; list) {
    for (Number num : list) {
        System.out.println(num); // Number 타입의 요소를 출력
    }
}

// 사용 예제
List&lt;Integer&gt; intList = Arrays.asList(1, 2, 3);
List&lt;Double&gt; doubleList = Arrays.asList(1.1, 2.2, 3.3);

printNumbers(intList);    // 출력: 1, 2, 3
printNumbers(doubleList); // 출력: 1.1, 2.2, 3.3</code></pre>
<h2 id="10-제네릭-메서드-generic-method">10) 제네릭 메서드 (Generic Method)</h2>
<blockquote>
<p>타입 매개변수를 사용하는 메서드 <code>static &lt;E&gt; List&lt;E&gt; asList(E[] a)</code></p>
</blockquote>
<pre><code class="language-java">// 제네릭 타입 매개변수를 사용하는 메서드 정의
public static &lt;E&gt; List&lt;E&gt; asList(E[] array) {
    return Arrays.asList(array); // 배열을 리스트로 변환하여 반환
}

// 사용 예제
String[] stringArray = {&quot;Hello&quot;, &quot;World&quot;};
List&lt;String&gt; stringList = asList(stringArray); // 제네릭 메서드를 사용하여 리스트 생성
System.out.println(stringList); // 출력: [Hello, World]</code></pre>
<h2 id="11-타입-토큰-type-token">11) 타입 토큰 (Type Token)</h2>
<blockquote>
<p>런타임에 제네릭 타입 정보를 제공하기 위해 사용하는 클래스 리터럴  <code>String.class</code></p>
</blockquote>
<pre><code class="language-java">// 런타임에 타입 정보를 얻기 위해 사용하는 타입 토큰
public &lt;T&gt; T createInstance(Class&lt;T&gt; clazz) throws Exception {
    // 클래스 타입 T를 기반으로 새로운 인스턴스를 생성
    return clazz.getDeclaredConstructor().newInstance();
}

// 사용 예제
String str = createInstance(String.class); // String 클래스의 인스턴스 생성
System.out.println(str); // 출력: 빈 문자열 (String의 기본 생성자 사용)</code></pre>
<h1 id="코틀린에서의-제네릭-자바의-단점을-다-커버해줄까">코틀린에서의 제네릭... 자바의 단점을 다 커버해줄까?</h1>
<h2 id="1-제네릭이란-1">1) 제네릭이란?</h2>
<p>코틀린에서도 제네릭은 자바와 마찬가지로 클래스나 함수가 다양한 타입을 처리할 수 있도록 한다. 코틀린의 제네릭은 자바보다 더 강력하고 간결한 문법을 제공한다.</p>
<h2 id="2-제네릭-클래스">2) 제네릭 클래스</h2>
<pre><code class="language-kotlin">// 제네릭 클래스 정의
class Box&lt;T&gt;(var value: T)

// 사용 예
val stringBox = Box(&quot;Hello&quot;)
println(stringBox.value)</code></pre>
<h2 id="3-제네릭-함수">3) 제네릭 함수</h2>
<pre><code class="language-kotlin">// 제네릭 함수 정의
fun &lt;T&gt; printArray(array: Array&lt;T&gt;) {
    for (element in array) {
        println(element)
    }
}

// 사용 예
val stringArray = arrayOf(&quot;A&quot;, &quot;B&quot;, &quot;C&quot;)
printArray(stringArray)</code></pre>
<h2 id="4-코틀린의-in과-out-키워드">4) 코틀린의 <code>in</code>과 <code>out</code> 키워드</h2>
<p>코틀린에서는 공변성(Covariance)과 반공변성(Contravariance)을 명시적으로 나타내기 위해 <code>in</code>과 <code>out</code> 키워드를 사용한다.</p>
<ul>
<li><p><strong><code>out</code> 키워드 (공변성)</strong>:</p>
<ul>
<li><code>T</code>를 반환하는 데 사용된다.</li>
<li>읽기 전용이다.</li>
<li>예: <code>Producer&lt;T&gt;</code>는 <code>T</code>를 생성하거나 반환한다.</li>
</ul>
<pre><code class="language-kotlin">class Box&lt;out T&gt;(val value: T) // T는 읽기 전용</code></pre>
</li>
<li><p><strong><code>in</code> 키워드 (반공변성)</strong>:</p>
<ul>
<li><code>T</code>를 입력받는 데 사용된다.</li>
<li>쓰기 전용이다.</li>
<li>예: <code>Consumer&lt;T&gt;</code>는 <code>T</code>를 소비한다.</li>
</ul>
<pre><code class="language-kotlin">class Box&lt;in T&gt; {
    fun setValue(value: T) { /* ... */ }
}</code></pre>
</li>
</ul>
<h2 id="5-와일드카드-대신-사용-">5) 와일드카드 대신 사용: <code>*</code></h2>
<p>코틀린은 자바의 <code>?</code> 와일드카드 대신 <code>*</code>을 사용하여 불특정한 타입을 나타낸다.</p>
<p>예:</p>
<pre><code class="language-kotlin">fun printList(list: List&lt;*&gt;) {
    for (item in list) {
        println(item)
    }
}</code></pre>
<h2 id="6-코틀린에서의-로-타입-raw-type">6) 코틀린에서의 로 타입 (Raw Type)</h2>
<p>자바에서는 제네릭 타입을 명시하지 않은 경우 <strong>로 타입 (Raw Type)</strong> 이라고 한다. 코틀린에서는 로 타입을 사용할 수 없으며, 항상 타입을 명시해야 한다. 따라서 타입 안정성을 보장하고, 컴파일 시에 타입 검사를 강제한다.</p>
<p>예를 들어, 자바에서는 다음과 같은 로 타입을 사용할 수 있다:</p>
<pre><code class="language-java">List list = new ArrayList(); // 로 타입 사용
list.add(&quot;Hello&quot;);
list.add(123); // 서로 다른 타입 추가 가능</code></pre>
<p>코틀린에서는 다음과 같이 타입을 명시해야 한다:</p>
<pre><code class="language-kotlin">val list: MutableList&lt;Any&gt; = mutableListOf() // 모든 타입을 허용하려면 Any 사용
list.add(&quot;Hello&quot;)
list.add(123)</code></pre>
<p>로 타입을 사용할 수 없기 때문에 코틀린에서는 제네릭 타입을 명확히 지정하여 타입 안정성을 높인다.</p>
<h2 id="자바와-코틀린-제네릭의-주요-차이점">자바와 코틀린 제네릭의 주요 차이점</h2>
<ul>
<li><p><strong>키워드 차이</strong>:</p>
<ul>
<li>자바: <code>? extends T</code>, <code>? super T</code></li>
<li>코틀린: <code>out T</code>, <code>in T</code></li>
</ul>
</li>
<li><p><strong>타입 소거 (Type Erasure)</strong>:</p>
<ul>
<li>자바: 런타임에 제네릭 타입 정보가 제거된다.</li>
<li>코틀린: 동일하게 타입 소거가 적용되지만, <code>reified</code> 키워드를 통해 런타임 타입을 유지할 수 있다.</li>
</ul>
<pre><code class="language-kotlin">inline fun &lt;reified T&gt; checkType(value: Any) {
    if (value is T) {
        println(&quot;Value is of type \${T::class.simpleName}&quot;)
    }
}</code></pre>
</li>
<li><p><strong>기본 타입</strong>:</p>
<ul>
<li>자바: 제네릭은 항상 참조 타입만 사용한다.</li>
<li>코틀린: <code>List&lt;Int&gt;</code>와 같은 기본 타입 제네릭을 지원한다.</li>
</ul>
</li>
<li><p><strong>로 타입 (Raw Type)</strong>:</p>
<ul>
<li>자바: 로 타입을 사용할 수 있다.</li>
<li>코틀린: 로 타입을 사용할 수 없으며, 항상 타입을 명시해야 한다.</li>
</ul>
</li>
</ul>
<h2 id="요약">요약</h2>
<p>자바는 강력하지만 복잡한 제네릭 문법을 사용하며, <code>?</code> 와일드카드와 <code>extends</code>/<code>super</code>로 타입을 제한한다. 코틀린은 간결한 문법 (<code>in</code>, <code>out</code>)과 <code>*</code>를 사용하며, <code>reified</code>를 통해 런타임에서도 제네릭 타입을 사용할 수 있는 이점이 있다. 코틀린에서는 로 타입을 사용할 수 없기 때문에 타입 안정성을 높이고, 컴파일 시 타입 검사를 강제한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/54836ea0-719b-4fe5-b25b-2908e8af7dfa/image.png" /></p>
<h1 id="주저리-주저리-🔥">주저리 주저리 🔥</h1>
<h2 id="왜-아직-자바-공화국인가🧐">왜 아직 자바 공화국인가...🧐</h2>
<p>결국 확실히.. 자바의 안 좋은 점 대부분은 코틀린이 잘 보완해준다는 것... 자바랑 거의 100% 호환도 된다는 데 심지어 파ㅊ님이라는 트친님이 말한 말 중 아래와 같은 말이 나오는 것 보면 호환 잘텐데...</p>
<blockquote>
<p>자바는 코틀린 바이너리를 디컴파일하면 나오는 언어입니다
보안 전문가들만 만지면 되는 거예요</p>
</blockquote>
<p>그런데 왜 아직 자바 공화국일까?</p>
<p>이유는 리팩토링 비용과 굳이 잘 돌아가는 것 건드려야 하는 이유가 없어서 일 것 같긴 함 자바가 지금 23까지 나왔는데 8버전을 쓰는 곳들이 대부분인 거보면.. 대체제가 있어도 안 써서 우리나라 백은 자바가 대부분 잡을 것 같긴 하다라는 생각이 듦</p>
<h2 id="제네릭-어디까지-알아야-할까-🙄">제네릭 어디까지 알아야 할까? 🙄</h2>
<p>제네릭은 <strong>쓰는 방법만 알고</strong> 와일드 카드 부분은 거의 쓰는 게 아니라 라이브러리 뜯어볼 때 참고용으로 알고 있는 정도로 공부하면 되지 않을까? 라는 생각이 들었음</p>
<p>그리고 스터디 시간에 이야기 나온 게 있는데 제네릭을 너무 많이 좋아하는 팀리더가 있을 경우, 팀 전체가 힘들어질 수 있다고 했었음 </p>
<p>결국..사실 제네릭이든 스트림이든 팀 컨벤션에 맞춰서 적절히 쓰는 게 정답이지 않을까 싶다..</p>
<blockquote>
<p>출처</p>
</blockquote>
<ul>
<li><a href="https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%A0%9C%EB%84%A4%EB%A6%ADGenerics-%EA%B0%9C%EB%85%90-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%B3%B5%ED%95%98%EA%B8%B0">자바 제네릭(Generics) 개념 &amp; 문법 정복하기</a></li>
<li><a href="https://madplay.github.io/post/dont-use-raw-types">[이펙티브 자바 3판] 아이템 26. 로 타입은 사용하지 말라</a></li>
<li><a href="https://mangkyu.tistory.com/241">[JAVA] 제네릭과 와일드카드 타입에 대해 쉽고 완벽하게 이해하기(공변과 불공변, 상한 타입과 하한 타입)</a></li>
<li><a href="https://velog.io/@semi-cloud/Effective-Java-%EC%95%84%EC%9D%B4%ED%85%9C-26-%EB%A1%9C-%ED%83%80%EC%9E%85%EC%9D%80-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EB%A7%90%EB%9D%BC">아이템 26</a></li>
<li><a href="https://github.com/woowacourse-study/2022-effective-java/blob/main/05%EC%9E%A5/%EC%95%84%EC%9D%B4%ED%85%9C_29/%EC%9D%B4%EC%99%95%EC%9D%B4%EB%A9%B4%20%EC%A0%9C%EB%84%A4%EB%A6%AD%20%ED%83%80%EC%9E%85%EC%9C%BC%EB%A1%9C%20%EB%A7%8C%EB%93%A4%EB%9D%BC.pdf">이왕이면 제네릭 타입으로 만들라</a></li>
<li><a href="https://kangmanjoo.tistory.com/136">https://kangmanjoo.tistory.com/136</a></li>
</ul>