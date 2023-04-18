# 5주차 - CPU 스케줄링

# 기본 개념

## CPU-입출력 버스트 사이클

- CPU 스케줄링의 성공은 프로세스들의 다음과 같은 관찰된 성질에 의해 좌우
    - 프로세스의 실행은 CPU 실행과 입출력 대기의 사이클로 구성
    - CPU 버스트로 시작하여, 뒤이어 입출력 버스트가 발생, 
    이어 또 다른 CPU 버스트가 발생, 이어 또다른 입출력 버스트 등으로 진행
    - 마지막 CPU 버스트는 실행을 종료하기 위한 시스템 요청과 함께 끝남
- **CPU 스케줄링은 CPU 버스트 부분에 할당**

<img width="350" alt="image" src="media/CPU-scheduling-img/Untitled.png">
<br>
<br>

## CPU 스케줄러

- OS는 준비 큐에 있는 프로세스들 중에서 하나를 선택해 실행

- 준비 큐는 반드시 선입 선출 방식의 큐는 아님
 <br>

## 선점 및 비선점 스케줄링

<img width="600" alt="image" src="media/CPU-scheduling-img/Untitled 1.png">
<br>
<br>

- CPU 스케줄링이 발생하는 상황들

1. 프로세스가 실행 상태에서 대기 상태로 전환될 때
2. 프로세스가 실행 상태에서 준비 상태로 전환될 떄
3. 프로세스가 대기 상태에서 준비 상태로 전환될 때
4. 프로세스가 종료할 때

- **비선점 스케줄링**

    - 조건 1,4 하에서만 스케줄링이 발생하는 경우 → 협조적 스케줄링

- **선점 스케줄링**

    - 비선점 이외의 모든 스케줄링

<br>
<br>

# 스케줄링 알고리즘

## 스케줄링 기준
<br>

### 비교 기준

- CPU 이용률
<br>

- 처리량
<br>
: 단위 시간당 완료된 프로세스의 개수
<br>

- 응답 시간
<br>

- 총 처리 시간

: 프로세스의 제출 시간과 완료 시간의 간격
<br>

= 준비 큐에서 대기한 시간 + CPU에서 실행한 시간 ~~**+ 입출력 시간**~~

<br>
- 대기 시간(waiting time)

: **준비 큐에서 대기하는 시간**

→ CPU 스케줄링 알고리즘은 프로세스 실행 시간과 입출력 시간에는 영향을 미치지 않음

<aside>
❗ 총처리 시간, 대기 시간, 응답 시간은 줄이고, CPU 이용률과 처리량은 늘리는 것이 바람직

</aside>
<br>
<br>

## 선점 VS 비선점 스케줄링

### 선점 : 프로세스가 현재 실행되고 있는 프로세스의 남은 시간보다 짧은 버스트를 가지면, 
현재 실행중인 프로세스를 선점

### 비선점 : 실행중인 프로세스가 CPU 버스트를 완료할 때까지 선점하지 않음

<br>

## 선입 선처리(FCFS) 스케줄링

- 가장 간단한 CPU 스케줄링 알고리즘

- **CPU를 먼저 요청하는 프로세스가 CPU를 먼저 할당 받음**

- 선입 선출(FIFO)로 구현

- 평균 대기 시간이 긴 경우가 있음

<img width="800" alt="image" src="media/CPU-scheduling-img/Untitled 2.png">
<br>
<br>

- **평균 대기 시간 구하는 방법 확인!**

- **평균 총 처리 시간 구하는 방법 확인!**

### 문제점 : **CPU 버스트가 짧은 프로세스가 긴 프로세스 뒤에 나열됨**

- 특히, **선입 선처리 알고리즘은 대화형 시스템에서 문제됨**

<br>
<br>

## 최단 작업 우선(SJF) 스케줄링

- **CPU 버스트가 가장 짧은 프로세스에게 할당**

- **평균 대기시간을 최적화 시킴**

<img width="800" alt="image" src="media/CPU-scheduling-img/Untitled 3.png">
<br>
<br>

- 해당 예시는 **도착시간이 고려되지 않음**

