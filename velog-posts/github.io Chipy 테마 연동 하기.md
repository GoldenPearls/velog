<h1 id="githubio-blog-만들기">github.io blog 만들기</h1>
<h2 id="1-tmi">1) TMI</h2>
<p>에서 블로그를 운영하고 있고, 팔로우도 100명을  넘었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3f7c738d-963b-4526-aa53-317ec20774c4/image.png" /></p>
<p>하지만.. 옮기지는 않고 두 곳을 운영할까 고민중... <strong>Velog에 단점이 내가 쓴 글 한 눈에 안보여 ㅠㅠㅠㅠ</strong></p>
<p>Github Page를 통한 블로깅을 시도했으나 까다로운 설치와 커스터마이징이,어렵다기에 테마 선택 시 사용자 수가 많고 계속  update 되고있으며,  내  마음에 들고 사용자가많은 테마인 <a href="https://github.com/cotes2020/jekyll-theme-chirpy">Chipy</a>를 선택!!</p>
<h2 id="2-local에서-테스트-하기-전의-세팅">2) Local에서 테스트 하기 전의 세팅</h2>
<blockquote>
<p><a href="https://www.irgroup.org/posts/jekyll-chirpy/">Jekyll-Chirpy-테마 글쓰기, 커스마이징 등</a>
<a href="https://jjikin.com/posts/Jekyll-Chirpy-%ED%85%8C%EB%A7%88%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(2023-6%EC%9B%94-%EA%B8%B0%EC%A4%80)">Jekyll-Chirpy-테마를-활용한-Github-블로그-만들기(2023-6월-기준)</a> </p>
</blockquote>
<ol>
<li>리포지토리 <code>fork</code> 해와서  생성하기</li>
</ol>
<ul>
<li>꼭 리포지토리명을   <code>github 유저이름.github.io</code>로 해야 한다고 다!!</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ba804212-34fe-4099-8e41-6a6823df1e0b/image.png" /></p>
<ol start="2">
<li>branch를 master에서 main으로 변경하고 Branch protection rule도 기본값 (체크 x)으로 설정</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b07b61da-641f-4346-b9cf-bbd6495f57e3/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e792ddd2-8c3f-4a6e-b0eb-a09f62d7570c/image.png" />
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8766155f-73e3-4313-ab0e-76ae5dae7be3/image.png" /></p>
<ol start="3">
<li>git clone 해오기</li>
</ol>
<ul>
<li>넣어둘 폴더로 이동 해서 clone 해오기</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0ca2568f-abc7-4fb6-b3a6-09e06824052b/image.png" /></p>
<pre><code class="language-jsx">cd blog
git clone https://github.com/GoldenPearls/GoldenPerals.github.io.git</code></pre>
<h1 id="local에서-세팅">Local에서 세팅</h1>
<blockquote>
<p>참고 : <a href="https://junstar92.tistory.com/5">별준 : 루비 설치 하기</a></p>
</blockquote>
<ol>
<li>CMD로 Ruby 설치 하기</li>
</ol>
<blockquote>
<p>꼭 3. 이상 설치 할 것 !</p>
</blockquote>
<ol start="2">
<li>Ruby를 설치했다면 버전을 검색시 나올 것임</li>
</ol>
<pre><code class="language-jsx">cd GoldenPerals.github.io
ruby -v</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6dcefcd1-9818-4d14-bd6b-ab3054d3dbbd/image.png" /></p>
<p>이렇게만 설치하고 서버 실행하려고 하면 이런 에러가 나올 수도 있음 그런 경우는  <code>환경 변수 설정</code>이 필요함</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f45f43a4-8214-4e2f-848c-0b7ac29187f8/image.png" /></p>
<ol start="2">
<li>환경 변수 설정이 필요 Path 에서 편집</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f94734d6-e67e-4f9f-a644-f224264b0aa3/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/33a3b039-2919-4ee7-a89c-124e4004ff4d/image.png" /></p>
<pre><code class="language-jsx">C:\Users\rmawn\AppData\Local\Microsoft\WindowsApps</code></pre>
<ol start="3">
<li>jekyll  실행을 위해 필요한 모듈 설치</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0c1d675f-0341-47b3-a015-aecc6926476f/image.png" /></p>
<ol start="4">
<li>npm을 통해 node.js 모듈 설치</li>
</ol>
<pre><code class="language-jsx">npm install &amp;&amp; npm run build</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ac853e67-6313-4ebf-a208-642aef312503/image.png" /></p>
<ol start="5">
<li>설치 완료 후 아래 명령어를 통해 로컬에서 jekyll을 실행</li>
</ol>
<pre><code class="language-jsx">jekyll serve</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f710e210-be75-4270-86df-c936a55d35e3/image.png" /></p>
<h3 id="🙄-문제-발생">🙄 <strong>문제 발생</strong></h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/bd7fa754-ede0-42d6-9a3c-ef3c184a1643/image.png" /></p>
<p>먼저 위에서 처럼 </p>
<ol>
<li>환경변수 추가</li>
<li><code>Gemfile</code> 파일 수정</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/343c2a30-b6ff-4e33-b098-8800ddb60167/image.png" /></p>
<ol start="3">
<li>원래의 코드</li>
</ol>
<pre><code class="language-jsx"># frozen_string_literal: true

