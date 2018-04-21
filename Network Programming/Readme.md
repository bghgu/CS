# 네트워크 프로그래밍(TCP-IP)

## 1.기본

1. 네트워크 프로그래밍 = 소켓 프로그래밍
2. 소켓을 기반으로 한다.
3. 네트워크로 연결된 둘 이상의 컴퓨터 사이에서의 데이터 송수신 프로그램 작성 의미

## 2. 소켓

1. 네트워크 연결 도구

2. 운영체제에 의헤 제공되는 소프트웨어 장치

3. 프로그래머에게 데이터 송수신에 대한 물리적, 소프트웨어적 세세한 신경을 쓰지 않게 한다.

4. TCP 소켓은 전화기에 비유

   ### 서버의 소켓 생성

   클라이언트보다 먼저 생성 되어야 한다.

   서버 소켓, 리스닝 소켓

   1. 소켓 생성

      **socket**

      서버의 소켓과 클라이언트의 소켓 생성 방법에는 차이가 있다.

      ```
      SOCKET socket = socket(PF_INET, SOCK_STREAM, 0); //(IPV4 프로토콜, TCP, 0)
      ```
      TCP는 SOCK_STREAM, UDP는 SOCK_DGRAM

   2. 소켓에 ip와 port 할당

      **bind**

      ```
      SOCKADDR_IN servAddr;
      servAddr.sin_family = AF_INET; //IPV4 주소
      servAddr.sin_addr.s_addr = htonl(INADDR_ANY); //어떤 ip로부터 접속을 받겠다.
      servAddr.sin_port = htons(atoi(argv[1])); //포트번호 할당
      bind(socket, (SOCKADDR*)&servAddr, sizeof(servAddr));
      ```

   3. 연결 가능한 상태의 소켓

      **listen**

      ```
      listen(socket, 5); //(소켓, 연결 요청 가능 개수)
      ```

   4. 연결 요청의 수락

      **accept**

      ```
      SOCKADDR_IN clntAddr;
      int szClntAddr;
      hClntSock = accept(socket, (SOCKADDR*)&clntAddr, &szClntAddr);
      ```

      연결 요청이 수락되어야 데이터의 송 수신이 가능

      수락 된 이후에 데이터의 송 수신은 양방향으로 가능하다.

   ### 클라이언트의 소켓 생성

   소켓의 생성과 연결 요청으로 구분

   1. 소켓 생성

      ```
      SOCKET Socket = socket(PF_INET, SOCK_STREAM, 0);
      ```

   2. 연결 요청

      ```
      SOCKADDR_IN servAddr;
      servAddr.sin_family = AF_INET;
      servAddr.sin_addr.s_addr = inet_addr(argv[1]); //서버의 주소 할당
      servAddr.sin_port = htons(atoi(argv[2])); //서버의 포트 할당
      connect(socket, (SOCKADDR*)&servAddr, sizeof(servAddr);
      ```

5. WSAStartup

   winsock의 초기화, winsock 함수 호출을 위한 라이브러리의 메모리 로드를 의미

   ```
   WSADATA wsaData;
   WSAStartup(MAKEWORD(2, 2), &wsaData); //winsock의 버전값(2.2), WSADATA 구조체의 포인터 주소
   ```
   종료

   ```
   WSACleanup();
   ```

6. 리눅스와 윈도우의 소켓 차이

   1. 리눅스는 소켓을 파일 입출력과 같이 처리

      **write**와 **read**

      **리눅스는 소켓도 파일로 간주하기 때문에 저 수준 파일 입출력 함수를 기반으로 소켓 기반의 통신이 가능하다.**

   2. 윈도우는 소켓을 파일 입출력과 별도로 처리

      **recv**와 **send**

      * send

      ```
      send(hClntSock, message, sizeof(message), 0); //(보낼 소켓, 보낼 메시지 버퍼, 버퍼의 크기, 0)
      ```

      * recv

      ```
      recv(hSocket, message, sizeof(message) - 1, 0); //(받을 소켓, 받을 메시지 버퍼, 버퍼의 크키, 0)
      ```

7. TCP 소켓에 존재하는 입출력 버퍼

   * 입출력 버퍼는 TCP 소켓 각각에 대해 별도로 존재한다.
   * 입출력 버퍼는 소켓 생성시 자동으로 생성된다.
   * 소켓을 닫아도 출력버퍼(send, write)에 남아있는 데이터는 계속해서 전송이 이루어진다.
   * 소켓을 닫으면 입력버퍼(recv, read)에 남아있는 데이터는 소멸된다.
## 3. TCP
1. 연결 지향형 프로토콜
2. 데이터의 경계가 없다.
3. 전화(받았는지, 못받았는지 확인이 가능하다.)
4. UDP에 비해 전송 속도가 느리다.
5. 서버 소켓과 클라이언트 소켓의 구분이 있다.
6. 전송 순서대로 데이터가 수신된다.
7. 중간에 데이터가 소멸되지 않는다.
8. 소켓대 소켓은 1대1 연결 구조

## 4. UDP
1. 비 연결 지향향 프로토콜
2. 데이터의 경계가 있다.
3. 우편(받았는지, 못받았는지 확인이 불가능하다.)
4. TCP에 비해 전송 속도가 빠르다.
5. 서버 소켓과 클라이언트 소켓의 구분이 없다. 즉 1개만 있으면 된다.
6. 전송 순서와 상관없다.
7. 데이터 손실 및 파손의 우려가 있다.
8. 한번에 보낼 수 있는 데이터의 크기가 제한된다.

## 5. 주소와 포트

