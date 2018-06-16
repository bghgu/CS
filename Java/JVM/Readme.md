# JVM(Java Virtual Machine)

## 0. 목차

1. 개요
2. 특성
3. 구성
4. 실행과정

## 1. 개요
* 자바 가상 머신
* Java Application을 Class Loader를 통해 읽어 들여 Java API와 함께 실행하는 것이다.
* Java ByteCode를 실행할 수 있는 주체이다.
* 인터프리터나 JIT 컴파일 방식으로 다른 컴퓨터 위에서 Java ByteCode를 실행할 수 있도록 구현한다.
* Java ByteCode는 플랫폼에 독립적이다.
* 모든 JVM은 JVM 규격에 정의된 대로 Java ByteCode를 실행한다.
* 이론적으로 모든 자바 프로그램은 CPU나 운영체제의 종류와 무관하게 동작할 것을 보장한다.

## 2. 특성

* 자바 가상 머신은 스택 기반이다.
* 대다수의 명령어가 스택 선두에서 피연산자를 택하고 결과는 다시 스택에 넣는다.
* 포인터를 지원하지만, C 처럼 주소 값을 임의로 조작이 가능한 포인터 연산은 불가능하다.
* GC(Garbage Collection)을 사용한다.
* 메모리 관리가 가능하다.

## 3. 구성

### 3-1. Class Loader

* JVM 내로 class(.class)를 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈이다.
* Runtime 시점에 클래스를 로딩하게 해주며 클래스의 인스턴스를 생성하면 클래스 로더를 통해 메모리에 로드하게 된다.

### 3-2. Runtime Data Areas

* JVM이 프로그램을 수행하기 위해 OS로 부터 별도로 할당 받은 메모리 공간을 의미한다.

  #### PC Register

  * CPU는 명령어를 수행하는 동안 필요한 정보를 Register라고 하는 CPU내의 기억장치를 사용한다.

  * Stack - Base로 동작한다.
  * 각 Thread 별로 하나 씩 존재하며, 현재 수행 중인 JVM 명령어의 주소를 가지게 된다.
  * 만약 Native Method를 수행한다면 PC Register는 undefined 상태가 된다.
  * PC Register에 저장되는 명령어의 주소는 Native Pointer 일 수도 있고, Method ByteCode일 수도 있다.
  * Native Method를 수행할 때에는 JVM을 거치지 않고 API를 통해 바로 수행하게 된다.

  #### JVM Stack

  * JVM Stack은 Thread의 수행정보를 Frame을 통해서 저장하게 된다.
  * Thread가 시작될 때 생성되며, 각 Thread 별로 생성이 되기 때문에 다른 Thread는 접근할 수 없다.
  * Methode가 호출 되면 Method와 Method 정보는 Stack에 쌓이게 되며 Method 호출이 종료될 때 Stack point에서 제거 된다.
  * Method 정보는 해당 Method의 매개변수, 지역변수, 임시변수 그리고 주소(Method 호출한 주소)등을 저장하고, Method 종료시 메모리 공간이 사라진다.

  ### Native Method Stack

  * Java 외의 언어로 작성된 Native Code들을 위한 Stack, 즉 JNI(Java Natice Interface)를 통해 호출되는 C/C++ 등의 코드를 수행하기 위한 Stack

  #### Method Area(Class Area, Static Area)

  * 모든 Thread가 공유하는 Memory 영역이다.
  * Method Area는 Class, Interface, Method, Field, Static 변수 등의 Byte Code 등을 보관한다.

  #### Heap

  * 프로그램 상에서 Runtime시 Dynamic으로 할당하여 사용하는 Area이다.
  * .class를 이용해 instance를 생성하면 Heap에 저장된다.

### 3-3. Execution Engine

* Load된 Class의 ByteCode를 실행하는 Runtime Module이다.
* Class Loader를 통해 JVM 내의 Runtime Data Areas에 배치된 ByteCode는 Execution Engine에 의해 실행되며, 실행 엔진은 Java ByteCode를 명령어 단위로 읽어서 실행한다.
* 최초의 JVM은 Interperter 방식이기 때문에 속도가 느린 단점이 있었지만, JIT Complier 방식을 통해 이 점을 보완했다.
* JVM은 모든 코드를 JIT Compiler 방식으로 실행하지 않고, Interpreter 방식을 사용하다가 일정한 기준을 넘어서면 JIT Compiler 방식으로 실행한다.

## 4. 실행 과정

1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다. JVM은 이 메모리를 용도에 따라 여러 영역(Runtime Data Areas)으로 나누어 관리한다.
2. Java Compiler(javac)가 Java SourceCode(.java)를 읽어들여 Java ByteCode(.class)로 변환한다.
3. Class Loader를 통해 class 파일들을 JVM으로 Loading한다.
4. Loading된 class 파일들은 Execution Engine를 통해 해석된다.
5. 해석된 ByteCode는 Runtime Data Areas에 배치되며 실질적인 수행이 이루어지게 된다. 이러한 과정 속에서 필요에 다라 Thread Synchronization과 같은 GC 작업을 수행한다.

