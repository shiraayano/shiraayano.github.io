### BS架构（Browser-Server架构）
**BS架构**，即Browser-Server架构，是一种基于浏览器和服务器的架构模式。它的主要特点是：

1. **客户端**：用户通过浏览器访问应用程序，无需安装专门的软件。
2. **服务器端**：所有的业务逻辑和数据处理都在服务器端完成，客户端只负责显示和交互。
3. **优点**：
    - 易于维护和升级：只需在服务器端进行更新，客户端无需任何操作。
    - 跨平台：只要有浏览器，就可以访问应用程序，无论是PC、手机还是平板。
4. **缺点**：
    - 对网络依赖较强：需要稳定的网络连接。
    - 性能受限：由于所有操作都在服务器端完成，可能会受到服务器性能和网络带宽的限制。

### CS架构（Client-Server架构）
**CS架构**，即Client-Server架构，是一种基于客户端和服务器的架构模式。它的主要特点是：

1. **客户端**：用户需要安装专门的软件，客户端负责部分业务逻辑和数据处理。
2. **服务器端**：服务器负责主要的业务逻辑和数据处理，客户端与服务器进行数据交互。
3. **优点**：
    - 性能较好：客户端可以分担部分计算任务，减轻服务器压力。
    - 功能丰富：客户端软件可以提供更丰富的功能和更好的用户体验。
4. **缺点**：
    - 维护和升级较复杂：需要在每个客户端进行更新。
    - 跨平台性较差：不同平台需要开发不同版本的客户端软件。

### 总结
+ **BS架构**适用于需要频繁更新和跨平台访问的应用，如Web应用、在线服务等。
+ **CS架构**适用于需要高性能和丰富功能的应用，如桌面软件、企业内部系统等。



### 实现网络传输的三个要素
1. **使用IP地址**：准确地定位网络上一台或多台主机。
2. **使用端口号**：定位主机上的特定应用。
3. **规范网络通信协议**：可靠、高效地进行数据传输。

### 通信要素1：IP地址
#### 3.1 作用
IP地址用来给网络中的一台计算机设备做唯一的编号。

#### 3.2 IP地址分类
1. **IPv4**：
    - 占用4个字节。
    - 例如：192.168.0.1
2. **IPv6**：
    - 占用16个字节。
    - 例如：2001:0db8:85a3:0000:0000:8a2e:0370:7334



### IP地址分类方式2
1. **公网地址**：
    - 用于万维网（Internet）。
    - 例如：8.8.8.8（Google的公共DNS服务器）。
2. **私有地址**：
    - 用于局域网（LAN）。
    - 例如：192.168.0.1（常见的路由器地址）。

### 本地回路地址
+ **127.0.0.1**：本地回路地址，用于测试本机网络配置和网络应用。

### 域名
域名是便捷的记录IP地址的方式，便于人们记忆和使用。例如：

+ www.baidu.com
+ www.atguigu.com
+ www.bilibili.com
+ www.id.com
+ www.mi.com
+ www.vip.com

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731841401748-b525df35-e29c-4e41-8598-22d48b6d5f90.png)

### 通信要素2：端口号
#### 作用
+ 端口号可以唯一标识主机中的进程（应用程序）。
+ 不同的进程分配不同的端口号。
+ 端口号的范围是0~65535。

### InetAddress的使用
#### 5.1 作用
+ `InetAddress`类的一个实例就代表一个具体的IP地址。

#### 5.2 实例化方式
1. `InetAddress getByName(String host)`：获取指定IP对应的`InetAddress`的实例。
2. `InetAddress getLocalHost()`：获取本地IP对应的`InetAddress`的实例。

#### 5.3 常用方法
1. `getHostName()`：获取主机名。
2. `getHostAddress()`：获取IP地址



```plain
import java.net.InetAddress;
import java.net.UnknownHostException;

public class InetAddressExample {
    public static void main(String[] args) {
        try {
            // 获取指定IP地址的InetAddress对象
            InetAddress inet1 = InetAddress.getByName("192.168.23.31");
            System.out.println(inet1);

            // 获取指定域名的InetAddress对象
            InetAddress inet2 = InetAddress.getByName("www.atguigu.com");
            System.out.println(inet2); // www.atguigu.com/122.228.95.175

            // 获取本地主机的InetAddress对象
            InetAddress inet3 = InetAddress.getLocalHost();
            System.out.println(inet3); // DESKTOP-QCP2QPI/192.168.21.107

        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}

```