1. IPV4 주소 체계

   총 32비트(8비트.8비트.8비트.8비트)

   클래스 A : 1.0.0.1 ~ 126.255.255.254, **AAA.xxx.xxx.xxx**

   클래스 B : 128.0.0.1 ~ 191.255.255.254, **BBB.BBB.xxx.xxx**

   클래스 C : 192.0.0.1 ~ 223.255.255.254, **CCC.CCC.CCC.xxx**

   클래스 D : 224.0.0.0 ~ 239.255.255.255

   클래스E : 240.0.0. ~ 254.255.255.255

   클래스 A의 첫번째 바이트 범위 : 0 ~ 127, 항상 0으로 시작

   클래스 B의 첫번째 바이트 범위 : 128 ~ 191, 항상 10으로 시작

   클래스 C의 첫번째 바이트 범위 : 192 ~ 223, 항상 110으로 시작

2. PORT

   16비트, 0이상 65535이하

   0 ~ 1023은 Well-known Port, 용도가 이미 결정되어 있다.

## 6. 바이트 변환

1. 네트워크 바이트는 **빅 엔디안** 기준

2. cpu마다 저장 방식이 다르다.

3. 빅 엔디안

   상위 바이트 값을 작은 번지수에 저장

   0x1234567 -> 0x12 0x34 0x45 0x78 

4. 리틀 엔디안

   인텔 CPU는 **리틀 엔디안**

   상위 바이트 값을 큰 번지수에 저장

   0x12345678 -> 0x78 0x56 0x34 0x12

   산술연산유닛(ALU)에서 메모리를 읽는 방식이 메모리 주소가 낮은 쪽에서부터 높은 쪽으로 읽기 때문에 산술 연산의 수행이 더 쉽다.

5. htons, htonl

   host to network

   l : long 자료형, 4바이트, ip주소

   s : short 자료형, 2바이트, 포트번호

   내가 쓰는 pc는 인텔 cpu, 리틀 엔디안이고 네트워크는 빅 엔디안이기 때문에 변환해야 한다.

   ```
   //서버
   servAddr.sin_addr.s_addr = htonl(INADDR_ANY);
   servAddr.sin_port = htons(atoi(argv[1]));
   //클라이언트
   servAddr.sin_addr.s_addr = inet_addr(argv[1]);
   servAddr.sin_port = htons(atoi(argv[2]));
   ```
## 7.TCP 연결, 3 way handshake

1. IP는 3계층(네트워크 계층)이고, TCP & UDP는 4계층(전송 계층)

2. 서로의 통신을 위해 확인하고, 연결하는 과정이 3번의 요청/응답 후에 연결된다.

   ![img](http://cfile24.uf.tistory.com/image/267C5D39537EDD2C176BD3)

   1. Client -> Server : SYN

      SYN : 서버에게 연결 요청

   2. Server -> Client : ACK + SYN

      서버는 SYN 데이터를 받고 SYN_RCV 상태로 변경 된다.

      ACK : 1번 메시지에 대한 응답

      SYN : 클라이언트도 포트를 열어 달라는 메시진

   3. Client -> Server : ACK

      ACK : 2번에서 받은 메시지에 응답을 보낸다.


   이와 같이 3번의 통신이 정상적으로 이루어지면서, 서로의 포트가 ESTABLISHED 상태가 된다.

3. SYN : 연결 요청

   SYN을 보낸 쪽은 ACK가 올 때 까지 기다리고 있다.

4. ACK : 응답

5. status

   Closed : 닫힌 상태

   LISTEN : 포트가 열린 상태로 연결 요청 대기 중

   SYN_RCV : SYNC 요청을 받고 상대방의 응답을 기다리는 중

   ESTABLISHED : 포트 연결 상태
## 8.TCP 종료, 4 way handshake
![img](http://cfile21.uf.tistory.com/image/2678E035537EEE9126A109)

1. 통신을 종료하고자 하는 Client가 서버에게 FIN 패킷을 보내고 자신은 FIN_WAIT_1 상태로 대기한다.
2. FIN 패킷을 받은 서버는 해당 포트를 CLOSE_WAIT으로 바꾸고 잘 받았다는 ACK 를 Client에게 전하고 ACK를 받은 Client는 상태를 FIN_WAIT_2로 변경한다.

그와 동시에 Server에서는 해당 포트에 연결되어 있는 Application에게 Close()를 요청한다.

3. Close() 요청을 받은 Application은 종료 프로세스를 진행시켜 최종적으로 close()가 되고 server는 FIN 패킷을 Client에게 전송 후 자신은 LAST_ACK 로 상태를 바꾼다.

4. FIN_WAIT_2 에서 Server가 연결을 종료했다는 신호를 기다리다가 FIN 을 받으면 받았다는 ACK를 Server에 전송하고 자신은 TIME_WAIT 으로 상태를 바꾼다. 

   (TIME_WAIT 에서 일정 시간이 지나면 CLOSED 되게 된다.)

최종 ACK를 받은 서버는 자신의 포트도 CLOSED로 닫게 된다.

## 9.TCP 문제점
* 문제점

  클라이언트는 문장 단위로 데이터를 송 수신 하기 때문에 데이터의 경계가 없는 TCP에서 문제가 발생한다.

  서버는 send/write 함수를 이용해 데이터를 전송 하기 때문에 문제되지 않는다.

* 해결책

  서버로 부터 전송한 데이터의 길이만큼 읽어 들이기 위한 작업이 필요하다.

  즉, 서버는 사전에 데이터를 얼만큼 보낼지 미리 클라이언트에게 보내야 한다.

  클라이언트는 사전에 서버로 부터 받은 데이터의 길이 만큼, 서버로 부터 데이터를 수신 받으면 된다.

