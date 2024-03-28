<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c45c6aa5-d29c-411d-accd-4c7107248a35/image.png" /></p>
<blockquote>
<p>예전에 작성한 독서 후기인 <a href="https://velog.io/@prettylee620/%ED%95%84%EB%8F%85-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%98%A8%EB%B3%B4%EB%94%A9-%EA%B0%80%EC%9D%B4%EB%93%9C-2%EC%9E%A5#4-%EC%A7%81%EC%A0%91-%EB%B6%80%EB%94%AA%ED%98%80%EB%B3%B4%EB%A9%B4-%EA%B9%A8%EB%8B%AB%EC%9E%90">필독 개발자 온보딩 가이드 2장</a>에 보면 NullPointException에 대한 설명을 적어뒀는데 자바 기본 다시 공부하면서 나와서 한  번 더 정리할 겸 정리해봄</p>
</blockquote>
<h1 id="nullpointexception">NullPointException</h1>
<h2 id="1-null이란">1. Null이란?</h2>
<p>택배를 보낼 때 제품은 준비가 되었지만, 보낸 주소지가 아직 결정되지 않아서, 주소지가 결정될 때까지는 주소지를 비워둬야 한다.</p>
<p>참조형 변수에는 항상 <strong>객체가 있는 위치</strong>를 가르키는 <code>참조값</code>이 들어간다. 그런데 아직 가리키는 대상이 없거나 가리키는 대상을 <strong>나중에 입력하고 싶다면? null을 넣어둘 수 있다.</strong></p>
<p>null은 값이 존재하지 않는, 없다는 뜻으로 만약 계속 인스턴스를 아무도 참조 하지 않는다면 <strong>JVM의 GC(가비지 컬렉션)</strong>가 <strong>더이상 사용하지 않는 인스턴스라 판단하고 해당 인스턴스를 자동으로 메모리에서 제거</strong>해준다.</p>
<h2 id="2-nullpointexception이란">2. NullPointException이란?</h2>
<p>택배를 보낼 때 주소지 없이 택배를 발송하면 어떤 문제가 발생할까? 택배가 제대로 도착을 못하겠지..? 만약 참조값이 없이 객체를 찾아간다면..? 
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4ae9bd99-55a1-48c6-9f63-e88527747f89/image.png" />
발생하는 것이 <code>NullPointException</code>    </p>
<h3 id="1-nullpointexception이라는-뜻">1) NullPointException이라는 뜻</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/985897f1-b97f-4079-bdd4-867fac24a4d8/image.png" /></p>
<blockquote>
<p>이름 그대로 null를 가르키다(Pointer)인데, 이때 발생하는 예외이다. <strong>null은 없다는 뜻</strong>이므로 <strong><em>결국 주소가 없는 곳을 찾아갈 때 발생하는 예외</em></strong></p>
</blockquote>
<p>객체를 참조할 때는 .(dot)를 사용한다. 참조값이 null이라면 값이 없다는 뜻으로, 찾아갈 수 있는 객체(인스턴스)가 없다. </p>
<blockquote>
<p><code>NullPointerException</code>은 이처럼 <strong>null에 .(dot)을 찍었을 때 발생</strong>한다.</p>
</blockquote>
<h3 id="2-멤버-변수와-null">2) 멤버 변수와 null</h3>
<ol>
<li>Data  클래스<pre><code class="language-java">package ref;
</code></pre>
</li>
</ol>
<p>public class Data{
    int value;
}</p>
<pre><code>2. BigData 클래스
```java
package ref;

public class BigData{
    Data data;
    int count;
}</code></pre><ol start="3">
<li><p>메인</p>
<pre><code class="language-java">package ref;
public class NullMain3 {
public static void main(String[] args) {
  BigData bigData = new BigData();
  System.out.println(&quot;bigData.count=&quot; + bigData.count);
  System.out.println(&quot;bigData.data=&quot; + bigData.data);
  //NullPointerException
  System.out.println(&quot;bigData.data.value=&quot; + bigData.data.value); 
}
}</code></pre>
</li>
<li><p>실행결과</p>
<pre><code>bigData.count=0
bigData.data=ref.Data@x002
bigData.data.value=0</code></pre></li>
<li><p>이유</p>
</li>
</ol>
<ul>
<li>bigData.count 를 출력하면 0 이 출력된다. (int count는 <code>기본 자료형</code>이라서 0으로 자동 초기화)</li>
<li>bigData.data 를 출력하면 참조값인 null 이 출력된다. 이 변수는 아직 아무것도 참조하고 있지 않다.(<code>참조형</code>은 null로 초기화 됨)</li>
<li>bigData.data.value 를 출력하면 data 의 값이 null 이므로 null 에 . (dot)을 찍게 되고, 따라서 참조 할 곳이 없으므로 NullPointerException 예외가 발생한다</li>
</ul>
<ol start="6">
<li>예외 발생 과정<pre><code>bigData.data.value
x001.data.value //bigData는 x001 참조값을 가진다.
null.value //x001.data는 null 값을 가진다.
NullPointerException //null 값에 .(dot)을 찍으면 예외가 발생한다</code></pre></li>
</ol>
<h4 id="해결방법">해결방법</h4>
<blockquote>
<p>Data 인스턴스를 만들고 BigData.data 멤버 변수에 참조값을 할당하면 된다.</p>
</blockquote>
<pre><code class="language-java">package ref;
public class NullMain4 {
 public static void main(String[] args) {
 BigData bigData = new BigData();
 bigData.data = new Data();
 System.out.println(&quot;bigData.count=&quot; + bigData.count);
 System.out.println(&quot;bigData.data=&quot; + bigData.data);
 System.out.println(&quot;bigData.data.value=&quot; + bigData.data.value);
 }
}</code></pre>
<h2 id="3-코드-동작을-이해하기-위해-다양한-실험을-해보자nullpointerexception-원인-파악하기">3. 코드 동작을 이해하기 위해 다양한 실험을 해보자(NullPointerException 원인 파악하기)</h2>
<blockquote>
<p>어떤 메소드가 호출이 된 것은 알겠는데 도대체 <strong>어떤 경로로 그 메소드가 호출됐는지 알아내지 못하는 경우</strong>가 있다. 이럴 때는 <code>예외</code>를 던지거나 <code>스택 트레이스</code>를 출력해보거나 아니면 <code>디버거</code>를 붙여 호출 경로를 살펴보는 등의 시도</p>
</blockquote>
<ul>
<li>여러 가지 시도를 해보며 코드가 어떻게 동작하는지 알아두자.</li>
</ul>
<h3 id="1-여기서-잠깐-스택-트레이스란">1) 여기서 잠깐! 스택 트레이스란?</h3>
<blockquote>
<p>출처
<a href="https://jaehoney.tistory.com/51">https://jaehoney.tistory.com/51</a>
<a href="https://okky.kr/articles/338405">https://okky.kr/articles/338405</a></p>
</blockquote>
<h4 id="개념">개념</h4>
<ul>
<li><p>프로그램이 시작된 시점부터 현재 위치까지의 메서드 호출 목록</p>
</li>
<li><p>예외가 어디서 발생했는지 알려주기 위해 JVM을 생성</p>
<h4 id="필요-이유">필요 이유</h4>
</li>
<li><p>스택 트레이스를 읽는 능력은 선택이 아닌 필수</p>
</li>
<li><p>무턱대고 오류내용을 복붙하고 해결을 위한 코드도 복붙한다면 직면한 문제는 해결할 수 있지만 발전 없이 머물러 있게 됨</p>
</li>
<li><p>강사님도 항상 강조하는 내용</p>
<h4 id="그렇다면-읽는-법">그렇다면 읽는 법?</h4>
<pre><code class="language-JAVA">public class StackTraceTest 
{
  public static void main(String[] args) 
  {
      one();
  }

  public static void one()
  {
      two();
  }

  public static void two()
  {
      three();
  }

  public static void three()
  {
      Integer.parseInt(&quot;abcde&quot;);
  }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0bc51219-6345-49e0-899d-cfc22c9ee627/image.png" /></p>
</li>
</ul>
<ol>
<li><p>스택트레이스는 에러가 발생된 시점부터 프로그램이 시작된 시점까지 거슬러 올라가면서 출력되기 때문에 <strong>먼저 실행된 메서드가 가장 아래</strong></p>
</li>
<li><p>나도 보려고 노력하지만 겁먹기 마련이다. 대부분 처음 시작하는 분들이 그렇더라 </p>
</li>
<li><p>하지만 에러의 진정한 원인은 가장 아래쪽(초기)에 있는 <code>Caused by:</code>로 시작되는 줄부터 아래로 세줄이면 충분</p>
<pre><code class="language-java">Caused by: java.lang.NullPointerException
  at com.mycompany.service.impl.PortalManagerImpl.deleteMenuItem(PortalManagerImpl.java:603)
  at com.mycompany.service.impl.PortalManagerImpl.deletePortal(PortalManagerImpl.java:358)</code></pre>
</li>
<li><p>위의 내용은 com.mycompany.service.impl.PortalManagerImpl' 클래스의 <code>deletePortal</code> 메소드 358라인에서 같은 클래스의 <code>deleteMenuItem</code>메소드를 호출했는데 해당 메소드 603번 째 줄에서 널포인터 예외가 발생했다라고 해석</p>
</li>
</ol>
<p><strong>okky의 질문</strong>
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/44408d1c-8078-468d-b5c6-1a9b2be04488/image.png" /></p>
<blockquote>
<p><strong>okky의 답변</strong>
<code>deleteMenuItem()</code>은 재귀 호출을 하는 메서드라서 혼동이 되신 것 같습니다. 스택트레이스의 인용하신 부분은 &quot;603번 째 줄에서 deleteMenuItem()을 호출할 때&quot;가 아니라 &quot;호출된 deleteMenuItem() 메서드의 내부의 603번 째 줄&quot;임</p>
</blockquote>
<p>🐇 <strong>좀 더 자세히 설명하자면,</strong>
deleteMenuItem() 메서드 내부에서 getMenuItems(item.getPortal().getId(), item.getId()) 메서드를 호출하려고 합니다. 이때, item이 null인 경우 NullArgumentException이 발생하고 예외가 던져집니다.</p>
<ol start="5">
<li><code>PortalManagerImpl</code> 클래스 소스<pre><code class="language-java">if (item == null) {
 throw new NullArgumentException(&quot;item&quot;);
}
</code></pre>
</li>
</ol>
<p>//중간 생략
List children = getMenuItems(item.getPortal().getId(), item.getId()); // 603번째 줄</p>
<p>for (PortalMenu child : children) {
    deleteMenuItem(child);
 }</p>
<p> ```</p>
<h3 id="2-nullpointerexception의-원인">2) NullPointerException의 원인</h3>
<ul>
<li>많은 수의 지원자들이 <code>children</code>이나 <code>item.getId()</code> 등에 널값이 들어간 것 같다고 답했다고 한다. 이론적으로 해당 라인에서 널값이 들어갈 수 있는 모든 경우의 수는,</li>
</ul>
<blockquote>
<ol>
<li>children</li>
<li>item</li>
<li>item.getPortal()</li>
<li>item.getPortal().getId()</li>
<li>item.getId()</li>
</ol>
</blockquote>
<ul>
<li>이 중 적어도 두 가지, 즉 2번 혹은 3번으로 가능성을 바로 좁히지 못한다면 그것은 널포인터 예외의 의미를 정확하게 파악하지 못하고 있기 때문이라고 한다.</li>
</ul>
<blockquote>
<p>널포인터 예외는 단순하게 변수에 널값이 들어가서 생기는 오류가 아니다. <code>널포인터 예외</code>는 <strong>명확하게 객체의 널레퍼런스에 대해 메소드 호출이나 필드 참조 등의 작업을 했을 때 발생하는 문제</strong>라는 것을 이해한다면 이런 문제는 곧바로 원인을 좁힐 수 있어야 한다.</p>
</blockquote>
<ul>
<li><p>즉, 1번의 경우처럼 단순히 변수에 널값을 할당하는 것만으로는 절대로 널포인터 예외가 날 수 없다. 그리고 만일 4 번 <code>item.getPortal().getId()</code>이나 5번 <code>item.getId()</code>이 널이라면 이는 널 레퍼런스에 대한 호출이 아니라 널값을 <code>getMenuItems</code>라는 <strong>메소드의 인자로 넘기는 것 뿐이기 때문에 역시 널포인터 예외의 원인이 될 수 없다.</strong></p>
</li>
<li><p>물론 <code>getMenuItem</code> 메소드 안에서 <strong>해당 인자에 대한 널체크 없이 값을 사용하다가 예외가 날 수도 있겠지만</strong> 이 경우엔 절대로 트레이스 상에 <strong>굵은 글자로 표시된 603번 째에서 예외를 뿌리지 않는다.</strong></p>
</li>
<li><p>그렇다면 남은 가능성은 2번 'item'이 널이거나 3번 'item.getPortal()'이 널인 경우뿐인데, 'item' 변수는 위에서 널체크를 하기 때문에 603번 째 줄에서 절대로 널값을 가질 수 없다. 그렇기 때문에 답은 3번이 되는 것</p>
</li>
</ul>
<h3 id="3-읽어보면-좋은-글">3) 읽어보면 좋은 글</h3>
<p><a href="https://okky.kr/questions/311337">개발은 암기과목이 아닙니다</a></p>
<h3 id="4-논외-visual-studio와-visual-studio-code">4) 논외 Visual Studio와 Visual Studio Code</h3>
<blockquote>
<p>스택 트레이스 를 읽는 법을 찾다가 알게 된 것인데... 둘은 완전히 다르다는 것
Visual Studio는 IDE(통합 개발 환경)이며 Visual Studio Code는 Sublime Text 및 Atom과 같은 리치 텍스트 편집기로
도구 간의 차이점은 IDE와 텍스트 편집기 그 이상이라고 한다.
IDE는 코드 작성, 편집, 디버깅 및 실행을 위한 강력한 도구로 텍스트 편집기에서는 코드를 작성하고 편집할 수만 있다. 코드를 실행하거나 자동으로 실행되도록 플러그인을 다운로드하려면 텍스트 편집기에서 나가야 할 수도 있다고 함.. 깊게 공부 안하고 돌리기만 해서... 몰랐다.</p>
</blockquote>
<h3 id="5-이런-실험을-할-때-디버거-십분-활용">5) 이런 실험을 할 때 디버거 십분 활용</h3>
<ol>
<li>실행 중인 코드를 잠시 정지시키고 실행 중인 스레드, 스택 트레이스, 변숫값 등을 확인할 수 있다.</li>
<li>디버거를 붙여 이벤트 발생시킨 후 코드가 해당 이벤트를 어떻게 처리하는지 단계적으로 확인</li>
<li>브레이크 포인트는 디버거에서 코드 실행을 중지시키는 지점을 설정하는 도구로 이를 통해 해당 지점에서 코드의 실행 상태를 분석하고 변수 값을 확인할 수 있다.</li>
</ol>
<h4 id="intellij에서-브레이크-포인트-설정-방법">intellij에서 브레이크 포인트 설정 방법</h4>
<blockquote>
<p>IntelliJ IDEA를 열고 디버그할 프로젝트를 로드</p>
</blockquote>
<ol>
<li>디버그하고 싶은 코드 파일을 엽니다.</li>
<li>브레이크 포인트를 설정하려는 줄에 마우스 커서를 가져갑니다.</li>
<li>해당 줄의 왼쪽 마진(라인 넘버 부분)을 클릭하면 브레이크 포인트가 설정됩니다. 또는, 해당 줄을 클릭한 후 <code>Ctrl + F8 (Windows/Linux)</code> 또는 <code>Command + F8 (Mac)</code>을 누르면 컨텍스트 메뉴가 나타납니다. 이 메뉴에서 <code>Toggle Line Breakpoint</code>를 선택하면 <strong>브레이크 포인트가 설정</strong>됩니다.</li>
<li>설정한 브레이크 포인트는 <code>빨간 동그라미</code>로 표시됩니다.</li>
<li>디버그 모드로 실행하려면 해당 클래스 또는 메서드 내에서 마우스 우클릭하여 &quot;Debug&quot; 옵션을 선택하거나, 코드 에디터 상단의 &quot;Run&quot; 또는 &quot;Debug&quot; 버튼을 클릭합니다.</li>
<li>프로그램이 브레이크 포인트에 도달하면 실행이 일시 정지됩니다. 이때 디버거 창에서 변수 값을 확인하거나 단계별로 코드를 실행해볼 수 있습니다.</li>
</ol>
<h3 id="🍊-디버거는-강력한-기능을-제공하지만-가끔은-로그나-print를-넣어두는-것이-코드의-동작을-이해하는-것이-가장-쉬운-방법">🍊 디버거는 강력한 기능을 제공하지만 가끔은 로그나 print를 넣어두는 것이 코드의 동작을 이해하는 것이 가장 쉬운 방법</h3>
<ul>
<li>다만, 멀티스레드 애플리케이션 같은 복잡한 상황에서 print문을 이용한 디버깅은 잘못된 결과를 도출할 수 있다는 점에서 유의</li>
</ul>
<h3 id="쉽지만-유용한-방법">쉽지만 유용한 방법</h3>
<ul>
<li>원래 코드가 아니라 내가 수정 중인 코드가 실행되고 있는 사실을 눈에 띄게 알려주는 문장을 프로그램이 처음 실행되는 시점에 출력</li>
</ul>