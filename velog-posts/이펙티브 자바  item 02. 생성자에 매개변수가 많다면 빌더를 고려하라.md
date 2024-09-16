<h1 id="item-02-생성자에-매개변수가-많다면-빌더를-고려하라">item 02. 생성자에 매개변수가 많다면 빌더를 고려하라</h1>
<blockquote>
<p><a href="https://mellona-log.gitbook.io/log/programming-lanuage/java/effective-java/item-02.">gitbook repo 버전</a></p>
</blockquote>
<blockquote>
<p>정적 팩터리와 생성자에는 똑같은 제약이 하나 있다. <strong>선택적 매개변수가 많을 때 적절히 대응하기 어렵다</strong>는 점이다.</p>
</blockquote>
<h2 id="클래스용-생성자-혹은-정적-팩토리의-모습">클래스용 생성자 혹은 정적 팩토리의 모습</h2>
<blockquote>
<p><code>선택 매개변수</code>가 <strong>많을 때</strong> 대안에 대해 알아보자.</p>
</blockquote>
<h3 id="첫-번째-대안--점층적-생성자-패턴">첫 번째 대안 : 점층적 생성자 패턴</h3>
<blockquote>
<p>프로그래머들은 이럴 때, <code>점층적 생성자 패턴(telescoping constructor pattern)</code>을 즐겨 사용했다.</p>
</blockquote>
<h4 id="점층적-생성자-패턴이란">점층적 생성자 패턴이란?</h4>
<p>필수 매개변수만 받는 생성자, 필수 매개변수와 선택 매개변수 1개를 받는 생성자, 선택 매개변수를 2개까지 받는 생성자... 형태로 <strong>선택 매개변수를 전부 다 받는 생성자까지 늘려가는 방식</strong>이다.</p>
<pre><code class="language-java">public class NutritionFacts {
    // 필수 필드
    private final int servingSize; // (ml, 1 회 제공량)
    private final int servings;    // (회, 총 n회 제공량)

    // 선택적 필드
    private final int calories;    // (1회 제공량당)
    private final int fat;         // (g/1 회 제공량)
    private final int sodium;      // (mg/1 회 제공량)
    private final int carbohydrate;// (g/1 회 제공량)

    // 필수 필드만 받는 생성자
    public NutritionFacts(int servingSize, int servings) {
        this(servingSize, servings, 0); // 다른 생성자 호출
    }

    // 필수 필드 + 선택적 필드 (calories)
    public NutritionFacts(int servingSize, int servings, int calories) {
        this(servingSize, servings, calories, 0); // 다른 생성자 호출
    }

    // 필수 필드 + 선택적 필드 (calories, fat)
    public NutritionFacts(int servingSize, int servings, int calories, int fat) {
        this(servingSize, servings, calories, fat, 0); // 다른 생성자 호출
    }

    // 필수 필드 + 선택적 필드 (calories, fat, sodium)
    public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium) {
        this(servingSize, servings, calories, fat, sodium, 0); // 다른 생성자 호출
    }

    // 모든 필드를 받는 생성자 (최종 생성자)
    public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
        this.servingSize = servingSize;
        this.servings = servings;
        this.calories = calories;
        this.fat = fat;
        this.sodium = sodium;
        this.carbohydrate = carbohydrate;
    }
}
</code></pre>
<p>이 클래스의 인스턴스를 만들려면 원하는 매개변수를 모두 포함한 생성자 중 <strong>가장 짧은 것을 골라 호출</strong>하면 된다.</p>
<pre><code class="language-java">NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27);</code></pre>
<p>이런 생성자의 경우, 사용자가 설정하길 원치 않는 매개변수까지 포함하기 쉬운데, 그런 매개변수에도 값을 지정해줘야 한다.</p>
<blockquote>
<p>결국, 점층적 생성자 패턴도 쓸 수는 있지만, <strong>매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵다</strong></p>
</blockquote>
<p>매개변수를 유효한지 생성자에서만 확인하면 일관성 유지 가능</p>
<h3 id="두-번째-대안--자바빈즈javabeans-patteren-패턴">두 번째 대안 : 자바빈즈(javaBeans patteren) 패턴</h3>
<h4 id="자바빈즈-패턴이란">자바빈즈 패턴이란?</h4>
<p>매개변수가 없는 생성자로 객체를 만든 후, <code>세터(setter) 메서드</code>들을 호출해 원하는 매개변수의 값을 설정하는 방식</p>
<pre><code class="language-java">public class NutritionFacts {
    // 필수 필드 (기본값 -1로 초기화)
    private int servingSize = -1; // 필수
    private int servings = -1;    // 필수

    // 선택적 필드 (기본값 0으로 초기화)
    private int calories = 0;
    private int fat = 0;
    private int sodium = 0;
    private int carbohydrate = 0;

    // 기본 생성자
    public NutritionFacts() { }

    // 세터 메서드들
    public void setServingSize(int val) {
        servingSize = val;
    }

    public void setServings(int val) {
        servings = val;
    }

    public void setCalories(int val) {
        calories = val;
    }

    public void setFat(int val) {
        fat = val;
    }

    public void setSodium(int val) {
        sodium = val;
    }

    public void setCarbohydrate(int val) {
        carbohydrate = val;
    }

    // 추가로 필요하다면 각 필드를 반환하는 getter 메서드도 정의할 수 있다.
}
</code></pre>
<h4 id="자바--빈즈--패턴의--장점">자바  빈즈  패턴의  장점</h4>
<ul>
<li>인스턴스를 만들기 쉬움</li>
<li>더 읽기 쉬운 코드</li>
<li>클라이언트 코드&#x20;</li>
</ul>
<pre><code class="language-java">NutritionFacts cocaCola = new NutritionFacts();
cocaCola.setServingSize(240);
cocaCola.setSe rvings(8);
cocaCola.setCalories(100);
cocaCola.setSod ium(35);
cocaCola.setCa rbohyd rate(27);</code></pre>
<h4 id="자바-빈즈-패턴의-단점">자바 빈즈 패턴의 단점</h4>
<ul>
<li>자바빈즈 패턴에서는 <strong>객체 하나를 만들려면 메서드를 여러 개 호출</strong>해야 하고, <strong>객체가 완전히 생성되기 전까지는</strong> <code>일관성(consistency)</code>이 <strong>무너진 상태</strong>에 놓이게 된다.</li>
<li>일관성이 깨진 객체가 만들어지면, 버그를 심은 코드와 그 버그 때문에 런타임에 문제를 겪는 코드가 물리적으로 멀리 떨어져 있기 때문에 디버깅도 만만치 않음 =&gt; 이로 인해 <code>클래스불변</code>으로 만들 수 없음</li>
<li>스레드 안정성을 얻으려면 프로그래머가 추가 작업 필요</li>
<li>대안으로 freeze 메서드가 있으나 확실히 호출해줬는지를 컴파일러가 보증 할 방법이 없어서 런타임 오류에 취약하다.</li>
</ul>
<h3 id="세-번째-대안---빌더-패턴builder-pattern">세 번째 대안 :  빌더 패턴(Builder pattern)</h3>
<blockquote>
<p>점층적 생성자 패턴의 안전성과 자바 빈즈 패턴의 가독성을 겸비하며, 빌더 패턴은 (파이썬과 스칼라에 있는) <code>명명된 선택적 매개변수</code>를 흉내낸 것</p>
</blockquote>
<h4 id="빌더-패턴이란">빌더 패턴이란?</h4>
<ol>
<li>클라인언트는 필요한 객체를 직접 만드는 대신, <strong>필수 매개변수만으로 생성자(혹은 정적 팩토리)를 호출해 빌더 객체를 얻는다.</strong></li>
<li>빌더 객체가 제공하는 일종의 세터 메서드들로 원하는 선택 매개변수들을 설정한다.</li>
<li>마지막으로, <strong>매개변수가 없는</strong> <code>build 메서드</code>를 호출해  우리에게 필요한 (보통은 불변인) 객체를 얻는다.</li>
</ol>
<blockquote>
<p>빌더는 생성할 클래스 안에 정적 멤버 클래스로 만들어두는 게 보통</p>
</blockquote>
<pre><code class="language-java">public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // 필수 매개변수
        private final int servingSize;
        private final int servings;

        // 선택 매개변수 - 기본값으로 초기화한다.
        private int calories = 0;
        private int fat = 0;
        private int sodium = 0;
        private int carbohydrate = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings = servings;
        }

        public Builder calories(int val) {
            calories = val;
            return this;
        }

        public Builder fat(int val) {
            fat = val;
            return this;
        }

        public Builder sodium(int val) {
            sodium = val;
            return this;
        }

        public Builder carbohydrate(int val) {
            carbohydrate = val;
            return this;
        }

        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize = builder.servingSize;
        servings = builder.servings;
        calories = builder.calories;
        fat = builder.fat;
        sodium = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}
