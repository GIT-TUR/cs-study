## DNS 질문

<details>
    <summary>
        <strong style="font-size: 20px">DNS란 무엇인가요?</strong>
    </summary>
    도메인 네임 시스템으로, 인터넷 도메인 이름을 IP 주소로 변환하는 시스템입니다.
    <br/>
    <details>
        <summary>
            <strong>DNS는 몇 계층 프로토콜인가요?</strong>
        </summary>
        애플리케이션 계층 프로토콜로, OSI 7 모델의 응용 계층입니다. 사용자 애플리케이션(브라우저)이 요청하는 도메인 이름을 IP 주소로 변환하는 서비스를 제공하므로 애플리케이션 계층 프로토콜로 분류됩니다.
        <br/>
    </details>
    <details>
        <summary>
            <strong>TCP/UDP 중 어떤 것을 사용하나요?</strong>
        </summary>
        단일 요청과 응답으로 완료되어 복잡한 연결이 필요하지 않고 빠르게 통신할 수 있으며, 응답이 오지 않으면 단순히 쿼리를 재전송하면 되기 때문에 기본적으로 UDP를 사용합니다. 하지만 DNS 응답 크기가 512바이트를 초과하거나 신뢰성이 필요한 작업에서는 TCP를 사용합니다.
        <br/>
    </details>
    <details>
        <summary>
            <strong>DNS 조회 과정에는 어떤 것들이 있나요?</strong>
        </summary>
        <br/>
        재귀적 쿼리와 반복적 쿼리가 있습니다.
        재귀적 쿼리는 클라이언트가 DNS 리졸버에게 도메인 이름에 대한 최종 응답을 요청하는 방식이고,
        반복적 쿼리는 DNS 서버가 알고 있는 정보만 응답하고, 다음 단계의 서버 정보를 클라이언트에게 알려주는 방식입니다.
        일반적으로 사용자의 컴퓨터가 로컬 DNS 리졸버에게 재귀적 쿼리를 요청하고, 리졸버는 다른 DNS 서버들과 반복적 쿼리를 통해 응답을 찾습니다.
    </details>
    <br/>
</details>
<details>
    <summary>
        <strong style="font-size: 20px">DNS 쿼리 과정에서 손실이 발생하면 어떻게 처리할까요?</strong>
    </summary>
    <br/>
    <details>
        <summary>
            <strong>캐싱된 DNS 쿼리가 잘못되면 어떻게 에러를 보정할까요?</strong>
        </summary>
        <ul>
          <li>1. 시간 초과 매커니즘 : 쿼리를 보낸 후 일정 시간동안 응답이 오지 않으면 시간 초과로 간주하고 재시도합니다.</li>
          <li>2. 재전송 : UDP 기반 DNS 쿼리는 응답이 오지 않으면 쿼리를 재전송합니다. 백오프 시간을 점진적으로 증가시키며 재전송하고(1, 2, 4초,...) 대부분의 리졸버는 2-3회 재시도합니다.</li>
          <li>3. 대체 서버 사용 : 특정 DNS 서버가 응답하지 않으면, 다른 DNS 서버로 쿼리를 보냅니다.</li>
          <li>4. DNS 페일오버 : 권한 있는 네임 서버는 보통 여러 대가 중복 구성되어 있어, 하나가 실패해도 다른 서버가 응답할 수 있습니다.</li>
          <li>5. TCP 폴백 : UDP 쿼리가 실패하거나 응답이 잘린 경우, 더 안정적인 TCP를 사용한 쿼리로 전환합니다.</li>
          <li>6. EDNS0(Extension Mechanisms for DNS) : 현대적인 DNS 구현에서는 더 큰 패킷 크기와 추가 옵션을 지원하는 EDNS0을 사용합니다</li>
        </ul>
        <br/>
    </details>
    <br/>
</details>
<details>
    <summary>
        <strong style="font-size: 20px">리졸버에 대해 아는 만큼 설명해주세요</strong>
    </summary>
    기본적으로 사용자가 입력한 도메인 이름을 IP 주소로 바꿔주는 기능을 합니다. 재귀적으로 사용자 대신 DNS 계층 구조를 탐색하여 도메인의 최종 IP 주소를 찾아내고, 이미 해석한 도메인 이름과 IP 주소의 매핑 정보를 캐싱합니다.
    <br/>
</details>
<details>
    <summary>
        <strong style="font-size: 20px">DNS 스푸핑은 무엇인가요?</strong>
    </summary>
    공격자가 DNS 시스템을 속여 합법적인 도메인 이름을 악의적인 IP 주소로 연결하도록 만듭니다.
    <ul>
      <li>1. 가로채기 : 공격자는 사용자와 DNS 서버 사이의 통신을 가로챕니다.</li>
      <li>2. 위조된 응답 전송 : 공격자는 실제 DNS 서버보다 먼저 위조된 DNS 응답을 사용자에게 보냅니다.</li>
      <li>3. 캐시 감염 : 위조된 정보가 DNS 캐시에 저장되어, 이후의 모든 사용자 요청도 악의적인 목적지로 연결됩니다.</li>
    </ul>
    <br/>
    <details>
        <summary>
            <strong>DNS 스푸핑으로부터 보호하기 위한 방법에는 무엇이 있을까요?</strong>
        </summary>
        <ul>
          <li>DNSSEC(DNS Security Extensions) 사용: 디지털 서명을 통해 DNS 데이터의 무결성 검증</li>
          <li>DNS over HTTPS(DoH) 또는 DNS over TLS(DoT) 사용: DNS 쿼리의 암호화</li>
          <li>DNS 서버의 보안 패치 최신화</li>
          <li>신뢰할 수 있는 DNS 제공업체 사용</li>
          <li>네트워크 모니터링을 통한 비정상적인 DNS 활동 감지</li>
        </ul>
        <br/>
    </details>
</details>
