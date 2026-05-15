```
Data and Computer Communications CH 07~08
├─ CHAPTER 7. Data Link Control Protocols
│  ├─ Data Link Control Protocols
│  │  ├─ Frame synchronization
│  │  ├─ Flow control
│  │  ├─ Error control
│  │  ├─ Addressing
│  │  ├─ Control and data
│  │  └─ Link management
│  │
│  ├─ Flow Control
│  │  ├─ Receiver buffer
│  │  ├─ Receiver processing delay
│  │  └─ Buffer overflow
│  │
│  ├─ Stop-and-Wait Flow Control
│  │  ├─ Frame transmission
│  │  ├─ ACK
│  │  ├─ Waiting before next frame
│  │  └─ Link utilization
│  │
│  ├─ Sliding Windows Flow Control
│  │  ├─ Multiple frames in transit
│  │  ├─ Receiver window
│  │  ├─ Transmitter window
│  │  ├─ ACK number
│  │  ├─ Sequence number
│  │  ├─ Receive Not Ready
│  │  └─ Piggyback ACK
│  │
│  ├─ Error Control Techniques
│  │  ├─ Error detection
│  │  ├─ Positive acknowledgment
│  │  ├─ Retransmission after timeout
│  │  ├─ Negative acknowledgment and retransmission
│  │  ├─ Lost frames
│  │  └─ Damaged frames
│  │
│  ├─ Automatic Repeat Request, ARQ
│  │  ├─ Stop-and-Wait ARQ
│  │  ├─ Go-Back-N ARQ
│  │  └─ Selective-Reject ARQ
│  │
│  ├─ Stop-and-Wait ARQ
│  │  ├─ Single frame transmission
│  │  ├─ Waiting for ACK
│  │  ├─ Timeout
│  │  ├─ Retransmission
│  │  ├─ Damaged frame
│  │  ├─ Damaged ACK
│  │  └─ Alternate numbering
│  │
│  ├─ Go-Back-N ARQ
│  │  ├─ Sliding-window basis
│  │  ├─ Outstanding frames
│  │  ├─ RR, Receive Ready
│  │  ├─ REJ, Reject
│  │  ├─ Discarding subsequent frames
│  │  └─ Retransmission from error frame
│  │
│  ├─ Selective-Reject ARQ
│  │  ├─ Selective retransmission
│  │  ├─ Receiver buffering
│  │  ├─ Reduced retransmission
│  │  ├─ Larger buffer requirement
│  │  ├─ Complex transmitter logic
│  │  └─ Satellite link use
│  │
│  └─ High Level Data Link Control, HDLC
│     ├─ Station types
│     │  ├─ Primary
│     │  ├─ Secondary
│     │  └─ Combined
│     ├─ Link configurations
│     │  ├─ Unbalanced
│     │  └─ Balanced
│     ├─ HDLC frame structure
│     ├─ Bit stuffing
│     ├─ Address field
│     ├─ Information field
│     └─ Frame Check Sequence, FCS
│
└─ CHAPTER 8. Multiplexing
├─ Multiplexing
│  ├─ MUX
│  ├─ DEMUX
│  ├─ Multiple inputs
│  └─ Multiple outputs
│
├─ Frequency Division Multiplexing, FDM
│  ├─ Frequency bands
│  ├─ Subcarrier modulation
│  ├─ Composite signal
│  ├─ Bandpass filters
│  └─ Guard bands
│
├─ Time Division Multiplexing, TDM
│  ├─ Time slots
│  ├─ Interleaved data stream
│  └─ Data link control on TDM channels
│
├─ Wavelength Division Multiplexing, WDM
│  ├─ Multiple light beams
│  ├─ Different wavelengths
│  ├─ Optical fiber links
│  ├─ Optical amplifiers
│  └─ Demultiplexing by wavelength
│
├─ Duplex Access Techniques
│  ├─ Frequency-division duplex, FDD
│  ├─ Time-division duplex, TDD
│  ├─ Propagation delay
│  ├─ Burst transmission time
│  └─ Guard time
│
└─ Multiple Channel Access Techniques
├─ Frequency division multiple access, FDMA
├─ Uplink frequency bands
├─ Downlink frequency band
├─ Time division multiple access, TDMA
└─ Time slots
```

# 1. 서론 data link control protocols

**직접 연결된 두 장치가 데이터를 프레임 단위로 안전하고 질서 있게 주고받기 위한 규칙 묶음**

