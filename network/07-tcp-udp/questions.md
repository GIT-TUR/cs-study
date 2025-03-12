# TCP/UDP 질문 정리

<details>
<summary><strong>Go-Back-N ARQ의 동작 방식과 목적은 무엇인가요?</strong></summary>

ARG(Automatic Repeat reQuest, 자동 재전송 요청) : 오류가 발생한 패킷을 재전송하는 프로토콜

Go-Back-N ARQ : 손실되거나 오류가 발생한 패킷 이후의 모든 패킷을 다시 전송하는 방식

동작 방식 : 송신자는 N개의 프레임을 연속적으로 전달하면, 수신자는 올바르게 수신한 패킷에 관해서 ACK를 보낸다. 만약 특정 프레임이 손실되거나 오류가 발생하면, 그 패킷 이후의 모든 패킷을 재전송한다. 송신자가 ACK를 일정시간동안 받지 못한다면 해당 프레임부터 Go-Back하여 다시 전송

목적 : 신뢰성 있는 데이터 전송 보장, 손실 및 손상된 데이터 복구

</details>
<br/>
<details>
<summary><strong>흐름 제어란 무엇인가요?</strong></summary>
    
수신자가 처리할 수 있는 속도에 맞춰 송신자의 데이터 전송 속도를 조절하는 메커니즘
    
네트워크 송신자가 너무 많은 데이터를 빠르게 전송하게 되면 수신 버퍼오버플로우가 발생할 수 있어 흐름 제어가 필요. Stop-and-Wait, Sliding Window가 있음
    
<details>
<summary><strong>흐름 제어가 필요하지 않은 재전송 기법이 있을까요? 있다면 설명해주세요.</strong></summary>

Selective Repeat ARQ : Go-Back-N ARQ와 다르게 손실된 패킷만 재전송하며, 손실되지 않는 패킷들은 버퍼에 저장하고 이후에 올바른 순서로 조립하기 때문에 수신자의 처리 속도를 고려하지 않아 흐름제어가 크게 필요하지 않는다.

</details>

</details>
<br/>
<details>
<summary><strong>SYN 플러드 공격(SYN flood attack)에 대해 설명하고, 이에 대한 방어책을 설명해주세요.</strong></summary>
    
SYN 플러드 공격은 SYN 패킷만 대량으로 보내고 응답을 보내지 않는 TCP의 3-way handshake 과정에서 발생하는 취약점을 악용한 디도스 공격. 
    
SYN 쿠키를 사용해서 서버가 클라이언트의 요청을 저장하지 않아도 TCP 연결을 처리할 수 있다. 동일한 ip에서 SYN 공격이 들어온다면 제한을 걸거나 방화벽을 설치한다.
</details>
<br/>
<details>
<summary><strong>TCP가 신뢰성을 보장하는 방법에 대해 설명해주세요.</strong></summary>
1. 3-way Handshake를 통한 신뢰할 수 있는 연결 보장<br/>
2. 슬라이딩 윈도우 및 흐름 제어를 통한 데이터 전송 속도 조절<br/>
3. ACK(확인 응답) 및 재전송(ARQ) 메커니즘<br/>
4. 시퀀스 번호와 윈도우 크기를 활용한 정렬 및 중복 방지<br/>
5. 체크섬을 이용한 오류 감지 및 무결성 보장<br/><br/>

<details>
<summary><strong>HTTP/3는 왜 UDP를 사용할까요?</strong></summary>
        
HTTP/3는 UDP 기반의 QUIC(Quick UDP Internet Connections) 프로토콜을 사용
        
1. TCP에서 신뢰성을 보장하기 위해 3-way handshake를 사용하는데 이 과정에서 네트워크 왕복 시간이 길어져 속도가 느려지는데, QUIC는 udp 기반으로 핸드셰이크 과정이 없이 데이터를 전송하므로 더 빠르다.<br/>
2. TCP는 패킷 손실이 발생하면 전체 스트림이 지연되지만 QUIC는 개별 스트림을 독립적으로 처리해서 성능 향상.<br/>
3. TCP는 보안이 기본이 아니기 때문에 TLS로 보안을 강화했어야했는데, QUIC는 암호화가 기본적으로 적용되어 있음.<br/><br/>
</details><br/>
<details>
<summary><strong>브라우저는 어떤 서버가 TCP, UDP를 사용하는지 어떻게 알 수 있을까요?</strong></summary>
        
DNS 조회 과정에서 확인, ALPN(Application-Layer Protocol Negotiation)으로 포로토콜 확인..?
</details><br/>
<details>
<summary><strong>새로운 통신 프로토콜을 개발할 때 TCP, UDP를 사용해 구현한다고 하면, 어떤 기준으로 프로토콜을 선택할건가요?</strong></summary>

파일 전송 같이 데이터 손실이 없어야하고 신뢰성이 더 중요한 경우는 TCP. <br/>
온라인 게임이나, 스트리밍 같이 지연 시간이 더 중요한 경우는 UDP.

</details>
</details>
