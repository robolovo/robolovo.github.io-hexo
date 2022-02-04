---
title: 프로세스와 가상 메모리
date: 2022-02-02 13:58:04
categories: Develop
---

<br>

### 프로그램 Program
- <b>A sequence of machine instructions.</b>
- 컴퓨터 디스크에 저장되어 있는 실행 가능한 실행 파일이다.
- 머신 인스트럭션(명령어) + 프로그램이 사용하는 데이터들의 집합이다.

<br>
<br>

### 프로세스 Process
- 프로그램을 실행 시켰을 때 생성되는 인스턴스(또는 실행 중인 프로그램의 인스턴스)이다.
- 모든 프로세스는 각자 자신만의 가상 주소 공간을 가진다.
- 경쟁을 통해 CPU를 할당받아 실행되기를 기다린다.
- 디스크에 있는 프로그램이 메모리에 올라오면서 Ready 상태가 된다.
- Time Sharing에 의해서 자기 차례가 되면 CPU에 의해 실행된다(Running 상태).

<br>
<br>

### 쓰레드 Thread
- “<b>프로세스 내에서 실행되는 흐름의 단위</b>”
- 특정 프로세스 내에서 스레드가 수행될 때 해당 스레드는 프로세스가 소유하고 있는 메모리에 대해서만 접근이 가능하다. → 다른 프로세스에 의해 소유된 메모리는 숨겨져 있고 접근이 불가능하다.
- 프로세스 내의 주소 공간이나 자원들(힙 공간 등)을 같은 프로세스 내에 스레드끼리 공유하면서 실행된다.

<br>
<br>

### 가상 메모리 Virtual Memory
- 프로세스의 logical memory와 physical memory를 분리하기 위해 생겨났다.
- 가상 메모리는 메인 메모리와 디스크에 의해서 OS가 알아서 관리한다.
- 프로세스가 실제 필요로 하는 부분만 메모리로 올리는 <b>Demand-Paging</b> 기법을 사용한다.
<img height="500" src="images/가상 메모리.jpg" width="800"/>
- 장점
    - 한 프로그램이 물리 메모리의 한계를 넘어서까지 주소공간을 확장시킬 수 있도록 해준다.
        - 하나의 프로세스 logical memory가 physical memory보다 커지는 것도 가능하며, 여러 프로세스의 logical memory 총합이 physical memory보다 커지는 것도 가능한 것이다.
    - 가상 메모리가 동시에 활성화된 다수의 프로세스들이 서로 보호된 상태에서 메인 메모리를 공유할 수 있도록 해 준다.

<br>
<br>

### Demand-Paging
- Demanding-page는 실제로 필요한 <b>page</b>만 물리 메모리로 가져오는 방식을 이야기한다.
- 물리 메모리에서 페이지를 가져올 때 <b>페이지 교체 알고리즘(Page Replacement Algorithm)</b>에 따라 교체하는데, 이 글에서는 따로 정리하지 않았다.

<br>
<br>

### 페이지 Page
- <b>가상 메모리를 사용하는 최소 크기 단위</b>이다.
- 메모리에 데이터가 로드와 언로드 되는것을 반복하다보면 메모리에 fragmentation이 발생하게 된다. (간단히 말해서, 메모리 중간 중간에 구멍이 생겨 낭비되는 공간이 생긴다는 뜻.)
- 결국 메모리는 남아 있지만 정작 원하는 크기의 데이터(메모리 중간 중간에 생긴 공간보다 큰)를 물리 메모리로 로드하지 못하게 되는 상황이 생길 수 있는 것이다.
- 이를 막기 위해 운영체제가 만든 것이 page라는 최소 크기 단위인 것이다.

<br>
<br>

### 페이지 테이블 Page Table
<img height="350" src="images/pagetable.png" width="450"/>

- 필요 page에 접근하려 하면, 결국 가상 메모리 주소에 대응하는 물리 메모리 주소를 찾아내 물리 메모리 주소를 얻어와 하는데, 이 때 필요한 것이 페이지 테이블(page table)이다.
- 가상 페이지와 물리 페이지의 매핑 정보를 담고 있는 테이블이고, 가상 주소를 물리 주소로 변환해 준다. 가상 페이지 번호로 인덱스된다.
- 메인 메모리의 커널 영역에 저장된다.
- 메모리 내 페이지 테이블의 위치를 나타내기 위해 페이지 테이블의 시작 주소를 나타내는 <b>페이지 테이블 레지스터</b>가 하드웨어에 포함되어 있다.
- valid 비트에 따라 페이지 히트와 페이지 미스로 나뉜다.
    - valid 비트가 1이면 해당 페이지가 메인 메모리에 존재 하고, 페이지 히트.
    - valid 비트가 0이면 해당 페이지가 메인 메모리에 존재하지 않고, 페이지 미스(페이지 폴트).