- 최단 작업 우선 스케줄링은 **선점권이 있거나 없을 수 있음**

- 비선점형 스케줄링

<img width="650" alt="image" src="media/CPU-scheduling-img/Untitled 4.png">
<br>
<br>

<aside>
❗ 대기시간 : 큐에서 기다린 시간 / 시작 - 도착 = 대기

</aside>

<aside>
❗ 총 처리 시간 : 최종 끝난 시간 - 들어온 시간

</aside>

- 선점형 스케줄링

<img width="650" alt="image" src="media/CPU-scheduling-img/Untitled 5.png">
<br>
<br>

### SJF의 가장 치명적인 단점 : 다음 CPU 버스트의 길이를 알 방법이 없음

-  OS는 버스트 길이를 모름

-  최단 작업 우선 스케줄링에 근사하도록 시도

→ **다음 CPU 버스트가 앞의 버스트와 길이가 유사하다고 간주하고 진행**

-  연구용으로만 사용됨 ~ 일반적인 스케줄링에서는 쓰지 않음

-  **실시간 스케줄링**에 사용 (임베디드 시스템)

<br>
<br>

## 라운드-로빈(Round-robin) 스케줄링 / 시분할 TimeSharing

- **시분할 시스템을 위해 특별히 설계**

- 무조건 **선점형**

- **스케줄러는 준비 큐를 돌아가면서 한번에 한 프로세스에 한 번의 시간 할당량 만큼 CPU를 할당**

<img width="650" alt="image" src="media/CPU-scheduling-img/Untitled 6.png">
<br>
<br>

### 단점 :  **문맥 교환**

- 라운드 로빈 스케줄링의 성능은 시간 할당량의 크기에 매우 많은 영향을 받음

ex) 1번 실행을 위해 세팅되어 있는 상태에서 2번 실행 상태로 세팅 하기위해 시간이 걸림

- 시간 할당량이 매우 크면, 선입 선처리 정책과 같음

- 시간 할당량이 매우 작으면 **매우 많은 문맥 교환**을 야기

<img width="600" alt="image" src="media/CPU-scheduling-img/Untitled 7.png">
<br>
<br>

## 우선 순위(Priority) 스케줄링

- 우선 순위가 각 프로세스에게 주어지고 **CPU는 가장 높은 우선순위를 가진 프로세스에 할당 됨**

<img width="800" alt="image" src="media/CPU-scheduling-img/Untitled 8.png">
<br>
<br>

- 선점이나 비선점일 수 있음

- 선점형 우선 순위 스케줄링 알고리즘
    - 새로 도착한 프로세스의 우선 순위가 현재 실행되는 프로세스의 우선 순위보다 높으면 CPU를 선점
- 비선점형 우선 순위 스케줄링 알고리즘
    - 단순히 준비 큐의 머리 부분에 새로운 프로세스를 넣음
<br>
<br>

### 무한 봉쇄 또는 기아 상태

- 부하가 과중한 컴퓨터 시스템에서는 높은 우선 순위의 프로세스들이 꾸준히 들어와서 낮은 우선 순위의 프로세스들이 CPU를 사용하지 못하게 될 수도 있음

: SJF도 발생할 수 도 있음 (하지만 실제로 SJF는 사용하지 않음)

→ 에이징(aging)으로 해결

: **오래 대기하는 프로세스들의 우선 순위를 점진적으로 증가시킴**

<img width="800" alt="image" src="media/CPU-scheduling-img/Untitled 9.png">
<br>
<br>

## 다단계 큐(Multi-level Queue) 스케줄링

<img width="500" alt="image" src="media/CPU-scheduling-img/Untitled 10.png">
<br>
<br>

- 준비 큐를 다수의 별도 큐로 나눔 → 우선순위가 젤 높은 큐 ~ 우선순위가 젤 낮은 큐

- 프로세스의 비율을 정해서 우선순위가 높은 프로세스부터 순차적으로 진행

- 실제적으로는 적용이 힘듬 → 피드백 적용

## 다단계 피드백 큐(Multilevel Feedback Queue) 스케줄링