source &quot;https://rubygems.org&quot;

gemspec

group :test do
  gem &quot;html-proofer&quot;, &quot;~&gt; 5.0&quot;
end</code></pre>
<ol start="4">
<li>수정</li>
</ol>
<pre><code class="language-jsx"># frozen_string_literal: true

source &quot;https://rubygems.org&quot;

gemspec

group :test do
  gem &quot;html-proofer&quot;, &quot;~&gt; 5.0&quot;
end

gem &quot;tzinfo&quot;       # 시간대 관리 라이브러리
gem &quot;tzinfo-data&quot;  # Windows에서 tzinfo를 지원하기 위한 데이터</code></pre>
<ol start="6">
<li>cmd 껐다가 다시 켜서 확인해보기</li>
</ol>
<pre><code class="language-jsx">jekyll serve</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4577b948-a8b2-492b-b7cc-6a2d52a88a32/image.png" /></p>
<ol start="7">
<li>웹브라우저에서 127.0.0.1:4000 주소로 블로그가 정상적으로 표시되는지 확인하고 블로그 내 여러 메뉴 및 기능들도 정상 동작하는지 확인</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/612687e4-7490-4f68-8d08-92db45e2de9a/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/58c63c98-fce9-4af0-a80e-668bcc89f588/image.png" /></p>
<pre><code class="language-rust"># frozen_string_literal: true

source &quot;https://rubygems.org&quot;

gemspec

group :test do
  gem &quot;html-proofer&quot;, &quot;~&gt; 5.0&quot;
end

gem &quot;tzinfo&quot;       # 시간대 관리 라이브러리
gem &quot;tzinfo-data&quot;  # Windows에서 tzinfo를 지원하기 위한 데이터
</code></pre>
<h2 id="글-쓰는-시간을-줄이기-위한--플러그인">글 쓰는 시간을 줄이기 위한  플러그인</h2>
<blockquote>
<p><a href="https://github.com/jekyll/jekyll-compose">https://github.com/jekyll/jekyll-compose</a></p>
</blockquote>
<h2 id="배포하기">배포하기</h2>
<ol>
<li>배포하기 전 gitgnore 세팅하기</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/beb0ace2-c081-4389-8723-3b52daa3d78b/image.png" /></p>
<ul>
<li>우선, <code>.gitignore</code> 파일을 열어서 아래 내용을 주석 처리</li>
</ul>
<pre><code class="language-jsx"># Misc
#_sass/dist
#assets/js/dist</code></pre>
<ol start="2">
<li>배포하기</li>
</ol>
<pre><code class="language-jsx">git add .
git commit -m &quot;docs: add new blog post&quot;
git push</code></pre>
<ol start="3">
<li>setting &gt; page &gt; git action 추가
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/cb6253bb-ef56-4dc0-98a2-e6073bf194bc/image.png" /></li>
</ol>
<ul>
<li>configure까지 해줘야 함</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e95923a4-4544-446f-bc0a-3f37f955572d/image.png" /></p>
<ol start="4">
<li>로컬이랑 맞춰줘야 함</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/51eb7b1b-9512-4b0f-b59a-e42440c1f450/image.png" /></p>
<ol start="5">
<li>커스터마이징을 위한 _config.yml 수정하기</li>
</ol>
<blockquote>
<p><a href="https://github.com/focuschange-test/focuschange-test.github.io/blob/main/_config.yml">참고 깃허브</a></p>
</blockquote>
<pre><code class="language-jsx">git add . 
git commit -m &quot;chore: update config.yml settings&quot;
git push</code></pre>
<p>훔... 일단 배포만 해두고 ... 지금 gitbook 테마가 더 마음에 들어서 gitbook에만 해둘까? 아님 github.io랑 연결해서 할 수 있는 방법을 찾을까 고민중임</p>
<p>내 <a href="https://mellona-log.gitbook.io/log">gitbook</a></p>