## 1. Frame synchronization

**프레임 경계 맞추기**

010100/101101/001001이런 데이터가 주어졌을 때 여기까지가 한 프레임이라고 끊기

###

## 2. Flow control

**송신자가 수신자가 가능한 용량보다 많은 데이터 보내지 않게하기**

송신자가 무작정 빠르게 보내면 버퍼 오버플로우가 날 수 있어서

## 3. Error control

**프레임 손상 시 어떻게 할 것인지의 규칙**

오류를 감지하고, ACK나 NAK 같은 응답을 받고, 필요하면 재전송하는 방식으로 신뢰성을 올림. 뒤에서 나오는 **ARQ**가 여기에 해당

## 4. Addressing

**누가 보냈고 누가 받을지를 표시**

점대점이면 중요성이 떨어져 보여도 여러 장치가 공유하는 링크에서 중요

## 5. Control and data

**제어정보와 실제 데이터 구분**

데이터 전송할 때 실제 데이터와 제어 정보를 같이 보내기 때문에

제어 정보: 주소, 순서 번호, 오류 검사용 FCS, ACK 정보 등등

실제 데이터: 사용자가 보내는 실제 데이터

## 6. Link management

**링크를 설정하고 유지하고 해제하는 절차**

통신을 하는데 에로사항이 없는지 체크하기. 직접적인 통신과 관련되어있다기보다는 사전 준비.

# 2. Flow Control

**송신자가 수신자의 처리 능력을 넘어서 데이터를 보내지 못하게 조절하는 기술**

### 발생 원인

- buffer: 수신받은 데이터를 잠깐 저장하는 공간. frame이 제대로 왔는지 확인하고, 순서가 맞는지 보고, 필요한 제어 정보를 해석하고, 그다음 상위 계층으로 넘긴다

보내는 쪽은 빠르게 프레임을 밀어 넣을 수 있는데, 받는 쪽은 그걸 버퍼에 저장하고 검사하고 상위 계층으로 넘겨야 하니까 시간이 걸린다

그리고 이 버퍼는 한정되어있다.

버퍼가 꽉 찼는데 송신자가 데이터를 계속 밀어넣으면 오버플로우가 발생한다.

넘친 데이터는 손실된다.

### 왜 데이터 블록째로 송신하지 않고 frame단위로 나눠서 송신하는가?

1. 수신자의 버퍼 크기 문제
2. 오류와 재전송 비용
   - 프레임이 길수록 그 안의 어느 한 비트라도 깨질 확률이 커진다. 그런데 프레임 단위로 오류 검사를 하니까, 긴 프레임 하나가 깨지면 그 긴 프레임 전체를 다시 보내야 한다. 반대로 작은 프레임 여러 개로 나누면, 오류가 난 일부 프레임만 다시 보내면 된다.
3. 공유 매체에서의 공정성
   - 여러 장치가 같은 매체를 나눠 쓰는 상황에서 한 장치가 엄청 긴 데이터 블록을 계속 붙잡고 보내면, 다른 장치들은 기다려야 한다. 그래서 한 station이 매체를 너무 오래 점유하지 못하게 작은 프레임 단위로 끊는 게 좋다. 그래야 다른 송신자들도 중간중간 전송 기회를 얻을 수 있기 때문.

## 1. Stop-and-Wait Flow Control

**프레임 하나 보내고, ACK 받을 때까지 기다리는 방식**

- ACK(Acknowledgement): 수신자가 데이터 받았다는 응답

- 단점
  - 프레임 하나 보내고 ACK가 돌아올 때까지 링크가 놀 수 있다. 특히 거리가 멀어서 propagation delay가 크면, 실제 데이터 전송 시간보다 기다리는 시간이 더 길어질 수 있어. 그래서 link utilization 문제가 나온다.

![link utilization](/static/images/networkImg/ch7-stop-and-wait-Flow-Control.png)

- T: 송신자
- R: 수신자
- a: propagation delay
- 1: Transmission time
- 파란막대: Frame
- 회색막대: ACK

* Stop-and-Wait Flow Control에서 총 걸리는 시간 = t0(기준시각) + 1(Transmission time) + 2a(propagation delay)이다.

* 따라서 link utilization(링크 활용률)이 떨어진다.
* U = 1 / (1 + 2a)
  - a가 작을수록 좋다. 작을수록 활용률이 높아지기 때문에
