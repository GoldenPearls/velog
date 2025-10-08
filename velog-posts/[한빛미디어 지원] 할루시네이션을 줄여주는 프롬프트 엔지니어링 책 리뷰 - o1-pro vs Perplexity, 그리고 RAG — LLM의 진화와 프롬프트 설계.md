<blockquote>
<p>&quot;한빛미디어 서평단 &lt;나는리뷰어다&gt; 활동을 위해서 책을 협찬 받아 작성된 서평입니다.&quot;</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2675b803-381f-43a6-bce5-6cfd8bb6fffb/image.png" /></p>
<h1 id="1-프롬프트-엔지니어링-ai와-대화하는-기술">1. “프롬프트 엔지니어링, AI와 대화하는 기술”</h1>
<p>— 할루시네이션을 줄이고 LLM의 잠재력을 끌어내는 방법</p>
<blockquote>
<p>숙련된 장인이 도구의 미묘한 특징을 이해하듯,
<strong>프롬프트 엔지니어링(Prompt Engineering)</strong>은 AI의 언어 감각을 조율하는 기술입니다.</p>
</blockquote>
<h2 id="개요-프롬프트-엔지니어링이란">개요) 프롬프트 엔지니어링이란?</h2>
<p>Large Language Model(LLM)은 이미 다양한 분야에서 우리의 일상과 업무를 바꾸고 있습니다.
하지만 LLM은 <strong>“어떻게 물어보느냐에 따라 전혀 다른 답”</strong>을 주는 존재이기도 하죠.</p>
<p>그래서 등장한 개념이 바로 <strong>프롬프트 엔지니어링</strong>입니다.
이는 LLM이 가진 잠재력을 최대한 끌어내기 위한 “소통 설계 기술”입니다.</p>
<p>소통 설계로서의 프롬프트 엔지니어링이 중요합니다. </p>
<blockquote>
<p>특히, 할루시네이션(그럴듯한데 틀린 답) 을 줄이려면 프롬프트만이 아니라 RAG·가드레일·사후 검증까지 세트로 가져가야 합니다.</p>
</blockquote>
<h1 id="2-책-내용-훑어보기">2. 책 내용 훑어보기</h1>
<h2 id="1-llm의-그림자-할루시네이션hallucination">1) LLM의 그림자, ‘할루시네이션(Hallucination)’</h2>
<p>AI의 대답이 그럴듯하지만 <strong>틀릴 때</strong>, 우리는 그것을 <em>할루시네이션</em>이라 부릅니다.
즉, 모델이 <strong>입력과 무관하거나 사실이 아닌 출력을 생성</strong>하는 현상입니다.</p>
<table>
<thead>
<tr>
<th>유형</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>🧾 사실적 할루시네이션</td>
<td>실제 사실을 잘못 제시하는 경우</td>
</tr>
<tr>
<td>🔗 논리적 할루시네이션</td>
<td>논리적 연결이 어긋나는 경우</td>
</tr>
<tr>
<td>🌀 문맥적 할루시네이션</td>
<td>맥락과 전혀 상관없는 응답을 하는 경우</td>
</tr>
</tbody></table>
<blockquote>
<p>👉 따라서 LLM의 답변은 <strong>“항상 검증되어야 한다”</strong>는 점을 기억해야 합니다.
신뢰할 수 있는 데이터와 정교한 프롬프트 설계가 필수죠.</p>
</blockquote>
<h3 id="책이-말하는-llm-파이프라인과-정렬alignment">책이 말하는 LLM 파이프라인과 정렬(Alignment)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e2d3aa5b-449a-4e9a-966a-598caef32831/image.png" /></p>
<p>LLM 구성 절차 — 트랜스포머 모델 → 사전학습 → 지침 미세조정(Instruction FT) → 정렬 모델(Aligned) 로 이어지는 단계. </p>
<p>우리가 사용하는 <strong>상용 LLM은 이미 일정 수준의 정렬이 되어 있으나,</strong> 프롬프트 설계와 검증을 붙여야 서비스 품질이 올라갑니다.</p>
<h2 id="2-성능을-높이는-프롬프팅-4가지-핵심-기법">2) 성능을 높이는 프롬프팅 4가지 핵심 기법</h2>
<h3 id="1️⃣-제로샷--푸샷-프롬프팅-zero-shot--few-shot">1️⃣ 제로샷 &amp; 푸샷 프롬프팅 (Zero-shot / Few-shot)</h3>
<p>프롬프트를 설계할 때 <strong>예시를 주느냐, 안 주느냐</strong>의 차이입니다.</p>
<h4 id="🔹-제로샷-zero-shot">🔹 제로샷 (Zero-shot)</h4>
<blockquote>
<p>“예시 없이, 오직 지시만으로”
간결하지만 복잡한 작업에는 부정확할 수 있습니다.</p>
</blockquote>
<p>📍 예시</p>
<blockquote>
<p>“다음 문장의 감정을 분석해줘.”</p>
</blockquote>
<h4 id="🔹-푸샷-few-shot">🔹 푸샷 (Few-shot)</h4>
<blockquote>
<p>“몇 개의 예시를 함께 제시”
모델이 작업 방식을 더 쉽게 이해하게 됩니다.</p>
</blockquote>
<p>📍 예시</p>
<pre><code>이 영화는 정말 지루했다 - 부정
배우들의 연기는 인상 깊었다 - 긍정</code></pre><blockquote>
<p>연구 결과에 따르면 <strong>3개의 푸샷 예시를 제공했을 때 정확도가 52% 향상</strong>되기도 했습니다.</p>
</blockquote>
<h4 id="좋은-예시의-3가지-원칙">좋은 예시의 3가지 원칙</h4>
<table>
<thead>
<tr>
<th>원칙</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>🎯 관련성과 명확성</td>
<td>예시가 실제 작업과 직접적으로 관련</td>
</tr>
<tr>
<td>🌈 다양성과 대표성</td>
<td>여러 케이스가 고르게 포함</td>
</tr>
<tr>
<td>🧩 형식 일관성</td>
<td>입력·출력 구조가 동일하게 유지</td>
</tr>
</tbody></table>
<blockquote>
<p>즉, 푸샷은 모델에게 <strong>“작업을 가르치는 미니 훈련 세트”</strong>를 만드는 과정입니다.</p>
</blockquote>
<h3 id="2️⃣-cot-chain-of-thought-프롬프팅">2️⃣ CoT (Chain-of-Thought) 프롬프팅</h3>
<p><strong>“정답을 맞히는 게 아니라, 생각의 과정을 보여주는 것.”</strong></p>
<p>CoT는 모델에게</p>
<blockquote>
<p>“이 문제를 풀기 위해 어떤 단계를 거칠까?”
“각 단계에서 무엇을 계산해야 하지?”
를 스스로 생각하게 만드는 기법입니다.</p>
</blockquote>
<p>📈 이렇게 하면 모델이 <strong>자기 검증(Self-check)</strong> 과정을 거치며
복잡한 논리적 문제에서의 오류를 줄일 수 있습니다.</p>
<blockquote>
<p>예를 들어 수학 문제, 코딩 디버깅, 논리 추론에서 탁월한 효과를 보입니다.</p>
</blockquote>
<h3 id="3️⃣-rag-retrieval-augmented-generation">3️⃣ RAG (Retrieval-Augmented Generation)</h3>
<p><strong>검색 증강 생성 기법</strong></p>
<p>LLM이 “세상의 모든 최신 정보”를 알 수는 없습니다.
RAG는 이런 한계를 극복하기 위해 <strong>검색(Search)</strong> 능력을 붙여줍니다.</p>
<h4 id="⚙️-rag의-3단계-구조">⚙️ RAG의 3단계 구조</h4>
<ol>
<li><strong>Retrieve (검색)</strong> – 외부 지식 기반에서 관련 정보를 찾는다.</li>
<li><strong>Augment (증강)</strong> – 질문과 함께 이 정보를 모델에 제공한다.</li>
<li><strong>Generate (생성)</strong> – 검색 결과를 바탕으로 답변을 생성한다.</li>
</ol>
<blockquote>
<p>마치 <strong>오픈북 시험</strong>을 보는 것과 같습니다.
모델이 스스로 검색해 근거 있는 답변을 작성하죠.</p>
</blockquote>
<h4 id="💪-rag의-장점">💪 RAG의 장점</h4>
<ul>
<li>✅ 최신 정보 접근 가능</li>
<li>🧠 할루시네이션 감소</li>
<li>🔍 출처 제시로 투명성 확보</li>
<li>🏢 도메인 특화 및 개인화 가능</li>
</ul>
<h3 id="⚔️-cot-vs-rag-다른-목적-다른-강점">⚔️ CoT vs RAG: 다른 목적, 다른 강점</h3>
<table>
<thead>
<tr>
<th>비교 항목</th>
<th>OpenAI o1-pro</th>
<th>Perplexity</th>
</tr>
</thead>
<tbody><tr>
<td>핵심 기술</td>
<td><strong>CoT (논리적 추론 중심)</strong></td>
<td><strong>RAG (검색 중심)</strong></td>
</tr>
<tr>
<td>강점</td>
<td>수학, 코딩, 분석 등 깊은 사고</td>
<td>최신 정보, 지역 상점, 실시간 트렌드</td>
</tr>
<tr>
<td>약점</td>
<td>실시간 검색 불가</td>
<td>복잡한 논리 추론에 약함</td>
</tr>
</tbody></table>
<blockquote>
<p>📍 o1-pro는 “생각을 깊게 하는 모델”,
📍 Perplexity는 “세상을 빠르게 탐색하는 모델”이라 할 수 있습니다.</p>
</blockquote>
<h3 id="4️⃣-프롬프트-엔지니어링-자체가-할루시네이션-예방-기술">4️⃣ 프롬프트 엔지니어링 자체가 ‘할루시네이션 예방 기술’</h3>
<p>LLM은 <strong>트랜스포머 구조</strong>와 <strong>셀프 어텐션(Self-Attention)</strong> 메커니즘으로
문맥 내 단어의 중요도를 스스로 판단합니다.</p>
<p>이 구조는 이미 일정 수준의 <strong>정렬(Alignment)</strong> 과정을 거친 상태이지만,
프롬프트 엔지니어링을 통해 우리는 모델이 <strong>더 집중하고, 덜 흔들리도록</strong> 유도할 수 있습니다.</p>
<blockquote>
<p>🎯 “잘 설계된 프롬프트는 모델을 혼란에서 구해준다.”</p>
</blockquote>
<h2 id="3-할루시네이션을-막는-추가-기술들">3) 할루시네이션을 막는 추가 기술들</h2>
<table>
<thead>
<tr>
<th>접근 방식</th>
<th>설명</th>
<th>현실적 적용 난이도</th>
</tr>
</thead>
<tbody><tr>
<td>데이터 품질 개선</td>
<td>학습 데이터 자체를 정제</td>
<td>🔺 어려움 (모델 개발자 영역)</td>
</tr>
<tr>
<td>모델 아키텍처 개선</td>
<td>구조적 개선으로 추론력 강화</td>
<td>🔺 어려움</td>
</tr>
<tr>
<td>사후 검증 (Post-verification)</td>
<td>외부 데이터, 자기 교정, 인간 검토</td>
<td>✅ 현실적</td>
</tr>
</tbody></table>
<blockquote>
<p>특히 “사후 검증(Post Verification)”은 RAG와 함께 실무에서 매우 유용합니다.
LLM이 생성한 답변을 <strong>외부 지식 기반</strong>이나 <strong>자기 교정(Self-Critique)</strong> 으로 한 번 더 점검하는 방식입니다.</p>
</blockquote>
<h2 id="4-자주-받는-질문faq">4) 자주 받는 질문(FAQ)</h2>
<p>Q. o1-pro(추론형)인데, 지역 가게 영업시간이 자꾸 틀려요.
A. 그건 모델의 목적과 입력 파이프라인 문제. o1-pro는 추론·코딩 등에 강점, 영업시간은 RAG/검색 도구 연결이 핵심.</p>
<p>Q. 파인튜닝하면 다 해결되나요?
A. 도메인 스타일 적응엔 좋지만, 최신성/근거/검증은 여전히 RAG·가드레일이 필요.</p>
<p>Q. 블로그용 예시 데이터는?
A. 푸샷 예시를 카테고리 균형/형식 일관/명확성 기준으로 직접 선별해라. 잘못된 예시는 성능을 오히려 악화시킨다.</p>
<h1 id="3-할루시네이션을-줄여주는-프롬프트-엔지니어링-책이란">3. 할루시네이션을 줄여주는 프롬프트 엔지니어링 책이란?</h1>
<h2 id="1-이-책이-실전서인-이유-rag·인덱싱·그라운딩·평가">1) 이 책이 ‘실전서’인 이유: RAG·인덱싱·그라운딩·평가</h2>
<h3 id="1️⃣-인덱싱-파이프라인-load-→-split-→-store">1️⃣ 인덱싱 파이프라인: Load → Split → Store</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ed83f3be-dd96-4f9f-afc3-04a66a95f12b/image.png" /></p>
<p>LangChain으로 디렉터리 로드, <strong>문서 분할(chunk_size/overlap)</strong>, 벡터스토어 저장까지 한 번에. 현업에서 바로 쓸 수 있게 매개변수의 의미를 설명해 줍니다.</p>
<h3 id="2️⃣-rag-아키텍처-검색·증강·생성">2️⃣ RAG 아키텍처: 검색·증강·생성</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f868ea6f-8d3c-491e-b63c-5157aa31b810/image.png" />
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9cd000da-781d-4dfc-b732-3a8660d8d033/image.png" /></p>
<p><strong>RAG의 단계별 설계</strong> —</p>
<ul>
<li><strong>질의 변환</strong>(Query Transformation)으로 사용자의 질문을 검색 친화적 질의로 바꾸고,</li>
<li><strong>임베딩/유사도 검색/문서 분할</strong>을 통해 <strong>가장 관련 문맥</strong>을 찾아,</li>
<li><strong>증강(Augment)</strong> 단계에서 맥락과 함께 답변을 생성한다.
하이라이트는 <strong>“근거가 없으면 답하지 말라”</strong>는 <strong>그라운딩 프롬프트 규칙</strong>(사진 4 하단 예시). 서비스 신뢰도의 생명줄이다.</li>
</ul>
<h3 id="3️⃣-에이전트도구메모리계획">3️⃣ 에이전트/도구/메모리/계획</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9cea7601-2490-4f97-8788-dfc49ce69ca5/image.png" /></p>
<p><strong>ReAct/에이전트 개념</strong> — 툴 호출·증거 수집·계획을 엮어 <strong>스스로 태스크를 수행하는 에이전트</strong>를 만듭니다. 보고서 생성·로그 분석·FAQ 자동화에 유용.</p>
<h3 id="4️⃣-신뢰성-평가-truthfulqa-halueval-fever-factscore">4️⃣ 신뢰성 평가: TruthfulQA, HaluEval, FEVER, FACTSCORE</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f25c6bb0-5f1c-4def-9e99-005d89cea3cc/image.png" />
<strong>평가 벤치마크</strong> — 단순 정답률이 아니라 <strong>진실성·근거성·사실성</strong>을 봅니다. 현업에서 “잘 말하는 모델”이 아니라 <strong>“바르게 말하는 모델”</strong> 을 고르는 기준이 됩니다.</p>
<h3 id="5️⃣-할루시네이션-유형과-cot의-효과">5️⃣ 할루시네이션 유형과 CoT의 효과</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/6c354234-e8c1-42cf-93b4-b49ffcf7b537/image.png" /></p>
<p>유형별 사례와 <strong>Pineapple 모음 개수</strong> 문제에서 CoT를 적용했을 때 <strong>오답→정답</strong>으로 달라지는 과정을 한 컷 도식으로 보여주며, “풀이 과정을 말하게 하라”는 메시지가 직관적으로 전달됩낟,</p>
<h2 id="2-이-전자책의-주요-장점-5가지">2) 이 전자책의 <strong>주요 장점 5가지</strong></h2>
<ol>
<li><p><strong>최신 LLM 도구·예제 기반 실전성</strong>
OpenAI·Gemini·LangChain 등으로 <strong>바로 따라할 수 있는 프로젝트</strong>가 촘촘합니다. 코드·설계·프롬프트까지 <strong>엔드투엔드</strong>로 연결됩니다.</p>
</li>
<li><p><strong>할루시네이션 예방 전술 총정리</strong>
프롬프트 엔지니어링, 데이터 품질·모델 아키텍처 개선, <strong>사후 검증(그라운딩·자기 교정)</strong> 을 <strong>실습형으로</strong> 익힙니다.</p>
</li>
<li><p><strong>RAG·지식 그래프·멀티에이전트</strong>
검색 증강부터 그래프 결합, 에이전트(툴 호출·계획·메모리)까지 <strong>프로덕션 관점</strong>에서 구현해 봅니다.</p>
</li>
<li><p><strong>실전 예제의 다양성</strong>
백과사전 챗봇, 실시간 QA 에이전트, 트렌드 분석 등 <strong>서비스 완성형</strong> 예제가 “모델 호출”을 넘어 <strong>시스템 설계 역량</strong>을 키워줍니다.</p>
</li>
<li><p><strong>입문~실무자까지 한 권 커버</strong>
파이썬·ML 베이스로 <strong>고급 프롬프팅·평가·책임 있는 AI 설계</strong> 까지 <strong>체계적</strong>으로 넘깁니다.</p>
</li>
</ol>
<h2 id="3-추천-독자--활용-시나리오">3) 추천 독자 &amp; 활용 시나리오</h2>
<ul>
<li><strong>정확성과 신뢰성을 높여야 하는 개발자/엔지니어</strong>: 고객지원, 문서 QA, 내부 검색.</li>
<li><strong>MLOps·AI 서비스 담당자</strong>: 데이터 품질·RAG·지식 그래프·평가 체계를 <strong>운영</strong>에서 굴려야 하는 팀.</li>
<li><strong>도메인 전문가/컨텐츠 팀</strong>: “근거 제시가 필요한” 리서치·리포팅 자동화.</li>
<li><strong>스타트업</strong>: 고비용 파인튜닝 대신 <strong>API + RAG + 가드레일</strong>로 <strong>가성비</strong> 솔루션을 빠르게.</li>
</ul>
<h2 id="4-읽으며-얻은-인사이트-5">4) 읽으며 얻은 인사이트 5</h2>
<ol>
<li><strong>“추론형 vs 검색형”</strong> 을 구분하면 도구 선택이 빨라진다. (o1-pro ↔ Perplexity)</li>
<li><strong>프롬프트만으론 부족</strong>하다. 반드시 <strong>근거·검증</strong>을 붙여야 한다.</li>
<li><strong>문서 분할과 임베딩 품질</strong>이 RAG의 절반을 먹고 들어간다. (chunk 설계, overlap 튜닝)</li>
<li><strong>벤치마크는 선택이 아니라 필수</strong>. TruthfulQA/HaluEval/FEVER/FACTSCORE로 “잘 말함”이 아닌 “바르게 말함”을 측정.</li>
<li><strong>제약 조건(guardrail)</strong> 문구가 품질을 좌우한다. “근거 없으면 모름” 한 줄의 힘.</li>
</ol>
<h2 id="5-좋았던-점">5) 좋았던 점</h2>
<ul>
<li>도해·캡션이 풍부해서 <strong>팀 온보딩 자료</strong>로 쓰기 좋다.</li>
<li>코드·아키텍처·프롬프트가 <strong>한 흐름</strong>으로 이어진다.</li>
<li>“그럴듯한데 틀린 답”을 <strong>어떻게 잡는지</strong> 구체적이다.</li>
</ul>
<h2 id="6-한줄-평--별점">6) 한줄 평 &amp; 별점</h2>
<blockquote>
<p><strong>“멋진 답변”이 아니라 **“신뢰 가능한 답변”</strong> 을 만드는 법을, 설계–코드–평가까지 연결해주는 실전서.**
<strong>⭐️⭐️⭐️⭐️☆ (4.6/5)</strong> — RAG/그라운딩/가드레일을 일단 이 책대로만 구현해도 서비스 품질이 체감으로 달라진다.</p>
</blockquote>
<h3 id="요약">요약</h3>
<ul>
<li>LLM의 최대 리스크는 <strong>할루시네이션</strong>.</li>
<li><strong>프롬프트 설계 + RAG + CoT + 사후 검증</strong>이 현업 <strong>가성비 최강 스택</strong>.</li>
<li>이 전자책은 인덱싱→검색→증강→생성→평가까지 <strong>엔드투엔드</strong>로 잡아준다.</li>
</ul>
<blockquote>
<p>정확성과 신뢰성을 높여야 하는 개발자/엔지니어라면 읽어볼 추천 도서이다.</p>
</blockquote>