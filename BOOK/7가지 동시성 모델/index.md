# 7가지 동시성 모델

* 동시성
  * 여러 일을 한꺼번에 **다루는** 데 관한 것
  * 여러개의 논리적 통제 흐름(threads of control)을 갖는다. 병렬로 실행될 수도 있고, 그렇지 않을 수도 있다.
  * ex) 1개의 코어가 여러 Process를 수행하는 것은 *동시적*이지만, *병렬적*인 것은 아니다.

* 병렬성
  * 여러 일을 한꺼번에 **실행하는** 데 관한 것
  * 논리적 통제 흐름은 하나가 될 수도 있고, 여러개가 될 수도 있다.
  * ex) 2개의 코어가 같은 형태의 연산을 수행하고 있다면, *병렬적*이지만, *동시적*인 것은 아니다.


## Thread와 Lock

* Java의 synchronized keyword(C#의 MethodImpl Attribute)로 객체를 잠가 공유 자원에 대한 접근 유일성을 보장할 수 있다.
  * 이 경우, Read/Write Lock을 보장해야 한다.
* **Dead-lock**
  * 한 Thread가 2개 이상의 Lock을 확보하려고 하는 경우 발생한다.
  * Lock을 확보한 상태에서 외부 Method를 호출 하는 경우(+외부 Method가 Lock을 확보 하려고 시도하는 경우) 발생할 수 있다.
  * **Best Practice**
    * 공유되는 변수에 대한 접근을 반드시 동기화 한다.
    * Write/Read Thread 모두 동기화 되어야 한다.
    * 여러개의 Lock을 미리 정해진 공통 순서에 따라 요청한다.
    * Lock을 가진 상태에서 외부 Method를 호출하지 않는다.
    * Lock은 최대한 짧게 확보한다.
* [Double-checked locking Anti-Pattern](https://en.wikipedia.org/wiki/Double-checked_locking)
  * [Double-checked locing과 Singleton 패턴](http://gampol.tistory.com/entry/Double-checked-locking%EA%B3%BC-Singleton-%ED%8C%A8%ED%84%B4)