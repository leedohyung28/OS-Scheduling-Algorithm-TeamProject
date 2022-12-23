# Operation-System-project-

한국기술교육대학교 운영체제 (process scheduling) 팀프로젝트 

<br>

## Usage 👨🏻‍🔧


1. Choice Sceduling algorithm 🤔
2. ADD Process 🪵
3. ADD Core 🔥
4. Run 🚀


<br>



## 💻 개발 환경 


`Back end`
- `Python`

`front end`
- `python tkinter`

<br>

## 개발 기간 ⏰

- **2022.03.24 ~ 2022.05.08 ( 총: 46일 )** 

<img src="https://user-images.githubusercontent.com/91319157/209250019-99c7ec9e-d074-4230-9ac4-522ef864b760.png" width="97%">

<br><br>

## 👋🏻 프로젝트 소개 
<br>
Process Scheduling Simulator 프로젝트는 Basic five scheduling algorithms과 Your own algorithm을 구현하여 Process Scheduling을 동작한다.

<br>

Process Scheduling은 Muti-core Processor로 이루어져, P core와 E core를 각 사용자에 맞추어 사용할 수 있다. 

<br>

코드로 구현된 Process Scheduling algorithm을 Visualization하여 Process Scheduling을 보기 쉽게 한다.
***

<br><br>

Basic five scheduling algorithms은 FCFS, 
RR(Time quantum = δ), SPN, SRTN, HRRN으로 구성 돼있다. 
<br><br>

## • Basic five scheduling algorithms
| Basic scheduling algorithms | Preemptive |  Criteria |
| :---:  | :---: | :---: |
| FCFS(First-Come-First-Service) |  X | Arrival Time |
| RR(Round-Robin)  |  O | Arrival Time(Time quantum= δ) |
| SPN(Shortest-Process-Next)  | X | Burst Time |
| SRTN(Shortest-Remaining-Time-Next) |  0 | Remaining Burst Time |
| HRRN(High-Response-Ratio-Next) |  X | Response ratio |

[표01. Basic five scheduling algorithms]

<br><br><br>

## input & output 🎤
<br>

Process Scheduling은 사용자로부터 최대 15개의 Process, 최대 4개의 processor, Arrival time

<br>

for each process, Burst time for each process, Time quantum을 입력 받는다. 또 각 scheduling

<br>

기법 별로 Gantt chart, WT(Waiting Time) for each process, TT(Turnaround Time) for each 

<br>

process, NTT(Normalized Turnaround Time) for each process, 소비전력을 출력한다.

<br>

### • System properties
| Core   | 성능  |  전력 | 대기 전력 |
| :---:  | :---: | :---: | :---: |
| E |  1초에 1의 일을 처리 | 1W | 0.1W |
| P |  1초에 2의 일을 처리 | 3W | 0.1W |

[표02. System properties]

<br>
<br>

Scheduling은 1초 단위로 이루어지고, P core에 할당된 작업의 남은 일의 양이 1이어도,1초를 소모한다고 가정한다.


<br><br>

## 알고리즘 도식화 🖼

<img src="https://user-images.githubusercontent.com/91319157/209252941-09b42e0e-1670-4466-9752-3c4e98dc467b.png" height="75%">

[그림02. 알고리즘 도식화]

<br><br><br>

## WTQ(waiting Time Quantum)_New algorithm

<br>

## 아이디어 제시 
<br>
SPN에서 Burst time이 작은 순서대로 작업을 진행하기 때문에 계속해서 Burst Time이 작은 Process가 ready_queue에 들어오게 된다면, 

Burst Time이 큰 Process는 계속해서 뒤로 밀리게 되어 아무리 일찍 Process에 들어오게 되더라도 반환 시간이 늦어지게 된다. 이 문제를 

해결하려고 한다. 따라서 waiting_time_quantum을 추가하였다. 이는 최소 대기 시간이다. 최소 대기 시간이 지나면 우선 순위로 지정하여 작업을 시작한다.


이번 프로젝트의 방향성은 사용자의 편의성을 최우선으로 고려한다. 따라서, waiting_time_quantum의 값을 사용자가 지정할 수 있다. 만약 

waiting_time_quantum을 작게 설정한다면 Arrival Time이 우선순위가 되므로 FCFS와 같은 역할을 수행할 수 있고, waiting_time_quantum을 

크게 설정한다면, SPN과 같은 역할을 수행한다. 따라서 SPN에서 생기는 무한대기 현상을 해결해 줄 수 있으며, 사용자가 원하는 방향에 따라서 알고리즘 기법을 택할 수 있다. 

<br><br>

## 핵심 데이터 구조

- ready_queue_waiting_time (리스트)
- waiting_time_quantum 

<br>

 ready_queue_waiting_time은 ready_queue에 Process가 있을 경우에 1초 당 1씩 증가시킨다. 따라서 설정해준 waiting_time_quantum보다 ready_queue_waiting_time의 원소 중 하나가 같거나 커지게 되면, 즉 기다리고 있는 Process가 waiting_time_quantum을 경과하면, 해당 Process를 먼저 처리한다

<br>

<img src="https://user-images.githubusercontent.com/91319157/209253296-ac8cb691-937e-42ef-96d3-9b758c9c5667.png" width="50%">

[그림15. ready_queue_waiting_time]

<br>

### WTQ 구현 방법

<br>

- 이 알고리즘은 기본적으로 SPN을 계승한 알고리즘이다. 따라서, 기본 틀은 SPN과 같다. SPN과 같이 process_number_and_burst_time을 사용하여 Burst Time을 오름차순으로 정렬하여 작은 Burst Time을 가진 process부터 작업을 진행한다. 

<br>

<img src="https://user-images.githubusercontent.com/91319157/209253541-a6cfb9dc-09f9-4bdb-92b2-e09b9d23cefb.png">

[도식화06. Flow chart]

<br>

먼저, ready_queue_waiting_time으로 설정된 기다리는 시간이 얼마나 되었는지 확인한다. 

<br>

<img src="https://user-images.githubusercontent.com/91319157/209254558-c859261f-04e0-4d2a-b043-67dd6d86dd6b.png" width="90%">

[그림16. WTQ]

<br>

waiting_time_quantum만큼 기다리는 Process가 있다면, ready_queue 맨 앞에 넣어 우선적으로 실행한다. [그림16]처럼 P1은 먼저 왔지만, Burst Time이 오름차순으로 정렬되어 제일 늦게 실행된다. 만약, P1이 사용자가 설정한 waiting_time_quantum 이상 기다렸다면, ready_queue 맨 앞에 삽입한다.

<br><br>


## GUI Overview ✅
<br>

<img src="https://user-images.githubusercontent.com/91319157/209257960-91a665ee-bd8e-4d8b-a0c1-c5e11272ae6c.png">


<br>
<br>
<br>






<br>
<br>

## 감사합니다 

<img src="https://user-images.githubusercontent.com/91319157/208434073-c834c893-2aed-4ded-a079-dff65540063f.gif" width="30%"> 