<br>
<br>

### Page Hit / Page Miss 
- **페이지 히트**
  - 접근하고자 하는 가상 주소에 매핑되는 물리 페이지가 있을 때. 페이지가 메모리에 존재한다.
- **페이지 미스**
  - 접근하고자 하는 가상 주소에 매핑되는 물리 페이지가 없을 때. 페이지는 디스크에 존재한다.
- **페이지 미스 후 절차**</br>
  →   페이지 미스</br>
  →   운영체제에게 도움을 요청</br>
  →   페이지 폴트 핸들러(page fault handler)호출</br>
  →   요청된 페이지를 메인 메모리의 어디에 배치할 것인지 결정해서 디스크에서 가져오도록 함</br>
  →   컨텍스트 스위치(context switch)를 통해 잠시 다른 프로세스에게 제어를 넘겨줌</br>
  →   디스크가 가상 페이지를 메인 메모리에 로드하는 작업을 완료하면 인터럽트를 발생 시켜서 페이지 폴트가 발생했던 원래 프로세스로 다시 제어를 옮김</br>
  →   변화된 물리 페이지의 정보를 바탕으로 페이지 테이블 엔트리를 갱신하고, 페이지 폴트를 일으켰던 명령어로 다시 리턴하여 해당 명령어를 재실행</br>
  →   메인 메모리에 요청된 페이지가 로드되어 있기 때문에 해당 명령어를 재실행 하면 페이지 히트가 발생</br>

<br>
<br>

### TLB(Translation Lookaside Buffer)   ←   하드웨어 캐시
- 페이지 테이블은 메인 메모리에 저장되기 때문에, 실제 주소를 얻기 위한 메모리 접근 한 번과 데이터를 얻기 위한 또 한 번의 접근이 필요하다.
- TLB는 이러한 접근 성능을 높이기 위해 사용되는 페이지 테이블의 캐시로, TLB에는 최근에 참조된 <b>페이지 테이블 엔트리(PTE)</b>들이 저장된다.
- 즉, 주소 변환(translation)을 하는데 페이지 테이블을 룩업 하는게 아니라 CPU 옆에 놓고 바로 주소 변환을 해주는 장치이다.
- 처음에는 OS가 다 참조 해주지만, OS가 한번 가져왔던 페이지 테이블 엔트리는 TLB에 놓고서 그 다음부터 TLB로 translation한다.
- TLB는 메인 메모리 내의 페이지 개수보다 훨씬 더 적은 수의 엔트리를 가지고 있기 때문에, TLB 미스는 실제 페이지 미스보다 더 빈번히 발생한다.
- **TLB 미스** (2가지 경우로 나뉨)
  - **해당 가상 페이지가 물리 페이지에 맵핑되어 있는 경우**
    - 이러한 경우 메모리 계층에 접근하여 해당 가상 페이지에 대한 PTE를 가져오고, 이를 TLB에 반영해준다. 그리고 해당 PTE를 바탕으로 가상 주소를 물리 주소로 변환하여 메모리 계층에 접근하면 된다.
  - **해당 가상 페이지가 물리 페이지에 맵핑되어 있지 않은 경우**
    - 이러한 경우 메모리 계층에 접근하여 가져오는 PTE의 정보를 보고 페이지 폴트 예외를 발생시킨다. 그러면 페이지 폴트 핸들러는 특정 페이지를 추방하고 새로운 페이지를 가져온 뒤 이에 맞게 PTE와 TLB의 정보를 갱신해준다. 이제 다시 페이지 폴트를 유발했던 명령어를 재실행하면 바로 앞에서 설명했던 'TLB 미스인데 해당 가상 페이지가 물리 페이지에 맵핑되어 있는 경우'가 된다.


<br>
<br>
<br>

### 참조 사이트
- [프로세스와 스레드의 차이](https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html)
- [가상 메모리 (Virtual memory)](http://egloos.zum.com/sweeper/v/2988689)

<br>

### 참조 문헌
- [컴퓨터 구조와 설계 ARM edition](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788964213452) 5장 메모리 기술

<br>
<br>