# Java - Networking and Sockets

**Java Networking**
- 2개 이상의 컴퓨터 기기가 연결되어 서로 자원을 공유할 수 있는 상태 혹은 개념

**Java Socket Programming**
- 서로 다른 컴퓨팅 기기 간의 데이터를 공유할 수 있는 기능 제공

<br/>

## Table of Contents
1. [Networking](#1-networking)
2. [Socket Programming](#2-socket-programming)
3. [References](#3-references)

<br/>

## 1. Networking
인터넷과 연결되어 있는 컴퓨터는 아래 다이어그램처럼 TCP 또는 UDP를 사용하여 서로 통신한다.

<img src="https://docs.oracle.com/javase/tutorial/figures/networking/1netw.gif" />

Java로 네트워킹 프로그램을 작성할 때는 위의 Application 계층에서 작성하게 된다. 따라서 TCP, UDP 계층을 프로그램 개발자가 신경 쓸 필요는 없다. `java.net` 패키지의 클래스를 사용함으로써 시스템 독립적인 네트워크 통신을 구현할 수 있다. 하지만, 여기서 어떤 Java 클래스를 사용할지 결정하려면 TCP와 UDP가 어떻게 다른지 이해해야 한다.

### 1.1 TCP
- Transmission Control Protocol
- 두 개의 네트워크 애플리케이션 간에 안정적인 데이터 흐름을 제공하는 연결 기반 프로토콜
- <u>전송되는 데이터의 순서를 보장한다.</u> 순서가 잘못된 경우 에러가 발생한다.
- 안정적인 통신이 필요한 애플리케이션을 위한 point-to-point 채널을 제공한다.
- 추가 오버헤드로 인해 속도가 느려지거나 안정적인 연결이 아예 무효화될 수도 있다.
- 예시)
	- HTTP(Hypertext Transfer Protocol)
	- FTP(File Transfer Protocol)
	- Telent

### 1.2 UDP
- User Datagram Protocol
- 두 개의 네트워크 애플리케이션 간에 보장되지 않는 통신을 제공하는 프로토콜
- Datagram\*을 한 애플리케이션에서 다른 애플리케이션으로 전송한다.
- TCP와 달리 연결 기반 프로토콜이 아니다.

📌 많은 방화벽과 router가 UDP 패킷을 허용하지 않도록 구성되어 있다. 방화벽 외부의 서비스에 연결하는 데 문제가 있거나 클라이언트가 서비스에 연결하는 데 문제가 있는 경우 시스템 관리자에게 UDP가 허용되어 있는지 문의해야 한다.

```plain
*Datagram
	- 독립적인 데이터 패킷
	- 우편 서비스를 통해 편지를 보내는 것과 유사하다.
	- 전송 순서는 중요하지 않으며, 보장되지도 않는다.
	- 각 메시지는 서로 독립적이다.
```

### 1.3 TCP와 UDP
**상황: 예를 들어, 클라이언트 요청이 있을 때 현재 시간을 전송하는 서버가 있을 때**
클라이언트가 패킷을 놓친 상황이 발생하였다. 이때 클라이언트가 두 번째 시도에서 패킷을 수신할 때 시간이 부정확할 수 있으므로 패킷을 다시 보내는 것은 실제로 의미가 없다. 클라이언트가 2번 요청했는데 서버에서 패킷을 순서대로 받지 못하더라도 클라이언트는 패킷이 잘못되었다는 것을 파악하고 다른 요청을 할 수도 있다. 이러한 경우 성능 저하를 유발하고, 서비스의 사용성을 저해할 수 있으므로 TCP는 적합하지 않다.

**상황: `ping` 명령**
`ping` 명령의 목적은 네트워크를 통해 두 애플리케이션 간의 통신을 테스트하는 것이다. 실제로 `ping`은 연결 상태를 확인하기 위해 끊어지거나 고장난 패킷에 대해 알아야 한다. 이 경우도 안정적인 채널을 보장할 필요가 없다.

## 2. Socket Programming

<br/>

### 2.1 Overview of Sockets
여러 application의 한 종류인 client-server application의 경우 다음을 보장해야 한다.
- Client와 server의 통신은 안정적이어야 한다.
- Client와 server 간 전달되는 데이터는 누락되어서는 안 된다.
- Server가 보낸 순서와 동일한 순서로 데이터가 client에 전달되어야 한다.

이러한 요구 사항을 지키기 위해 우리는 종종 TCP(Transmission Control Protocol)을 이용한다.
TCP를 통해 통신하려면 client와 server는 서로 connection을 설정해야 한다.
Connection을 설정한 server와 client는 각각 connection에 binding 된 socket으로부터 데이터를 읽거나 socket에 데이터를 작성함으로써 통신을 할 수 있다.

그렇다면, 더 정확하게 'Socket'이라는 것은 무엇일까?

### 2.2 What is a Socket?
- 네트워크 위에서 실행 중인 2개 이상의 프로그램이 형성하는 2-way(양방향) communication link의 하나의 endpoint*
- Socket class는 client-server 프로그램 사이의 connection을 나타내는 데에 주로 사용된다.
- Socket은 Port number(포트 번호)와 binding 된다.
- TCP 계층에서 socket을 통해 데이터가 전송되어야 할 application을 식별할 수 있다.
- java.net package는 Socket과 ServerSocket class를 제공한다.
  - Socket class
    - Java 프로그램 <-> 다른 Java 프로그램 간의 양방향 connection의 한 쪽을 구현한 class
    - <span style="color: orange">Platform-dependent으로 구현되어 있다.</span>
    - Java 프로그램에서 특정 시스템의 자세한 세부 정보를 숨긴다.
    - <span style="color: orange">Natvie code에 의존하는 대신 platform-independent한 방식으로 네트워크 통신이 가능하다.</span>
  - ServerSocket class
    - Server 측을 구현한 class
    - 즉, server가 client에 대한 연결을 수신하고 수락하는 데 사용할 수 있다.

```plain
*endpoint
	- IP 주소 + port number의 조합
	- 모든 TCP 연결은 2개의 endpoint로 고유하게 식별 가능
	- 이렇게 하면 host와 server 사이에 여러 개의 connection들을 생성 가능

```

### 2.3 More about Socket

| # | Server-side | Client-side |
| - | - | - |
| 1 | 네트워크 위에서 특정 application을 실행한다. | |
| 2 | 실행된 application은 특정 port number에 binding 된 Socket을 가진다. | |
| 3 | | 실행 중인 server의 host name, port name을 가진다. |
| 4 | | Connection 요청을 위해 server에 rendezvous를 시도한다. Connection 요청 시 본인의 port number 등 자신을 식별할 수 있는 정보를 함께 보낸다.* |
| 5 | Server가 connection 요청을 수락한다. | |
| 6 | Server는 요청받은 port number에 binding 된 새로운 socket을 얻는다. 또한, 원격 endpoint도 client의 주소와 port number로 설정된다.* | |
| 7 | | Connection 설정 후 socket이 성공적으로 생성된다. |
| 8 | | Client는 해당 socket을 사용하여 server와 통신이 가능하다. |
| 9 | Client와 socket을 통해 통신 가능하다. | Server와 socket을 통해 통신 가능하다.

<br/>

<img src="https://docs.oracle.com/javase/tutorial/figures/networking/5connect.gif"/>

<img src="https://docs.oracle.com/javase/tutorial/figures/networking/6connect.gif"/>

<br/>

*일반적으로 port number는 system에 의해 할당된다.  
*새로운 socket이 있어야 연결된 client의 요구 사항을 처리하면서 connection 요청에 대한 원래 socket에 대해 계속 수신 대기가 가능하다.

<br/>

### 2.4 If you want to connect Web
Web에 연결하는 경우는 Socket class보다 URL class와 그와 관련된 URLConnection, URLEncoder class가 더 적합할 수 있다. 실제로, URLs 방식은 web에 접속하기 위한 비교적 높은 수준의 connection이며, 실제 구현의 일부분에 socket이 사용되었다.

<br/>

### 2.5 Reading from and Writing to a Socket

- `EchoClient`: `EchoServer`에 연결하는 client
- `EchoServer`: Client로부터 데이터를 수신하여 다시 전달하는 server

이때, client는 [Echo Protocol](https://datatracker.ietf.org/doc/html/rfc862)을 지원하는 모든 host에 연결할 수 있다.  
참고로, 아래 예제는 client가 server에 사용자로부터 입력받은 text를 보내면, server가 그를 다시 echo 해주는 예제이다.  
여기서 client가 HTTP server 같은 더 복잡한 server과 통신하게 되는 경우, 물론 client program도 복잡해진다.  
아래는 기본적인 예제를 다지는 정도로 학습하면 좋다.

1. Socket을 open 한다.
2. Socket의 input stream, ouput stream을 open 한다.
3. Server의 protocol에 따라 stream에서 읽고, stream에 쓴다.
4. Stream을 닫는다.
5. Socket을 닫는다.

기본적인 단계는 위와 같이 진행되며, server에 따라 step 3번의 구현 내용이 조금씩 달라진다. 다른 step들은 거의 동일하게 유지된다.

```Java

/*
 * Copyright (c) 1995, 2013, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 
import java.io.*;
import java.net.*;
 
public class EchoClient {
    public static void main(String[] args) throws IOException {
         
        if (args.length != 2) {
            System.err.println(
                "Usage: java EchoClient <host name> <port number>");
            System.exit(1);
        }
 
        String hostName = args[0];
        int portNumber = Integer.parseInt(args[1]);
 
        /*
        * try-with-resources
        * 생성된 resource를 Java Runtime이 자동으로 닫는다.
        * 이때 resource를 생성한 역순으로 닫히며,
        * Socket에 연결된 stream은 socket 자체가 닫히기 저넹 닫혀야 하므로 이를 쉽게 보장해 줄 수 있다.
        */
        try (

            /*
            * 1st statement
            * 새로운 Socket 객체를 생성하고, 이름을 echoSocket으로 지정한다.
            * 이때 연결하려는 네트워크 기기에서 사용할 host name, port number가 필요하다.*
            */
            Socket echoSocket = new Socket(hostName, portNumber);

            /*
            * 2nd statement
            * Socket의 output stream을 가져와서 out이라는 이름의 PrintWriter를 open한다.
            * Unicode 문자의 writer 역할을 담당한다.
            * Socket에 연결된 stream이므로 socket 자체가 닫히기 전에 닫혀야 한다.
            */
            PrintWriter out =
                new PrintWriter(echoSocket.getOutputStream(), true);

            /*
            * 3rd statement
            * Socket의 input stream을 가져와서 해당 stream에 in이라는 이름의 BufferedReader를 open한다.
            * Unicode 문자의 reader 역할을 담당한다.
            * Socket에 연결된 stream이므로 socket 자체가 닫히기 전에 닫혀야 한다.
            */
            BufferedReader in =
                new BufferedReader(
                    new InputStreamReader(echoSocket.getInputStream()));
            
            BufferedReader stdIn =
                new BufferedReader(
                    new InputStreamReader(System.in))
        ) {
            String userInput;
            while ((userInput = stdIn.readLine()) != null) { // 사용자가 end-of-input 문자(Ctrl + C)를 입력할 때까지 반복
                // 사용자의 입력을 `EchoServer`로 전달한다.
                out.println(userInput);

                // Socket에 연결된 BufferedReader의 정보를 한 줄씩 읽는다.
                // Server가 정보를 `EchoClient`로 다시 echo 할 때까지 기다린다.
                // in.readLine()로부토 읽어 온 정보를 출력한다.
                System.out.println("echo: " + in.readLine());
            }
        } catch (UnknownHostException e) {
            System.err.println("Don't know about host " + hostName);
            System.exit(1);
        } catch (IOException e) {
            System.err.println("Couldn't get I/O for the connection to " +
                hostName);
            System.exit(1);
        } 
    }
}
```

```Java
/*
 * Copyright (c) 2013, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 
import java.net.*;
import java.io.*;
 
public class EchoServer {
    public static void main(String[] args) throws IOException {
         
        if (args.length != 1) {
            System.err.println("Usage: java EchoServer <port number>");
            System.exit(1);
        }
         
        int portNumber = Integer.parseInt(args[0]);
         
        try (
            ServerSocket serverSocket =
                new ServerSocket(Integer.parseInt(args[0]));
            Socket clientSocket = serverSocket.accept();     
            PrintWriter out =
                new PrintWriter(clientSocket.getOutputStream(), true);                   
            BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream()));
        ) {
            String inputLine;
            while ((inputLine = in.readLine()) != null) {
                out.println(inputLine);
            }
        } catch (IOException e) {
            System.out.println("Exception caught when trying to listen on port "
                + portNumber + " or listening for a connection");
            System.out.println(e.getMessage());
        }
    }
}
```

<br/>

*만약 연결하려는 네트워크 기기 정보(host name, IP 주소)에 대한 유효성 검사를 실행하려면 아래와 같은 절차를 따를 수 있다.  
  1. 주소가 `echoserver.example.com`이고, 수신 대기 중인 port number가 7번인 컴퓨터에서 실행 중인 프로그램이 있다.
  2. 만약 `EchoServer` class를 예제 server로 사용하는 경우 아래의 명령어(command)를 실행시키면 된다.
   ```sh
   $ java EchoServer 7
   ```
   3. 만약 `EchoClient` class를 예제 client로 사용하는 경우 아래의 명령어를 실행시키면 된다.
   ```sh
   $ java EchoClient echoserver.example.com 7
   ```

<br/>

### 2.6 Writing the Server Side of a Socket
여기서는 Knock Knock jokes를 예제로 구현해 볼 예정이다. Knock Knock jokes는 보통 다음과 같이 진행된다.

Server: Knock knock!  
Client: 거기 누구세요?  
Server: Dexter  
Client: Dexter 누구요?  
Server: 호랑 가시 나무 가지를 가지고 있는 Dexter halls  
Client: 응?

이 예제는 독립적으로 실행되는 2개의 Java program, 즉 client-server로 구성된다.  
구현되는 class에 대한 내용은 아래 표를 참고하면 된다.   

| Side | Class | Description |
| - | - | - |
| Client | `KnockKnockClient` | 위의 `EchoClient`와 거의 유사하다. |
| Server | `KnockKnockServer` | 위의 `EchoServer`와 거의 유사하다. Listening port, establishing connection, reading form and writing to the socket과 같은 작업을 수행한다. |
| Server | `KnockKnockProtocol*` | Jokes를 제공하며, current joke, current state* 값을 추적하고, current state에 따라 joke를 다양한 text 조각들로 반환한다. |

<br/>

*Protocol: Client-server가 통신에 사용하기로 합의한 언어를 의미한다.  
*Current state: Sent knock knock, Set clue 등

아래에서는 구체적인 구현에 대해 살펴볼 것이다. 이때 위의 `Echo*`와 겹치는 부분은 생략한다.
먼저, server program은 특정 port에서 listening (수신 대기) 할 객체를 만드는 것부터 시작된다.

```Java
/*
 * Copyright (c) 1995, 2014, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 
import java.net.*;
import java.io.*;
 
public class KnockKnockServer {
    public static void main(String[] args) throws IOException {
         
        if (args.length != 1) {
            System.err.println("Usage: java KnockKnockServer <port number>");
            System.exit(1);
        }
 
        int portNumber = Integer.parseInt(args[0]); // 아직 다른 application에서 사용되지 않는 port를 선택해야 한다.
 
        try ( 
            /*
            * ServerSocket은 java.net 패키지의 class이다.
            * Client-server 연결에서 server 측에 대한 system-independent한 구현을 제공한다.
            * ServerSocket의 constructor(생성자)는 지정된 port number에서 listening (수신 대기) 할 수 없는 경우 (E.g., 해당 port number가 이미 사용 중인 경우) 예외를 던진다. 예외가 발생한다면 `KnockKnockServer`를 종료시킬 수밖에 없다.
            */
            ServerSocket serverSocket = new ServerSocket(portNumber);

            /*
            * 성공적으로 server가 해당 port에 binding 된 후 ServerSocket 객체가 생긴 다음 단계이다.
            * Client로부터 연결을 수락하는 단계이다.
            * `accpet()` method: Client가 시작될 때까지 기다렸다가 해당 server의 host와 port에 연결을 요청한다. 만약 성공한다면, client의 IP 주소와 port number(server 컴퓨터의 port로 새로 지정된다.)와 동일하게 설정된 Socket 객체를 반환한다.
            */
            Socket clientSocket = serverSocket.accept();
            PrintWriter out =
                new PrintWriter(clientSocket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream()));
        ) {
         
            String inputLine, outputLine;
             
            // Initiate conversation with client
            KnockKnockProtocol kkp = new KnockKnockProtocol();
            outputLine = kkp.processInput(null); // Server가 client에게 가장 먼저 보내는 첫 번째 메시지를 가져온다.
            out.println(outputLine); // Client socket에 연결된 `PrintWriter`에 정보를 기록하여 client에게 메시지를 전송한다.
 
            while ((inputLine = in.readLine()) != null) { // Input stream에서 읽기를 반복한다.
                outputLine = kkp.processInput(inputLine); // Client 응답이 KnockKnockProtocol 객체에 전달되고, 
                out.println(outputLine);
                if (outputLine.equals("Bye."))
                    break;
            }
        } catch (IOException e) {
            System.out.println("Exception caught when trying to listen on port "
                + portNumber + " or listening for a connection");
            System.out.println(e.getMessage());
        }
    }
}
```

<br/>

아래는 `KnockKnockProtocol`에 대한 설명이다.  
`KnockKnockProtocol` class는 client-server가 통신하는 데 사용하는 프로토콜을 구현하였다.  
`KnockKnockProtocol`의 역할 및 특징은 다음과 같다.  
- Client와 server가 대화 중 어느 위치에 있는지 추적한다.
- Client의 문장에 대한 server의 응답을 제공한다.
- 모든 knock의 text가 포함되어 있으며, client가 server의 문장에 대해 적절한 응답을 제공하도록 한다.

모든 client-server pair에는 서로 대화하는 프로토콜이 있어야 하며, 그렇지 않으면 주고받는 데이터가 무의미해진다.  
Client-server가 사용하는 프로토콜은 작업을 수행하는 데 필요한 통신에 따라 달라진다.

```Java

/*
 * Copyright (c) 1995, 2008, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 
import java.net.*;
import java.io.*;
 
public class KnockKnockProtocol {
    private static final int WAITING = 0;
    private static final int SENTKNOCKKNOCK = 1;
    private static final int SENTCLUE = 2;
    private static final int ANOTHER = 3;
 
    private static final int NUMJOKES = 5;
 
    private int state = WAITING;
    private int currentJoke = 0;
 
    private String[] clues = { "Turnip", "Little Old Lady", "Atch", "Who", "Who" };
    private String[] answers = { "Turnip the heat, it's cold in here!",
                                 "I didn't know you could yodel!",
                                 "Bless you!",
                                 "Is there an owl in here?",
                                 "Is there an echo in here?" };
 
    public String processInput(String theInput) {
        String theOutput = null;
 
        if (state == WAITING) {
            theOutput = "Knock! Knock!";
            state = SENTKNOCKKNOCK;
        } else if (state == SENTKNOCKKNOCK) {
            if (theInput.equalsIgnoreCase("Who's there?")) {
                theOutput = clues[currentJoke];
                state = SENTCLUE;
            } else {
                theOutput = "You're supposed to say \"Who's there?\"! " +
                "Try again. Knock! Knock!";
            }
        } else if (state == SENTCLUE) {
            if (theInput.equalsIgnoreCase(clues[currentJoke] + " who?")) {
                theOutput = answers[currentJoke] + " Want another? (y/n)";
                state = ANOTHER;
            } else {
                theOutput = "You're supposed to say \"" + 
                clues[currentJoke] + 
                " who?\"" + 
                "! Try again. Knock! Knock!";
                state = SENTKNOCKKNOCK;
            }
        } else if (state == ANOTHER) {
            if (theInput.equalsIgnoreCase("y")) {
                theOutput = "Knock! Knock!";
                if (currentJoke == (NUMJOKES - 1))
                    currentJoke = 0;
                else
                    currentJoke++;
                state = SENTKNOCKKNOCK;
            } else {
                theOutput = "Bye.";
                state = WAITING;
            }
        }
        return theOutput;
    }
}
```

<br/>

아래는 `KnockKnockClient`에 대한 설명이다.  
- Client program을 실행할 때 server는 이미 실행 중이고, port를 listening하며 client의 연결 요청을 기다리고 있어야 한다.
- Client program은 먼저 server의 host name과 port로 지정된 socket을 열어야 한다.

참고로, 아래 명령어는 `KnockKnockServer`를 실행하는 컴퓨터의 host name과 port number를 사용하여 `KnockKnockClient`를 실행시키는 명령어이다.

```sh
$ java KnockKonckClient knockknockserver.example.com 4444
```

> <span style="color: orange">Remember that the server gets a new socket as well.</span>

이때 client의 socket은 client의 컴퓨터에서도 사용 가능한 port에 binding 되어야 한다. 이렇게 함으로써 server의 socket과 client의 socket이 연결되는 것이다.

```Java

/*
 * Copyright (c) 1995, 2013, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
 
import java.io.*;
import java.net.*;
 
public class KnockKnockClient {
    public static void main(String[] args) throws IOException {
         
        if (args.length != 2) {
            System.err.println(
                "Usage: java EchoClient <host name> <port number>");
            System.exit(1);
        }
 
        String hostName = args[0];
        int portNumber = Integer.parseInt(args[1]);
 
        try (
            Socket kkSocket = new Socket(hostName, portNumber);
            PrintWriter out = new PrintWriter(kkSocket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(
                new InputStreamReader(kkSocket.getInputStream()));
        ) {
            BufferedReader stdIn =
                new BufferedReader(new InputStreamReader(System.in));
            String fromServer;
            String fromUser;
 
            while ((fromServer = in.readLine()) != null) { // 먼저 server가 말하고, client가 들어야 한다.
                System.out.println("Server: " + fromServer);
                if (fromServer.equals("Bye."))
                    break;
                 
                fromUser = stdIn.readLine();
                if (fromUser != null) {
                    System.out.println("Client: " + fromUser);
                    out.println(fromUser); // Socket에 연결된 out stream을 통해 text를 server로 보낸다.
                }
            }
        } catch (UnknownHostException e) {
            System.err.println("Don't know about host " + hostName);
            System.exit(1);
        } catch (IOException e) {
            System.err.println("Couldn't get I/O for the connection to " +
                hostName);
            System.exit(1);
        }
    }
}
```


<br/>

## 3. References
- [「Trail: Custom Networking」, 『The Java Tutorial』, Oracle](https://docs.oracle.com/javase/tutorial/networking/index.html)