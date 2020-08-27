---
title:  "예시와 함께 하는 Dart 가이드"
excerpt: "Official Dart language samples로 Dart 빠르게 훑기"


categories:
-  Flutter
tags:
-  Dart
last_modified_at: 2020-08-28TO20:30:00+09:00
---
- [빠르게 훑자 Dart](#빠르게-훑자-dart)
  - [Hello World](#hello-world)
  - [변수](#변수)
  - [흐름제어문](#흐름제어문)
  - [함수](#함수)
  - [주석](#주석)
  - [패키지 사용](#패키지-사용)
  - [클래스](#클래스)
  - [상속](#상속)
  - [믹스인](#믹스인)
  - [인터페이스와 추상 클래스](#인터페이스와-추상-클래스)
  - [Async](#async)
  - [예외처리](#예외처리)

## 빠르게 훑자 Dart

공식문서 + 영어로 공부하는 것이 제일 빨리 실력이 느는 것 같다

언제나 공식문서부터 읽기! [Dart language Samples](https://dart.dev/samples)

Dart는 Google에서 만들었다 보니까 문서가 아주 잘되어 있다.

Language Tour, Libraries Tour도 따로 제공한다.

내 나름대로 정리해보았다.
아직 실력이 부족해 오역이 있을 수 있다.

### Hello World

```Dart
// Hello World
void main() {
	print('Hello, World!');
}
```

### 변수

```Dart
// 변수
// Dart는 type-safe합니다.
// 하지만 타입을 명시하지 않아도 됩니다.
var name = 'Voyager I';
var year = 1977;
var antennaDiameter = 3.7;
var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];
var image = {
  'tags': ['saturn'],
  'url': '//path/to/saturn.jpg'
};
```

### 흐름제어문

```Dart
// 흐름 제어 문
// if-else 문
if (year >= 2001) {
	print('21st century');
} else if (year >= 1901) {
	print('20th century');
}
// for-each 문
for (var object in flybyObjects) {
	print(object);
}
// for 문
for (int month = 1; month <= 12; month++){
	print(month);
}
// while 문
while (year < 2016) {
	year += 1;
}
// 더 알아보기 : break, continue, switch and case, assert
```

### 함수

```Dart
// 함수
// 권장 : 파라미터와 리턴값 타입을 명시하세요
int fibonacci(int n) {
	if (n == 0 || n == 1) return n;
	return fibonacci(n - 1) + fibonacci(n - 2);
}
var result = fibonacci(20);
// 화살표 함수
// 한 줄로 선언하는 함수입니다.
// 함수 인수로 익명 함수를 넘겨줄 때 유용합니다.
flybyObjects.where((name) => name.contains('turn')).forEach(print);
// 또한, 보다시피 함수를 인수로 사용할 수 있다.
// 최상위 레벨 함수인 print()를 forEach() 함수의 인자로 넘겨줬다.
// 더 알아보기 : optional params, default param vals, and lexical scope
```

### 주석

```Dart
// 주석
// Dart는 //를 사용한다
/// 문서화 주석은 ///를 사용한다
/// IDE등의 도구들이 doc comments를 특별하게 인식한다.
/* 이러한 형태의 주석도 지원한다. */

```

### 패키지 사용

```Dart
// 패키지 사용
import 'dart:math'; //코어 라이브러리
import 'package:test/test.dart'; //외부 패키지에서의 라이브러리
import 'path/to/my_other_file.dart'; //파일
// 더 알아보기 : library prefixes, show and hide, and lazy loading through the deferred keyword
```

### 클래스

```Dart
// 클래스
// 예시는 3개의 속성, 2개의 생성자, 1개의 메소드를 갖는다. (+ 게터 메소드)
class Spacecraft {
	String name;
	DateTime launchDate;

	// 생성자
	Spacecraft(this.name, this.launchDate) {
		// ...
	}
	
	// 이름있는 생성자
	Spacecraft.unlaunched(String name) : this(name, null);
	
	int get launchYear =>
		launchDate?.year; //read-only non-final property

	// 메소드
	void describe() {
		print('Spacecraft: $name');
		if (launchDate != null) {
			int years =
				DateTime.now().difference(launchDate).inDays ~/
					365;
			print('Launched: $launchYear ($years years ago)';
		} else {
			print('Unlaunched');
		}
	}
}
// 위의 예시를 다음과 같이 사용한다
var voyager = Spacecraft('Voyager I', DateTime(1977, 9, 5));
voyager.describe();
var voyager3 = Spacecraft.unlaunched('Voyager III');
voyager3.describe();
// 더 알아보기 : initializer lists, optional new and const,
// redirecting constructors, factory constructors,
// getters, setters, and much more
```

### 상속

```Dart
// 상속
// 단일 상속만을 갖는다
class Orbiter extends Spacecraft {
	double altitude;
	Orbiter(String name, DateTime launchDate, this.altitude)
		: super(name, launchDate);
}
// 더 알아보기 : extending classes, optional @override annotation, and more
```

### 믹스인

```Dart
// 믹스인
// 믹스인이란 다중 클래스 상하관계에서 코드 재사용을 하는 방법이다
// 다음 예시가 믹스인으로 사용할 수 있는 클래스의 예시이다
class Piloted {
	int astronauts = 1;
	void describeCrew() {
		print('Number of astronauts: $astronauts');
	}
}
// 위 클래스를 다음과 같이 믹스인 한다 (with)
class PilotedCraft extends Spacecraft with Piloted {
	// ...
}
```

### 인터페이스와 추상 클래스

```Dart
// 인터페이스와 추상 클래스
// Dart는 interface 키워드가 없다.
// 모든 클래스들은 암묵적으로 인터페이스를 정의하므로, 어떠한 클래스에서도 implement 할 수 있다.
class MockSpaceship implements Spacecraft {
	// ...
}
// 추상 클래스
abstract class Describable {
	void describe(); // 추상 메소드(빈 바디)

	void describeWithEmphasis() {
		print('========');
		describe();
		print('========');
	}
}
```

### Async

```Dart
// Async
// 콜백 지옥을 피하기 위함
// 그리고 코드를 좀 더 가독성있게 만들기 위함
// by using async and await
const oneSecond = Duration(seconds: 1);
// ...
Future<void> printWithDelay(String message) async {
	await Future.delayed(oneSecond);
	print(message);
}
// async and await을 사용하지 않은, 위와 동일한 기능을 하는 예시
Future<void> printWithDelay(String message) {
	return Future.delayed(oneSecond).them((_) {
		print(message);
	});
}
// Async의 가독성을 보여주는 더 확실한 예시
Future<void> createDescriptions(Iterable<String> objects) async {
  for (var object in objects) {
    try {
      var file = File('$object.txt');
      if (await file.exists()) {
        var modified = await file.lastModified();
        print(
            'File for $object already exists. It was modified on $modified.');
        continue;
      }
      await file.create();
      await file.writeAsString('Start describing $object in this file.');
    } on IOException catch (e) {
      print('Cannot create description for $object: $e');
    }
  }
}
// 더 알아보기 : async funcs, Future, Stream, and the asynchronous loop (await for).
```

### 예외처리

```Dart
// 예외처리
// 예외를 발생시키려면 throw
if (astrounauts == 0) {
	throw StateError('No astronauts.');
}
// 예외처리에는 try, on, catch를 사용
try {
	for (var object in flybyObjects) {
		var description = await File('$object.txt').readAsString();
		print(description);
	}
} on IOException catch (e) {
	print('Could not describe object" $e');
} finally {
	flybyObjects.clear();
}
// try는 동기 그리고 비동기 함수 둘다 사용 가능하다. 
// 더 알아보기 : stack traces, rethrow, and the diff between err and exception
```
