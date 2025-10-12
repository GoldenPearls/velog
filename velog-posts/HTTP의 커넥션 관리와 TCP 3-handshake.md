<blockquote>
<p>&quot;이 글은 http 책 읽고 스터디 하기 위해 적은 글입니다.&quot;</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/04811b08-aed8-440b-9435-6c8015de21ac/image.png" /></p>
<p>Key Point</p>
<ul>
<li>Http는 어떻게 TCP 커넥션을 사용하는가?</li>
<li>TCP 커넥션의 지연, 병목, 막힘</li>
<li>병렬 커넥션, keep-alive 커넥션, 커넥션 파이프라인을 활용한 HTTP의 최적화</li>
<li>커넥션 관리를 위해 따라야 할 규칙들</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/993be018-e990-4cf4-9fe2-ce26486a0cb0/image.png" /></p>
<h1 id="tcp-커넥션">TCP 커넥션</h1>
<blockquote>
<p>패킷 교환 네트워크 프로토콜들의 계층화된 집합인 TCP/IP를 통해 이루어진다.</p>
</blockquote>
<h1 id="1-패킷-교환-네트워크-프로토콜이란">1. 패킷 교환 네트워크 프로토콜이란?</h1>
<blockquote>
<p>패킷 교환 네트워크 프로토콜은 데이터를 일정 크기의 작은 단위인 '패킷(Packet)'으로 분할해서, 각 <strong>패킷이 네트워크를 통해 개별적으로 전송되는 방식을 따르는 통신 방법에서 사용하는 규약</strong>이다.</p>
</blockquote>
<h2 id="1-패킷-교환-네트워크의-구조와-동작-원리">1) 패킷 교환 네트워크의 구조와 동작 원리</h2>
<ul>
<li>데이터를 송신 측에서 패킷으로 분할한다.</li>
<li>각 패킷에는 목적지 주소 등 제어 정보가 담긴 헤더가 붙는다.</li>
<li>패킷들은 서로 다른 경로로 독립적으로 전달될 수 있다.</li>
<li>수신 측에서는 패킷을 원래의 데이터로 재조립한다.</li>
</ul>
<h2 id="2-대표적인-패킷-교환-네트워크-프로토콜">2) 대표적인 패킷 교환 네트워크 프로토콜</h2>
<ul>
<li>IP(Internet Protocol): 패킷의 전달 경로 지정과 목표지 주소 부여 등, 가장 근본적인 패킷 처리 규약.</li>
<li>TCP(Transmission Control Protocol): 신뢰성 보장(데이터의 순서, 오류 검출 및 재전송 등)을 담당하며, IP 위에서 동작하는 상위 계층 프로토콜.</li>
<li>UDP(User Datagram Protocol): 오류 제어나 순서 보장은 하지 않고 빠른 전송을 중시하는 비연결형 프로토콜.</li>
<li>X.25: 전화망 기반 공중 데이터 교환망에서 사용된 초기 패킷 교환 프로토콜.</li>
</ul>
<h2 id="3-패킷-교환-프로토콜의-주요-특징">3) 패킷 교환 프로토콜의 주요 특징</h2>
<ul>
<li>네트워크 자원을 효율적으로 공유할 수 있다.</li>
<li>대역폭을 여러 사용자가 효율적으로 나눠쓰기 적합하다.</li>
<li>장애 시 다른 경로로 <strong>우회가 가능해 신뢰성이 높다.</strong></li>
<li>오늘날의 인터넷, 사설망(LAN/WAN) 등 거의 모든 컴퓨터 네트워크에서 표준으로 사용된다</li>
</ul>
<blockquote>
<p>즉, 패킷 교환 네트워크 프로토콜은 인터넷과 같은 네트워크에서 데이터를 쪼개어 전송·전달하고 재조합하는 규칙(대표적으로 TCP, IP, UDP, X.25 등)을 의미한다는 점이 핵심이다.</p>
</blockquote>
<h1 id="2-커넥션이-맺어지고-난-후">2. 커넥션이 맺어지고 난 후</h1>
<h2 id="1--3방향-핸드셰이크와-4방향-핸드셰이크">1)  3방향 핸드셰이크와 4방향 핸드셰이크</h2>
<p>일단 커넥션이 맺어지면 클라이언트와 서버 컴퓨터 간에 주고받은 메시지들은 손실 혹은 손상되거나 순서가 바뀌지 않고 안전하게 전달된다.</p>
<ol>
<li>브라우저가 <a href="http://www.joes-hardware.com%EB%9D%BC%EB%8A%94">www.joes-hardware.com라는</a> 호스트 명을 추출한다.</li>
<li>브라우저가 이 호스트 명에 대한 IP 주소를 찾는다.</li>
<li>브라우저가 포트 번호(80)을 얻는다.</li>
<li>브라우저가 202.43.78.3의 80포트로<code>TCP 커넥션을 생성</code>한다.</li>
<li>브라우저가 서버로 HTTP GET 요청 메시지를 보낸다.</li>
<li>브라우저가 서버에서 온 HTTP 응답 메세지를 읽는다.</li>
<li>브라우저가 커넥션을 끊는다.</li>
</ol>
<blockquote>
<p>우리는 이걸 3방향 핸드셰이크와 4방향 핸드셰이크라고 한다.</p>
</blockquote>
<blockquote>
<p>TCP는 <code>3방향 핸드셰이크(3-way handshake)</code>라는 방식을 사용해 연결을 수립한다.</p>
</blockquote>
<p>세 가지 방식의 악수인데, 말 그대로 세 번의 메시지 교
환을 통해 클라이언트와 서버가 서로 데이터를 주고받을 준비를 하는 과정을 말한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/3b1269ed-7735-4b6a-9888-60f3c5a0ba02/image.png" /></p>
<p><strong>Q. 주고받는 내용만 파악하면 될 것 같은데, 왜 상태까지 함께 확인하는 걸까?</strong></p>
<p>그 이유는 나중에 <strong>실제 데이터를 송수신할 때 이 상태를 보고 전송 가능 여부를 파악</strong>하기 때문이다. 마치 가게에서 밥을 먹으려고 하는데 문 앞에 ‘영업 종료’ 또는 ‘브
레이크 타임’이라고 적혀 있으면 출입할 수 없고 ‘영업 중’이라고 적혀 있어야만 밥을 먹을 수 있는 것과 같다.</p>
<blockquote>
<p>TCP의 연결 종료 방식을 4방향 핸드셰이크(4-way handshake)</p>
</blockquote>
<p>TCP 또한 더 이상 보낼 데이터가 없는데 연결
을 지속하는 것은 비효율적이라고 생각해 데이터 통신이 끝나면 <strong>연결을 끊는 과정</strong>을 거친다.&#x20;</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/f5c7d310-6776-4fe4-9668-99d754dd4c18/image.png" /></p>
<h2 id="2-신뢰할-수-있는-데이터-전송-통로인-tcp">2) 신뢰할 수 있는 데이터 전송 통로인 TCP</h2>
<p>HTTP 커넥션은 몇몇 사용 규칙을 제외하고는 TCP 커넥션에 불과하다. 그렇기에 TCP를 제대로 알아야 하는데 TCP는 HTTP에게 신뢰할 만한 통신 방식을 제공한다.&#x20;</p>
<p><strong>Q1. 그렇다면 신뢰성 있는 통신이란 무엇일까?</strong></p>
<p>컴퓨터 세상에서 신뢰성이 있다는 것은 <strong>오류가 없다는 뜻</strong>이다. 즉, 언제 어디서든 데이터를 온전히 가져다줄 거라는 믿음이 있는 것이다.</p>
<p><strong>Q2. TCP는 패킷의 유실 문제를 해결해주는데.. 어떤 방식으로 해결해줄까?</strong></p>
<p>어떤 패킷이 사라졌는지 파악하기 위해 <strong>패킷마다 번호를 붙이고</strong> 정확히 목적지에 도착했는지 확인하기 위해 <strong>하나의 확인 절차</strong>를 추가했다. ⇒ 이로 인해 충돌 없이 순서에 맞게 HTTP 데이터를 전달한다.</p>
<p><strong>Q3. 데이터를 받았다라는 의사소통이 가능한 방법은?</strong></p>
<p><code>TCP 헤더</code>이다. IP를 포함해 모든 프로토콜은 데이터의 앞에 헤더(header)라는 정보를 추가해 전송하는데 헤더 안에는 <strong>해당 데이터에 대한 정보가 담겨 있다.</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/4c6f51ec-c091-40d6-b80e-4fcbf00a091f/image.png" /></p>
<p>비유하자면 택배 상자에 붙어 있는 운송장 스티커이며, 프로토콜에 따라 필요한 정보가 다르다 보니 출발지. 도착지 같은 공통 부분을 제외하면 헤더는 프로토콜마다 조금씩 다른 형태와 크기를 가지고 있다.</p>
<h2 id="3-tcp-스트림은-세그먼트로-나뉘어-ip-패킷을-통해-전송된다">3) TCP 스트림은 세그먼트로 나뉘어 IP 패킷을 통해 전송된다.</h2>
<p>TCP는 IP 패킷이라는 작은 조각을 통해 데이터를 전송하는데.. HTTP가 최상위 계층으로 HTTP가 메세지를 전송하고자 할 경우, 현재 연결되어 있는 TCP 커넥션을 통해서 메시지 데이터의 내용을 순서대로 보낸다.</p>
<p><strong>HTTP에 보안(S)을 더한 HTTPS</strong>&#x20;</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e4cc4337-12f7-4451-93f3-dcddcd68ab50/image.png" /></p>
<p>암호화는 사실 HTTTPS가 아닌 다른 곳에서 담당하는데, 바로 <code>SSL(Secure Sockets Layer)</code>이다. SSL은 클라이언트와 서버가 서로 데이터를 암호화해 통신할 수 있게 돕는 보안 계층</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/dc1ede24-f25c-4b4f-94f4-4f99d8a01ee9/image.png" /></p>
<blockquote>
<p>여기서 TLS이란?;</p>
</blockquote>
<p>당시 공개된 SSL 2.0에 몇 가지 취약점이 발견되어 이를 해결하기 위해 아
예 구조를 재설계해 SSL 3.0을 배포했는데, 그 이후 <strong>기존 버전과 구분하기 위해</strong> 3.0 다음부터 등장한 SSL의 이름을 TLS로 변경했다.</p>
<p><strong>세그먼테이션</strong></p>
<ol>
<li>TCP는 <code>세그먼트</code>라는 단위로 데이터 스
트림을 잘게 나누고, 세그먼트를 <code>IP 패킷</code>라고 불리는 봉투에 담아서 인터넷을 통해
&#x20;데이터를 전달한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0c1a04fa-3c93-48ff-8d5e-173e9a064cb8/image.png" /></p>
<ol start="2">
<li>각 TCP 세그먼트는 하나의 IP 주소에서 다른 IP 주소로 IP 패킷에 담겨 전달된다.
<br />이 IP 패킷들 각각은 다음을 포함한다.<ol>
<li>IP 패킷 헤더 : 발신지, 목적지 IP 주소, 크기, 기타 플래그</li>
<li>TCP 세그먼트 헤더 : TCP 포트 번호, TCP 제어 플래그, 데이터의 순서와 무결성 검사하기 위해 사용되는 숫자값</li>
<li>TCP 데이터 조각</li>
</ol>
</li>
</ol>
<h2 id="4-tcp-커넥션-유지하기">4) TCP 커넥션 유지하기</h2>
<blockquote>
<p>TCP는 <strong>포트 번호</strong>를 통해서 여러 개의 커넥션을 유지한다.</p>
</blockquote>
<p>포트번호</p>
<ul>
<li>회사 직원의 내선전화와 같다.</li>
<li><code>IP 주소</code>는 <strong>해당 컴퓨터에 연결</strong>되고, <code>포트번호</code>는 <strong>해당 애플리케이션으로 연결</strong></li>
</ul>
<p><strong>TCP 커넥션의 네 가지 값으로 식별 : 유일한 커넥션 생성</strong></p>
<ul>
<li>발신지 IP 주소</li>
<li>발신지 포트</li>
<li>수신지 IP 주소</li>
<li>수신지 포트</li>
</ul>
<blockquote>
<p>서로 다른 두 개의 TCP 커넥션은 네 가지 주소 구성요소의 값이 모두 같을 수 없다. 다만 일부가 같을 수는 있다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/60244fda-fb48-417f-ae32-b300d024186a/image.png" /></p>
<h2 id="5-tcp-소켓-프로그래밍">5) TCP 소켓 프로그래밍</h2>
<blockquote>
<p>운영체제는 TCP 커넥션의 생성과 관련된 여러 기능을 제공한다.</p>
</blockquote>
<p><strong>TCP 프로그래밍 인터페이스</strong></p>
<ul>
<li>소켓 API의 주요 인터페이스<ul>
<li>HTTP 프로그래머에게 TCP와 IP의 세부사항들을 숨긴다.</li>
<li>소켓 API는 유닉스 운영체제용으로 먼저 개발&#x20;</li>
<li>TCP 종단 데이터 구조를 생성하고, 원격 서버의 TCP 종단에 그 종단 데이터 구조를 연결하여 데이터 스트림을 읽고 쓸 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>TCP 종단 데이터 구조를 생성하고, 원격 서버의 TCP 종단에 그 종단 데이터 구조를 연결하여 데이터 스트림을 읽고 쓸 수 있다는 의미</p>
</blockquote>
<ul>
<li>TCP 종단 데이터 구조: 컴퓨터에서 네트워크 통신을 할 때, TCP 소켓을 생성하면 해당 소켓에 연결된 다양한 버퍼(데이터 저장 공간), 시퀀스 번호, 연결 관리 정보 등, 데이터를 송수신하기 위한 구조체가 운영체제 내부에서 구성됨.</li>
<li>원격 서버 TCP 종단: TCP는 항상 송신자와 수신자(클라이언트와 서버) 양쪽 종단(endpoint) 간에 연결이 형성됨</li>
<li>연결: TCP 프로토콜은 <code>세 방향 핸드셰이크 과정</code>을 거쳐 두 종단에 논리적으로 연결을 만드는 과정이다. 이 연결을 통해 양쪽 컴퓨터는 신뢰성 있게 데이터를 주고받을 수 있다.</li>
</ul>
<p><strong>동작 방식</strong></p>
<ul>
<li>애플리케이션(예: 웹 브라우저, 서버 프로그램)이 소켓 API를 통해 TCP 연결을 요청하면 운영체제는 해당 TCP 종단점(Endpoint) 구조를 만들고 관리한다.</li>
<li>연결이 성립되면, 프로그램은 이 소켓(TCP 연결) 통해 데이터를 '스트림' 형태로 읽고 쓸 수 있다. 즉, 파일을 다루듯이 TCP 연결 상에서 데이터를 쪽쪽 읽거나 쓸 수 있게 됨.</li>
<li>TCP는 전송 순서 보장, 오류 검출 및 재전송 등으로 신뢰성을 제공하며 <code>스트림(이어진 데이터 흐름) 형태</code>로 동작한다.</li>
</ul>
<blockquote>
<p>즉, 운영체제가 TCP 연결을 위해 내부적으로 데이터를 송수신할 수 있는 구조(버퍼 등)를 만들고, 이 구조를 원격 서버의 TCP와 연결해, 서로 실시간으로 데이터를 주고받을 수 있다는 뜻이다. 프로그래밍에서는 소켓을 통해 이 연결을 다루고, 결과적으로 TCP 연결을 통해 파일이나 문자열 스트림처럼 네트워크 데이터를 읽고 쓸 수 있다.</p>
</blockquote>
<ul>
<li>TCP API<ul>
<li>기본적인 네트워크 프로토콜의 핸드셰이킹, TCP 데이터 스트림과 IP 패킷 간의 분할 및 재조립에 대한 모든 세부사항을 외부로부터 숨긴다.</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/c711f057-15e2-4f02-bee5-1a7e0576ebfd/image.png" /></p>
<p>그림에 대한 부가설명</p>
<blockquote>
<p>클라이언트와 <strong>서버가 TCP 소켓 인터페이스를 사용하여 상호작용하는 방법</strong>을 순서도로 나타낸 것이다.</p>
</blockquote>
<ul>
<li>TCP 3-way Handshake<ul>
<li>&#x20;<strong>클라이언트(C3: 서버의 IP:포트로 연결한다(connect))</strong>&#xc640; 서버(S4: 커넥션을 기다린다(accept)) 사이에 <code>연결(connection)</code>을 수립하는 과정</li>
<li>이미지의 C3와 S4 과정은 이 3-way Handshake가 성공적으로 완료되어 연결이 맺어지는 순간을 포괄적으로 나타낸다.&#x20;</li>
<li>3-way Handshake 자체는 순서도에 명시된 C3-S4 사이에 SYN-SYN/ACK-ACK의 패킷 교환으로 이루어진다.</li>
</ul>
</li>
<li>TCP 4-way Handshake<ul>
<li>클라이언트와 서버가 연결(connection)을 <code>종료(close)</code>하는 과정입니다. 이미지의 C8(커넥션을 닫는다(close))와 S9(커넥션을 닫는다(close)) 과정은 이 4-way Handshake를 포괄적으로 나타냄</li>
<li>4-way Handshake 자체는 FIN-ACK-FIN-ACK의 패킷 교환으로 이루어진다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>이미지의 순서도는 TCP 소켓 통신을 이용한 일반적인 HTTP 요청/응답의 흐름을 클라이언트와 서버의 역할 분담과 소켓 함수 호출(socket, bind, listen, accept, connect, read, write, close) 중심으로 보여주는 것이며, <strong>그 과정 속에 TCP 3-way Handshake (연결 수립)와 TCP 4-way Handshake (연결 종료)가 포함되어 있다.</strong></p>
</blockquote>
<h1 id="3-tcp의-성능에-대한-고려">3. TCP의 성능에 대한 고려</h1>
<p>HTTP는 TCP 바로 위에 있는 계층이기 때문에 HTTP 트랙잭션의 성능은 그 아래
&#x20;계층인 TCP 성능에 영향을 받는다.</p>
<h2 id="1-http-트랜잭션-지연">1) HTTP 트랜잭션 지연</h2>
<p>HTTP 요청 과정에서 어떤 네트워크 지연이 발생하는지 살펴보면서 TCP 성능에 대한 이야기를 알아볼 예정이라고 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/e1bf80ed-1fcd-41bd-a15b-0d3768dd9329/image.png" /></p>
<p>이 그림은 HTTP의 주요 커넥션, 전송, 처리의 지연을 보여준다. <strong>트랜잭션을 처리하는 시간</strong>은 TCP 커넥션을 설정하고, 요청하고, 응답 메세지를 보내는 것에 비하면 <strong>상당히 짧다.</strong></p>
<p>대부분의 HTTP 지연은 TCP 네트워크 지연 때문에 발생한다.</p>
<p><strong>🔍 HTTP 트랜잭션에서 발생하는 4가지 주요 지연</strong></p>
<table>
<thead>
<tr>
<th>단계</th>
<th>발생 원인</th>
<th>주요 지연 요인</th>
<th>소요 시간 (과거 기준)</th>
</tr>
</thead>
<tbody><tr>
<td>1. 이름 분석</td>
<td>URI의 호스트명을 IP 주소로 변환해야 함.</td>
<td>DNS 이름 분석 (DNS Resolution)</td>
<td>수십 초 (현재는 밀리초 단위로 매우 빠름)</td>
</tr>
<tr>
<td>2. 연결 수립</td>
<td>클라이언트가 서버에 TCP 커넥션을 요청하고 응답을 기다림.</td>
<td>TCP 3-way Handshake</td>
<td>1~2초 (현재는 1초 미만으로 빠름)</td>
</tr>
<tr>
<td>3. 요청 전송 및 처리</td>
<td>클라이언트의 HTTP 요청 메시지가 서버에 전달되고 처리됨.</td>
<td>요청 메시지 전송 시간 및 서버 처리 시간</td>
<td>메시지 크기, 거리, 네트워크 속도 등에 따라 다름</td>
</tr>
<tr>
<td>4. 응답 전송</td>
<td>웹 서버가 HTTP 응답 메시지를 클라이언트에게 보냄.</td>
<td>응답 메시지 전송 시간</td>
<td>메시지 크기, 거리, 네트워크 속도 등에 따라 다름</td>
</tr>
</tbody></table>
<p>HTTP 요청을 보내고 응답을 받기까지의 총 시간은 다음의 4가지 주요 네트워크 지연 시간의 합이다.&#x20;</p>
<ol>
<li>DNS 찾기 (호스트명 $$→$$ IP 주소)</li>
<li>TCP 연결 (3-way Handshake)</li>
<li>요청 처리 (요청 전송 및 서버 처리)</li>
<li>응답 전송 (서버 $$→$$ 클라이언트 응답 전송)</li>
</ol>
<blockquote>
<p>💡 참고: 텍스트에 언급된 지연 시간(수십 초, 1~2초)은 과거 인터넷 환경 기준이며, 현재는 DNS 캐싱과 인프라 발전 덕분에 대부분 훨씬 빠르게 처리된다.</p>
</blockquote>
<h2 id="2-tcp-3-way-handshake-지연">2) TCP 3-way Handshake 지연</h2>
<blockquote>
<p>TCP 3-way Handshake에 의한 지연은 현재 HTTP/2를 사용하더라도 여전히 존재한다.</p>
</blockquote>
<p>HTTP/2는 HTTP 프로토콜 계층의 성능을 획기적으로 개선했지만, 전송 계층(Transport Layer)인 TCP 위에서 동작하기 때문에 TCP 자체의 특성에서 오는 지연을 완전히 없애지는 못한다.</p>
<h3 id="1-tcp-handshake-지연의-원인"><strong>1. TCP Handshake 지연의 원인</strong></h3>
<p>TCP 연결을 새로 설정할 때마다 다음과 같은 <code>왕복 시간(RTT: Round-Trip Time)</code>이 발생한다.</p>
<table>
<thead>
<tr>
<th>순서</th>
<th>주체</th>
<th>패킷 (플래그)</th>
<th>지연 발생</th>
</tr>
</thead>
<tbody><tr>
<td>1단계</td>
<td>클라이언트 → 서버</td>
<td>SYN (커넥션 생성 요청)</td>
<td>1 RTT (왕복 시간)</td>
</tr>
<tr>
<td>2단계</td>
<td>서버 → 클라이언트</td>
<td>SYN + ACK (요청 수락 및 응답)</td>
<td></td>
</tr>
<tr>
<td>3단계</td>
<td>클라이언트 → 서버</td>
<td>ACK (커넥션 완료 확인)</td>
<td></td>
</tr>
</tbody></table>
<ul>
<li>TCP 3-way Handshake: 연결을 수립하기 위해 3번의 패킷 교환(SYN - SYN/ACK - ACK)이 필요하며, 이는 최소 1 RTT의 지연을 발생시킨다.</li>
<li>TLS/SSL Handshake (필수): 대부분의 HTTP/2 통신은 보안상의 이유로 TLS 위에서 이루어지며, 이는 다시 1~2 RTT의 지연을 추가로 발생시킨다.</li>
</ul>
<p>따라서 새로운 연결을 수립할 때는 최소 2~3 RTT의 지연이 발생한다. 사실 이 책에서는 이미 존재하는 커넥션을 재활용하는 것이 해결책이라고 했는데 <strong>이미 2, 3에서 해결책이 나오기 했다.</strong></p>
<h3 id="2-http2의-해결책"><strong>2. HTTP/2의 해결책</strong></h3>
<p>HTTP/2는 이 지연 자체를 제거하지는 못하지만, 지연의 영향을 최소화하도록 설계되었다.</p>
<table>
<thead>
<tr>
<th>지연 최소화 전략</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>단일 연결 유지</td>
<td>HTTP/1.1은 여러 요청을 위해 여러 개의 TCP 연결을 생성했지만, HTTP/2는 하나의 TCP 연결만 사용하여 모든 요청과 응답을 다중화(Multiplexing)하여 전송한다.</td>
</tr>
<tr>
<td>재연결 최소화</td>
<td>이 단일 연결을 오랫동안 유지(Connection Persistency)하여, 매번 요청 시마다 새로운 3-way Handshake를 수행하는 것을 방지한다.</td>
</tr>
</tbody></table>
<h3 id="3-완전한-지연-해결-http3의-등장">3. <strong>완전한 지연 해결 (HTTP/3의 등장)</strong></h3>
<p>이 TCP Handshake 지연 문제를 근본적으로 해결하기 위해 등장한 것이 바로 HTTP/3이다.&#x20;</p>
<ul>
<li>HTTP/3는 TCP 대신 UDP 기반의 <code>QUIC 프로토콜</code>을 사용합니다.</li>
<li>QUIC은 자체적으로 연결 수립 및 TLS 핸드셰이크를 통합하여 최초 연결 시 1 RTT로 줄이고, 재연결 시 0 RTT (즉시 데이터 전송 가능)를 목표로 하여 Handshake 지연을 거의 제거한다.</li>
</ul>
<h3 id="4-chrome의-http-버전-사용-전략">4. <strong>Chrome의 HTTP 버전 사용 전략</strong></h3>
<p>Chrome은 최고의 성능을 위해 가장 최신 버전을 우선적으로 시도하며, 서버 환경에 따라 자동으로 전환된다.</p>
<p><strong>우선순위 (가장 빠른 것부터 시도)</strong></p>
<table>
<thead>
<tr>
<th>우선순위</th>
<th>버전</th>
<th>기반 프로토콜</th>
<th>지연 감소 방법</th>
</tr>
</thead>
<tbody><tr>
<td>1순위</td>
<td>HTTP/3</td>
<td>UDP (QUIC)</td>
<td>TCP Handshake 지연 자체를 제거 (새 연결 1 RTT, 재연결 0 RTT).</td>
</tr>
<tr>
<td>2순위</td>
<td>HTTP/2</td>
<td>TCP</td>
<td>하나의 연결을 오래 유지하여 반복적인 Handshake 회피.</td>
</tr>
<tr>
<td>3순위</td>
<td>HTTP/1.1</td>
<td>TCP</td>
<td>최종 대체 버전.</td>
</tr>
</tbody></table>
<p><strong>작동 방식</strong></p>
<ul>
<li>Chrome은 서버가 HTTP/3를 지원하는지 확인 후, 가능하면 가장 빠른 HTTP/3로 연결을 시도한다.</li>
<li>HTTP/3 연결이 안 되면 HTTP/2로, 그것도 안 되면 HTTP/1.1로 자동 전환된다.</li>
</ul>
<blockquote>
<p>결론: Chrome을 사용하면 웹사이트가 지원하는 가장 최신 버전(HTTP/3)을 이용해 TCP 연결 지연을 최소화한 환경에서 웹을 이용할 수 있다.</p>
</blockquote>
<h3 id="tcp-신뢰성-기능이-http-성능을-저해하는-요인">TCP <strong>신뢰성 기능이</strong> HTTP <strong>성능을 저해하는 요인</strong></h3>
<table>
<thead>
<tr>
<th>요인</th>
<th>작동 원리</th>
<th>$\text{HTTP}$에 미치는 영향</th>
</tr>
</thead>
<tbody><tr>
<td>1. 확인응답 지연 (Delayed ACK)</td>
<td>ACK를 즉시 보내지 않고, 0.1~0.2초 대기하며 같은 방향으로 나갈 데이터 패킷에 ACK를 '편승' 시키려 함.</td>
<td>요청-응답 패턴인 HTTP에서는 편승 기회가 적어 ACK가 지연되면서 성능 저하를 유발.</td>
</tr>
<tr>
<td>2. 느린 시작 (Slow Start)</td>
<td>새 커넥션은 초기 전송 속도(혼잡 윈도우)를 낮게 제한하고, 성공적인 전송을 확인하며 속도를 점진적으로 높여나감.</td>
<td>새 커넥션마다 초기 전송이 느려져 HTTP 트랜잭션의 성능을 저해.</td>
</tr>
<tr>
<td>3. 네이글 알고리즘 (Nagle’s Algorithm)</td>
<td>작은 데이터를 최대 크기가 될 때까지 버퍼링하거나, 모든ACK를 받을 때까지 전송을 지연시켜 네트워크 효율을 높임.</td>
<td>작은 HTTP 메시지가 지연되며, 확인응답 지연과 결합 시 성능 저하가 심해짐. (성능 향상을 위해 TCP_NODELAY로 비활성화 가능)</td>
</tr>
<tr>
<td>4. TIME_WAIT 지연</td>
<td>커넥션 종료 후 2MSL (최대 세그먼트 수명주기의 2배, 보통 2분) 동안 해당 포트 재사용을 제한함.</td>
<td>부하 테스트 등 특정 상황에서 포트 고갈을 일으켜 새로운 커넥션 생성을 막아 성능을 제한함.</td>
</tr>
</tbody></table>
<h2 id="🌐-http2-및-http3의-대응-전략"><strong>🌐</strong> HTTP/2 <strong>및 HTTP/3의 대응 전략</strong></h2>
<p>HTTP의 최신 버전들은 TCP 자체를 수정할 수 없으므로, 상위 계층에서 TCP 문제의 영향을 최소화하거나 TCP 자체를 대체한다.</p>
<h3 id="1-http2-tcp-기반"><strong>1. HTTP/2 (TCP 기반)</strong></h3>
<ul>
<li>대응: TCP 연결을 하나만 맺고 오래 유지하는 <code>지속 커넥션</code>과 <code>다중화(Multiplexing)</code>를 사용한다.</li>
<li>효과: 느린 시작과 핸드셰이크 지연을 한 번만 겪고, 이후에는 연결을 재활용하므로 위 세 가지 TCP 지연 요인의 반복적인 발생을 차단한다.</li>
</ul>
<h3 id="2-http3-udpquic-기반"><strong>2. HTTP/3 (UDP/QUIC 기반)</strong></h3>
<ul>
<li>대응: 전송 프로토콜을 UDP 기반의 QUIC으로 교체했다.</li>
<li>효과: TCP를 사용하지 않으므로 TCP <strong>핸드셰이크, 느린 시작, TIME\_WAIT 지연 문제</strong>가 근본적으로 사라진다. QUIC은 자체적으로 효율적인 혼잡 제어 및 신뢰성을 확보하여 HTTP 성능을 극대화다.</li>
</ul>
<blockquote>
<p>HTTP/3의UDP를 쓰면... 신뢰성이 없지 않나라는 의문..</p>
</blockquote>
<p>전통적으로 신뢰성 있는 통신을 담당했던 TCP와 달리, UDP는 패킷의 순서, 손실 여부 등을 확인하지 않고 단순히 데이터를 전송한다.</p>
<p>하지만 HTTP/3는 UDP 위에서 동작하는 <strong>QUIC</strong>이라는 프로토콜을 사용하며, QUIC이 TCP가 제공했던 <strong>신뢰성 기능을 자체적으로 내장하고 있기 때문에 문제가 없다.</strong></p>
<h1 id="4-http-커넥션-관리">4. HTTP 커넥션 관리</h1>
<h2 id="1-connection-헤더와-홉별-통제">1) Connection 헤더와 '홉별' 통제</h2>
<p>HTTP는 클라이언트와 서버 사이에 프락시/캐시 서버와 같은 <code>중개 서버(홉)</code>를 허용한다.</p>
<ul>
<li>Connection 헤더의 역할: 현재 인접한 두 HTTP 애플리케이션(홉) 사이의 커넥션에만 적용될 옵션(예: <code>close</code>)을 지정.</li>
<li>헤더 보호 (Header Safeguarding): Connection 헤더에 나열된 헤더 필드들은 다음 중개 서버로 전달되지 않도록 메시지 전달 시 삭제되어야 한다. 이는 특정 커넥션 옵션이 다른 커넥션에 영향을 미치는 것을 방지한다.</li>
</ul>
<h2 id="2-순차적-처리로-인한-성능-저하">2) 순차적 처리로 인한 성능 저하</h2>
<p>웹페이지가 여러 객체(HTML, 이미지 등)로 구성되어 있을 때, <strong>각 트랜잭션을 순차적으로 처리하면 성능 문제가 발생한다.</strong></p>
<ul>
<li>지연 발생: 각 객체마다 새로운 커넥션을 맺어야 하므로, 반복적인 핸드셰이크 지연과 느린 시작 지연이 발생</li>
<li>사용자 경험 저하: 객체가 순차적으로 로드되는 동안 사용자는 웹페이지가 텅 비어있는 것을 보게 되어 심리적 지연을 느낀다.</li>
</ul>
<h2 id="3-성능-향상을-위한-4가지-커넥션-기술">3) 성능 향상을 위한 4가지 커넥션 기술</h2>
<blockquote>
<p>HTTP 연결 관리 : <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Connection_management_in_HTTP_1.x">https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Connection_management_in_HTTP_1.x</a></p>
</blockquote>
<p>HTTP는 위와 같은 지연을 줄이기 위해 다음과 같은 커넥션 관리 기술을 사용한다.</p>
<ol>
<li><code>병렬(Parallel)</code> 커넥션: 여러 개의 커넥션을 동시에 맺어 여러 트랜잭션을 동시에 처리하여 로딩 속도를 개선한다. (가장 기본적인 개선 방법)</li>
<li><code>지속(Persistent)</code> 커넥션: 커넥션을 끊지 않고 재활용하여 커넥션을 맺고 끊는 지연을 제거다.</li>
<li><code>파이프라인(Pipelined)</code> 커넥션: 공유된 커넥션을 통해 여러 요청을 순차적으로 보낸 후 응답을 순차적으로  받는다.(지속 커넥션 기반)</li>
<li><code>다중(Multiplexed)</code> 커넥션 (HTTP/2, HTTP/3): 하나의 TCP (또는 QUIC) 커넥션을 통해 여러 요청과 응답을 병렬로 처리하여 성능을 극대화</li>
</ol>
<h2 id="4-http-커넥션의-관리와-최적화-기법">4) HTTP 커넥션의 관리와 최적화 기법</h2>
<h3 id="1-http-단기-연결-모델-short-lived-connections">1. HTTP 단기 연결 모델 Short-lived connections</h3>
<p>HTTP의 초기 모델(HTTP/1.0 기본 모델)인 단기 연결 방식은 각 HTTP 요청이 독립적인 새 $$TCP$$ 커넥션을 통해 완료되는 방식이다.</p>
<p><strong>📉 단기 연결의 비효율성</strong></p>
<p>이 모델의 가장 큰 문제는 <strong>TCP의 효율성을 활용하지 못한다는 것</strong>이다.</p>
<ol>
<li>반복적인 TCP 핸드셰이크: 각 요청마다 TCP 커넥션 설정 과정인 핸드셰이크가 연속적으로 발생하여 시간이 많이 소요된다.</li>
<li>Slow Start 문제: TCP는 지속될수록 전송 효율이 높아지는(Warm Connection) 특성이 있지만, 단기 연결은 매번 새로운(Cold) 연결을 사용하므로,<strong>TCP의 느린 시작 (Slow Start)</strong> 지연을 반복적으로 겪게 되어 최적의 성능을 달성하지 못한다.</li>
</ol>
<p><strong>📌 버전별 적용</strong></p>
<table>
<thead>
<tr>
<th>HTTP 버전</th>
<th>기본 동작</th>
<th>단기 연결 사용 조건</th>
</tr>
</thead>
<tbody><tr>
<td>$$HTTP/1.0$$</td>
<td>단기 연결</td>
<td>$$Connection$$ 헤더가 없거나 값이 <code>close</code>일 때.</td>
</tr>
<tr>
<td>$$HTTP/1.1$$</td>
<td>지속 연결 (기본)</td>
<td><code>Connection: close</code> 헤더가 명시적으로 전송될 때만 사용됩니다.</td>
</tr>
</tbody></table>
<blockquote>
<p>지속된 연결을 지원하지 않는 오래된 시스템을 사용하는 경우가 아니라면, 이 모델을 사용할 이유가 없다.</p>
</blockquote>
<h3 id="2-병렬-커넥션-parallel-connection">2. 병렬 커넥션 (Parallel Connection)</h3>
<blockquote>
<p>HTTP/1.1 이전에는 웹페이지의 다수 객체(HTML, 이미지 등)를 순차적으로 내려받는 방식이 주를 이뤘는데, 이는 각 트랜잭션마다 새로운 TCP 커넥션을 맺고 끊는 <code>오버헤드(HandShake지연, Slow Start지연)</code>로 인해 매우 느렸다.</p>
</blockquote>
<ul>
<li>원리: 클라이언트가 여러 개의 TCP 커넥션을 동시에 맺어 다수의 HTTP 트랜잭션을 병렬로 처리한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/33526a6a-b2dc-4a31-ae48-4f11f374ea8b/image.png" /></p>
<ul>
<li>장점:<ul>
<li>각 커넥션의 지연 시간을 겹치게 하여 총 지연 시간을 단축</li>
<li>클라이언트의 인터넷 대역폭을 한 커넥션이 독점하는 것을 방지하고 잔여 대역폭을 활용</li>
<li>화면에 여러 객체가 동시에 로드되는 것을 보여주어 사용자에게 더 빠르게 느껴지는 심리적 효과를 제공한다.</li>
</ul>
</li>
<li>한계:<ul>
<li>클라이언트의 대역폭이 좁으면 병렬 처리에 따른 성능 이득이 미미하거나, 오히려 다수의 커넥션 생성 부하로 순차적 처리보다 더 느려질 수 있다.</li>
<li>서버는 과부하 방지를 위해 <strong>클라이언트당 허용하는 병렬 커넥션 수(대부분 4~8개)를 제한</strong>한다. 수백 명의 사용자가 과도하게 커넥션을 열면 서버 자원(메모리)이 고갈되어 성능이 저하된다.</li>
</ul>
</li>
</ul>
<h3 id="3-지속-커넥션persistent-connections">3. 지속 커넥션(Persistent Connections)</h3>
<p>사이트 지역성의 특성(대부분의 HTTP 요청이 같은 웹 서버로 향하는 경향)을 활용하여, TCP 커넥션을 유지하여 <strong>재사용하는 기술</strong>이다. 이는 병렬 커넥션의 단점을 보완한다.</p>
<ul>
<li>원리: 트랜잭션이 완료된 후에도 클라이언트나 서버가 끊기 전까지 TCP 커넥션을 계속 유지하여 다음 HTTP 요청에 재사용한다.<ul>
<li>새로운 TCP 핸드셰이크가 필요 없고 TCP의 성능 향상 기능을 활용할 수 있다.</li>
<li>이 연결은 영원히 열려 있는 것이 아니다.&#x20;</li>
<li>유휴 연결은 일정 시간이 지나면 닫힌다</li>
<li>서버는 <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Keep-Alive"><code>Keep-Alive</code></a>헤더를 사용하여 연결을 유지해야 하는 최소 시간을 지정할 수 있다</li>
</ul>
</li>
<li>장점:<ul>
<li>새 커넥션을 맺고 끊는 시간과 대역폭을 절약한다.</li>
<li>매번 TCP 느린 시작 지연을 피하고 이미 <strong>튜닝된 커넥션을 활용하여 더 빠르게 데이터를 전송할 수 있다.</strong></li>
<li>서버에 필요한 커넥션의 총 수를 줄여준다.</li>
</ul>
</li>
<li>종류 및 동작:<ul>
<li>Keep- Alive Connection (HTTP /1.0+)&#x20;</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/5d5d3cfe-8bd9-496e-880e-8447de21dc51/image.png" /></p>
<ul>
<li>HTTP/1.0 연결 :  기본적으로 지속적이지 않는다. Connection 이외의 값으로 설정하면 <code>close</code>(보통 <code>retry-after</code>) 지속된다.</li>
<li>HTTP/1.1 :  지속성이 기본이며 헤더는 더 이상 필요하지 않는다.</li>
<li>단점<ul>
<li>유휴 상태일 때에도 서버 리소스를 소모하고, 과부하 상태에서는 <a href="https://developer.mozilla.org/en-US/docs/Glossary/Denial_of_Service">서비스 거부(DoS) 공격이</a> 발생할 수 있다.</li>
<li>이러한 경우, <strong>유휴 상태가 되는 즉시 종료되는 비지속형 연결을 사용</strong>하면 더 나은 성능을 얻을 수 있다.</li>
</ul>
</li>
</ul>
<h3 id="4-지속-커넥션의-진화-keep-alive에서-http11까지">4. 지속 커넥션의 진화: Keep-Alive에서 HTTP/1.1까지</h3>
<p><strong>1. HTTP/1.0+의 Keep-Alive 커넥션 (실험적 지속 연결)</strong></p>
<blockquote>
<p><code>HTTP/1.0</code>은 기본적으로 <strong>요청마다 새로운 TCP커넥션을 맺는 단기 연결 모델을 사용</strong>했으나, 성능 개선을 위해 <strong>실험적인 Keep-Alive 지속 커넥션을 지원하도록 확장</strong>되었다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7140a0bb-e689-4cd7-9d08-f64298564246/image.png" /></p>
<ul>
<li>성능 이점: 매 트랜잭션마다 커넥션을 맺고 끊는 작업(TCP 핸드셰이크)을 생략하고, TCP 느린 시작(Slow Start) 지연을 피할 수 있어 총 응답 시간이 단축된다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7ec4747b-d059-42e6-975c-2a39f189768a/image.png" /></p>
<ul>
<li>동작 방식 (핸드셰이크):<ul>
<li>클라이언트는 커넥션 유지를 요청하기 위해 <code>Connection: Keep-Alive</code> 헤더를 요청에 포함한다.</li>
<li>서버가 이에 동의하면 응답에도 같은 헤더를 포함하며, 이 헤더가 없으면 클라이언트는 서버가 응답 후 커넥션을 끊을 것으로 추정한다.</li>
</ul>
</li>
<li>옵션 제어: $$Keep-Alive$$ 헤더의 <code>timeout</code> (유지 시간) 및 <code>max</code> (처리할 트랜잭션 수) 파라미터로 커넥션 유지 조건을 설정할 수 있지만, 이는 요청 사항일 뿐 보장되지는 않는다.</li>
<li>제한 사항: 커넥션 유지를 위해서는 엔터티 본문이 <code>Content-Length</code> 또는 청크 전송 인코딩을 통해 정<strong>확한 길이 정보</strong>를 가지고 있어야 <strong>메시지의 끝과 다음 메시지의 시작을 구분할 수 있다.</strong></li>
</ul>
<blockquote>
<p><strong>keep-alive는 사용하지 않기로 결정되어 HTTP/1.1 명세에서 빠졌다.</strong> 하지만 아직도 브라우저와 서버 간에 keep-alive 핸드셰이크가 널리 사용되기 때문에, HTTP 애플리케이션은 그것을 처리할 수 있게 개발해야 한다.</p>
</blockquote>
<p><strong>2. HTTP/1.1의 지속 커넥션 (표준 지속 연결) :</strong> 홉별 헤더의 엄격한 제거 규칙</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/8afaa69d-339b-44df-b369-34ba72ccd078/image.png" /></p>
<p>$$HTTP/1.0$$ Keep-Alive의 설계 문제를 개선하여 HTTP/1.1에서는 더 안정적인 지속 커넥션이 표준으로 도입되었으며, 기본적으로 활성화된다. Connection 헤더는 커넥션 종료 여부를 제어하는 데 사용된다.</p>
<ul>
<li>종료 조건: 커넥션 종료를 원하는 애플리케이션은 <code>Connection: close</code> 헤더를 명시적으로 보내야 한다.</li>
<li>동시 커넥션 제한: 서버 과부하를 방지하기 위해 단일 사용자 클라이언트는 서버당 넉넉잡아 두 개의 지속 커넥션만 유지하는 것이 권장된다.</li>
<li>규칙 1: <strong>홉별 헤더 제거 필수</strong><ul>
<li>프락시는 메시지를 <strong>다음 홉(서버 또는 클라이언트)</strong>&#xc73c;로 전달하거나 캐시에 저장하기 전에, $$Connection$$ 헤더와 $$Connection$$ 헤더에 명시된 모든 필드($$Keep-Alive$$ 포함)를 반드시 제거해야 한다.</li>
<li>목적: 이는 $$Connection$$ 헤더가 다음 연결에 오해를 주어 발생하는 '멍청한 프락시' 문제를 방지하기 위함이다. $$Proxy-Authenticate$$, $$Transfer-Encoding$$ 등 Connection에 명시되지 않은 다른 홉별 헤더도 마찬가지로 제거해야 한다.</li>
</ul>
</li>
<li>규칙 2: <strong>독립적인 지속 커넥션 관리</strong><ul>
<li>HTTP/1.1에서 별도의 설정이 없는 한 모든 커넥션은 <code>지속 커넥션은 기본</code>이다.</li>
<li>&#x20;<strong>종료 조건:</strong>  프록시는 클라이언트와의 커넥션과 서버와의 커넥션을 독립적으로 관리하며, 커넥션 종료를 원하는 애플리케이션은 <code>Connection: close</code> 헤더를 명시적으로 보내야 한다.</li>
<li>유연성: <code>Connection</code> 헤더 값과 관계없이 클라이언트와 서버는 언제든지 커넥션을 끊을 수 있다. 클라이언트는 커넥션이 중간에 끊길 경우 요청을 재시도할 수 있도록 준비되어 있어야  한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>Q. Connection: close와 커넥션 강제 종료의 차이</strong></p>
</blockquote>
<p>종료 조건인 명시적 조건과 언제든 Connection 헤더 값과 관계없이 커넥션을 끊을 수 있는 것은 모순되는 것이 아닌 HTTP/1.1의 커넥션 종료 정책 두 가지 측면에서 설명하고 있는 것이다.</p>
<table>
<thead>
<tr>
<th>정책</th>
<th>내용</th>
<th>의미</th>
</tr>
</thead>
<tbody><tr>
<td>정책 1: Connection: close 명시</td>
<td>커넥션 종료를 원하는 애플리케이션은 $$Connection: close$$ 헤더를 명시적으로 보내야 한다.</td>
<td>정상적인 종료 요청(Graceful Shutdown)을 위한 $$HTTP$$ 프로토콜 규칙이다. 클라이언트 또는 서버가 <em>미래에</em> 더 이상 이 커넥션을 사용하지 않을 것임을 상대방에게 공식적으로 알리는 것</td>
</tr>
<tr>
<td>정책 2: 유연한 강제 종료</td>
<td>$$Connection$$ 헤더 값과 관계없이 클라이언트와 서버는 언제든지 커넥션을 끊을 수 있다.</td>
<td>$$TCP$$ 계층의 속성이자 시스템의 안정성 보장을 위한 규칙. 상대방의 동의 없이도 서버 과부하, <strong>타임아웃, 네트워크 오류 등의 비정상적인 상황</strong>에서 커널 레벨에서 $$TCP$$ 연결을 강제로 끊을 수 있음을 의미한다.</td>
</tr>
</tbody></table>
<p><strong>📌 차이점 요약</strong></p>
<table>
<thead>
<tr>
<th>구분</th>
<th>$$Connection: close$$ 명시</th>
<th>유연한 강제 종료</th>
</tr>
</thead>
<tbody><tr>
<td>목적</td>
<td>정상적, 의도적 커넥션 종료 요청</td>
<td>시스템 부하, 타임아웃, 오류로 인한 긴급/강제 종료</td>
</tr>
<tr>
<td>작용 계층</td>
<td>$$HTTP$$ (애플리케이션)</td>
<td>$$TCP$$ (전송)</td>
</tr>
<tr>
<td>결과</td>
<td>커넥션 종료 후 다음 요청은 새 커넥션으로 처리</td>
<td>응답 도중 연결이 끊기거나(행), 요청이 실패하여 재시도 필요</td>
</tr>
</tbody></table>
<p>따라서, <code>Connection:Close</code>는 규칙에 따른 부드러운 종료 절차를 의미하며, 언제든지 커넥션을 끊을 수 있다는 것은 시스템 레벨에서 발생하는 예외적인 상황에 대한 대비와 탄력성을 강조하는 것이다.&#x20;</p>
<blockquote>
<p>이 유연성 때문에 클라이언트는 응답을 완전히 받기 전에 연결이 끊어질 경우 요청을 재시도할 수 있도록 준비되어 있어야 한다.</p>
</blockquote>
<blockquote>
<p><strong>Q. 홉별 헤더가 뭘까?(Hop - by - HopHeader)</strong></p>
</blockquote>
<p>홉별 헤더는 HTTP 메시지를 전송하는 인접한 두 엔드포인트(홉), 즉 <strong>클라이언트와 프락시, 또는 프락시와 서버 사이에만 유효한 정보를 담는 헤더</strong>이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/7ab96a6c-e2b1-46a3-beda-d406e9a2f2d0/image.png" /></p>
<ul>
<li>'홉(Hop)'의 의미: HTTP 통신 경로에서 메시지가 거쳐가는 각각의 <strong>중개 서버(프락시, 게이트웨이) 또는 최종 서버 자체를 의미</strong>한다.</li>
<li>작용 범위: 홉별 헤더는 메시지가 <strong>다음 홉으로 전달되기 전</strong>에 반드시 <strong>제거</strong>되어야 한다. 이 헤더가 다음 홉에 전달되면, 그 서버는 이 헤더가 자신과 인접한 서버(앞선 홉) 사이의 연결에 대한 것이라고 오해하게 되어 통신 오류를 유발할 수 있다 (이것이 '멍청한 프락시' 문제의 원인).</li>
<li>대표적인 예시:<ul>
<li><code>Connection</code>: 연결 관리 옵션(예: <code>close</code>, <code>Keep-Alive</code>).</li>
<li><code>Proxy-Authenticate</code>, <code>Proxy-Connection</code>: 프락시 인증 및 연결에 관련된 정보.</li>
<li><code>Transfer-Encoding</code>: 메시지 본문의 인코딩 방식(예: 청크).</li>
<li><code>Upgrade</code>: 프로토콜 업그레이드 요청(HTTP/1.1에서 $$WebSocket$$ 등)</li>
</ul>
</li>
</ul>
<p><strong>3.</strong> $$HTTP/2$$ <strong>및</strong> $$HTTP/3$$ <strong>환경에서의</strong> $$Connection$$ <strong>헤더</strong></p>
<p>최신 $$HTTP$$ 버전은 커넥션 관리 방식을 근본적으로 바꿈으로써 $$Connection$$ 헤더의 역할을 대부분 소멸시켰다.</p>
<ul>
<li>역할 소멸: HTTP/2의 <strong>단일 TCP커넥션 다중화</strong>와 HTTP/3의 QUIC(UDP)기반 다중화로 인해 커넥션 유지가 프로토콜의 기본 전제가 되었다. 따라서 Connection : Keep- Alive 같은 홉별 헤더는 불필요해졌으며, 커넥션 관련 옵션은 프레임 계층에서 자동 처리된다.</li>
<li>프락시 역할 변화 :  프락시가 HTTP/2와 HTTP/1.1 간의 프로토콜을 변환해야 할 때, Connection 헤더의제거규칙은 여전히 유효하다. 프락시는 HTTP/2의 커넥션 관리 정보를 HTTP/1.1의 $$Connection$$ 헤더로 변환하더라도, 이를 다음 홉으로 전달하기 전에 반드시 제거해야 한다.</li>
</ul>
<p><strong>4. 프록시의 종류와 규칙 준수</strong></p>
<p>$$HTTP$$ 메시지를 중개하는 모든 프락시(포워드 프락시, 리버스 프락시)는 프락시의 종류나 위치와 관계없이 홉별 헤더 제거 규칙을 엄격히 준수해야 한다.</p>
<table>
<thead>
<tr>
<th>프락시 종류</th>
<th>위치 및 역할</th>
<th>$$Connection$$ 헤더 규칙</th>
</tr>
</thead>
<tbody><tr>
<td>포워드 $$프락시$$</td>
<td>클라이언트 명시 지정 (내부망 등)</td>
<td>$$클라이언트↔프락시$$ 간의 홉별 헤더를 제거하고 서버로 전달</td>
</tr>
<tr>
<td>리버스 $$프락시$$</td>
<td>서버 앞단 (로드 밸런싱, 보안)</td>
<td>$$클라이언트↔프락시$$ 간의 홉별 헤더를 제거하고 서버로 전달</td>
</tr>
</tbody></table>
<blockquote>
<p>결론적으로, $$Connection$$ 헤더 자체는 $$HTTP/1.1$$ 통신에서 여전히 사용되지만, 현대의 프락시는 규칙을 철저히 지켜 다음 홉으로 전달하지 않음으로써 과거HTTP/1.0의 연결 정체 문제를 성공적으로 방지하고 있다.</p>
</blockquote>
<p><strong>5. Keep-Alive와 '멍청한 프락시' 문제</strong></p>
<p>지속 커넥션, 특히 Keep-Alive는 Connection 헤더가 <code>홉별(Hop-by-Hop) 헤더</code>라는 특성 때문에 중개 서버 환경에서 심각한 문제를 일으킨다.</p>
<p><strong>문제 발생 메커니즘</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/22126eaa-2b53-4526-8952-5f75236ce5fe/image.png" /></p>
<ol>
<li>무조건 전달: 멍청한 프락시($$Connection$$ 헤더 처리를 모르는 프락시)가 클라이언트의 <code>Connection: Keep-Alive</code> 요청을 다음 홉 서버에 그대로 전달한다.</li>
<li>오해와 불일치:<ul>
<li>서버: 프락시가 자신에게 커넥션 유지를 요청한 것으로 오해하고 <code>Connection: Keep-Alive</code>를 응답에 포함한다.</li>
<li>클라이언트: 프락시로부터 받은 이 헤더를 통해 프락시가 커넥션 유지를 수락했다고 오해한다.</li>
</ul>
</li>
<li>연결 정체 (Hang): 실제로는 Keep-Alive를 이해하지 못하는 프락시가 서버가 먼저 커넥션을 끊기를 기다리는 동안, 클라이언트가 재활용된 커넥션으로 두 번째 요청을 보낸다. 프락시는 이를 예상치 못하고 해당 요청을 무시하여 클라이언트 커넥션이 타임아웃될 때까지 멈추는(Hang) 문제가 발생한다.</li>
</ol>
<h3 id="5-http-파이프라인-pipelining의-원리-제약-및-대체">5. $$HTTP$$ 파이프라인 ($$Pipelining$$)의 원리, 제약 및 대체</h3>
<p>$$HTTP$$ 파이프라인은 <strong>HTTP/1.1에서 지속 커넥션 (Persistent Connection)의 성능을 극대화</strong>하기 위해 도입된 기술이다.&#x20;</p>
<blockquote>
<p>이는 HTTP/1.0의 기본 모델인 순차적 전송 (응답을 받은 후에만 다음 요청 전송)으로 인해 발생하는 네트워크 지연 문제를 해결하려 했다.</p>
</blockquote>
<p><strong>1. 파이프라인의 원리와 이점</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/409f99b7-2409-4d21-b8d9-edf3f9d90c19/image.png" /></p>
<p><code>파이프라인</code>은 <strong>동일한 지속 연결을 통해 응답이 도착하기를 기다리지 않고 연속적인</strong> $$HTTP$$ <strong>요청을 전송</strong>하는 프로세스이다. 요청들은 서버에 도달하기 전에 큐에 쌓인다.</p>
<ul>
<li>성능 이점:<ul>
<li>$$RTT$$ (왕복시간)감소 : 대기 시간이 긴 네트워크 상황에서 요청/응답 왕복으로 인한 시간을 줄여 전송 대기 시간을 단축시킨다.</li>
<li>$$TCP$$ 효율성: 여러 개의 요청을 TCP의 <code>MSS (최대 세그먼트 크기)</code> 내에 압축하여 전송함으로써 이론적으로 성능 향상을 가져올 수 있다.</li>
<li>커넥션 지연 제거: 지속 커넥션을 사용하므로 매 요청마다 $$TCP$$ 커넥션을 맺고 끊는 지연을 방지한다.</li>
</ul>
</li>
</ul>
<p><strong>2. 파이프라인의 엄격한 제약 사항과 복잡성</strong></p>
<p>파이프라인은 설계상 다음과 같은 엄격한 규칙과 복잡성을 내포하고 있으며, 이로 인해 올바르게 구현하고 디버깅하기가 매우 어렵습니다.</p>
<table>
<thead>
<tr>
<th>카테고리</th>
<th>제약 사항</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>순서 보장</td>
<td>$$HTTP$$ 응답은 요청 순서와 같게 와야 한다.</td>
<td>$$HTTP$$ 메시지에는 순번이 없어 응답이 순서 없이 도착하면 정렬할 방법이 없다. 이 규칙을 지키지 않으면 오류가 발생합한다.</td>
</tr>
<tr>
<td>멱등성 ($$Idempotency$$)</td>
<td>비멱등(non-idempotent) 요청은 파이프라인을 통해 보내면 안 된다.</td>
<td>POST와 같이 서버 상태를 변경하는 요청은 재차 보낼 경우 문제가 발생할 수 있다. 에러 발생 시 클라이언트가 서버에서 처리된 요청을 정확히 알 수 없기 때문이다. GET, HEAD, PUT, DELETE와 같은 <strong>멱등 메서드만 파이프라인 처리가 가능하다.</strong></td>
</tr>
<tr>
<td>커넥션 $$확인$$ $$및$$ $$복구$$</td>
<td>지속 커넥션인지 확인 후 파이프라인을 시작해야 한다.</td>
<td>클라이언트는 커넥션이 언제 끊어지더라도, 완료되지 않은 요청을 언제든지 다시 보낼 준비가 되어 있어야 한다 (예: 서버가 10개 중 5개만 처리하고 임의로 커넥션을 끊을 수 있음).</td>
</tr>
</tbody></table>
<p><strong>3. 현대 브라우저에서 파이프라인이 비활성화된 이유</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a91fdbf9-b38c-45ff-ba8d-1f01fa47f9b1/image.png" /></p>
<p>이러한 근본적인 제약과 현실적인 문제 때문에 $$HTTP$$ 파이프라인은 최신 브라우저에서 기본적으로 비활성화되어 있으며, 대부분의 경우 성능 향상 효과가 미미하다.</p>
<ul>
<li>버그가 있는 프록시 : $$Connection$$ 헤더를 올바르게 처리하지 못하는 버그가 있는 프락시가 여전히 흔하여, 예측하고 진단하기 어려운 이상하고 불규칙적인 동작을 유발한다.</li>
<li>헤드 오브 라인 블로킹 ($$Head-of-Line Blocking, HOL$$): 응답이 요청 순서대로 와야 한다는 규칙 때문에, 앞선 요청에 대한 응답 처리가 지연되면 뒤따르는 모든 요청의 응답도 함께 지연된다.</li>
<li>성능 예측의 어려움: 리소스 크기, 유효 $$RTT$$, 대역폭 등 다양한 요소가 성능 향상에 영향을 미치는데, 중요한 메시지가 덜 중요한 메시지보다 지연되는 비효율적인 전송이 발생할 수 있다.</li>
</ul>
<p><strong>4. HTTP/2 의 대체 기술: 멀티플렉싱</strong></p>
<ul>
<li>파이프라인이 겪는 $$HOL$$ 블로킹과 복잡성을 해결하기 위해 HTTP/2는 <strong>멀티플렉싱 (Multiplexing)</strong>&#xc774;라는 더 나은 알고리즘으로 대체되었다.&#x20;</li>
<li>멀티플렉싱은 단일 $$TCP$$ 커넥션을 통해 요청과 응답을 순서에 관계없이 독립적으로 처리하고 전송할 수 있어, $$HOL$$ 블로킹 문제를 근본적으로 해소한다.</li>
<li>멀티플렉싱 기반의 서버는  프로세스의 생성없이 다수의 클라이언트에게 서비스를 제공할 수 있다.</li>
<li>멀티플렉싱은 물리적 장치의 효율성을 위해&#xc11c;<strong>, 최소한의 물리적 요소로 최대한의 데이터를 전달하려는 데 사용되는 기술</strong>을 말한다. 클라이언트의 수에 상관없이, 서비스를 제공하는 프로세스(서버)의 수는 하나다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/0462e027-b20c-4958-9ad1-4e28a96b7444/image.png" /></p>
<blockquote>
<p>멀티플렉싱(Multiplexing)은 HTTP/2와 HTTP/3의 핵심 기술로, 단일 커넥션을 통해 여러 개의 독립적인 요청과 응답을 동시에 처리하는 방식을 의미한다.</p>
</blockquote>
<p>멀티플렉싱은 요청과 응답 메시지를 <strong>프레임(Frame)</strong>&#xc774;라는 작은 단위로 나누고, 이 프레임들을 하나의 커넥션 위에서 서로 섞어서(인터리빙, interleaving) 전송한다.</p>
<ol>
<li>스트림(Stream): 각각의 요청-응답 쌍은 스트림이라는 가상의 논리적 채널을 통해 독립적으로 처리</li>
<li>프레임(Frame): $$HTTP$$ 메시지는 $$헤더$$ 프레임과 $$데이터$$ 프레임으로 분할된다.</li>
<li>섞어 전송 (Interleaving): 클라이언트와 서버는 서로 다른 스트림에 속한 프레임들을 하나의 물리적 커넥션을 통해 네트워크로 보낸다.</li>
<li>재조립: 수신 측에서는 이 프레임들을 다시 원래의 스트림별로 분류하여 완전한 $$HTTP$$ 메시지로 재조립한다.</li>
</ol>
<blockquote>
<p>멀티플렉싱의 효과: $$HOL Blocking$$ 해결</p>
</blockquote>
<p>멀티플렉싱의 가장 큰 장점은 $$HTTP/1.1$$ 파이프라인의 핵심 문제였던 헤드 오브 라인 블로킹을 해결한다는 점이다.</p>
<table>
<thead>
<tr>
<th>$$HTTP/1.1$$ 파이프라인</th>
<th>$$HTTP/2$$ 멀티플렉싱</th>
</tr>
</thead>
<tbody><tr>
<td>순서 제약: 응답은 요청 순서대로 와야 한다.</td>
<td>순서 무관: 요청과 응답을 독립적인 스트림으로 처리하여 순서에 관계없이 도착할 수 있다.</td>
</tr>
<tr>
<td>$$HOL$$ 블로킹: 첫 번째 요청의 처리가 지연되면, 뒤따르는 모든 요청의 응답이 함께 대기한다.</td>
<td>$$HOL$$ 해소: 스트림이 독립적이기 때문에, 하나의 요청이 지연되어도 다른 요청의 처리가 막히지 않고 계속 진행된다.</td>
</tr>
</tbody></table>
<p><strong>🔍 커넥션 효율성</strong></p>
<ul>
<li>$$HTTP/2$$: 단일 $$TCP$$ 커넥션을 사용한다.</li>
<li>$$HTTP/3$$: 단일 $$QUIC$$ ($$UDP$$ 기반) 커넥션을 사용하며, 이는 $$TCP$$ 자체의 $$HOL$$ 블로킹($$패킷$$ 손실 시 발생하는 문제)까지 해결하여 효율성을 극대화한다.</li>
</ul>
<h3 id="5-http-커넥션-종료-관리-불확실성과-우아한-끊기">5) HTTP 커넥션 종료 관리: 불확실성과 우아한 끊기</h3>
<blockquote>
<p>$$HTTP$$ 커넥션의 종료는 명확한 기준이 없으며, 모든 $$HTTP$$ 클라이언트, 서버, 프락시는 언제든지 $$TCP$$ <strong>전송 커넥션을 임의로 끊을 수 있다.</strong>&#x20;</p>
</blockquote>
<p>이 임의 종료는 일반적인 메시지 전송 후에도 발생할 수 있지만, 에러 상황에서는 메시지 중간 등 엉뚱한 곳에서 발생할 수도 있다.</p>
<p><strong>1. 임의 커넥션 끊기와</strong> $$Content-Length$$ <strong>문제</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/936ed33e-b1ab-4f49-a2a3-926e9513a000/image.png" /></p>
<p>지속 커넥션(특히 파이프라인)의 경우, <strong>서버는 일정 시간 유휴 상태에 있는 커넥션을 임의로 끊을 수 있다.</strong></p>
<ul>
<li>문제 상황: 서버가 커넥션을 끊는 시점에 <strong>클라이언트가 데이터를 전송하고 있다면</strong>, 클라이언트의 요청 메시지는 중간에 문제가 생겨 실패한다.</li>
<li>Content-Length의 역할: 모든 $$HTTP$$ 응답은 본문의 정확한 크기를 나타내는 $$Content-Length$$ 헤더를 가져야 한다.<ul>
<li>오래된 서버 문제: 일부 오래된 $$HTTP$$ 서버는 커넥션을 끊음으로써 데이터 전송이 끝났음을 알리는 방식으로 동작했기 때문에, 이 헤더를 생략하거나 잘못된 값을 응답하는 경우가 있다.</li>
<li>수신자 처리: 클라이언트나 프락시는 커넥션이 끊어졌을 때, 전달된 엔터티 길이와 $$Content-Length$$ 값이 일치하지 않거나 헤더가 아예 없으면 데이터의 정확성을 의심하고 서버에게 다시 확인해야 한다.</li>
<li>프락시 규칙: <code>캐시 프락시</code>의 경우, 오류 복합 발생을 최소화하기 위해 해당 응답을 캐시해서는 안 되며, Content-Length를 정정하려 하지 말고 메시지를 받은 그대로 전달해야 한다.</li>
</ul>
</li>
</ul>
<p><strong>2. 커넥션 끊기와 멱등성(Idempotency)</strong></p>
<p>예상치 못한 커넥션 끊김에 대응할 수 있는 능력이 $$HTTP$$ 애플리케이션에 요구된다. 특히 파이프라인 커넥션에서는 서버가 미처리 요청을 남겨둔 채 커넥션을 끊을 수 있기 때문에 문제가 복잡해진다.</p>
<ul>
<li>멱등성 ($$Idempotency$$): 트랜잭션을 <strong>한 번 실행하든 여러 번 실행하든 항상 같은 결과를 반환</strong>하는 속성을 의미한다.</li>
<li>안전한 재시도: $$GET$$, $$HEAD$$, $$PUT$$, $$DELETE$$, $$TRACE$$, $$OPTIONS$$ 메서드는 멱등하다고 간주된다. 이러한 요청은 커넥션이 끊겨도 재시도해도 안전하다.</li>
<li>위험한 재시도: POST와 같은 비멱등(non-idempotent) 요청은 반복될 경우 서버의 데이터가 중복되거나 변형될 위험이 있다 (예: 온라인 주문 중복).<ul>
<li>규칙: 클라이언트는 POST와 같은 비멱등 요청을 파이프라인을 통해 보내면 안 되며, 커넥션 끊김이 발생했을 경우 자동으로 재시도해서는 안 된다.</li>
</ul>
</li>
</ul>
<p><strong>3. 우아한 커넥션 끊기 (</strong>$$Graceful Connection Close$$<strong>)</strong></p>
<p>$$TCP$$ 커넥션은 데이터를 읽거나 쓰기 위한 입력 큐와 출력 큐를 가진 <strong>양방향 채널</strong>이다. $$HTTP$$ 명세는 예기치 않은 끊김을 피하기 위해 우아하게 커넥션을 끊어야 한다'고 권고한다.</p>
<ul>
<li>전체 끊기 ($$close()$$): $$TCP$$ 커넥션의 입력 채널과 출력 채널을 모두 끊는 방식</li>
<li>절반 끊기 ($$shutdown()$$): $$TCP$$ 커넥션의 입력 채널이나 출력 채널 중 하나만 개별적으로 끊는 방식<ul>
<li>우아한 끊기의 구현: 일반적인 애플리케이션이 우아하게 커넥션을 끊으려면 자신의 출력 채널을 먼저 끊고, 상대방의 출력 채널이 끊기는 것을 기다려야 합니다.</li>
<li>절반 끊기의 안전성: 출력 채널을 끊는 것은 비교적 안전하지만, 클라이언트가 데이터 전송을 끝냈다고 확신할 수 없는 이상 입력 채널을 끊는 것은 위험하다.</li>
</ul>
</li>
<li>$$Connection Reset$$ $$by$$ $$Peer$$ $$에러$$: 이미 종료된 입력 채널에 데이터가 도착하면, 운영체제는 $$TCP connection reset by peer$$ 메시지를 클라이언트에 보낸다. 이 심각한 에러는 버퍼에 저장된, 아직 읽히지 않은 응답 데이터까지 모두 삭제시키는 부작용을 일으킬 수 있으며, 파이프라인 커넥션에서 특히 위험다.</li>
</ul>
<blockquote>
<p>결론: 우아한 종료는 리셋 위험 없이 커넥션을 온전히 종료하기 위해 출력 채널을 먼저 끊고 상대방의 종료를 기다리는 방식이며, 애플리케이션은 상대방이 절반 끊기를 구현했는지 확신할 수 없으므로, 강제 종료($$close()$$) 전에 입력 채널의 상태를 주기적으로 확인하여 리소스를 보호해야 한다.</p>
</blockquote>