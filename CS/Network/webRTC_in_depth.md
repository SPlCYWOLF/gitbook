# 🍳 WebRTC in depth

[ref 1](https://surprisecomputer.tistory.com/8?category=909008) [ref 2](https://millo-l.github.io/WebRTC-구현-방식-Mesh-SFU-MCU/) [ref3](https://andonekwon.tistory.com/59) [ref 4](https://rosypark.tistory.com/291?category=756213)

---

## 1. webRTC 서버의 종류

![https://blog.kakaocdn.net/dn/cgwqd2/btqTPx4qe3L/KhxJmMTD8hP61Vap7LXRQk/img.webp](https://blog.kakaocdn.net/dn/cgwqd2/btqTPx4qe3L/KhxJmMTD8hP61Vap7LXRQk/img.webp)

1. Signaling 서버 (P2P / Mesh)
   - uplink : N개, downlink: N개
   - 장점: 서버 자원 최소화, P2P => 빠른 속도 => 실시간성 보장
   - 단점: 1:N or N:M 연결에서 클라이언트 부하 급상승 => 느린 속도 => UX down
2. SFU (selective forwarding unit)
   - uplink : 1개, downlink: N개
     종단 간 미디어 트래픽을 중계하는 중앙 서버 방식
   - 장점: P2P 대비 클라이언트 부하 down
   - 단점: P2P 대비 속도 down, 서버 비용 up, 대규모 N:M 연결에서는 클라이언트가 많은 부하 감당
3. MCU (multi-point control unit)
   - uplink : 1개, downlink: 1개
     다수의 송출 미디어를 중앙 서버에서 하나로 가공 or 혼합 해서 유저들에게 전달
   - 장점: 클라이언트 부하 최소화, 위 두개 서버종류 대비 N:M 구조에 적합
   - 단점: 중앙 서버의 높은 컴퓨팅 파워 요구 => 돈 많이 듬, 높은 작업 비용 => 실시간성 & UX down

<br>

## 2. How does it work?

- Signaling :
  - peer 간의 커뮤니케이션 세션의 연결, 중계, 중단을 뜻함

- 시그널링 프로세스 :
  - SDP 를 교환 (피어 간의 네트워크 정보 공유)
  - peer들은 ICE candidate를 교환 (발신 피어 입장에서 상대 피어와 통신 가능한 방법 후보자들 뽑아서 보내라고함)
    1. 피어간 TURN 서버와 STUN 서버를 교환
    2. 서로 가능한 STUN서버와 TURN서버 정보를 교환
    3. peer 간에 사용해 통신할 최적의 후보 통신 방법 선별
  - webRTC 연결 완료

- 시그널링 프로세스 (실 생활 비유)
  1. A 가 B에게 데이트 신청 하고픔
  2. A는 B에게 접근하기 위해,  B가 받아줄 만한 데이트 플랜들을 리스트 업 함
  3. A는 B에게 하트 시그널을 보냄 (데이트 플랜들을 보내고 선택권을 줌)
  4. B는 하트 시그널을 받고, 원하는 데이트 플랜을 답장해줌
  5. 결정된 데이트 플랜으로 A와 B는 만남을 가지게 되고, 헤어지기 까지 유지됨

<br>

## 3. 필수 용어 정리

- STUN server

  - Session Traversal Utilities for NAT

  - 공용 인터넷 망에 위치,

    라우터의 NAT 뒤에 있는 peer가 공인 ip 주소를 요청할 때,

    해당 주소를 확인하고 접근 가능한 ip port 정보를 알려주는 역할

    - NAT 클라이언트가 STUN 서버로 요청 보냄 => 자신의 public IP 를 응답 받음.

      고로, NAT 환경에서도 P2P 통신을 가능케 함

  - 대부분이 STUN 이용하여 연결 성공적으로 함

  > 요약: 외부 네트워크 주소를 얻는데 사용됨

- NAT

  - Network Address Translation
  - 외부 네트웍에 알려진 것과 다른 IP 주소를 사용하는 내부 내트웍에서 IP 조수를 변환하는 프로세스
  - 주소 변환 기능은 라우터나 방화벽에 설치됨
  - NAT 환경에서는 private IP 를 별도로 가지기 때문에 P2P 통신 불가.
  - 종류 2가지 :
    1. static NAT
    2. dynamic NAT

- TURN server

  - Traversal Using Relays around NAT
  - STUN 서버의 개념을 포함한 Super set
  - peer들간의 미디어 스트리밍을 릴레이하기 위해 사용함
  - 서로 공용주소 가짐

  > P2P 연결 실패하면, 트래픽 중계하는데 활용됨

- SDP

  - Session Description Protocol

  - 멀티 미디어 세션 파라미터를 협상하는 프로토콜.

    미디어에 대한 meta data로,

    1. 사용할 수 있는 코덱
    2. 사용되는 프로토콜
    3. bit rate
    4. bandwidth 등

    서로간의 네트워크 정보를 공유하는 프로토콜.

- ICE

  - interactive connectivity establishment
  - client 가 모든 통신 가능한(필수적인) 주소를 식별하는 프로세스. 결과적으로 STUN 메세지를 TURN 서버로 요청 및 응답함.