# network

**1. OSI 7 계층**

- OSI 7계층이 등장한 이유와 계층이 나누어진 이유
- 계층 간 데이터 캡슐화/역캡슐화 과정의 동작 원리
- TCP/IP 4계층

> [OSI 7 계층 정리](./01-osi-7-layers/main.md)

**2. MAC**

- MAC 주소의 구조와 원리
- 유니캐스트, 멀티캐스트, 브로드캐스트
- 스위치의 MAC 주소 학습 프로세스

> [MAC 정리](./02-media-access-control/main.md)

**3. ARP**

- ARP의 존재 이유
- ARP의 동작 방식
- ARP 요청의 비대칭적 설계의 장점과 단점
- ARP 캐시

> [ARP 정리](./03-address-resolution-protocol/main.md)

**4. IP**

- IP 주소의 구조와 설계
- IPv4, IPv6
- IP 패킷의 구조와 각 필드의 위치와 설계 목적
- IP Fragmentation
- 서브네팅과 CIDR
- DHCP

> [IP 정리](./04-internet-protocol/main.md)

**5. NAT**

- NAT 등장 이유
- NAT 테이블 구조와 관리 방식
- 정적 NAT, 동적 NAT, PAT
- NAT Traversal
- NAT와 방화벽의 관계
- IPv6에서도 사용하려는 이유

> [NAT 정리](./05-network-address-translation/main.md)

**6. 라우팅**

- 라우팅 기본 원리
- 라우팅 발전 과정(정적 라우팅, 동적 라우팅)
- 거리 벡터 라우팅과 링크 상태 라우팅의 차이
- 라우팅 테이블
- SDN

> [라우팅 정리](./06-routing/main.md)

**7. TCP/UDP**

- TCP의 3-way handshake, 4-way handshake가 3-way, 4-way인 이유
- TCP 흐름 제어, 혼잡 제어
- TCP 재전송 매커니즘
- UDP의 특성과 UDP가 실시간, DNS에서 유리한 이유

> [TCP/UDP 정리](./07-tcp-udp/main.md)

**8. HTTP/HTTPS**

- HTTP 버전별 등장 이유와 특징
- HOL, 멀티플렉싱
- HTTPS의 TLS 핸드셰이킹 과정
- HTTP/3에서 UDP를 이용해 QUIC을 구현한 방법

> [HTTP/HTTPS 정리](./08-http-https/main.md)

**9. 대칭키/비대칭키**

- 대칭키 암호화 원리
- 비대칭키 암호화 원리
- RSA
- 대칭키와 비대칭키를 함께 사용하는 하이브리드 방식

> [대칭키/비대칭키 정리](./09-symmetric-asymmetric-keys/main.md)

**10. 쿠키와 세션**

- 쿠키와 세션이 필요한 이유
- 쿠키의 동작 원리
- 세션의 동작 원리
- 쿠키와 세션을 사용할 때 고려해야하는 것
- JWT

> [쿠키와 세션 정리](./10-cookies-sessions/main.md)

**11. DNS**

- DNS의 등장 이유
- DNS의 계층적 구조
- DNS 리졸버의 동작 방식
- DNS 캐싱

> [DNS 정리](./11-domain-name-system/main.md)

**12. 로드 밸런싱**

- 로드밸런싱 기본 원리
- 로드밸런싱 알고리즘
- 헬스 체크 매커니즘
- L4, L7 로드 밸런싱의 차이

> [로드 밸런싱 정리](./12-load-balancing/main.md)
