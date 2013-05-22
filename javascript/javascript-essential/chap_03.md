03장 - 객체
====================================

* 자바스크립트 데이터 타입
	* 숫자
	* 문자열
	* 불리언(true/false)
	* null
	* undefined
* 이외에는 모두 객체
	* 숫자, 문자열과 불리언은 메소드가 있기 때문에 유사 객체
	* 값이 정해지면 변경되지 않는다 immutable, 불변성
* 객체
	* 이름과 값이 있는 속성을 포함하는 컨테이너? 컨테이너?
	* 속성의 이름은 문자열이면 모두 가능 - 빈 문자열도 포함
	* 속성의 값은 undefined를 제외한 자바스크립트의 모든 값이 사용
	* 클래스가 필요 없음class-free
	* 새로운 속성의 이름이나 값에 제약사항이 없음
	* 데이터를 한 곳에 모으고 구조화 하는데 유용
	* 다른 객체를 포함 가능

### 01 객체 리터럴
```javascript
var empty_object = { };

 var stooge = {
 	"first-name" : "Jerome",
	"last-name" : "Howard"
 };
```
* 속성property의 이름은 어떤 문자열이라도 가능
	* 빈 문자열도 포함
* 속성의 이름은 예약어가 아닌 경우 따옴표 생략 가능
* 쉼표(')는 "속성-값" 구분하는데 사용

```javascript
var flight = {
	airline : "Oceanic",
	number : 815,
	departure : {
		IATA : "SYD",
		time : "2004-09-22 14:55",
		city : "Sydney"
	},
	arrival : { 
		IATA : "LAX",
		time : "2004-09-23 10:42",
		city : "Los Angeles"
	}
};
```'

### 02 속성값 읽기
* 속성의 값 읽는 방법
	* 대괄호([])를 이용
	* 마침표 표기법
	```javascript
	stooge["first-name"] // "Jerome"
	flight.departure.IATA	// "SYD"
	```
* 객체에 존재하지 않는 속성을 읽으려고 하면 undefined를 반환
```javascript
stooge["middle-name"]		//undefined
flight.status				// undefined
stooge["FIRST-NAME"]		// undefined : 대소문자 구분
```
* || 연산자를 사용하여 기본값 지정 가능
```javascript
var middle = stooge["middle-name"] || "{none}";
var status = flight.status || "unknown";
```
* 존재하지 않는 속성, 즉 undefined의 속성을 참조하려 할 때 TypeError 예외가 발생
	* 방지방법 : && 연산자 사용
	```javascript
	flight.equipemt							// undefined
	flight.equipemt.model						// throw "TypeError"
	flight.equipemt && flight.equipemt.model		// undefined
	```

### 03 속성값의 갱신
* 객체의 값은 할당에 의해 갱신
* 객체에 속성이 존재하면 해당 속성의 값만 변경됨 
```javascript
stooge['first-name'] = 'Jerome';
```
* 객체에 속성이 존재하지 않는 경우 속성이 객체에 추가됨
```javascript
stooge['middle-name'] = 'Lester';
stooge.nickname = 'Curly';
flight.equipment = {
	model : 'Boeing 777'
}
```

### 04 참조
* 객체는 참조 방식으로 전달
* 복사되지 않음

### 05 프로토타입prototype
* **자바 스크립트에서 제일 어려운 부분**이라고 생각함
* 모든 객체는 속성을 상속하는 프로토타입 객체에 연결됨
	* 객체 리터럴로 생성되는 모든 객체는 자바스크립트의 표준 객체인 Object의 속성인 prototype 객체에 연뎔됨
* 객체 생성시 해당 객체의 프로토타입이 될 객체 선택 가능
* 예제 : Object 객체에 create 메소드 추가
	* create : 넘겨받은 객체를 프로토타입으로 하는 새로운 객체를 생성
	```javascript
	if (typeof Object.create !== 'function') {
		Object.create = function (o) {
			var F = function () {};
			F.prototype = o;
			return new F();
		};
	}
	var another_sooge = Object.create(stooge);
	```
* 프로토타입을 연결해도 객체에는 영향을 끼치지 않음
* 프로토타입 연결은 오로지 객체의 속성을 읽을 때만 사용 
* 프로토타입 관계는 동적(**프로토타입 체인**)
	* 프로토타입에 새로운 속성 추가시 - 해당 프로토타입을 근간으로 하는 객체들에도 즉각적으로 속성이 반영됨 

### 06 리플렉션reflection
* 객체에 어떤 속성들이 있는지는 특정 속성을 접근해서 반환값 확인
	* typeof 연산자 사용
	```javascript
	typeof flight.number		// 'number'
	typeof flight.status		// 'string'
	typeof flight.arrival	// 'object'
	typeof flight.manifest	// 'undefined'
	```
* 프로토타입 체인 상의 속성을 반환하는 경우도 있음
```javascript
typeof flight.toString		// 'function'
typeof flight.constructor	// 'function'
```
* 리플렉션 사용시 원하지 않는 속성 배제방법
	* 함수값을 배제하는 방법
	* 객체에 특정 속성이 있는지를 확인하여 true/false 값을 반환하는 hasOwnProperty 메소드 사용
		- hasOwnProperty는 프로토타입 체인을 바라보지 않음
		```javascript
		flight.hasOwnProperty('number')				// true
		flight.hasOwnProperty('constructor')			// false
		```

### 07 열거enumeration
* for in 구문을 이용하면 객체에 있는 모든 속성이름을 열거할 수 있음
	* 이름순으로 나온다는 보장이 없음
```javascript
var nam;
for (name in another_stooge) {
	if (typeof another_sooge[name] !== 'function') {
		document.writeln(name + ': ' + another_stooge[name]);
	}
}
```
* 특정순으로 속성 이름들이 나열되기를 원한다면 특정배열로 지정하고 이 배열을 이용하여 객체의 속성을 열거
	* 객체의 속성이름을 알고 있어야 하는군.
	* 프로토타입 체인에 있는 속성 노출 위험 감소
```javascript
var i;
var properties = {
	'first-name',
	'middle-name',
	'last-name',
	'profession'
};

for (i = 0; i < properties.length; i += 1) {
	document.writeln(properties[i] + ': ' + another_stooge[properties[i]]);
}
```


### 08 삭제
* **delete** 연산자를 이용하여 객체의 속성 삭제 가능
	* 객체에 해당 속성이 있을 경우에만 삭제
	* 프로토타입의 속성인 경우에는?
	* 프로토타입을 쓰고 있는 객체들에는 어떤 영향을 끼칠까?
	```javascript
	another_stooge.nickname		// 'Moe'
	
	//another_stooge 에서 nickname을 제거하면
	//프로토타입에 있는 nickname이 나타남
	
	delete another_stooge.nickname;
	
	another_stooge.nickname 		// '???'
	```
	
### 09 최소한의 전역변수 사용 
* 자바스크립트는 전역변수 사용이 쉽다.
* 프로그램의 유연성은 약화시키므로 가능하면 사용하지 않는 것이 좋다.
* 전역변수 사용의 최소화
	* 전역변수를 하나 만든다.
	```javascript
	var MYAPP = {};
	```
	이제 이 변수를 다른 전역분스를 위한 컨테이너로 사용
	```javascript
	MYAPP.stooge = {
		'first-name' : 'Joe',
		'last-name' : 'Howard'
	};
	
	MYAPP.flight = {
		airline : "Oceanic",
		number : 815,
		departure : {
			IATA : "SYD",
			time : "2004-09-22 14:55",
			city : "Sydney"
		},
		arrival : { 
			IATA : "LAX",
			time : "2004-09-23 10:42",
			city : "Los Angeles"
		}
	}
	```
	> 이러한 방법으로 애플리케이션에 필요한 전역변수를 이름하나로 관리하면 다른 애플리케이션이나 위젯 또는 라이브러리들과 연동할 때 문제점을 최소화할 수 있다. MYAPP.sooge가 명시적으로 전역변수라는 것을 나타내기 때문에 프로그램의 가독성도 높인다.