### TCP协议
1. **通信的两个应用进程**：客户端、服务端。
2. **建立连接**：使用TCP协议前，须先建立TCP连接，形成基于字节流的传输数据通道。
3. **三次握手**：传输前，采用“三次握手”方式，点对点通信，是可靠的。
4. **重发机制**：TCP协议使用重发机制，当一个通信实体发送一个消息给另一个通信实体后，需要收到另一个通信实体确认信息，如果没有收到确认信息，则会再次重复发送消息。
5. **大数据量传输**：在连接中可进行大数据量的传输。
6. **释放连接**：传输完毕，需释放已建立的连接，效率较低。

### UDP协议
1. **通信的两个应用进程**：发送端、接收端。
2. **数据包**：将数据、源、目的封装成数据包（传输的基本单位），不需要建立连接。
3. **不可靠传输**：发送不管对方是否准备好，接收方收到也不确认，不能保证数据的完整性，故是不可靠的。
4. **数据报大小限制**：每个数据报的大小限制在64K内。
5. **无需释放资源**：发送数据结束时无需释放资源，开销小，通信效率高。
6. **适用场景**：适用于音频、视频和普通数据的传输，例如视频会议。



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731850434927-e1039cea-e6b7-4add-8359-f1b2ec23e1a2.png)

### TCP三次握手
**三次握手**是TCP协议在建立连接时使用的过程，确保双方都准备好进行通信。具体步骤如下：

1. **第一次握手**：
    - 客户端发送一个SYN（同步序列编号）包到服务器，表示客户端希望建立连接。
    - 服务器接收到SYN包后，进入SYN-RECEIVED状态。
2. **第二次握手**：
    - 服务器发送一个SYN-ACK（同步确认）包到客户端，表示服务器同意建立连接，并确认客户端的SYN包。
    - 客户端接收到SYN-ACK包后，进入SYN-RECEIVED状态。
3. **第三次握手**：
    - 客户端发送一个ACK（确认）包到服务器，表示客户端确认服务器的SYN-ACK包。
    - 服务器接收到ACK包后，进入ESTABLISHED状态，连接建立完成。



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731850473777-200564ad-9864-425a-9312-52d991ca49e3.png)

### TCP四次挥手
**四次挥手**是TCP协议在断开连接时使用的过程，确保双方都能正常关闭连接。具体步骤如下：

1. **第一次挥手**：
    - 客户端发送一个FIN（结束）包到服务器，表示客户端希望断开连接。
    - 服务器接收到FIN包后，进入CLOSE-WAIT状态。
2. **第二次挥手**：
    - 服务器发送一个ACK（确认）包到客户端，表示服务器确认客户端的FIN包。
    - 客户端接收到ACK包后，进入FIN-WAIT-2状态。
3. **第三次挥手**：
    - 服务器发送一个FIN包到客户端，表示服务器也希望断开连接。
    - 客户端接收到FIN包后，进入CLOSING状态。
4. **第四次挥手**：
    - 客户端发送一个ACK包到服务器，表示客户端确认服务器的FIN包。
    - 服务器接收到ACK包后，进入CLOSED状态，连接断开完成。



### Socket类
**Socket**类是网络编程中用于实现通信的基本单元。网络上具有唯一标识的IP地址和端口号组合在一起构成唯一能识别的标识符——套接字（Socket）。利用套接字开发网络应用程序早已被广泛采用，成为事实上的标准。网络通信其实就是Socket间的通信。

#### 主要特点
+ **通信的两端都要有Socket**：是两台机器间通信的端点。
+ **数据传输**：Socket允许程序把网络连接当成一个流，数据在两个Socket间通过I/O传输。
+ **客户端和服务端**：一般主动发起通信的应用程序属客户端，等待通信请求的为服务端。

#### Socket分类
1. **流套接字（Stream Socket）**：
    - 使用TCP提供可依赖的字节流服务。
    - **ServerSocket**：实现TCP服务器套接字，等待请求通过网络传入。
    - **Socket**：实现客户端套接字，是两台机器间通信的端点。
