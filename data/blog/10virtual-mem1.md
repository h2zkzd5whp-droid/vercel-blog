Virtual Memory I (가상 메모리 구현)
│
├─ 1. Paging (페이징)
│   ├─ 개념
│   │   ├─ 물리 메모리를 고정 크기 블록으로 분할 → Frame
│   │   ├─ 논리 메모리를 같은 크기 블록으로 분할 → Page
│   │   ├─ 페이지 크기 = 2의 거듭제곱 (보통 4KB)
│   │   └─ 물리 메모리는 비연속(noncontiguous) 할당 가능
│   │
│   ├─ 주소 변환 (Address Translation)
│   │   ├─ 가상 주소 = <VPN :: Offset>
│   │   ├─ VPN(가상 페이지 번호) → 페이지 테이블 인덱스
│   │   ├─ 페이지 테이블 → PFN(물리 프레임 번호) 결정
│   │   └─ 물리 주소 = <PFN :: Offset>
│   │   예) 32bit 가상 / 20bit 물리 / 4KB 페이지
│   │       → Offset 12bit, VPN 20bit, PTE 2²⁰개
│   │
│   ├─ 페이지 테이블 (Page Table)
│   │   ├─ OS가 관리, 프로세스마다 1개
│   │   ├─ VPN당 PTE 1개
│   │   └─ PTE 구성 비트
│   │       ├─ Valid(V) : 사용 가능 여부 (0이면 메모리에 없음)
│   │       ├─ Reference(R) : 접근됨 여부
│   │       ├─ Modify(M) : dirty 여부 (쓰기 발생 시)
│   │       ├─ Protection : R / W / X 권한
│   │       └─ PFN : 물리 프레임 번호
│   │
│   ├─ 장점
│   │   ├─ 물리 메모리 할당 쉬움 (free frame만 가져옴)
│   │   ├─ 외부 단편화 없음
│   │   ├─ page out 쉬움 (전부 같은 크기)
│   │   ├─ 보호 쉬움
│   │   └─ 공유 쉬움
│   │
│   └─ 단점
│       ├─ 내부 단편화 존재
│       ├─ 성능 오버헤드 (주소당 메모리 2회 참조) → 해결: TLB
│       └─ 공간 오버헤드 (페이지 테이블이 큼)
│           → 해결: multi-level / inverted page table
│
├─ 2. Demand Paging (요구 페이징)
│   ├─ 개념 : 필요할 때만 페이지를 메모리에 적재
│   │   └─ 효과: I/O↓, 메모리↓, 응답속도↑, 사용자↑
│   ├─ 메인 메모리를 page cache로 사용 → 가득 차면 교체(eviction)
│   ├─ 쫓겨난 페이지 → disk(swap file), dirty일 때만 write
│   │
│   ├─ Page Fault (페이지 폴트)
│   │   ├─ evicted 페이지 접근 → exception 발생 (회복 가능)
│   │   └─ Page Fault Handler 동작
│   │       ① swap file에서 페이지 위치 찾기 (invalid PTE 이용)
│   │       ② 빈 프레임으로 read
│   │       ③ PTE를 valid로 갱신
│   │       ④ 실패한 명령 재시작
│   │       (빈 프레임 없으면 → page replacement algorithm)
│   │
│   ├─ 동작 이유 : Locality
│   │   ├─ Temporal locality (시간 지역성)
│   │   └─ Spatial locality (공간 지역성)
│   │
│   └─ "Demand"인 이유
│       ├─ 프로세스 시작 시 모든 PTE valid = false
│       ├─ 실행하면 코드/데이터 페이지에서 즉시 fault (Cold miss)
│       └─ 실제 demand된 것만 적재
│
└─ 3. Segmentation (세그멘테이션)
    ├─ 개념
    │   ├─ 메모리를 논리적 단위로 분할 (code, stack, heap…)
    │   ├─ 가변 크기, 순서 무관
    │   ├─ 가상 주소 = <Segment# :: Offset>
    │   └─ 세그먼트별 독립적 증가/축소 가능
    │
    ├─ HW 지원
    │   ├─ Segment Table (segment#당 base/limit 쌍)
    │   └─ 변환: offset < limit 이면 base + offset, 아니면 protection fault
    │
    ├─ 장점
    │   ├─ 증가/축소 자료구조 처리 쉬움
    │   ├─ 세그먼트 단위 보호 쉬움
    │   └─ 공유 쉬움 (shared library 등)
    │
    └─ 단점
        ├─ Segment Table 큼 (HW 캐시 사용)
        └─ 외부 단편화 (가변 길이 → 동적 할당 문제)

[비교] Paging vs Segmentation
  ├─ 블록 크기      : 고정(4KB~64KB)        vs 가변
  ├─ 주소 지정      : page# + offset        vs segment# + offset
  ├─ 교체           : 쉬움(동일 크기)       vs 어려움(맞는 자리 탐색)
  ├─ 단편화         : 내부                  vs 외부
  ├─ 선형 주소공간  : 1개                   vs 다수
  ├─ 프로그래머 투명: Yes                   vs No
  ├─ 코드/데이터 분리 보호 : No             vs Yes
  └─ 발명 이유      : 큰 선형 주소공간      vs 논리적 독립 공간(공유·보호)

[하이브리드] Segmentation with Paging (IA-32)
  ├─ 세그먼트로 논리 단위 관리 + 페이지로 고정 분할
  ├─ 세그먼트가 "pageable" → 외부 단편화 제거
  └─ 변환 흐름: selector → segment descriptor → linear address
                → page directory → page table → page frame

# 1. Paging
## 1. 개념
**virtual memory → page table → physical memory**

- 프로세스가 사용하는 메모리를 물리 메모리 상의 비연속적인(noncontiguous) 위치에나누어 배치할 수 있게 한다.
- virtual-mem과 logical(physical)-mem을 동일한 크기로 자른다(4kb가 대중적)
- 크기가 n페이지인 프로그램을 실행하려면, n개의 빈 프레임(free frame)을 찾아 프로그램을 적재해야 한다
- 운영체제는 모든 빈 프레임을 추적한다
- 가상 주소를 물리 주소로 변환하기 위한 페이지 테이블(page table)을 설정

### 유저관점에서 추가 개념
- 유저는 연속적인 메모리만 본다
    - Virtual address space (VAS)

- 실제로 페이지들은 물리 메모리 전체에 흩어져(scattered) 저장된다.
    - 가상 주소를 물리 주소로 변환하는 매핑이 존재한다.
    - 이 매핑 과정은 프로그램에게 보이지 않는다.

- process A가 process B에 엑세스 못해서 자연스럽게 protection도 해결된다.
- Process A는 Process B의 메모리 구조나 페이지 매핑 정보를 알 수 없어야 한다. 
    - 왜냐: 
        - 다른 프로세스의 데이터를 읽을 수 있고
        - 다른 프로세스의 데이터를 수정할 수 있고
        - 시스템 전체의 보안과 안정성이 깨질 수 있으니까
- 그래서 절대 유저레벨에게 보여주지않는다

- 프로그램을 한 번 종료헀다가 재시작하면 vm은 같은 값이 나오지만 실제 물리 메모리는 다른 값이다.

## 2. page table는 어떻게 구성되어있나? 



