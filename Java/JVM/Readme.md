# JVM(Java Virtual Machine)

## 목차

1. 개요
2. 특성
3. 구성
4. 실행과정

## 단어

* Compiler
  * 각 소스코드 파일을 오브젝트파일로 변환시켜주는 역할을 한다.
* Loader(로더)
  * 목적 프로그램(기계어 파일)을 실행 가능한 파일로 변환하기 위해 컴퓨터의 주 기억 장소를 할당(Allocation)하거나, 여러개의 목적 프로그램을 연계 편집하여 CPU가 처리할 수 있는 프로그램으로 변환시킨다.
  * 프로그램을 실행하기 위하여 프로그램을 보조 기억 장치로부터 컴퓨터의 주 기억 장치에 올려 놓는 작업을 수행
  * 목적 프로그램들 끼지 연결(Linking)시키거나, 주 기억 장치를 재배치(Relocation)하는 증 포괄적인 작업을 수행
  * 할당(Allocation) -> 연결(Linking) ->  재배치(Relocation) -> 적재(Loading) 순으로 진행
* Linker
  * 모든 오브젝트 파일들을 하나의 오브젝트 파일로 합친다.

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

* JVM 내로 Class(.class)를 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈이다.
* Runtime 시점에 Dynamic으로 Class를 Load한다.
* jar 파일 내 저장된 Class들을 JVM 위에 탑재하고, 사용하지 않는 Class들은 메모리에서 삭제한다.
* class의 instacne를 생성하면 Class Loader를 통해 메모리에 Load하게 된다.
* Java는 Dynamic Code
* CompileTime이 아니라 Runtime 시에 참조한다. 즉 Class를 처음 참조할 때, 해당 Class를 Load하고 Link한다.

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
  * new 연산자로 생성된 instance를 저장한다.
    * Permanent Generation
      * 생성된 instance의 주소값이 저장된 공간이다.
    * New/Young Area
      * Eden : instance들이 최초로 생성되는 공간
      * Survivor 0 / 1 : Eden에서 참조되는 instance들이 저장되는 공간
    * Old 영역
      * New Area에서 일정 시간 참조되고 살아남은 객체들이 저장되는 공간
      * Eden 영역에 instance가 가득차게 되면 첫번째 GC가 발생한다.
      * Eden 영역에 있는 값들을 Survivor 1영역에 복사하고, 이 영역을 제외한 나머지 영역의 객체를 삭제한다.

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

## JIT(Just In Time) Compiler

* Interpreter 방식의 단점을 보완하기 위해 도입된 Compiler
* Interpreter 방식으로 실행하다가 일정한 기준을 넘어서면 ByteCode 전체를 Compile하여 NativeCode로 변환한다.
* 이후에는 더이상 Interpreter 방식으로 Compile하지 않고, NativeCode로 직접 실행한다.
* NativeCode는 Cache에 보관하기 때문에 한번 Compile된 Code는 빠르게 수행된다.
* JIT Compiler가 Compile하는 과정은 ByteCode를 Interpreting하는 방식보다 훨씬 오래 걸리므로 한 번만 실행되는 Code라면 Interpreter방식이 적절하다.