<img width="500" alt="image" src="media/CPU-scheduling-img/Untitled 11.png">
<br>

- 프로세스가 큐들 사이를 이동하는 것을 허용
<br>
<br>


# 스레드 스케줄링

## Pthread 스케줄링

<img width="800" alt="image" src="media/CPU-scheduling-img/Untitled 12.png">
<br>

- SCOPE_SYSTEM : 커널 레벨에서 스케줄링하겠다는 의미
<br>
<br>

# 다중 처리기 스케줄링

## 다중 처리기 스케줄링에 대한 접근 방법

### 대칭 다중 처리 (Symmetric multiprocessing: SMP)

1. 큐는 하나인데, 여러개의 CPU가 동시에 사용하는 것
    
    → 공평하게 CPU 동작 가능
    
2. CPU 각각 큐를 가지고 있는 경우
    
    → 불공평하게 CPU동작 가능 → 큐에 할당량이 몰리는 경우
    

<img width="450" alt="image" src="media/CPU-scheduling-img/Untitled 13.png">
<br>
<br>

## 다중코어 프로세서

- CPU의 처리속도보다 Memory의 처리속도가 훨씬 느림

메모리 멈춤 : 프로세서가 메모리를 접근할 때 데이터가 가용해지기를 기다리면서 많은 시간을 허비

→ 캐시 미스 등의 여러 원인 때문에 발생

<img width="700" alt="image" src="media/CPU-scheduling-img/Untitled 14.png">
<br>
<br>

위 과정을 효율적으로 구성하기 위해 다음과 같이 구현

<img width="700" alt="image" src="media/CPU-scheduling-img/Untitled 15.png">
<br>
<br>

## 부하 균등화 (Load balancing)

만약 CPU가 아래와 같이 각자 자기의 큐를 가지고 있는 시스템인 경우,

<img width="250" alt="image" src="media/CPU-scheduling-img/Untitled 16.png">
<br>
<br>

특정 CPU 하나의 큐에 유독 프로세스가 많이 도착한 경우, 
그 CPU만 바쁘고 나머지 CPU가 한가한 경우가 있을 수 있음

→ **로드 밸런싱 / (부하 균등화)를 통해 해결**

- 프로세스는 실행 해야지만 수행 시간이 얼마나 걸리는 지 알 수 있음 → 아래 방법으로 균형을 다시 맞출 수 있음

1. Push 이주 (migration)
    
    - 주기적으로 각 처리기의 부하를 검사하여 불균형 상태로 밝혀지면 과부하인 처리기에서 쉬고 있거나 덜 바쁜 처리기로 프로세스를 이동함
    
    - OS는 CPU가 얼마나 바쁜지 체크가 가능하기 때문에 체크 후에 밀어내는 방식
    
2. Pull 이주
    
    - 쉬고 있는 처리기가 바쁜 처리기를 기다리고 있는 프로세스를 가져와 실행 (꺼내감)
    

이러한 균형 과정을 통해 마무리하려고 했으나, 아래와 같은 현상 발생

<img width="650" alt="image" src="media/CPU-scheduling-img/Untitled 17.png">
<br>

- CPU가 여러개 인 상황에서, 각 CPU에 딸린 메모리가 따로 존재

- CPU에 바로 붙어있는 메모리에 접근하는 시간과, **옆에 있는 메모리에 접근하는 시간에는 차이가 존재**

- 오른쪽 CPU에서 A 프로세스를 실행하는 것이 빠르다고 판단하여 실행을 하기위해서는 오른쪽 CPU가 
왼쪽 메모리에 접근을 해야하만 하는 상황이 발생하게 됨

### 프로세스가 다른 처리기로 이주하면, 많은 비용(시간)이 발생하게 됨 → 처리기 친화성 등장
<br>

## 처리기 친화성

- 한 처리기에서 다른 처리기의 이주를 피하고 같은 처리기에서 프로세스를 실행시키려고 함

### 연성 친화성 : 가능하면 해당 프로세스에서 처리하려고 노력

