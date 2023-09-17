# Java
## Working with Files and APIs

### Table of Contents
[1. Java에서의 File API](#➲-java에서의-file-api)  
[2. Java에서의 File 기본 작업](#➲-java에서의-file-기본-작업)  
[3. 파일 입출력 관련 클래스](#➲-파일-입출력-관련-클래스)  
[4. 참고 자료](#➲-참고-자료)  

</br>

### ➲ Java에서의 File API
- Java에는 아래의 두 가지 파일 API가 존재한다.
  - `java.io.File`: Java 1.0(1966)부터 사용 가능한 API
  - `java.nio.file.Path`: Java 1.7(2011)부터 사용 가능한 최신 API

`java.io.File` API는 이때까지 진행되었던 수많은 프로젝트, 프레임워크 및 라이브러리에서 사용되어져 왔다. 그럼에도 불구하고 `java.nio.file.Path`는 일반적으로 오래되어 온 File API보다 더 나은 그 이상을 수행할 것이라고 기대되어져 오는데, 그 이유는 아래와 같다.

1. 파일 기능: 심볼릭 링크, 적절한 파일 속성 및 메타데이터 지원, ACL 등 지원
2. 더 나은 사용법: 파일 삭제 시 단순한 `false`가 아닌 의미 있는 오류 메시지와 함께 예외 발생
3. 디커플링: In-memory 파일 시스템에 대한 지원 활성화

물론, 새로운 Java에서의 File API를 다루는 것도 좋지만, 이번에는 `java.io.File`에 대한 내용을 다루어 보고자 한다. 조금 더 자세한 새로운 파일 API(`java.nio.file.Path`)에 대한 내용을 원한다면, 참고 자료의 첫 번째 링크를 참고하면 된다.

</br>

### ➲ Java에서의 File 기본 작업
#### 파일이나 디렉토리가 물리적으로 존재하는지 확인하는 프로그램
```Java
// In this Java program, we accepts a file or directory name
// from command line arguments. Then the program will check
// if that file or directory physically exist or not and it
// displays the property of that file or directory.

import java.io.File;

// Displaying file property
class FileProperty {
	  public static void main(String[] args) {

        // accept file name or directory name through
        // command line args
        String fname = args[0];

        // pass the filename or directory name to File
        // object
        File f = new File(fname);

        // apply File class methods on File object
        System.out.println("File name :" + f.getName());
        System.out.println("Path: " + f.getPath());
        System.out.println("Absolute path:" + f.getAbsolutePath());
        System.out.println("Parent:" + f.getParent());
        System.out.println("Exists :" + f.exists());

        if (f.exists()) {
            System.out.println("Is writable:"	+ f.canWrite());
            System.out.println("Is readable" + f.canRead());
            System.out.println("Is a directory:" + f.isDirectory());
            System.out.println("File Size in bytes " + f.length());
        }
    }
}
```

#### 디렉토리의 모든 내용을 표시하는 프로그램
```Java
// Java Program to display all
// the contents of a directory
import java.io.BufferedReader;
import java.io.File;
import java.io.IOException;
import java.io.InputStreamReader;

// Displaying the contents of a directory
class Contents {
	public static void main(String[] args) throws IOException {
        // enter the path and dirname from keyboard
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        System.out.println("Enter dirpath:");
        String dirpath = br.readLine();
        System.out.println("Enter the dirname");
        String dname = br.readLine();

        // create File object with dirpath and dname
        File f = new File(dirpath, dname);

        // if directory exists,then
        if (f.exists()) {
            // get the contents into arr[]
            // now arr[i] represent either a File or
            // Directory
            String arr[] = f.list();

            // find no. of entries in the directory
            int n = arr.length;

            // displaying the entries
            for (int i = 0; i < n; i++) {
                System.out.println(arr[i]);
                // create File object with the entry and
                // test if it is a file or directory
                File f1 = new File(arr[i]);
                if (f1.isFile())
                  System.out.println(": is a file");
                if (f1.isDirectory())
                  System.out.println(": is a directory");
            }
            System.out.println("No of entries in this directory " + n);
        }
        else
            System.out.println("Directory not found");
    }
}
```

</br>

### ➲ 파일 입출력 관련 클래스
#### File I/O
| Class | Description |
| - | - |
| `java.io.File` |	파일 및 디렉토리를 나타내는 클래스로, 경로 및 파일/디렉토리 조작을 위한 메서드를 제공합니다. |
| `java.nio.file.Path` (NIO) |	파일 및 디렉토리 경로를 다루는 더 유연한 API를 제공한다. |
| `java.nio.file.Files` (NIO) |	파일 및 디렉토리 조작을 위한 다양한 메서드를 제공한다. |
| `java.io.BufferedReader` |	문자 파일을 효율적으로 읽기 위한 버퍼 기반 Reader |
| `java.io.BufferedWriter` |	문자 파일을 효율적으로 쓰기 위한 버퍼 기반 Writer |
| `java.io.FileReader` |	문자 파일을 읽기 위한 Reader |
| `java.io.FileWriter` |	문자 파일을 쓰기 위한 Writer |
| `java.io.FileInputStream` |	바이너리 파일을 읽기 위한 InputStream |
| `java.io.FileOutputStream` |	바이너리 파일을 쓰기 위한 OutputStream |

#### HTTP I/O
| Class | Description |
| - | - |
| `java.net.HttpURLConnection` |	HTTP 요청을 보내고 응답을 받기 위한 클래스로, 웹 서버와 통신할 때 사용된다. |
| `java.net.URL` |	웹 리소스에 대한 URL을 나타내는 클래스로, HTTP 연결을 만들기 위해 사용된다. |

</br>

### ➲ 참고 자료
- https://www.marcobehler.com/guides/java-files
- https://www.geeksforgeeks.org/file-class-in-java/