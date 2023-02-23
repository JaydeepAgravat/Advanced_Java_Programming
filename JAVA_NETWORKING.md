# JAVA NETWORKING

## 1. What is Server Socket? Explain in detail with an example.Discuss the difference between the Socket and ServerSocket class

### Server Socket

- Java Socket programming is used for communication between the applications running on different JRE.

- Java Socket programming can be connection-oriented or connection-less.

- Socket and ServerSocket classes are used for connection-oriented socket programming.

- A socket is simply an endpoint for communications between the machines. The Socket class can be used to create a socket.

- The ServerSocket class can be used to create a server socket. This object is used to establish communication with the clients.

### Example of Java Socket Programming

#### Creating Server

- To create the server application, we need to create the instance of ServerSocket class.

- Here, we are using 6666 port number for the communication between the client and server.

- The accept() method waits for the client.

- If clients connects with the given port number, it returns an instance of Socket.

```java
ServerSocket ss = new ServerSocket(6666);
Socket s = ss.accept();
//establishes connection and waits for the client
```

#### Creating Client

- To create the client application, we need to create the instance of Socket class.

- Here, we need to pass the IP address or hostname of the Server and a port number.

- Here, we are using "localhost" because our server is running on same system.

```java
Socket s = new Socket("localhost",6666);
```

### Socket vs ServerSocket class

| Socket |                      Server Socket                       |                                                           |
| :----: | :------------------------------------------------------: | --------------------------------------------------------- |
|   1    |               Socket used at Client side.                | Server Socket used on the server side.                    |
|   2    |    It is used for sending the request to the server.     | It is used for listening to the client.                   |
|   3    | This class encapsulates the behavior of the active side. | This class encapsulates the behavior of the passive side. |
|   4    |           Establish connection with connect()            | Establish connection with listen()                        |
|   5    |        Socket s = new Socket (“localhost”,1111);         | ServerSocket ss = new ServerSocket(1111);                 |

## 2. what is Datagram Socket? Explain in detail with example

### Datagram Socket

- Java DatagramSocket and DatagramPacket classes are used for connection-less socket programming using the UDP instead of TCP.

- Constructors of DatagramSocket class:

- `DatagramSocket() throws SocketEeption`: it creates a datagram socket and binds it with the available Port Number on the localhost machine.

- `DatagramSocket(int port) throws SocketEeption`: it creates a datagram socket and binds it with the given Port Number.

- `DatagramSocket(int port, InetAddress address) throws SocketEeption`: it creates a datagram socket and binds it with the specified port number and host address.

### Example

```java
import java.net.*;

public class DSender{
    public static void main(String[] args) throws Exception{
        DatagramSocket ds = new DatagramSocket();

        String str = "Message sent by Datagram socket";

        InetAddress ip = InetAddress.getLocalHost();

        DatagramPacket dp = new DatagramPacket(str.getBytes(), str.length(),ip,3000);

        ds.send(dp);

        ds.close();
    }
}
// DatagramSocket() throws SocketEeption: it creates a datagram socket and binds it with the available Port Number on the localhost machine.

// DatagramPacket(byte[] barr, int length, InetAddress address, int port): it creates a datagram packet. This constructor is used to send the packets.

// void send(DatagramPacket p): It sends the datagram packet from the socket.

// close(): It closes the datagram socket.
```

```java
import java.net.*;

public class DReceiver{
    public static void main(String[] args) throws Exception{

        DatagramSocket ds = new DatagramSocket(3000);

        byte[] buf = new byte[1024];

        DatagramPacket dp = new DatagramPacket(buf, 1024);

        ds.receive(dp);

        String str = new String(dp.getData(),0,dp.getLength());

        System.out.println(str);

        ds.close();
    }
}

// DatagramSocket(int port) throws SocketEeption: it creates a datagram socket and binds it with the given Port Number.

// DatagramPacket(byte[] barr, int length): it creates a datagram packet. This constructor is used to receive the packets.

// void receive(DatagramPacket p): It receives the datagram packet from the socket.

//  byte[] getData(): It returns the data buffer.

//  int getLength(): It returns the length of the data to be sent or the length of the data received.
```

## 3. Write a TCP or UDP client and server program to do the following. Client send: ABC XYZ Response from Server: ZYX CBA

`ReverseClient.java`

```java
import java.net.*;
import java.io.*;

public class ReverseClient{
    public static void main(String[] args){
        try{
            Socket s = new Socket("localhost",1111);

            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);
            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);

            String str = "ABC XYZ";
            dos.writeUTF(str); 

            String reverse = dis.readUTF();
            System.out.println(reverse);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`ReverseServer.java`

```java
import java.net.*;
import java.io.*;