2. **数据报套接字（Datagram Socket）**：
    - 使用UDP提供“尽力而为”的数据报服务。
    - **DatagramSocket**：用于发送和接收UDP数据报包的套接字。



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731850676130-0ca79199-3136-4bd2-baca-d2aa38f8d997.png)





```plain
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TCPTest1 {
    // 客户端
    public void client() {
        try {
            // 创建一个Socket连接到服务器
            Socket socket = new Socket("localhost", 8888);
            System.out.println("客户端已连接到服务器");

            // 发送数据到服务器
            OutputStream outputStream = socket.getOutputStream();
            String message = "Hello, Server!";
            outputStream.write(message.getBytes());

            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // 服务端
    public void server() {
        try {
            // 创建一个ServerSocket
            ServerSocket serverSocket = new ServerSocket(8888);
            System.out.println("服务器已启动，等待客户端连接...");
            // 调用accept() 接收客户端的Socket
            Socket socket = serverSocket.accept();
            System.out.println("客户端已连接");

            // 接收数据
            InputStream inputStream = socket.getInputStream();
            byte[] buffer = new byte[1024];
            int len = inputStream.read(buffer);
            while (len != -1) {
                System.out.println(new String(buffer, 0, len));
                len = inputStream.read(buffer);
            }

            socket.close();
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        TCPTest1 test = new TCPTest1();
        // 启动服务端
        new Thread(() -> test.server()).start();
        // 启动客户端
        new Thread(() -> test.client()).start();
    }
}

```

+ 需要注意 使用 byte 传输时有可能会出现汉字乱码，这时候我们可以使用 ByteArrayOutputStream

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731851714011-e2641bd3-0103-46e4-a753-bf27fd33c22b.png)



### 客户端代码
java

