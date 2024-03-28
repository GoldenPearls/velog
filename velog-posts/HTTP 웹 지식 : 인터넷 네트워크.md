<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d43dca66-8606-4bd2-a16c-103b145d491f/image.png" /></p>
<blockquote>
<p>💡 <strong>간단 요약 :</strong> 
인터넷 통신은 IP 프로토콜을 통해 이뤄지고, TCP는 연결 지향적이고 신뢰성이 높은 가상 회선 방식, UDP는 간단하고 빠른 데이터그램 방식이야. TCP는 연결 설정 후 안전하게 데이터 전송하고, UDP는 빠르게 전송하되 순서나 에러에 대한 보장은 없어. 포트는 프로세스 식별에 쓰이고, DNS는 도메인 명을 IP 주소로 변환해줘.</p>
</blockquote>
<blockquote>
<p>🔗 사진과 강의 출처 : <a href="https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC">김영한님의 HTTP 웹 기본 지식</a></p>
</blockquote>
<h1 id="1-인터넷-통신">1. 인터넷 통신</h1>
<blockquote>
<p>어떤 방식으로 어떻게 수많은 복잡한 상황을 헤쳐서 도착할 수 있을까?</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d77191dd-9649-43a6-9a07-ea341fe8caf0/image.png" /></p>
<h1 id="2-ip인터넷-프로토콜-역할">2. IP(인터넷 프로토콜 역할)</h1>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/87f098e6-a385-4241-a8cd-060968e04cbf/image.png" /></p>
<ul>
<li>데이터가 안전하게 도달하기 위한 최소한의 규칙</li>
<li>지정한 <code>IP 주소(IP Address)</code>에 데이터 전달</li>
<li><code>패킷(Packet)</code>이라는 통신 단위로 데이터 전달</li>
</ul>
<p>IP 패킷에는 출발지 IP, 목적지 IP, 기타 전송데이터를 담고 전달하게 된다.</p>
<h2 id="클라이언트-패킷-전달">클라이언트 패킷 전달</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/38d766c9-6e81-41a8-9e96-ed09545c0930/image.png" /></p>
<h2 id="서버-패킷-전달">서버 패킷 전달</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/96d1cdf3-5149-47a2-adf8-685a5020f31e/image.png" /></p>
<h2 id="ip-프로토콜의-한계">IP 프로토콜의 한계</h2>
<ol>
<li><strong>비연결성</strong></li>
</ol>
<ul>
<li>패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송</li>
</ul>
<ol start="2">
<li><strong>비신뢰성</strong></li>
</ol>
<ul>
<li>중간에 패킷이 사라지면?</li>
<li>패킷이 순서대로 안오면? 중간에 다른 노드를 탈 가능성도 있음</li>
</ul>
<ol start="3">
<li><strong>프로그램 구분</strong></li>
</ol>
<ul>
<li>같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?</li>
</ul>
<h1 id="3-tcpudp">3. TCP/UDP</h1>
<blockquote>
<p>IP의 위와 같은 한계를 해결해주기 위한 해결책</p>
</blockquote>
<h2 id="인터넷-프로토콜-스택의-4계층">인터넷 프로토콜 스택의 4계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/1f57e7d3-20ef-4c2b-b363-f66a765c3962/image.png" /></p>
<p>네트워크 인터페이스 계층은 LAN카드 등등 포함한 것이고 IP 위에 전송 계층이 있으면서 IP의 한계를 보완해준다고 생각하면 된다.
<img alt="" src="https://velog.velcdn.com/images/prettylee620/post/41463f93-a2da-41c9-ab34-1ccffccf579c/image.png" /></p>
<ol>
<li>프로그램이 메세지 생성</li>
<li>SOCKET 라이브러리를 통해 OS 계층에 메세지 전달</li>
<li>그 위에 TCP 정보 생성이 씌워지게 되며, 메세지 데이터를 포함하게 된다.</li>
<li>또 그 위에 <code>IP 패킷</code>이 생성되며 씌워지게 되고, TCP 데이터까지 포함하게 된다.</li>
</ol>
<ul>
<li><code>packet</code>이란?<ul>
<li>컴퓨터 네트워크에서 데이터를 주고받을 때 정해 놓은 규칙</li>
<li>pack + bucket : 정보를 보낼 때 특정 형태에 맞추어 보낸다는 것</li>
<li>즉, 컴퓨터 간에 데이터를 주고받을 때 네트워크를 통해서 전송되는 데이터 조각</li>
<li>정체를 방지하기 위해 packet를 사용</li>
</ul>
</li>
</ul>
<ol start="5">
<li>LAN카드를 통해서 나갈 때 <strong>Ethernet frame</strong>이 씌워지게 됨</li>
</ol>
<ul>
<li><code>Ethernet frame</code>이란?<ul>
<li>LAN에 등록된 MAC 주소 등을 포함하게 됨</li>
<li>데이터 링크 계층 프로토콜의 데이터 단위이며, 기본 이더넷 물리 계층 전송 매커니즘을 사용한다.</li>
<li>이더넷 링크의 데이터 단위는 이더넷 프레임을 페이로드로 전송</li>
</ul>
</li>
</ul>
<h2 id="tcpip-패킷-정보">TCP/IP 패킷 정보</h2>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/a844b1cd-306d-4f89-a112-49abd931a600/image.png" /></p>
<h2 id="tcp-특징">TCP 특징</h2>
<h3 id="전송-제어-프로토콜transmission-control-protocol">전송 제어 프로토콜(Transmission Control Protocol)</h3>
<h3 id="연결지향--tcp-3-way-handshake-가상-연결-o-물리적-연결-x">연결지향 : <strong>TCP 3 way handshake (가상 연결 O, 물리적 연결 X)</strong></h3>
<ul>
<li>SYN : 접속 요청(동기화의 약자) ACK(승인) : 요청 수락</li>
<li>이렇게 되면 양쪽에서 접속 요청, 수락을 다 하는 것이라 <strong>클라이언트도 서버를 믿을 수 있고 서버도 클라이언트를 믿을 수 있다.(신뢰성)</strong></li>
<li>결국 응답이 안오면 연결이 안되있네 하고 데이터 전송을 안하게 되는 것</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ba162a1b-e1aa-49b8-a2dd-28df61cd7a12/image.png" /></p>
<h3 id="순서-보장">순서 보장</h3>
<ul>
<li>서버 내부에서 최적화도 가능함</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/79704da9-3b5f-419f-9124-80af0107631b/image.png" /></p>
<h3 id="신뢰할-수-있는-프로토콜">신뢰할 수 있는 프로토콜</h3>
<h3 id="데이터-전달-보증">데이터 전달 보증</h3>
<h3 id="현재는-대부분-tcp-사용">현재는 대부분 TCP 사용</h3>
<h2 id="tcp-제어-방법">TCP 제어 방법</h2>
<h2 id="udp-특징">UDP 특징</h2>
<ol>
<li>사용자 데이터그램 프로토콜(User Datagram Protocol)</li>
</ol>
<ul>
<li><strong>송신부와 수신부 간의 연결을 지원하지 않고</strong> 데이터 그램 형태의 통신 지원</li>
</ul>
<ol start="2">
<li>하얀 도화지에 비유(기능이 거의 없음)</li>
<li>연결 지향 X - TCP 3 way handshake x</li>
<li>데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름</li>
<li>정리</li>
</ol>
<ul>
<li>IP와 거의 같다 + PORT + 체크섬<ul>
<li>체크섬(checksum) : 데이터의 무결성 보장하여 오류 검출로 최소한의 신뢰성을 보장한다.</li>
</ul>
</li>
<li>애플리케이션에서 추가 작업 필요</li>
<li>하나의 pc에서 ip에서 어떤 애플리케이션인지 구분하는 방법 : port</li>
<li>TCP는 느리기에 http3가 나오면서 최적화하기 위해 UDP를 사용하면서 뜨고 있음</li>
</ul>
<h2 id="패킷-교환-방식">패킷 교환 방식</h2>
<blockquote>
<p><code>TCP (전송 제어 프로토콜)</code>는 가상 회선 방식을 사용하고, <code>UDP (사용자 데이터그램 프로토콜)</code>는 데이터그램 방식을 사용</p>
</blockquote>
<p>패킷 교환 방식은 가장 많이 사용하는 데이터 통신 방식으로, 가상 회선을 이용한 방식과 데이터 그램을 이용한 방식이 있다.</p>
<ol>
<li>가상 회선 방식 : 데이터를 주고받기 전에 패킷을 전송할 경로인 가상 회선을 설정해서 모든 패킷을 같은 경로로 전송한다.</li>
<li>데이터 그램 방식 : 패킷마다 최적의 경로로 전송되는 방식으로, 송신부에서 보낸 패킷의 순서와 수신부에 도착하는 패킷의 순서가 다를 수 있다.</li>
</ol>
<h1 id="4-port">4. PORT</h1>
<blockquote>
<p>즉, 같은 IP 내에서 프로세스를 구분하기 위한 것이 포트이다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/d2776701-2c95-4ec1-9bab-eac43f4c17c6/image.png" /></p>
<p>한 번에 둘 이상(서버와) 연결해야 한다면, 어떤 것에 대한 패킷인지 알 수 없다. 즉, 같은 IP 내에서 프로세스를 구분하기 위한 것이 포트이다.</p>
<h3 id="예시">예시</h3>
<blockquote>
<p>출발지 PORT와 목적지 PORT를 TCP 세그먼트가 포함하기 때문에 알 수 있다.</p>
</blockquote>
<ul>
<li>0 ~ 65535 할당 가능</li>
<li>0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋음</li>
<li>FTP - 20, 21</li>
<li>TELNET - 23</li>
<li>HTTP - 80</li>
<li>HTTPS - 443</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/ee223c71-9279-4137-92f5-b92c893895ee/image.png" /></p>
<h1 id="5-dns">5. DNS</h1>
<ol>
<li>IP는 기억하기 어렵다</li>
<li>IP는 변경될 수 있다.</li>
</ol>
<h2 id="dnsdomain-name-system">DNS(Domain Name System)</h2>
<ul>
<li>전화번호부</li>
<li>도메인 명을 IP 주소로 변환</li>
<li>숫자로 된 IP 주소를 사람이 이해하기 쉬운 문자 형태로 표현한 것</li>
<li>호스트 컴퓨터 이름(www), 소속 기관 이름(hankook), 소속 기관의 종류(co), 소속 국가명(kr) → <a href="http://www.hankook.co.kr">www.hankook.co.kr</a></li>
<li>문자로 된 도메인 네임을 컴퓨터가 이해할 수 있는 IP 주소로 변환하는 역할을 하는 시스템을 <strong>DNS(Domain Name System)</strong>라고 하며, 이런 역할을 하는 서버를 <strong>DNS 서버</strong>라 함 <strong>★</strong></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/prettylee620/post/2162e27d-9408-4297-81d2-591c34fd2a73/image.png" /></p>