public class ReverseServer{
    public static void main(String[] args){
        try{
            ServerSocket ss = new ServerSocket(1111);

            Socket s = ss.accept();

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);
            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);

            String str = dis.readUTF();

            StringBuilder sb = new StringBuilder(str);  
            sb.reverse();  

            String reverse =  sb.toString(); 
            dos.writeUTF(reverse);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
ZYX CBA
```

## 4. Write a client-server program using TCP or UDP where the client sends 10 numbers and server responds with the numbers in sorted order

`SortedClient.java`

```java
import java.net.*;
import java.io.*;
import java.util.Scanner;

public class SortedClient{
    public static void main(String[] args){
        try{
            Socket s = new Socket("localhost",1111);

            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);
            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);

            System.out.println("Enter size of array: ");
            
            Scanner sc = new Scanner(System.in);

            int n = sc.nextInt();

            int[] nums = new int [n];

            System.out.println("Enter element to array: ");

            dos.writeInt(n);

            for(int i=0; i<n; i++){
                nums[i] = sc.nextInt();
                dos.writeInt(nums[i]);
            }

            System.out.println("Sorted array: ");

            for(int i=0; i<n; i++){
                nums[i] = dis.readInt();
                System.out.print(nums[i]+" ");
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`SortedServer.java`

```java
import java.net.*;
import java.io.*;
import java.util.Arrays;

public class SortedServer{
    public static void main(String[] args){
        try{
            ServerSocket ss = new ServerSocket(1111);

            Socket s = ss.accept();

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);
            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);


            int n = dis.readInt();

            int[] nums = new int[n];

            for(int i=0; i<n; i++){
                nums[i] = dis.readInt();
            }

            Arrays.sort(nums);

            for(int i=0; i<n; i++){
                dos.writeInt(nums[i]);
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
Enter size of array: 
5
Enter element to array:
12
454
54
23
56
Sorted array:
12 23 54 56 454
```

## 5. Write a TCP-Server program to get the Date & Time details from server on the Client request.

`DateClient.java`

```java
import java.net.*;
import java.io.*;

public class DateClient{
    public static void main(String[] args){
        try{
            Socket s = new Socket("localhost",5217);

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);

            String receive = dis.readUTF();
            System.out.println(receive);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`DateServer.java`

```java
import java.net.*;
import java.io.*;
import java.util.Date;

public class DateServer{
    public static void main(String[] args){
        try{
            ServerSocket ss = new ServerSocket(5217);

            Socket s = ss.accept();

            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);

            Date date = new Date();
            String send = date.toString();

            dos.writeUTF(send);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
Thu Feb 23 16:45:28 IST 2023
```

## 6. Write a client-server program using TCP where client sends two numbers and server responds with sum of them.

`SumClient.java`

```java
import java.net.*;
import java.io.*;

public class SumClient{
    public static void main(String[] args){
        try{
            Socket s = new Socket("localhost",5217);

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);
            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);

            int x = 12;
            int y = 13;
            dos.writeInt(x);
            dos.writeInt(y); 
            
            int sum = dis.readInt();
            System.out.println(sum);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`SumServer.java`

```java
import java.net.*;
import java.io.*;


public class SumServer{
    public static void main(String[] args){
        try{
            ServerSocket ss = new ServerSocket(5217);

            Socket s = ss.accept();

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);
            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);

            int x = dis.readInt();
            int y = dis.readInt();

            int sum = x + y;

            dos.writeInt(sum);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
25
```

## 7. Write a client server program using TCP where client sends a string and server checks whether that string is palindrome or not and responds with appropriate messsage

`PalindromeClient.java`

```java
import java.net.*;
import java.io.*;

public class PalindromeClient{
    public static void main(String[] args){
        try{
            Socket s = new Socket("localhost",1111);

            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);
            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);

            String str = "ABACBA";
            dos.writeUTF(str); 

            String msg = dis.readUTF();
            System.out.println(msg);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`PalindromeServer.java`

```java
import java.net.*;
import java.io.*;

public class PalindromeServer{
    public static boolean isPalindrome(String str){

        String rev = "";
        boolean ans = false;
 
        for (int i = str.length() - 1; i >= 0; i--) {
            rev = rev + str.charAt(i);
        }
 
        if (str.equals(rev)) {
            ans = true;
        }

        return ans;
    }
    public static void main(String[] args){
        try{
            ServerSocket ss = new ServerSocket(1111);

            Socket s = ss.accept();

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);
            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);

            String str = dis.readUTF();
            String copy = str;
            str = str.toLowerCase();    
            boolean A = isPalindrome(str);

            String msg;

            if(A==true){
                msg = String.format("%s is palindrome.", copy);
            }
            else{
                msg = String.format("%s is not palindrome.", copy);
            }

            dos.writeUTF(msg);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
ABACBA is not palindrome.
```

## 8. Write a sample code for client send a "Hello" message to server.

`HelloClient.java`

```java
import java.net.*;
import java.io.*;

public class HelloClient{
    public static void main(String[] args){
        try{
            Socket s = new Socket("localhost",1111);

            OutputStream os = s.getOutputStream();
            DataOutputStream dos = new DataOutputStream(os);

            String str = "Hello";

            dos.writeUTF(str); 
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`HelloServer.java`

```java
import java.net.*;
import java.io.*;

public class HelloServer{
    public static void main(String[] args){
        try{
            ServerSocket ss = new ServerSocket(1111);
            Socket s = ss.accept();

            InputStream is = s.getInputStream();
            DataInputStream dis = new DataInputStream(is);

            String str = dis.readUTF();

            System.out.println("message: "+str);
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
Hello
```

## 9

## 10. Explain the following classes with their use

### URL Connection

- The Java URLConnection class represents a communication link between the URL and the application. 

- It can be used to read and write data to the specified resource referred by the URL.

```java
import java.io.*;
import java.net.*;

public class URLConnectionDemo{
    public static void main(String[] args){
        try{
            URL url = new URL("https://www.google.com/");

            URLConnection urlCon = url.openConnection();

            InputStream stream = urlCon.getInputStream();

            int i;

            while( (i=stream.read()) != -1 ){
                System.out.print((char)i);
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}

// Creates a URL from the given String.

// The openConnection() method returns a java.net.URLConnection, an abstract class whose subclasses represent the various types of URL connections.


// Returns the input stream of the URL connection for reading from the resource.
```

### DatagramSocket

- Java DatagramSocket class represents a connection-less socket for sending and receiving datagram packets. 
- It is a mechanism used for transmitting datagram packets over network.`
- A datagram is basically an information but there is no guarantee of its content, arrival or arrival time.

### DatagramPacket

- Java DatagramPacket is a message that can be sent or received. It is a data container. If you send multiple packet, it may arrive in any order. Additionally, packet delivery is not guaranteed.

### Example of DatagramSocket & DatagramPacket

```java
import java.net.*;

public class DSender{
    public static void main(String[] args) throws Exception{
        DatagramSocket ds = new DatagramSocket();

        String str = "Message sent by Datagram socket";

        InetAddress ip = InetAddress.getLocalHost();

        DatagramPacket dp = new DatagramPacket(str.getBytes(), str.length(),ip,3000);

        ds.send(dp);

        ds.close();
    }
}
// DatagramSocket() throws SocketEeption: it creates a datagram socket and binds it with the available Port Number on the localhost machine.

// DatagramPacket(byte[] barr, int length, InetAddress address, int port): it creates a datagram packet. This constructor is used to send the packets.

// void send(DatagramPacket p): It sends the datagram packet from the socket.

// close(): It closes the datagram socket.
```

```java
import java.net.*;

public class DReceiver{
    public static void main(String[] args) throws Exception{

        DatagramSocket ds = new DatagramSocket(3000);

        byte[] buf = new byte[1024];

        DatagramPacket dp = new DatagramPacket(buf, 1024);

        ds.receive(dp);

        String str = new String(dp.getData(),0,dp.getLength());

        System.out.println(str);

        ds.close();
    }
}

// DatagramSocket(int port) throws SocketEeption: it creates a datagram socket and binds it with the given Port Number.

// DatagramPacket(byte[] barr, int length): it creates a datagram packet. This constructor is used to receive the packets.

// void receive(DatagramPacket p): It receives the datagram packet from the socket.

//  byte[] getData(): It returns the data buffer.

//  int getLength(): It returns the length of the data to be sent or the length of the data received.
```

## 11. How do you get the IP address of a machine from its hostname?

`IPHost.java`

```java
import java.net.*;

public class IPHost{
    public static void main(String[] args){
        try{
            InetAddress local = InetAddress.getLocalHost();
            System.out.println("Host Name: "+local.getHostName());
            System.out.println("IP Adress: "+local.getHostAddress());
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
```

`OUTPUT:`

```cmd
Host Name: DESKTOP-F50Q5F8
IP Adress: 192.168.43.227
```

## 12. What are the differences between a TCP socket and UDP socket? How are they created in Java?

## 13. Write a java program where client sends a string as a message and server counts the characters in the received message from client. Server sends this value back to the client. Server should be able to serve multiple clients simultaneously
