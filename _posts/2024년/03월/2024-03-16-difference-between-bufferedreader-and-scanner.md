---
title: "[Java] BufferedReader VS Scanner"
excerpt: "Java에서 BufferedReader와 Scanner의 차이는 BufferedReader와 Scanner 각각의 예시는?"
date: 2024-03-16
last_modified_at: 2024-03-16
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 `BufferedReader`와 `Scanner`의 차이는?

## 2. Answer

### A. 사용 목적의 차이

* `BufferedReader`: 주로 파일이나 소켓과 같은 입력 스트림에서 텍스트를 읽기 위해 사용된다. 일반적으로 대량의 데이터를 읽을 때 사용하며, 줄 단위로 데이터를 읽는 것이 일반적이다.

* `Scanner`: 사용자 입력과 같이 작은 단위의 데이터를 파싱하고 읽기에 적합하다. `Scanner`는 정규 표현식을 사용하여 입력을 토큰으로 분할하고 다양한 타입으로 변환하는 메서드를 제공한다.

### B. 성능 차이

* `BufferedReader`: 문자 입력 스트림으로부터 텍스트를 버퍼링함으로써, 매번 읽을 때마다 입출력(`I/O`)을 줄여 성능을 향상시킨다. 큰 파일을 읽을 때 `BufferedReader`를 사용하는 것이 좋다.

* `Scanner`: 정규 표현식을 사용하여 입력을 파싱하는 추가 작업 때문에 `BufferedReader`보다 느릴 수 있다. 그러나 `Scanner`는 다양한 타입의 입력을 쉽게 처리할 수 있는 유연성을 제공한다.

### C. 사용 편의성

* `BufferedReader`: 예외 처리를 필요로 하며, 주로 `readLine()` 메서드를 통해 문자열을 읽는다.

* `Scanner`: 다양한 메서드 `nextInt()`, `nextDouble()`, `nextLine()` 등을 통해 다른 타입의 입력을 쉽게 처리할 수 있으며 사용이 상대적으로 간단하다.

## 3. Detail

### A. Scanner 예시 - 사용자 입력 읽기

```java
Scanner scanner = new Scanner(System.in);
System.out.print("Enter your name: ");
String name = scanner.nextLine();
System.out.print("Enter your age: ");
int age = scanner.nextInt();
System.out.println("Hello, " + name + ". You are " + age + " years old.");
scanner.close();
```

### B. Scanner 예시 - 파일에서 토큰화된 데이터 읽기

```java
try (Scanner scanner = new Scanner(new File("data.txt"))) {
  while (scanner.hasNext()) {
    String token = scanner.next();
    System.out.println(token);
  }
} catch (FileNotFoundException e) {
  e.printStackTrace();
}
```

### C. Scanner 예시 - 정규 표현식을 사용한 텍스트 파싱

```java
String input = "1 fish 2 fish red fish blue fish";
Scanner s = new Scanner(input).useDelimiter("\\s*fish\\s*");
System.out.println(s.nextInt());  // 1
System.out.println(s.nextInt());  // 2
s.close();
```

### D. BufferedReader 예시 - 파일에서 텍스트 읽기

```java
try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
  String line;
  while ((line = reader.readLine()) != null) {
    System.out.println(line);
  }
} catch (IOException e) {
  e.printStackTrace();
}
```

### E. BufferedReader 예시 - 소켓에서 데이터 읽기

```java
try (Socket socket = new Socket("example.com", 80);
  BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()))) {
    String line;
    while ((line = reader.readLine()) != null) {
      system.out.println(line);
    }
} catch (IOException e) {
  e.printStackTrace();
}
```

### F. Scanner의 다양한 메서드

`next()`: 다음 토큰을 문자열로 반환한다. 

* `String s = scanner.next();`

`nextLine()`: 현재 위치에서 다음 줄 끝까지 문자열을 읽고 반환한다. 

* `String line = scanner.nextLine();`

`nextInt()`, `nextDouble()`, `nextFloat()`: 각각 다음 토큰을 int, double, float 등의 지정된 타입으로 변환하여 반환한다. 

* `int i = scanner.nextInt();`

`hasNext()`, `hasNextLine()`, `hasNextInt()`, `hasNextDouble()`: 각각 다음에 읽을 토큰, 줄, 정수, 실수 등이 있는지를 boolean 값으로 반환한다. 

* `boolean hasInt = scanner.hasNextInt();`

`useDelimiter(String pattern)`: `Scanner` 객체가 토큰을 분리할 때 사용할 구분자를 지정한다. 기본값은 공백이다.

* `scanner.useDelimiter(",");`

`close()`: `Scanner` 객체를 닫는다. `Scanner` 객체를 더 이상 사용하지 않을 때 리소스를 해제하기 위해 호출한다.

* `scanner.close();`

`findInLine(String pattern)`: 현재 줄에서 지정된 패턴과 일치하는 내용을 찾아 반환한다.

* `String found = scanner.findInLine("\\d+"); // 숫자 찾기`

`nextBoolean()`: 다음 토큰을 boolean 값으로 읽는다. `true` 또는 `false` 문자열에 대해 대소문자를 구분하지 않는다.

* `boolean b = scanner.nextBoolean();`

`skip(String pattern)`: 입력에서 지정된 패턴과 일치하는 내용을 건너뛴다.

* `scanner.skip("##+");  // '#' 기호가 2개 이상 있는 부분을 건너뜀`


## 4. Reference

None