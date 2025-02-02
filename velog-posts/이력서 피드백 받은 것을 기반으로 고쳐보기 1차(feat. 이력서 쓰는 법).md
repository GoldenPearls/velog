<h1 id="tmi">Tmi</h1>
<h2 id="이력서-작성-모임--작당모의">이력서 작성 모임 : 작당모의</h2>
<p>11월 30일에 트위터에서 트친이 모집하는 작당모의에 다녀왔다..!
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/82325bc5-7cd4-4f30-a207-f4fbadaaf66d/image.png" /></p>
<p>사실 후기를 말하자면 3시간 동안 이력서를 쓰지는 못했고 미리 써둔 게 있어서 <strong>피드백</strong>을 받았다. 갔을 때 분야 별로 나눴음
백엔드, 게임 및 보안, 프론트엔드와 앱 한 팀 당 1분 씩 피드백 주실 쟁쟁한 분들이 계셨다..!</p>
<p>일단 갔을 때 인사 후 써온 사람들꺼 위주로 봐주심 약간 나는 뒷순서라 ㅠㅠㅠ 좀 잘려서 슬픈데... 이거 수정하고 나고 이직할 때쯤 한 번 더 피드백 요청 드려야 겠다.</p>
<p>다른 사람들꺼 또한 피드백 받은 것을 적었음</p>
<blockquote>
<p>그를 기반으로 이력서를 일부 수정하고 이력서를 다시 업데이트 해보자</p>
</blockquote>
<h2 id="수정하게-된-계기">수정하게 된 계기</h2>
<p>내가 회사를 다닐 때 이직 생각이 크지 않더라도 언제 회사가 망할 지 모르기에 미리 미리 업데이트 해두면 좋다고 했음 그래서 적어둔 것이 있긴 한데 완성은 아니었기에.. 수정한다.</p>
<hr />
<h1 id="이력서-작성-요령">이력서 작성 요령</h1>
<blockquote>
<p>먼저 내꺼 수정 전 다른 사람 이력서에 대한 피드백 나열을 정리해봄 + concat님 x 트위터
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1adeccf0-52d3-42f0-88e0-d80b669cf5c9/image.png" /></p>
</blockquote>
<h2 id="✏️-1-개발-경험-구체적으로-정리하기">✏️ 1. 개발 경험 구체적으로 정리하기</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9310cdf7-5536-4887-bf9f-ab86ab44edf1/image.png" /></p>
<h3 id="🏆-1-구체적인-기여-내용-명시">🏆 1) 구체적인 기여 내용 명시</h3>
<p>단순히 &quot;API 개발을 했습니다&quot;라고 적기보다, <strong>어떤 기여를 했고 어떤 개선을 이루었는지</strong>를 명확히 표현해야 한다.</p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;Spring 기반의 REST API 개발 시 전략 패턴(Strategy Pattern)을 적용하여 기존 서비스 로직 중복을 제거하고, 코드 유지보수성을 30% 향상시켰습니다.&quot;</strong></li>
<li><strong>&quot;Redis 캐싱 전략 도입으로 API 응답 속도를 평균 200ms 단축하고, 서버 자원 사용률을 15% 절감했습니다.&quot;</strong></li>
<li><strong>&quot;CI/CD 파이프라인 개선으로 기존 주 1회 배포를 매일 자동 배포 가능하도록 변경, 개발-배포 리드타임을 대폭 단축했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;REST API 개발 업무를 수행했습니다.&quot; (구체적인 기여 내용 없음)</li>
<li>&quot;캐싱을 사용했습니다.&quot; (무엇을 개선했는지 불분명)</li>
<li>&quot;코드 리팩토링을 했습니다.&quot; (구체적인 목표, 성과 제시 부족)  </li>
</ul>
<p>🧐 <strong>응답 시간 수치 개선의 근거 제시</strong><br />APM(New Relic, Datadog), 로그 분석(ELK 스택), 퍼포먼스 테스트(JMeter, Gatling), 클라우드 모니터링(AWS CloudWatch) 등을 활용한 <strong>객관적 데이터</strong>를 제공하면 신뢰도를 높일 수 있다. </p>
<blockquote>
<p>불가한 경우, 대략적인 지표라도 명시하는 것이 좋다.  </p>
</blockquote>
<h3 id="🔧-2-문제-해결-사례-추가">🔧 2) 문제 해결 사례 추가</h3>
<p>기술적인 문제(예: 웹소켓 동기화 문제)를 어떻게 해결했는지를 설명하자. <strong>문제 발생 배경, 해결 방법, 결과를 명확히 적어야 한다.</strong></p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;웹소켓 기반 실시간 알림 기능 구현 중 메시지 동기화 문제 발생. 서버 노드 간 메시지 상태 공유 미비가 원인이었으며, Redis Pub/Sub를 활용한 상태 브로드캐스팅 및 메시지 큐를 도입하여 문제를 해결했습니다. 그 결과, 알림 전송 실패율을 기존 5%에서 0.5% 이하로 줄였습니다.&quot;</strong></li>
<li><strong>&quot;서버 부하로 성능 저하가 발생. APM(New Relic) 분석을 통해 특정 API의 DB 쿼리 병목을 발견 후, 인덱스 추가 및 N+1 Query 제거를 수행하여 평균 응답 시간을 1.5초에서 700ms로 단축했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;웹소켓 문제를 해결했습니다.&quot; (어떤 문제인지, 해결 방법이 불명확)</li>
<li>&quot;성능 문제가 있어서 개선했습니다.&quot; (구체적인 상황, 원인, 해결책이 빠짐)  </li>
</ul>
<h3 id="🛠️-3-기술적-어려움과-해결-방안-강조">🛠️ 3) 기술적 어려움과 해결 방안 강조</h3>
<p>단순히 <strong>&quot;무엇을 했다&quot;</strong>가 아니라, <strong>&quot;어떤 어려움을 겪었고, 어떻게 해결했으며, 그 결과가 어떠했는지&quot;</strong>까지 서술하면 더욱 강력한 어필이 가능하다.</p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;MSA 전환 중 서버 간 인증 토큰 공유 이슈 발생. JWT 기반 토큰 전략 재검토 후 API Gateway에 OAuth 2.0 및 JWT 검증 로직을 도입하여 각 서비스 간 인증 일관성을 확보. 그 결과, 인증 실패율을 10%에서 1% 미만으로 낮췄습니다.&quot;</strong></li>
<li><strong>&quot;대규모 트래픽 증가로 인한 DB Connection Pool 고갈 문제 발생. Connection Pool 사이즈 조정, Read Replica 도입, 쿼리 최적화를 통해 시스템 안정성을 확보하고 피크 타임에도 장애 없이 요청 처리율을 유지했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;서버 구조를 개선했습니다.&quot; (어떤 어려움과 해결 과정이 있었는지 불명확)</li>
<li>&quot;트래픽 문제를 해결했습니다.&quot; (구체적인 접근 방식과 개선된 지표 부족)  </li>
</ul>
<hr />
<h2 id="🛠️-2-프로젝트-및-기술-스택-강화">🛠️ 2. 프로젝트 및 기술 스택 강화</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/40a65cce-202e-4698-b2ae-1739ddd22840/image.png" /></p>
<h3 id="1-🏗️-프로젝트-추가">1) 🏗️ 프로젝트 추가</h3>
<blockquote>
<p><a href="https://youtu.be/dhH4qQ7N8qY">면접관이 좋아하는 포트폴리오 - 이형</a></p>
</blockquote>
<p>팀 프로젝트나 스터디 프로젝트(예: 티켓팅 서버 프로젝트) 등을 진행하여 <strong>기술력을 보여줄 수 있는 포트폴리오</strong>를 추가하자. 프로젝트의 목표, 사용된 기술 스택, 팀 내 역할, 성과 등을 구체적으로 기술하면 자신의 기술력과 협업 능력을 효과적으로 강조할 수 있다.  </p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;티켓팅 서버 개선 프로젝트에서 Node.js와 Redis를 활용한 세션 관리 최적화를 담당했습니다. 이를 통해 동시 접속자 증가에도 서버 다운 없이 안정적인 응답을 유지했고, 최종적으로 동시 접속자 2배 증가에도 99% 이상의 요청 처리 성공률을 달성했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;티켓팅 서버 프로젝트를 진행했습니다.&quot; (프로젝트 목표, 역할, 성과 불명확)  </li>
</ul>
<h3 id="2-🧭-스택-선택-근거-설명">2) 🧭 스택 선택 근거 설명</h3>
<p>사용한 기술 스택의 선택 근거를 명확히 설명하자. 특히 서버리스 아키텍처나 스프링을 사용할 때, 어떤 기준으로 선택했는지 기술하면 좋다. 기술 선택의 이유를 설명하면, <strong>기술을 단순히 사용한 것이 아니라 장단점을 이해하고 적절하게 선택할 수 있는 능력을 갖추고 있음을 보여줄 수 있다.</strong>  </p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;서버리스 아키텍처를 도입한 이유는 초기 개발 비용 절감과 향후 트래픽 증가에 따른 유연한 확장성 확보였습니다. 이를 위해 AWS Lambda와 API Gateway를 활용해 인프라 관리 부담을 감소시키고, 트래픽 증가 시 자동 스케일링이 가능하도록 했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;AWS Lambda를 사용했습니다.&quot; (선택 이유, 장점 미기재)  </li>
</ul>
<h3 id="3-💻-백엔드-추상화-라이브러리-강조">3) 💻 백엔드 추상화 라이브러리 강조</h3>
<p>스프링 사용 시 <strong>백엔드 추상화 라이브러리를 어떻게 활용했는지</strong>를 강조하고, 빠르게 학습할 수 있는 능력을 드러내자. 이를 통해 <strong>새로운 기술을 배우고 적용하는 학습 능력과 적응력을 보여줄 수 있다.</strong>  </p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;Spring Data JPA와 같은 백엔드 추상화 라이브러리를 활용해 데이터 접근 로직을 단순화했습니다. 이를 통해 개발 초기 2주 내로 프로덕션 수준 기능 구현에 성공했고, 신규 인력 온보딩 시간을 단축하여 팀 생산성 향상에 기여했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;Spring을 사용했습니다.&quot; (추상화 라이브러리 활용 성과 및 속도 개선 언급 없음)  </li>
</ul>
<hr />
<h2 id="📊-3-성과와-문제-해결-방법-강조">📊 3. 성과와 문제 해결 방법 강조</h2>
<blockquote>
<p>관련 참고할 만한 글</p>
</blockquote>
<ul>
<li><a href="https://m.blog.naver.com/wantedlab/221100604211?utm_source=chatgpt.com">이력서 담당자가 말하는 좋은 이력서</a></li>
</ul>
<h3 id="1-🔢-성과를-숫자로-표현">1) 🔢 성과를 숫자로 표현</h3>
<p>성과를 <strong>수치화하여 표현</strong>하면 그 효과를 명확하게 전달할 수 있어 면접관이 쉽게 이해할 수 있다. 성능 개선, 처리 속도 향상, API 응답 시간 단축 등 <strong>구체적인 지표를 포함하여 작성하자.</strong>  </p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;API의 응답 시간을 기존 2.5초에서 700ms로 최적화하여 서비스의 성능을 크게 향상시켰습니다.&quot;</strong> </li>
<li><strong>&quot;데이터베이스 인덱싱 및 쿼리 최적화를 통해 쿼리 실행 시간을 평균 60% 단축했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;API 성능을 개선했습니다.&quot; (구체적인 성과가 없음)  </li>
<li>&quot;DB 최적화를 수행했습니다.&quot; (어떤 방식으로 최적화했는지 불명확)  </li>
</ul>
<h3 id="2-☁️-전문성-강조">2) ☁️ 전문성 강조</h3>
<p>AWS를 사용한 프로젝트 경험이 있다면 <strong>마이그레이션, 데브옵스, 인프라 설계 등의 경험을 구체적으로 작성</strong>하여 클라우드 환경에서의 전문성을 강조하자.  </p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;온프레미스에서 AWS로 마이그레이션을 진행하며, RDS와 S3를 활용하여 데이터 저장 및 백업 자동화를 구축했습니다.&quot;</strong>  </li>
<li><strong>&quot;CI/CD 파이프라인을 구축하여 배포 프로세스를 자동화하고, 평균 배포 시간을 70% 단축했습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;AWS를 사용했습니다.&quot; (어떤 서비스를 어떻게 활용했는지 불명확)  </li>
</ul>
<h3 id="3-⭐️-star-기법-활용">3) ⭐️ STAR 기법 활용</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/32a06a31-9349-4d35-8fe9-59eaf0d79ab5/image.png" /></p>
<p>문제 해결 경험을 구체적으로 설명할 때 <strong>STAR 기법(상황, 과제, 행동, 결과)</strong>을 적용하면 쉽게 작성 가능 해질 것!</p>
<p>✅ <strong>예시</strong></p>
<ul>
<li><strong>상황(Situation)</strong>: 피크 트래픽 시 서버 응답 속도가 5초 이상 지연됨.  </li>
<li><strong>과제(Task)</strong>: 성능 최적화를 통해 응답 속도 단축 필요.  </li>
<li><strong>행동(Action)</strong>: 쿼리 최적화 및 캐싱 적용.  </li>
<li><strong>결과(Result)</strong>: 응답 속도를 1초 이내로 개선.  </li>
</ul>
<hr />
<h2 id="🤝-4-협업과-성장-의지-강조">🤝 4. 협업과 성장 의지 강조</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c90da550-12cb-42bf-9222-c8a58611e38f/image.png" /></p>
<h3 id="1-🤝-협업-강조">1) 🤝 협업 강조</h3>
<p><strong>프로젝트에서의 협업 경험을 강조</strong>하자. 단순히 <strong>“무엇을 했는가”</strong>보다 <strong>“어떻게(HOW)”, “왜(WHY)”</strong>를 중심으로 서술하면 더욱 효과적이다.  </p>
<p>✅ <strong>좋은 예시</strong></p>
<ul>
<li><strong>&quot;Git과 Jira를 활용하여 협업 프로세스를 구축하고, 코드 리뷰 문화 정착을 통해 팀 내 코드 품질을 향상시켰습니다.&quot;</strong>  </li>
</ul>
<p>❌ <strong>좋지 않은 예시</strong></p>
<ul>
<li>&quot;팀원들과 협업했습니다.&quot; (구체적인 협업 방식이 없음)  </li>
</ul>
<h3 id="2-💡-기술명-강조">2) 💡 기술명 강조</h3>
<p><strong>주요 기술(WebSocket, Kafka 등)은 굵은 글씨로 강조</strong>하여 서류 검토자가 쉽게 눈에 띄도록 하자. 차별화된 기술을 강조하여 강점을 부각시키는 것이 중요하다.  </p>
<h3 id="3-🌱-성장-계획-기술">3) 🌱 성장 계획 기술</h3>
<p><strong>앞으로의 성장 계획(예: 무중단 서버 배포, 스트레스 테스트, 테스트 코드 작성 등)을 명확히 제시하여 기술적 성장 의지를 보여주자.</strong>  </p>
<p>✅ <strong>예시</strong></p>
<ul>
<li><strong>&quot;무중단 배포를 위한 블루-그린 배포 방식 학습 및 적용 예정.&quot;</strong>  </li>
<li><strong>&quot;스트레스 테스트 및 부하 분산 최적화를 위해 k6와 AWS Auto Scaling을 활용할 계획.&quot;</strong>  </li>
</ul>
<hr />
<h2 id="📝-5-이력서-서술-개선-및-대외-활동-정리">📝 5. 이력서 서술 개선 및 대외 활동 정리</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/62917778-553e-41e5-b923-147ace60b07b/image.png" /></p>
<h3 id="1-✂️-불필요한-대외-활동-제거">1) ✂️ 불필요한 대외 활동 제거</h3>
<blockquote>
<p> <strong>현재 진행 중인 활동은 회사 외의 딴짓하는 인상을 줄 수 있으므로, 완료된 활동만 기재</strong>하고, 그로 인해 성장한 점을 강조힌디. </p>
</blockquote>
<p>대외 활동이 완료된 후의 성과와 배운 점을 잘 서술하는 것이 중요합니다.</p>
<h3 id="2-💪-강점-강조-약점-숨기기">2) 💪 강점 강조, 약점 숨기기</h3>
<blockquote>
<p> <strong>강점을 최대한 부각하고, 약점은 드러나지 않도록 구성</strong>한다. </p>
</blockquote>
<p>예를 들어 게임 기획 경험이 있다면 <strong>기획 능력도 겸비한 개발자라는 점을 강조</strong>한다. 약점 대신 강점을 잘 어필하는 것이 이력서의 성공 열쇠이다.</p>
<h3 id="3-🏗️-기술의-안정성-강조">3) 🏗️ 기술의 안정성 강조</h3>
<blockquote>
<p> <strong>프론트엔드는 다양한 기술 사용을 보여주고, 백엔드는 안정적인 기술 스택만 적어 신뢰를 줄 수 있도록 하자</strong>. </p>
</blockquote>
<p><code>프론트엔드</code>는 빠르게 변화하는 기술들이기에 다양한 기술 경험을 드러내되, <code>백엔드</code>의 경우 안정성과 신뢰성을 강조하는 것이 중요하다.</p>
<h2 id="⚙️-6-기타-개선-사항">⚙️ 6. 기타 개선 사항</h2>
<ol>
<li><p>👀 시각적 강조 : 중요한 내용은 굵은 글씨 =&gt; 면접관은 이걸 중점으로 본다고 하심</p>
</li>
<li><p>🗂️ 이력서 템플릿과 플랫폼 적극 활용 :  <strong>다양한 이력서 템플릿을 비교하고, 자신에게 맞는 것을 사용</strong></p>
</li>
<li><p>🖨️ 인쇄 고려  : <strong>이력서는 인쇄했을 때도 가독성이 좋도록 구성하는 것이 중요</strong></p>
</li>
<li><p>🧩 이력서 모듈화 : <strong>이력서에 있는 항목들을 하나의 큰 틀로서 관리하기보다 개별 항목을 모듈화하여 여러 가지 버전을 쉽게 작성할 수 있도록 관리</strong>하자. 이력서의 모듈화를 통해 각기 다른 지원 직무에 맞게 빠르게 수정이 가능하도록 한다.</p>
</li>
</ol>
<h2 id="📌-7-개발자-이력서-관련-추가-팁">📌 7. 개발자 이력서 관련 추가 팁</h2>
<h3 id="1-❓-이력서-경력기술서-자기소개서-포트폴리오">1) ❓ 이력서? 경력기술서? 자기소개서? 포트폴리오?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4d3cc29a-0ef6-4b41-8827-8f6fad96006d/image.png" /></p>
<ul>
<li><strong>이력서</strong>: 핵심 경력과 학력, 기술 스택을 간결하게 나열하며 한눈에 정보를 파악할 수 있게 작성한다.  </li>
<li><strong>경력기술서</strong>: 주요 프로젝트의 역할, 성과, 기술 활용을 상세히 기술해 실무 능력을 강조한다.  </li>
<li><strong>자기소개서</strong>: 지원 동기와 성장 배경을 중심으로 기업에 기여할 비전을 스토리 형식으로 전달한다.  </li>
<li><strong>포트폴리오</strong>: 프로젝트 결과물, 문제 해결 과정, 기술 스택을 시각적 자료로 정리해 신뢰도를 제공한다.</li>
</ul>
<h3 id="2-💡-지원-서류가-중요한-이유">2) 💡 지원 서류가 중요한 이유</h3>
<p><strong>회사 입장에서는 지원자의 경력, 실력, 경험을 검증</strong>해야 한다. 1차적으로 회사 업무에 요구되는 항목들과 매칭되는지 확인하고, 2차적으로 그 수준과 신뢰성을 검증하기 위한 과제/면접의 근거자료로 사용된다.</p>
<h3 id="3-📚-이력서-작성을-위한-사전-준비">3) 📚 이력서 작성을 위한 사전 준비</h3>
<p><strong>지원할 기업의 JD(Job Description)를 읽고 KSA(Knowledge, Skill, Attitude)로 정리</strong>하여 본인과 매칭시켜본다.  </p>
<blockquote>
<p><strong>근거가 부족하다면 3개월, 6개월, 1년 계획을 세워 전문성의 근거를 만드자</strong>. (자격증, 블로그, 컨퍼런스, 스터디, 공모전, 해커톤, 네트워킹 등)</p>
</blockquote>
<h3 id="4-📖-이력서-작성의-3요소-3tory">4) 📖 이력서 작성의 3요소 (3tory)</h3>
<ul>
<li><strong>Territory</strong>: 지원한 Position에 맞게 자신의 전문성 영역을 서술합니다. Generalist인지 Specialist인지 명확히 하여 컨셉을 정리한다. <strong>예시:</strong> &quot;백엔드 최적화에 강한 개발자.&quot;  </li>
<li><strong>History</strong>: 전문성의 레퍼런스가 될 프로젝트나 경험을 중심으로 서술한다. 모든 이력을 나열하기보다 관련 있는 정보만 선택한다.*<em>(사실 신입이면 최대한 넣는 게 좋긴함)  *</em></li>
<li><strong>Story</strong>: Know-How와 Attitude를 중심으로 문제 해결 사례를 설명하고, STAR 기법과 수치화 등을 통해 자신의 능력과 태도를 드러낸다.</li>
</ul>
<hr />
<h2 id="8-이력서-포맷-및-핵심-포인트-✅만약-신입-경험이-많이-업다면">8. 이력서 포맷 및 핵심 포인트 ✅(만약 신입, 경험이 많이 업다면?)</h2>
<h3 id="1-bad-이력서-포맷">1) BAD 이력서 포맷</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0dcf06cd-57a3-4f2a-b2f0-552f76ff040e/image.png" /></p>
<h3 id="2-good-이력서-포맷">2) GOOD 이력서 포맷</h3>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3f7da63a-4db0-47b4-90f3-fcf240a0b2e8/image.png" /></p>
<ul>
<li><a href="https://newstartjoah.tistory.com/197">출처</a></li>
</ul>
<p>랠릿이 적절하게 잘 되어 있어서 이력서 포맷은 <code>랠릿</code>이나 <code>점핏</code> 이력서 포맷 참고하면 될 듯!</p>
<h3 id="3-✅-핵심-포인트">3) ✅ 핵심 포인트</h3>
<blockquote>
<p>이력서는 <strong>단순한 업무 나열이 아니라 본인의 기여와 성과를 강조하는 문서</strong>다. </p>
</blockquote>
<p>모호한 표현 대신 <strong>구체적인 문제 해결 과정과 수치 기반 성과</strong>를 포함해야 한다.  </p>
<p>&quot;API 개발을 했습니다&quot; 대신 <strong>&quot;전략 패턴 적용으로 코드 유지보수성을 30% 향상&quot;</strong>, &quot;성능을 개선했습니다&quot; 대신 <strong>&quot;쿼리 최적화로 응답 속도를 1.5초 → 700ms 단축&quot;</strong>처럼 <strong>문제 → 해결 방법 → 결과</strong> 구조로 서술하면 효과적이다.  </p>
<p>기술 스택도 단순 나열이 아니라 <strong>왜 사용했는지, 어떤 효과가 있었는지</strong>를 설명해야 한다. 협업 경험 역시 <strong>&quot;Git과 Jira 활용으로 코드 리뷰 문화 정착&quot;</strong>처럼 <strong>구체적인 방식과 성과</strong>를 강조하면 좋다.  </p>
<p>마지막으로, <strong>불필요한 내용은 삭제하고 JD에 맞는 경험을 중심으로 정리</strong>하자. 가독성을 위해 <strong>Rallit, Jumpit 등의 이력서 템플릿을 활용</strong>하는 것도 좋은 방법이다. <strong>이력서는 본인의 역량을 효과적으로 전달하는 도구</strong>라는 점을 잊지 말자. 🚀</p>
<h3 id="4-만약-신입이라면">4) 만약, 신입이라면?</h3>
<p><strong>1️⃣ 경험이 부족하더라도 문제 해결 과정과 역할을 강조하자</strong><br />신입 개발자는 실무 경험이 적기 때문에, <strong>국비 프로젝트, 학교 프로젝트, 공모전, 해커톤 등에서 본인이 맡았던 역할과 문제 해결 경험</strong>을 구체적으로 서술하는 것이 중요하다.  </p>
<p>❌ <strong>좋지 않은 예시</strong>  </p>
<ul>
<li>&quot;팀 프로젝트로 웹 서비스를 개발했습니다.&quot; (구체적인 역할과 기여도가 없음)  </li>
</ul>
<p>✅ <strong>좋은 예시</strong>  </p>
<ul>
<li>&quot;팀 프로젝트에서 백엔드 개발을 담당하며, Spring Boot 기반 REST API를 설계 및 구현하였습니다. 데이터베이스 쿼리 최적화를 통해 평균 응답 속도를 1.5초에서 700ms로 단축하였으며, JWT 기반 인증 시스템을 도입해 보안성을 강화했습니다.&quot;  </li>
</ul>
<p><strong>2️⃣ 기술 스택을 단순 나열하지 말고, 적용 과정과 효과를 설명하자</strong><br />&quot;React, Spring 사용&quot;처럼 단순 나열하는 대신, <strong>어떤 이유로 선택했고 어떻게 활용했는지</strong>를 설명하는 것이 좋다.  </p>
<p>❌ <strong>좋지 않은 예시</strong>  </p>
<ul>
<li>&quot;Spring Boot와 MySQL을 사용했습니다.&quot; (선택 이유와 기여 내용이 없음)  </li>
</ul>
<p>✅ <strong>좋은 예시</strong>  </p>
<ul>
<li>&quot;데이터 처리량이 많은 웹 서비스 개발을 위해 Spring Boot와 MySQL을 사용하였으며, Connection Pool을 적용해 DB 연결 부담을 줄였습니다.&quot;  </li>
</ul>
<p><strong>3️⃣ 협업 경험을 강조하자</strong><br />신입의 경우 기술력뿐만 아니라 <strong>협업 경험도 중요한 평가 요소</strong>가 된다.<br />특히 <strong>Git, Jira, Notion, 코드 리뷰 등의 협업 도구 사용 경험</strong>을 강조하면 플러스 요소가 될 수 있다.  </p>
<p>❌ <strong>좋지 않은 예시</strong>  </p>
<ul>
<li>&quot;팀원들과 협업했습니다.&quot; (어떤 방식으로 협업했는지 불명확)  </li>
</ul>
<p>✅ <strong>좋은 예시</strong>  </p>
<ul>
<li>&quot;Git을 활용하여 팀원들과 협업하였으며, Pull Request 기반 코드 리뷰 문화를 도입해 코드 품질을 향상시켰습니다. Jira를 통해 스프린트 계획을 수립하고, Notion을 사용해 문서를 체계적으로 관리했습니다.&quot;  </li>
</ul>
<p><strong>4️⃣ 성과를 수치로 표현하자</strong><br />실제 프로젝트에서 <strong>속도 개선, 사용성 향상, 트래픽 증가</strong> 등의 성과가 있었다면 <strong>가능한 한 수치를 포함하여 작성하는 것이 효과적</strong>이다.  </p>
<p>❌ <strong>좋지 않은 예시</strong>  </p>
<ul>
<li>&quot;웹 페이지의 성능을 개선했습니다.&quot; (얼마나 개선됐는지 모호함)  </li>
</ul>
<p>✅ <strong>좋은 예시</strong>  </p>
<ul>
<li>&quot;Lighthouse 성능 점수를 30점에서 85점으로 개선하였으며, 이미지 최적화 및 코드 분할을 통해 초기 로딩 속도를 3초에서 1.2초로 단축하였습니다.&quot;  </li>
</ul>
<p><strong>5️⃣ 불필요한 내용은 줄이고, JD에 맞는 경험을 중심으로 정리하자</strong><br />기업이 원하는 기술과 역할에 맞춰 이력서를 정리하는 것이 중요하다.<br />예를 들어, 지원하는 회사가 <strong>백엔드 개발자를 찾는다면</strong>, UI 디자인 경험보다는 <strong>API 개발 경험, DB 설계 경험, 성능 최적화 경험</strong>을 강조하는 것이 좋다.  </p>
<blockquote>
<p>📌 <strong>신입이라도 문제 해결 과정, 협업 경험, 기술 적용 사례를 구체적으로 적으면 강한 인상을 줄 수 있다.</strong>  </p>
</blockquote>
<hr />
<h1 id="내꺼-수정해보자😟">내꺼 수정해보자😟</h1>
<blockquote>
<p>이거 적으면서 이전꺼 고치려다가 랠릿 이력서 이전에 저장 잘못해서 업데이트 한 것 다 날림 ㅜㅜㅜㅜㅜ 진짜 한숨 쉬면서 다시 적는 중🥹🥹</p>
</blockquote>
<h2 id="1-👀위치-수정">1. 👀위치 수정</h2>
<h3 id="✅-추천-순서">✅ <strong>추천 순서</strong></h3>
<p>경력이 많지 않은 <strong>주니어 개발자</strong>라면 교육도 중요한 요소가 될 수 있으므로, 학력을 포함한 <strong>&quot;교육&quot;을 조금 더 위로 배치</strong>하는 것이 좋다고 함 그래서 순서를 먼저 수정해보고자 함  </p>
<h3 id="🏆-주니어-개발자를-위한-추천-순서">🏆 <strong>주니어 개발자를 위한 추천 순서</strong></h3>
<ol>
<li><strong>기본 정보</strong> (필수)  </li>
<li><strong>자기소개</strong> – 개발 철학, 강점, 목표  </li>
<li><strong>기술 스택</strong> – 사용 가능한 언어, 프레임워크, 툴  </li>
<li><strong>교육</strong> – 전공, 부트캠프, 관련 과정 등  </li>
<li><strong>경력</strong> – 실무 경험 (많지 않더라도 주요 역할 강조)  </li>
<li><strong>프로젝트</strong> – 개인/팀 프로젝트 및 기여도  </li>
<li><strong>포트폴리오</strong> – 깃허브, 블로그, 개인 웹사이트  </li>
<li><strong>자격증</strong> – 관련 기술 인증이 있다면 추가  </li>
<li><strong>대외활동</strong> – 해커톤, 오픈소스 기여, 스터디 등  </li>
<li><strong>외국어</strong> – 필요하면 공개  </li>
</ol>
<h3 id="✨-왜-이렇게-배치해야-할까">✨ <strong>왜 이렇게 배치해야 할까?</strong></h3>
<p>✅ <strong>경력이 짧다면 &quot;교육&quot;을 경력보다 위로 배치</strong> – 학력이나 수료 과정이 중요할 수 있음<br />✅ <strong>&quot;기술 스택&quot;을 초반에 배치</strong> – 개발자의 역량을 빠르게 어필 가능<br />✅ <strong>&quot;프로젝트&quot;를 경력 아래 배치</strong> – 실무 경험이 적다면 프로젝트를 보완 요소로 활용  </p>
<p>📌 <strong>Tip:</strong>  </p>
<ul>
<li><strong>경력이 많아질수록</strong> &quot;교육&quot;은 아래로 내려도 무방  </li>
<li><strong>주니어라도 프로젝트 경험이 강점이라면</strong> 프로젝트를 경력보다 위로 배치  </li>
</ul>
<p>그래서 순서를 기본 정보 &gt; 기술 스택 &gt; 자기 소개 &gt; 교육 &gt; 경력 &gt; 프로젝트 &gt; 포트폴리오 &gt; 자격증 &gt; 대외활동 순으로 넣어둠  </p>
<h2 id="2-기본-정보">2. 기본 정보</h2>
<h3 id="포괄적인-단어-선택">포괄적인 단어 선택</h3>
<p><code>LMS</code> 도메인 =&gt; <code>에듀테크</code> 도메인으로 변경하여, <strong>좀 더 포괄적</strong>으로 하는 것이 좋다.</p>
<p>LMS를 강조하게 되면, 같은 분야의 도메인으로 가게 되면, 장점이 되나 그렇지 않은 경우 단점이 될 수 있기에 좀 더 포괄적인 에듀테크 도메인으로 하자.</p>
<h3 id="중복되는-내용인-한-줄-소개는-과감히-삭제-자기소개에-초점을-맞춤">중복되는 내용인 한 줄 소개는 과감히 삭제 자기소개에 초점을 맞춤</h3>
<p>자기소개랑 겹쳐서 뭔가 적기가 굉장히 애매했다. 과감히 삭제해버리고 자기소개에 포함시켰다.</p>
<h2 id="3-자기소개">3. 자기소개</h2>
<table>
<thead>
<tr>
<th>전</th>
<th>후</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b85d1981-f25d-4c2f-9525-36535f0a8fa3/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7c2dfe29-fd5a-4ba2-b9b9-c98acd162a27/image.png" /></td>
</tr>
</tbody></table>
<h3 id="🔍-차이점-분석"><strong>🔍 차이점 분석</strong></h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>전</th>
<th>후</th>
<th>개선 포인트</th>
</tr>
</thead>
<tbody><tr>
<td><strong>구조</strong></td>
<td>정보가 길게 나열되어 있음</td>
<td><strong>WHY(목표) → WHAT(성과) → HOW(과정) 구조로 정리</strong></td>
<td><strong>읽기 쉬운 구조로 재정리</strong></td>
</tr>
<tr>
<td><strong>제목 활용</strong></td>
<td>일반적인 내용 나열</td>
<td><strong>&quot;효율과 가치를 함께 만들어가는 개발자&quot;</strong> 등 의미 있는 제목 추가</td>
<td><strong>읽기 전에도 핵심 메시지를 알 수 있도록 개선</strong></td>
</tr>
<tr>
<td><strong>문장 가독성</strong></td>
<td>긴 문장과 나열식 표현이 많음</td>
<td><strong>간결한 문장, 핵심 정보 강조, 문단 구분</strong></td>
<td><strong>가독성 향상 및 정보 전달력 강화</strong></td>
</tr>
<tr>
<td><strong>성과 표현</strong></td>
<td>블로그 글 개수, 조회 수 등 수치 강조</td>
<td><strong>성과(트렌딩 선정, 문의 증가) + 커뮤니티 기여 내용 추가</strong></td>
<td><strong>단순 수치 나열이 아닌 영향력을 강조</strong></td>
</tr>
<tr>
<td><strong>협업 및 성장</strong></td>
<td>기획팀과 협업 경험 언급</td>
<td><strong>배포 자동화 사례 추가 및 팀 기여도 강조</strong></td>
<td><strong>실제 업무에서의 기여도를 명확하게 표현</strong></td>
</tr>
</tbody></table>
<p><strong>📌 개선된 주요 요소</strong>  </p>
<p>✅ <strong>WHY(목표) → WHAT(성과) → HOW(과정) 구조로 정리</strong> → 핵심 메시지를 직관적으로 전달<br />✅ <strong>제목 추가로 내용 강조</strong> → <code>&quot;효율과 가치를 함께 만들어가는 개발자&quot;</code>, <code>&quot;기록이 남긴 흔적, 그리고 새로운 연결&quot;</code><br />✅ <strong>가독성 개선</strong> → 문단을 나누고, 긴 문장을 정리하여 정보 전달력 향상<br />✅ <strong>성과 강조</strong> → 블로그 운영이 단순한 활동이 아니라, <strong>개발자 커뮤니티 기여로 확장</strong><br />✅ <strong>협업 내용 강화</strong> → 팀 내 배포 자동화 기여도를 명확히 하여 실무 기여도 강조  </p>
<h3 id="📌-좀-더-개선해야-방향"><strong>📌 좀 더 개선해야 방향</strong></h3>
<blockquote>
<p>✅ <strong>기술적 깊이 추가</strong> → MyBatis 성능 최적화 경험, 이벤트 개발 사례 보강<br />✅ <strong>협업 과정 적기</strong> → 기획팀·퍼블리셔와의 협업 과정에서 <strong>문제 해결 사례 추가</strong> </p>
</blockquote>
<ol>
<li><p><strong>더 명확한 역할 및 강점 강조</strong>  </p>
<ul>
<li>기존 버전에서는 MyBatis 최적화에 초점을 맞췄지만, <strong>개선 버전에서는 백엔드 개발자로서의 역할(Spring 기반 유지보수, 이벤트 개발, 배포 자동화 기여 등)이 강조됨</strong>.  </li>
<li>이를 유지하면서, <strong>실제 맡은 업무 중 핵심적인 기여도를 더욱 부각</strong>하는 것이 좋음.  </li>
<li><strong>예시 추가 가능</strong> → &quot;이벤트 개발 중 특정 기능의 성능 개선을 위해 <del>한 방식 적용하여 응답 속도 ~</del>% 개선&quot;  </li>
</ul>
</li>
<li><p><strong>기술적인 경험의 깊이를 보강</strong>  </p>
<ul>
<li>개선 버전에서 배포 자동화 기여도가 강조되었지만, <strong>MyBatis 최적화 및 SQL 성능 개선 경험도 함께 녹여서 정리</strong>하면 더 균형 잡힌 자기소개가 될 수 있음.  </li>
<li><strong>예시 추가 가능</strong> → &quot;대량 데이터 조회 시 MyBatis의 <del>~ 전략을 적용하여 평균 응답 시간을 ~</del>ms 단축&quot;  </li>
</ul>
</li>
</ol>
<p>지금까지 회사에서 한 건 단순 업무라🥲🥲 개선사항 이런 것을 적을 수가 없음</p>
<p>솔직히 다 비슷한 업무만 하는데 성능 최적화 이런거는 돌아가는 운영 환경이라 고치지 말아야하기에 수치화 할 것도 없는 게 현실 🥹🥹 하하.. 그래도 이제 점 점.. 더 깊은 이해가 필요한 업무들이 주어지고 있으니 그걸 맡게 되면 업데이트 할 예정</p>
<h2 id="4-교육">4. 교육</h2>
<blockquote>
<p>최신순 위에 정렬 외에 고친 것 없음</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c1f79d03-6ac9-44ce-bc50-80abfbdcb70c/image.png" /></p>
<h2 id="5-경력gpt-이력서-도우미봇-이용">5. 경력(gpt 이력서 도우미봇 이용)</h2>
<blockquote>
<p>가장 적기 애매한... 아직도 많이 고쳐야하는 경력 사항..</p>
</blockquote>
<p>가장 적기 애매하고.. 나는 단순 업무만 해서 gpt에 <code>이력서 도우미 봇</code>을 만들어서 설정해서 도움을 받았음 
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7ae54a38-315f-47e1-a6f5-75250331c974/image.png" /></p>
<p>이런식으로 내가 한 업무, 여태까지 해온 것들을 쭉 나열하면 어느정도 도와줌.. 막막한 사람들에게 추천.. 솔직히 위에서는 <strong>평균 응답 시간을 1.5초에서 700ms로 단축</strong> 같이 적으라고는 했지만.. 내가 아직 그런게 없어서 ㅋㅋㅋ...</p>
<table>
<thead>
<tr>
<th>전</th>
<th>후</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/b80a0cc0-f585-4786-8c0e-e9ec61a075f6/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/373d51af-9c1e-46a8-b9a1-7ac3b5f752f2/image.png" /></td>
</tr>
</tbody></table>
<h3 id="전후-비교-및-개선점-분석"><strong>전후 비교 및 개선점 분석</strong></h3>
<h4 id="✅-전before과-후after-차이점">✅ <strong>전(before)과 후(after) 차이점</strong></h4>
<table>
<thead>
<tr>
<th>항목</th>
<th>전(before)</th>
<th>후(after)</th>
<th>개선된 점</th>
</tr>
</thead>
<tbody><tr>
<td><strong>문장 스타일</strong></td>
<td>설명이 포괄적이며, 추상적인 표현이 많음</td>
<td><strong>구체적인 수치, 기술 적용, 성과 중심 서술</strong></td>
<td>성과가 명확해지고, 객관적인 데이터 기반으로 개선</td>
</tr>
<tr>
<td><strong>업무 내용</strong></td>
<td>유지보수 및 이벤트 페이지 개발을 담당한다고 서술</td>
<td><strong>반복 업무 자동화, JS 및 백엔드 개선, 재사용성을 고려한 개발 방식 강조</strong></td>
<td>기존 업무를 단순 나열하는 대신, <strong>문제 해결과 성과를 포함</strong>하여 설명</td>
</tr>
<tr>
<td><strong>문제 해결 과정</strong></td>
<td>어려운 과제가 있을 경우 직접 시도하고 해결했다고 설명</td>
<td><strong>기획 문서화, 요구사항 정리, 코드 리뷰 프로세스 도입 등의 해결 프로세스 포함</strong></td>
<td>문제를 해결하는 <strong>논리적인 접근 방식과 팀 내 기여도를 강조</strong></td>
</tr>
<tr>
<td><strong>협업 및 커뮤니케이션</strong></td>
<td>기획팀 및 퍼블리셔와의 협업을 진행했다고 언급</td>
<td><strong>팀 프로젝트 개선, 배포 프로세스 최적화, 배포 실패 방지를 위한 체크리스트 구축 등 협업 프로세스 상세화</strong></td>
<td>단순히 협업했다는 내용에서 벗어나 <strong>구체적인 협업 방식과 기여도를 설명</strong></td>
</tr>
<tr>
<td><strong>성과 수치화</strong></td>
<td>&quot;기획자의 기획과 개발자의 관점 차이를 해결했다&quot; 등의 포괄적 서술</td>
<td><strong>&quot;배포 오류 50% 감소&quot;, &quot;이벤트 개발 시간 40% 단축&quot;, &quot;버그 수정 소요 시간 50% 단축&quot; 등 성과 수치화</strong></td>
<td><strong>정량적인 성과를 명시</strong>하여 이력서의 신뢰도 상승</td>
</tr>
</tbody></table>
<h3 id="🚀-추가-개선할-수-있는-부분"><strong>🚀 추가 개선할 수 있는 부분</strong></h3>
<h4 id="1-해결-과정이-더-상세해지면-좋음"><strong>1) 해결 과정이 더 상세해지면 좋음</strong></h4>
<ul>
<li><strong>배포 체크리스트 구축 과정</strong>에서 구체적인 도구 활용 여부(Jenkins, GitHub Actions 등)를 언급하면 좋을 것 같음.</li>
<li><strong>팀 내 피드백을 반영한 개선 사례</strong>가 있다면, &quot;팀 의견을 반영하여 ~ 개선하여 결과적으로 유지보수성을 향상시켰다&quot;는 식으로 설명 가능.</li>
</ul>
<h4 id="2-사용한-기술-스택과-도구-강조"><strong>2) 사용한 기술 스택과 도구 강조</strong></h4>
<ul>
<li><strong>어떤 기술 스택을 활용했는지 구체적으로 명시</strong>하면 기술 이해도가 더 돋보일 수 있음.<ul>
<li>예) &quot;CI/CD 환경에서 Jenkins를 활용하여 자동화 배포 프로세스를 구축함으로써 배포 오류율을 50% 감소&quot;</li>
<li>예) &quot;GitHub Actions을 활용한 배포 자동화 파이프라인 구축으로 평균 배포 시간을 30% 단축&quot;</li>
</ul>
</li>
</ul>
<h4 id="3-더-강한-차별점을-주기-위한-추가-요소"><strong>3) 더 강한 차별점을 주기 위한 추가 요소</strong></h4>
<ul>
<li><strong>기획/운영팀과의 협업 사례</strong>: 단순히 협업했다는 것보다 &quot;운영팀의 요청을 반영하여 개발 프로세스를 변경하고, 이를 통해 유지보수 비용을 절감&quot;한 사례 추가 가능</li>
<li><strong>코드 품질 향상 노력</strong>: &quot;테스트 코드 적용(TDD, 단위 테스트), 코드 리뷰 문화 정착&quot; 같은 개선 사례가 있다면 포함 추천</li>
</ul>
<h2 id="6-프로젝트">6. 프로젝트</h2>
<blockquote>
<p>후.. 이것도 애매하다 나는 한 프로젝트만 하는데..일단 회사 프로젝트는 두고.. 다른 것만 고침</p>
</blockquote>
<p>솔직히 학교에서 한 거는 진짜.. 개 후졌지만 넣을 게 별로 없었음.. 그래서 이번년도에 사이드프로젝트 하고 바꾸려고</p>
<table>
<thead>
<tr>
<th>전</th>
<th>후</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e6a404cd-39d8-4785-8f08-d7b517f137f3/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0dd0bdf3-c856-4d25-9f55-67acf7ed8b5d/image.png" /></td>
</tr>
</tbody></table>
<blockquote>
<p>이거는 국비 팀프로젝트</p>
</blockquote>
<table>
<thead>
<tr>
<th>전</th>
<th>후</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/862c72c5-79f9-47d0-bdc8-6473e7a216ed/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/9a23c1ae-3421-4684-8d97-239be3c098c9/image.png" /></td>
</tr>
</tbody></table>
<p>가장 많이 고쳐야 할 부분이 아닌가 싶다 ㅋㅋㅋㅋ</p>
<h2 id="7-포트폴리오">7. 포트폴리오</h2>
<blockquote>
<p>가장 보여주고 싶은 링크를 상단으로 gitbook은 삭제할까 고민중</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/17423c9a-e95b-482b-a56c-9b5429d67157/image.png" /></p>
<h2 id="8-자격증">8. 자격증</h2>
<blockquote>
<p>자격증도 마찬가지로 최신순으로 가장 상단에 둠</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/585e1205-4413-446a-826d-d995c7210f5b/image.png" /></p>
<h2 id="9-스터디-대외활동-관련">9. 스터디, 대외활동 관련</h2>
<h3 id="왜-했고-어떻게-발전하게-되었는가에-초점">왜 했고 어떻게 발전하게 되었는가에 초점</h3>
<table>
<thead>
<tr>
<th>전</th>
<th>후</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/37fd15f6-ba30-4435-aab1-a3ddec25883e/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/80771dfb-c0b3-4d76-934d-dee415c86a76/image.png" /></td>
</tr>
</tbody></table>
<p>인원, 벌금 등이 중요한 것이 아니라, 이것 스터디를 <code>왜 했고(WHY) 어떻게(HOW)</code> 발전했는지가 중요하다. 그래서 그것에 맞춰서 목표(WHY), 주요 활동 및 성과(HOW)로 수정하였다.</p>
<h2 id="전후-비교-및-개선-분석"><strong>전후 비교 및 개선 분석</strong></h2>
<h3 id="📌-주요-차이점"><strong>📌 주요 차이점</strong></h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>전</th>
<th>후</th>
<th>개선 방향</th>
</tr>
</thead>
<tbody><tr>
<td><strong>구조</strong></td>
<td>글또 10기 활동 개요 중심</td>
<td>WHY(목표) → HOW(주요 활동 및 성과)로 변경</td>
<td><strong>이유(WHY)와 과정(HOW) 중심으로 구조 개선</strong></td>
</tr>
<tr>
<td><strong>내용 초점</strong></td>
<td>인원, 벌금, 활동 기간 강조</td>
<td><strong>목표와 성과 중심(기술 성장, 커뮤니티 확장, 실질적 기여)</strong></td>
<td><strong>목적과 활동을 강조하여 발전 방향 명확화</strong></td>
</tr>
<tr>
<td><strong>목표 설정</strong></td>
<td>2주 1회 이상 블로그 작성</td>
<td><strong>기술적 사고 정리 + 글쓰기 개선에 대한 고민 포함</strong></td>
<td><strong>단순 글 작성 → 더 나은 글쓰기로 발전 목표 확대</strong></td>
</tr>
<tr>
<td><strong>성과 측정</strong></td>
<td>글을 꾸준히 작성하고 기록하는 것</td>
<td><strong>트렌딩 선정, 팔로워 증가, 실무 문제 해결 경험 공유</strong></td>
<td><strong>가시적인 성과(트렌딩 선정, 팔로워 증가) 강조</strong></td>
</tr>
<tr>
<td><strong>커뮤니티 활동</strong></td>
<td>별도 언급 없음</td>
<td><strong>백엔드 빌리지 등 5개 커뮤니티 활동을 통한 인사이트 확장</strong></td>
<td><strong>기술적 성장 외에도 커뮤니티에서의 배움 추가</strong></td>
</tr>
<tr>
<td><strong>취업 지원 기여</strong></td>
<td>개인 성장 중심</td>
<td><strong>취업 준비생들에게 도움 제공, 메일 문의 증가</strong></td>
<td><strong>커뮤니티 기여 및 영향력 강조</strong></td>
</tr>
</tbody></table>
<h3 id="📌-개선-포인트-요약"><strong>📌 개선 포인트 요약</strong></h3>
<p>✅ <strong>WHY(목표) &amp; HOW(성과) 중심으로 구조 정리</strong> → 글쓰기 활동의 <strong>목적과 성과를 명확히</strong> 함<br />✅ <strong>단순 글 작성이 아닌, 기술적 성장과 커뮤니티 기여 방향으로 발전</strong><br />✅ <strong>수치적 성과(트렌딩 선정, 팔로워 증가)를 포함해 가시적인 성과 강조</strong><br />✅ <strong>커뮤니티 활동을 통한 성장, 취업 준비생 지원 등의 영향력을 추가</strong>  </p>
<h2 id="10-마지막-정리">10. 마지막 정리</h2>
<h3 id="✅-최대한-중복을-줄이려고-노력"><strong>✅ 최대한 중복을 줄이려고 노력</strong></h3>
<p>이력서에 <strong>경력 프로젝트 및 경험이 많다 보니, 동일한 내용을 반복하지 않도록 조정</strong>했다.<br />특히, <strong>같은 기술적 기여가 여러 곳에서 언급되지 않도록 정리하여 가독성을 높이는 데 집중</strong>했다.  </p>
<h3 id="📌-정보의-우선순위-고려-순서-정리"><strong>📌 정보의 우선순위 고려 (순서 정리)</strong></h3>
<ul>
<li><strong>가장 중요한 정보부터 배치</strong> → <strong>VELOG 링크를 상단으로 올려, 블로그 활동을 강조</strong>  </li>
<li><strong>프로젝트 및 성과를 중요도 순으로 정리</strong> → 가장 눈에 띄는 성과를 먼저 배치  </li>
</ul>
<h3 id="📌-가독성-향상-길어지지-않도록-간결화"><strong>📌 가독성 향상 (길어지지 않도록 간결화)</strong></h3>
<ul>
<li>긴 문장을 줄이고 <strong>핵심 키워드 중심으로 정리</strong>  </li>
<li>목록, 소제목 등을 활용해 <strong>내용을 빠르게 이해할 수 있도록 구성</strong>  </li>
<li><strong>중요한 키워드는 굵게 강조</strong>하여 가독성을 향상  </li>
</ul>
<h3 id="📌-반복적인-업무만-한-것이-걸려-자동화-경험-강조"><strong>📌 반복적인 업무만 한 것이 걸려 자동화 경험 강조</strong></h3>
<p>단순한 유지보수나 반복 업무만 수행한 것처럼 보이지 않도록,<br /><strong>배포 자동화 프로그램 개발 사례를 포함하여 &quot;팀의 불편함을 해결하고 개선하는 능력&quot;을 강조</strong>했다.<br />→ <strong>비록 업무로 할당된 것은 아니지만, 팀 내 문제를 인식하고 개선한 사례</strong>이므로 중요한 경험으로 기록  </p>
<h3 id="📌-포트폴리오는"><strong>📌 포트폴리오는?</strong></h3>
<ul>
<li>이후 <strong>피그마(Figma)</strong>를 활용하여 <strong>시각적으로 정리된 포트폴리오를 제작할 계획</strong>  </li>
<li><strong>텍스트 기반 이력서에서 다 담을 수 없는 프로젝트 및 기술 스택을 시각적으로 표현</strong>  </li>
</ul>
<p><strong>📌 추가 개선 **  
✅ **이력서와 포트폴리오의 역할 분리</strong> → 이력서는 <strong>핵심적인 성과와 기여</strong>를 강조, 포트폴리오는 <strong>비주얼과 상세 설명</strong> 보완<br />✅ <strong>VELOG &amp; 자동화 사례를 주요 강점으로 활용</strong> → 기술 공유, 개발 문화 기여, 생산성 향상 등 <strong>차별화된 강점 강조</strong><br />✅ <strong>업무 외 기술적 성장 강조</strong> → <strong>커뮤니티 활동, 스터디 경험, 블로그 운영을 통해 얻은 실무 적용 가능한 인사이트 추가</strong><br />✅ 이후 사이드 프로젝트 진행 후 기록
✅ 오픈 소스 기여해보기 등으로 커뮤니티 활동, 기여 등 강조해보기(그냥 약간 작은 오픈 소스라도)</p>
<hr />
<h1 id="tmi-1">TMI</h1>
<p>이력서는 참 어렵지만.. 매번 써봐도 힘들어..그리고 단순 업무만 해온 나에게는 더더욱..🤣🤣
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f6aeb483-9f2b-4b7a-8503-3bab99f37d66/image.png" />
어렵다고 계속 미루는 게 아니라 조금씩 이라도 수정하고 부족해 보여도 지원하면서 서류 합격률이 낮으면 첨삭 받고 하는 것이 가장 베스트인 것 같긴 하다 ㅋㅋ ㅠ</p>
<h2 id="좋은-이력서란">좋은 이력서란</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/cdd7af8c-4ec0-464d-a573-ed3eaf47059e/image.png" /></p>
<p>사실 다들 좋은 이력서란 개인마다 갈리기 때문에 호불호가 덜 갈리는 이력서를 쓰는 게 가장 베스트가 아닐까 싶다...</p>
<p>짧지도 길지도 않은...? (사실 나도 잘 모르겠음)</p>
<blockquote>
<p>아마 이걸 기반으로 제 2차 작당모의랑 글또에서 재첨삭 받을 것 같음 + 사이드프로젝트 하나 더 하고 업데이트를 하지 않을까?</p>
</blockquote>
<p>일단 오늘이 글또 2배 포인트 마지막 날이라서 일단 내야겠다</p>
<h1 id="참고하면-좋은-포스팅들">참고하면 좋은 포스팅들</h1>
<h2 id="이력서-작성-플랫폼">이력서 작성 플랫폼</h2>
<ul>
<li><a href="https://www.surfit.io/">서핏</a></li>
<li><a href="https://www.rallit.com/">랠릿</a></li>
<li><a href="https://www.notion.so/Hi-I-m-James-d3bca45c81934514bcd00c346829d130?pvs=21">Hi, I'm James 👋</a> 
(Notion 템플릿은 이 분꺼 외에도 다양하게 있으니 찾아보세요!)</li>
</ul>
<h2 id="이력서-작성-관련">이력서 작성 관련</h2>
<ul>
<li><a href="https://wonny.space/writing/work/engineer-resume">개발자 이력서 작성하기(feat. 이력서 공개) | Wonny Log</a></li>
<li><a href="https://yozm.wishket.com/magazine/detail/2648/">뽑히는 개발자 이력서는 어떻게 만드나요? | 한날</a></li>
<li><a href="https://velog.io/@yukina1418/%EC%A3%BC%EB%8B%88%EC%96%B4-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%9D%B4%EB%A0%A5%EC%84%9C-%EC%93%B0%EB%8A%94-%EB%B2%95">주니어 개발자 이력서 쓰는 법</a></li>
<li><a href="https://github.com/codingmonster-tv/Awesome_Resume_Portfolio">Awesome_Resume_Portfolio
개발자의 서류 작성에 유용한 자료들을 모아두는 Repo입니다.</a></li>
<li><a href="https://techblog.woowahan.com/11998/">왕초보 신입 개발자의 우당탕탕 이력서 작성기|우아한형제들 기술 블로그</a></li>
<li><a href="https://speakerdeck.com/pluu/andeuroideu-gisul-iryeogseoyi-coeso-jogeon">안드로이드 기술 이력서의 최소 조건</a></li>
<li><a href="https://velog.io/@whatever/%EC%84%9C%EB%A5%98%ED%83%88%EB%9D%BD-80-%EC%9D%B4%EA%B2%83-%EB%95%8C%EB%AC%B8%EC%97%90-%EB%96%A8%EC%96%B4%EC%A7%84%EB%8B%A4">서류 탈락 80%, 이것 때문에 떨어진다.</a></li>
<li><a href="https://datarian.io/blog/why-you-should-create-resume-website">이력서, 웹서비스처럼 만들어야 하는 이유 4가지</a></li>
</ul>
<h2 id="취업-정보-사이트">취업 정보 사이트</h2>
<ul>
<li><a href="https://github.com/jojoldu/junior-recruit-scheduler">주니어 개발자를 위한 취업 정보 repo</a></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/45c91b07-5b6b-4232-a02c-62ef2fd8b6bd/image.png" /></p>