</code></pre>
<h4 id="메서드-연쇄method-chaining-혹은-플루언트-apifluent-api"><strong>메서드 연쇄(method chaining) 혹은 플루언트 API(fluent API)</strong></h4>
<ul>
<li><strong>NutritionFacts 클래스</strong> :  모든 매개변수의 기값들을 한 곳에 모아둠</li>
<li>빌더의 세터 메서드들은 빌더 자신을 반환하기 때문에 연쇄적으로 호출 할 수 있다.</li>
</ul>
<h4 id="클라이언트-코드의-모습">클라이언트 코드의 모습</h4>
<pre><code class="language-java">NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
    .calories(100)
    .sodium(35)
    .carbohydrate(27)
    .build();
</code></pre>
<h4 id="장점">장점</h4>
<ul>
<li>클라이언트 코드는 쓰기 쉽고, 무엇보다 읽기 쉽다.</li>
<li>빌더 패턴은 상당히 유연하다. 빌더 하나로 여러 객체를 순회하면서 만들 수 있고, 빌더에 넘기는 매개변수에 따라 다른 객체를 만들 수도 있다.</li>
<li>생성자로는 누릴 수 없는 사소한 이점으로, 빌더를 이용하면 <code>가변인수(varargs) 매개변수</code>를 <strong>여러 개 사용할 수 있다.</strong></li>
</ul>
<h4 id="단점">단점</h4>
<ul>
<li>객체를 만들려면, 그에 앞서 빌더부터 만들어야 한다. 빌더 생성 비용이 크지는 않지만 성능에 민감한 상황에서는 문제가 될 수 있다.</li>
<li>점층적 생성자 패턴보다는 코드가 장황해서 매개변수 가 4개 이상은 되어야 값어치를 한다. BUT, API는 시간이 지날수록 매개변수 가 많아지는 경향이 있음을 명심하자</li>
</ul>
<blockquote>
<p><strong>✔️</strong> <code>불변(immutable 혹은 immutability)</code>은 어떠한 변경도 허용하지 않는다는 뜻 으로, 주로 변경을 허용하는 가변(mutable) 객체와 구분하는 용도로 쓰인다. 대표적으로 String 객체는 한번 만들어지면 절대 값을 바꿀 수 없는 불변 객체다. 한편, <code>불변식(invariant)</code>은 프로그램이 실행되는 동안, 혹은 정해진 기간 동안 반드시 만족해야 하는 조건을 말한다. 다시 말해 <strong>변경을 허용할 수는 있으나 주어진 조건 내에서 만 허용한다는 뜻이다.</strong> 예컨대 리스트의 크기는 반드시 0 이상이어야 하니, 만약 한순간 이라도 음수 값이 된다면 불변식이 깨진 것이다.&#x20;</p>
<p>가변 객체에도 불변식은 존재할 수 있으며, 넓게 보면 불변은 불변식의 극단적 인 예라 할 수 있다.</p>
</blockquote>
<h4 id="계층적으로-설계된-클래스와-쓰기-좋은-빌더-패턴">계층적으로 설계된 클래스와 쓰기 좋은 빌더 패턴</h4>
<h4 id="1-추상-클래스-pizza">1. 추상 클래스 Pizza</h4>
<pre><code class="language-java">public abstract class Pizza {
    public enum Topping { HAM, MUSHROOM, ONION, PEPPER, SAUSAGE }
    final Set&lt;Topping&gt; toppings;

    abstract static class Builder&lt;T extends Builder&lt;T&gt;&gt; {
        EnumSet&lt;Topping&gt; toppings = EnumSet.noneOf(Topping.class);

        public T addTopping(Topping topping) {
            toppings.add(Objects.requireNonNull(topping));
            return self();
        }

        abstract Pizza build();

        // 하위 클래스는 이 메서드를 재정의(overriding)하여 &quot;this&quot;를 반환해야 한다.
        protected abstract T self();
    }

    Pizza(Builder&lt;?&gt; builder) {
        toppings = builder.toppings.clone(); // 아이템 50 참조
    }
}</code></pre>
<ul>
<li><code>Pizza</code> 클래스는 피자의 기본 속성을 정의하고, <code>Topping</code> 열거형을 포함</li>
<li><code>Builder</code> 내부 클래스는 제네릭 타입으로, 피자 빌더를 생성하는 데 필요한 메서드를 정의</li>
<li><code>addTopping</code> 메서드는 토핑을 추가하는 역할을 하며, <code>self</code> 메서드는 하위 클래스에서 구현되어야&#x20;</li>
</ul>
<h4 id="2-뉴욕-피자-nypizza">2. 뉴욕 피자 (NyPizza)</h4>
<pre><code class="language-java">public class NyPizza extends Pizza {
    public enum Size { SMALL, MEDIUM, LARGE }
    private final Size size;

    public static class Builder extends Pizza.Builder&lt;Builder&gt; {
        private final Size size;

        public Builder(Size size) {
            this.size = Objects.requireNonNull(size);
        }

        @Override
        public NyPizza build() {
            return new NyPizza(this);
        }

        @Override
        protected Builder self() {
            return this;
        }
    }

    private NyPizza(Builder builder) {
        super(builder);
        size = builder.size;
    }
}</code></pre>
<ul>
<li><code>NyPizza</code> 클래스는 <code>Pizza</code>의 하위 클래스이며, 피자의 크기(<code>Size</code>)를 추가로 정의</li>
<li><code>Builder</code> 클래스는 <code>Pizza.Builder</code>를 상속받아 뉴욕 피자 전용 빌더를 구현</li>
<li><code>build</code> 메서드는 <code>NyPizza</code> 객체를 반환하며, <code>self</code> 메서드는 자신을 반환</li>
</ul>
<p><strong>3. 칼초네 피자 (Calzone)</strong></p>
<pre><code class="language-java">public class Calzone extends Pizza {
    private final boolean sauceInside;

    public static class Builder extends Pizza.Builder&lt;Builder&gt; {
        private boolean sauceInside = false; // 기본값

        public Builder sauceInside() {
            sauceInside = true;
            return this;
        }

        @Override
        public Calzone build() {
            return new Calzone(this);
        }

        @Override
        protected Builder self() {
            return this;
        }
    }

    private Calzone(Builder builder) {
        super(builder);
        sauceInside = builder.sauceInside;
    }
}</code></pre>
<ul>
<li><code>Calzone</code> 클래스는 <code>Pizza</code>의 또 다른 하위 클래스로, 소스가 안에 들어가는지 여부를 나타내는 <code>sauceInside</code> 변수를 포함함</li>
<li><code>Builder</code> 클래스는 <code>sauceInside</code> 메서드를 통해 소스를 추가할 수 있는 기능을 제공</li>
</ul>
<p><strong>4. 클라이언트 코드 예시</strong></p>
<pre><code class="language-java">NyPizza pizza = new NyPizza.Builder(NyPizza.Size.SMALL)
    .addTopping(Pizza.Topping.SAUSAGE)
    .addTopping(Pizza.Topping.ONION)
    .build();