→ 운영체제가 동일한 처리기에서 프로세스를 실행시키려고 노력하는 정책을 가졌지만 보장하지는 않음

### 강성 친화성 : 프로세스가 다른 처리기로 절대 이주하지 않게 지정 가능 / 빠른 실행 보장

→ 이주로 인한 추가 비용 발생 방지 역할을 하게됨
<br>
<br>

# 실시간 CPU 스케줄링

## 실시간 컴퓨팅 / Phone → Call Service가 대표적

### 연성 실시간 시스템 (Soft Real-time System)

- 시간 제약조건이 덜 엄격

- delay가 발생하더라도 치명적이지 않은 서비스

### 경성 실시간 시스템 (Hard Real-time System)

- 마감시간에 반드시 완수해야 하는 가장 엄격한 제약 조건을 가짐

- 일반적인 OS가 아닌 Real-time OS에서 사용함

- 원자력 시스템, 로켓 발사 계산 등이 해당됨

## 우선순위 기반 스케줄링

- 실시간 프로세스에게 우선순위를 제일 높게 주어 그 서비스부터 먼저 처리될 수 있게 하여 딜레이를 최소화

→ 문제점은, 연성 실시간 기능을 제공하는 것뿐, 경성 실시간과 같은 마감시간을 절대적으로 맞춰야하는 환경에선 사용할 수 없음

- 경성 실시간을 이야기하기 위해선 프로세스들이 가지는 특성을 이야기해야함

### 경성 실시간 시스템을 위한 스케줄링에서 프로세스들이 가지는 특징

- **duration of period (주기)**

- **deadline (기한)**

- **processing time (처리 시간)**

<img width="600" alt="image" src="media/CPU-scheduling-img/Untitled 18.png">
<br>
<br>

## 기존 방식의 스케줄링 / 우선순위 정책 스케줄링

- 우선순위 정책을 이용하여 주기 태스크 스케줄

<img width="800" alt="image" src="media/CPU-scheduling-img/Untitled 19.png">
<br>
<br>

- P2의 우선순위가 높은 상황 → 수행 시간이 35초 이므로, 35초에 종료

- P1의 수행시간 20초를 진행하면, 주기를 P1의 실행 주기를 넘어가서 종료됨

→ 경성 실시간 시스템에서는 발생해서는 안되는 일 ~ 다른 스케줄링이 요구됨

## Rate-Monotonic 스케줄링

- 짧은 주기에 대해 먼저 처리를 진행

<img width="600" alt="image" src="media/CPU-scheduling-img/Untitled 20.png">
<br>

- 아래와 같은 곳에서 문제 발생

<img width="600" alt="image" src="media/CPU-scheduling-img/Untitled 21.png">
<br>

- 짧은 주기에 대해서 처리를 하기위해 P1 → P2 → P1으로 진행됨

- P2를 실행하려고 보니, **주기를 넘겨서 진행하게됨**
<br>
<br>

## Earliest deadline first 스케줄링 / edf 스케줄링

- 마감시간(주기)에 따라서 우선순위를 동적으로 부여

- 마감시간이 빠를수록 우선순위는 높아지고, 늦을수록 낮아짐

<img width="600" alt="image" src="media/CPU-scheduling-img/Untitled 22.png">
<br>
<br>
<br>


# 운영체제 사례들

## Linux 스케줄링

- CFS 스케줄링 (Completely Fiar Scheduler) / 공평하게 하는 스케줄링

- 연성 실시간 스케줄링과 일반 스케줄링 두개 구현

- vruntime이라는 가상 실행 시간과 레드 블랙 트리를 기반으로 스케줄링을 진행 → SJF와 비슷

## Winodws 스케줄링

- 실시간 스케줄링과 일반 스케줄링의 우선순위를 다르게 구현

- 다단계 피드백 큐를 사용해 우선순위가 오르락 내리락 함

## Solaris(Unix) 스케줄링

- 실시간 스케줄링을 위해 우선순위 높임

- 다단계 피드백 큐를 도입

- 프로세스가 수행을 하고 할당한 시간을 다 소비를 하게 되면, 우선순위를 낮추는 방향으로 진행됨