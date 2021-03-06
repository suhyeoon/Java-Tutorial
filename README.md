#  자바(Java)

## 🌟스레드(thread)의 상태
자바의 스레드는 임의의 시점에서 아래의 상태 중 하나로 존재합니다.

1. New
2. Runnable
3. Blocked
4. Waiting
5. Timed Waiting
6. Terminated

아래의 다이어그램은 임의의 순간의 다양한 스레드의 상태를 나타냅니다.

![thread status diagram](https://i.imgur.com/WaCy0Jf.png)

출처: <https://www.geeksforgeeks.org/lifecycle-and-states-of-a-thread-in-java/>

1. New Thread: 새로운 스레드가 생성되면, `new` 상태입니다. 이 상태에 있는 스레드는 아직 실행되지 않았습니다. 스레드가 `new` 상태에 있으면, 코드가 아직 실행되지 않았고, 시작되지 않은 것입니다.
2. Runnable 상태: 실행할 준비가 된 스레드는 `runnable` 상태로 이동합니다. 이 상태에서는 스레드가 이미 실행중이거나, 언제든지 실행될 준비가 되어있을 수 있습니다. 스레드가 실행될 시간을 주는 것은 스레드 스케쥴러의 책임입니다.  
   멀티 스레드 프로그램에서는 각 스레드에 고정된 시간이 할당됩니다. 각각의 모든 스레드는 잠시동안 실행 된 다음 일시 중지하고 다른 스레드가 실행 될 수 있도록 CPU를 다른 스레드에 양도합니다. 이렇게 되면, 실행할 준비가 되었거나, CPU를 기다리고 있거나, 이미 실행중인 모든 스레드들이 `runnable` 상태로 있게됩니다.
3. Blocked/Waiting 상태: 스레드가 일시적으로 비활성상태가 됬을 때, 스레드는 다음 두 가지 상태 중 하나의 상태가 됩니다.

   - Blocked
   - Waiting

   예를 들어, 스레드가 I/O가 끝나길 디가리고 있을 때, 스레드는 `blocked` 상태가 됩니다.  
   `blocked/waiting` 스레드를 다시 활성화하고 스케줄링하는 것은 스레드 스케쥴러의 책임입니다. 이런 상태에 있는 `runnable` 상태로 이동할 때 까지 더이상 실행을 계속 할 수 없습니다. 어느 스레드건 이 상태에 있으면 CPU cycle을 소비하지 않습니다.  
   `blocked` 상태에 있는 스레드는 현재 다른 스레드에 의해 lock 되어있는 보호된 코드 영역에 액세스하려고 했을 때, 차단된 상태입니다. 보호된 영역이 unlock되면 스케쥴러는 block된 스레드 중 하나를 선택해서 실행 가능 상태로 이동합니다.  
   또, 스레드는 조건에 따라 다른 스레드를 기다리는 상태에 있을 수도 있습니다. 이 조건이 충족되면 스케쥴러에 알림이 전송되고, 대기중인 스레드가 실행 가능 상태로 이동됩니다.  
   현재 실행중인 스레드가 `blocked/waiting` 상태로 이동하면, `runnable` 상태의 다른 스레드가 스레드 스케쥴러에 의해 실행되도록 스케쥴됩니다.  
4. Timed Waiting: 스레드는 `time out` 매개변수가 있는 메서드를 호출할 때, `waiting` 상태에 있게됩니다. 스레드는 `timeout`이 완료될 때까지 기다리거나, 알림이 수신될 때까지 이 상태에 있습니다. 예를 들어, 스레드가 sleep 또는 조건부 대기를 호출하면, `timed waiting` 상태로 이동하게 됩니다.
5. Terminated State: 스레드는 다음과 같은 이유로 종료됩니다.

   - 일반적으로 종료되었기 때문입니다. 이는 스레드의 코드가 완전히 프로그램에 의해 실행되었을 때 발생합니다.
   - `segmentation`(?) 실패 또는 처리되지 않은 예외와 같은 비정상적인 오류 이벤트가 발생했기 때문입니다.

   `terminated` 상태에 있는 스레드는 더이상 CPU cycle을 소비하지 않습니다.

### 👉 자바 코드로 스레드의 상태 구현하기

Java에서 현재 스레드의 상태를 얻는 방법은 `Thread.getState()` 메서드를 사용하는 것입니다. 자바는 `java.lang.Thread.State` 라는 클래스를 Enum으로 선언하여, 스레드의 상태를 정의합니다.

1. `Thread.State NEW`
2. `Thread.State RUNNABLE`
3. `Thread.State BLOCKED`
4. `Thread.State WAITING`
5. `Thread.State TIMED_WAITING`
   - timeout이 없는 `Object.wait`
   - timeout이 없는 `Thread.join`
   - `LockSupport.park`
6. `Thread.State TERMINATED`
   - `Thread.sleep`
   - timeout이 있는 `Object.wait`
   - timeout이 있는 `Thread.join`
   - `LockSupport.parkNanos`
   - `LockSupport.parkUntil`