```plain
import java.io.*;
import java.net.Socket;

public class FileClient {
    public static void main(String[] args) {
        try {
            // 创建一个Socket连接到服务器
            Socket socket = new Socket("localhost", 8888);
            System.out.println("客户端已连接到服务器");

            // 发送文件到服务器
            File file = new File("path/to/your/file.txt");
            FileInputStream fis = new FileInputStream(file);
            OutputStream os = socket.getOutputStream();

            byte[] buffer = new byte[1024];
            int len;
            while ((len = fis.read(buffer)) != -1) {
                os.write(buffer, 0, len);
            }

            fis.close();
            os.close();
            socket.close();
            System.out.println("文件发送成功");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 服务端代码
java

```plain
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class FileServer {
    public static void main(String[] args) {
        try {
            // 创建一个ServerSocket
            ServerSocket serverSocket = new ServerSocket(8888);
            System.out.println("服务器已启动，等待客户端连接...");

            // 接收客户端的连接
            Socket socket = serverSocket.accept();
            System.out.println("客户端已连接");

            // 接收文件
            InputStream is = socket.getInputStream();
            FileOutputStream fos = new FileOutputStream("path/to/save/received_file.txt");

            byte[] buffer = new byte[1024];
            int len;
            while ((len = is.read(buffer)) != -1) {
                fos.write(buffer, 0, len);
            }

            fos.close();
            is.close();
            socket.close();
            serverSocket.close();
            System.out.println("文件接收成功");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 说明
1. **客户端**：
    - 创建一个Socket连接到服务器。
    - 读取文件并通过Socket的输出流发送到服务器。
2. **服务端**：
    - 创建一个ServerSocket等待客户端连接。
    - 接收客户端发送的文件并保存到指定路径。



聊天室

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731852984101-b5913a89-0e9b-4ea4-a099-23fc1fd2378d.png)





UDP



### 发送端代码
java

```plain
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class UDPTest {
    public void sender() throws Exception {
        // 1. 创建DatagramSocket的实例
        DatagramSocket ds = new DatagramSocket();

        // 2. 将数据、目的地的IP，目的地的端口号都封装在DatagramPacket数据报中
        InetAddress inetAddress = InetAddress.getByName("127.0.0.1");
        int port = 9090;
        byte[] bytes = "我是发送端".getBytes("UTF-8");
        DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length, inetAddress, port);

        // 发送数据
        ds.send(packet);
        ds.close();
        System.out.println("数据发送成功");
    }
}
```

### 接收端代码
java

```plain
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class UDPTest {
    @Test
    public void receiver() throws Exception {
        // 1. 创建DatagramSocket的实例
        int port = 9090;
        DatagramSocket ds = new DatagramSocket(port);

        // 接收数据
        byte[] buffer = new byte[1024];
        DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
        ds.receive(packet);

        // 处理接收到的数据
        String receivedData = new String(packet.getData(), 0, packet.getLength(), "UTF-8");
        System.out.println("接收到的数据: " + receivedData);

        ds.close();
    }
}
```

### 说明
1. **发送端**：
    - 创建一个 `DatagramSocket` 实例。
    - 将数据、目的地的IP地址和端口号封装在 `DatagramPacket` 数据报中。
    - 发送数据报并关闭 `DatagramSocket`。
2. **接收端**：
    - 创建一个 `DatagramSocket` 实例并绑定到指定端口。
    - 接收数据报并处理接收到的数据。
    - 关闭 `DatagramSocket`。





### URL (Uniform Resource Locator)
#### 1. 作用
一个具体的URL就对应着互联网上某一资源的地址。它是定位和访问网络资源的关键。

#### 2. URL的格式
一个URL的典型格式如下：

```plain
http://192.168.21.107:8080/examples/abcd.jpg?name=Tom
```

+ **应用层协议**：`http`
+ **IP地址**：`192.168.21.107`
+ **端口号**：`8080`
+ **资源地址**：`/examples/abcd.jpg`
+ **参数列表**：`?name=Tom`

### URL类的实例化及常用方法
#### 实例化方式
**通过字符串创建URL对象**：

1. java

```plain
URL url = new URL("http://www.example.com");
```

**通过协议、主机、文件路径创建URL对象**：

2. java

```plain
URL url = new URL("http", "www.example.com", "/index.html");
```

**通过协议、主机、端口、文件路径创建URL对象**：

3. java

```plain
URL url = new URL("http", "www.example.com", 80, "/index.html");
```

#### 常用方法
**获取协议**：

1. java

```plain
String protocol = url.getProtocol();
```

**获取主机名**：

2. java

```plain
String host = url.getHost();
```

**获取端口号**：

3. java

```plain
int port = url.getPort();
```

**获取文件路径**：

4. java

```plain
String path = url.getPath();
```

**获取查询参数**：

5. java

```plain
String query = url.getQuery();
```



### 端口号
**作用**：

+ 用于区分同一台主机上的不同进程。
+ 不同的进程分配不同的端口号。

**范围**：

+ 0-65535

### 网络通信协议
网络通信协议有两套参考模型：

1. **OSI参考模型**：
    - 模型过于理想化，未能在因特网上进行广泛推广。
2. **TCP/IP参考模型（或TCP/IP协议）**：
    - 事实上的国际标准。

在传输层中涉及到两个协议：TCP和UDP。二者的对比如下：

#### TCP协议
+ **可靠的连接**：发送数据前，需要三次握手，断开连接时需要四次挥手。
+ **大数据量传输**：适合进行大数据量的传输。
+ **效率低**：由于需要建立连接和确认数据的接收，效率较低。

#### UDP协议
+ **不可靠的连接**：发送前不需要确认对方是否在，接收方也不确认数据的接收。
+ **数据报传输**：每个数据报的大小限制在64KB以内。
+ **效率高**：发送数据结束时无需释放资源，开销小，通信效率高。
+ **适用场景**：适用于音频、视频和普通数据的传输，例如视频会议。

### TCP的三次握手和四次挥手
**三次握手**：

1. 客户端发送SYN包到服务器，表示希望建立连接。
2. 服务器发送SYN-ACK包到客户端，表示同意建立连接。
3. 客户端发送ACK包到服务器，确认连接建立。

**四次挥手**：

1. 客户端发送FIN包到服务器，表示希望断开连接。
2. 服务器发送ACK包到客户端，确认收到断开请求。
3. 服务器发送FIN包到客户端，表示也希望断开连接。
4. 客户端发送ACK包到服务器，确认断开连接。

### TCP网络编程
TCP网络编程涉及到使用`Socket`和`ServerSocket`类来实现客户端和服务端之间的通信。客户端主动发起连接，服务端等待连接请求。

### UDP网络编程
UDP网络编程涉及到使用`DatagramSocket`和`DatagramPacket`类来实现数据报的发送和接收。UDP不需要建立连接，适合快速传输小数据量的场景





### TCP网络编程
#### 例题1：客户端发送内容给服务端，服务端将内容打印到控制台上
**客户端代码**：

java

```plain
import java.io.OutputStream;
import java.net.Socket;

public class TCPClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 8888);
            OutputStream os = socket.getOutputStream();
            os.write("Hello, Server!".getBytes());
            os.close();
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**服务端代码**：

java

```plain
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TCPServer {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(8888);
            Socket socket = serverSocket.accept();
            InputStream is = socket.getInputStream();
            byte[] buffer = new byte[1024];
            int len = is.read(buffer);
            System.out.println(new String(buffer, 0, len));
            is.close();
            socket.close();
            serverSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### 例题2：客户端发送文件给服务端，服务端将文件保存在本地
**客户端代码**：

java

```plain
import java.io.FileInputStream;
import java.io.OutputStream;
import java.net.Socket;

public class FileClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 8888);
            FileInputStream fis = new FileInputStream("path/to/your/file.txt");
            OutputStream os = socket.getOutputStream();
            byte[] buffer = new byte[1024];
            int len;
            while ((len = fis.read(buffer)) != -1) {
                os.write(buffer, 0, len);
            }
            fis.close();
            os.close();
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**服务端代码**：

java

```plain
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class FileServer {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(8888);
            Socket socket = serverSocket.accept();
            InputStream is = socket.getInputStream();
            FileOutputStream fos = new FileOutputStream("path/to/save/received_file.txt");
            byte[] buffer = new byte[1024];
            int len;
            while ((len = is.read(buffer)) != -1) {
                fos.write(buffer, 0, len);
            }
            fos.close();
            is.close();
            socket.close();
            serverSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### 例题3：从客户端发送文件给服务端，服务端保存到本地，并返回“发送成功”给客户端
**客户端代码**：

java

```plain
import java.io.FileInputStream;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.Socket;

public class FileClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 8888);
            FileInputStream fis = new FileInputStream("path/to/your/file.txt");
            OutputStream os = socket.getOutputStream();
            byte[] buffer = new byte[1024];
            int len;
            while ((len = fis.read(buffer)) != -1) {
                os.write(buffer, 0, len);
            }
            socket.shutdownOutput();

            InputStream is = socket.getInputStream();
            byte[] response = new byte[1024];
            int responseLen = is.read(response);
            System.out.println(new String(response, 0, responseLen));

            fis.close();
            os.close();
            is.close();
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**服务端代码**：

java

```plain
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class FileServer {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(8888);
            Socket socket = serverSocket.accept();
            InputStream is = socket.getInputStream();
            FileOutputStream fos = new FileOutputStream("path/to/save/received_file.txt");
            byte[] buffer = new byte[1024];
            int len;
            while ((len = is.read(buffer)) != -1) {
                fos.write(buffer, 0, len);
            }
            fos.close();

            OutputStream os = socket.getOutputStream();
            os.write("发送成功".getBytes());

            is.close();
            os.close();
            socket.close();
            serverSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### UDP网络编程
UDP网络编程涉及到使用`DatagramSocket`和`DatagramPacket`类来实现数据报的发送和接收。UDP不需要建立连接，适合快速传输小数据量的场景。

### URL编程
**Java后台**：将写好的Java程序部署在Tomcat服务器，启动Tomcat服务器。

**前台**：使用浏览器进行访问，需要使用URL（HTML+CSS+JavaScript）。

**URL的作用**：定位互联网上某一资源的地址。

**URL的格式**：

```plain
http://192.168.21.107:8080/examples/abcd.jpg?name=Tom
```

+ **应用层协议**：`http`
+ **IP地址**：`192.168.21.107`
+ **端口号**：`8080`
+ **资源地址**：`/examples/abcd.jpg`
+ **参数列表**：`?name=Tom`