Calzone calzone = new Calzone.Builder()
    .addTopping(Pizza.Topping.HAM)
    .sauceInside()
    .build();</code></pre>
<ul>
<li>클라이언트 코드는 <code>Builder</code>를 사용하여 쉽고 직관적으로 피자를 생성</li>
<li><code>NyPizza</code>와 <code>Calzone</code> 객체는 각각의 빌더를 통해 생성</li>
</ul>
<p><strong>요약</strong></p>
<p>각 하위 클래스는 자신의 특성을 추가하면서도 상위 클래스의 빌더 메서드를 재사용합니다. 이로 인해 클라이언트는 형변환을 걱정하지 않고도 다양한 피자 객체를 생성할 수 있다. 빌더 패턴은 유연성과 가독성을 높이며, 객체 생성 과정에서의 <code>복잡성</code>을 줄여줌</p>
<blockquote>
<p><strong>✔️ 생성자나 정적 팩터리가 처리해야 할 매개변수가 많다면 빌더 패턴을 선택하는 게 낫다.</strong> 매개변수 중 다수가 필수가 아니거나 같은 타입이면 특히 더 그렇다. 빌더는 점층적 생성자보다 클라이언트 코드를 읽고 쓰기가 훨씬 간결하고, 자바빈즈보다 훨씬 안전하다.</p>
</blockquote>
<p>static을 사용하지 말고.. 하게 되면... 결국 메모리에 빌더가 남아있다는&#x20;</p>