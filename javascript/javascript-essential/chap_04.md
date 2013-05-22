04장 - 함수
====================================

### 01 함수 객체

### 02 함수 리터럴

### 03 호출

### 04 인수 배열argument

### 05 반환

### 06 예외

### 07 기본 타입에 기능 추가

### 08 재귀적 호출

### 09 유효범위Scope

### 10 클로저Closure

### 11 롤백

### 12 모듈

### 13 연속호출cascade

### 14 커링curry

### 메모이제이션memoization

### 기타
* prototype - Function.prototype에 연결되어 있다. 
* 함수 생성
	* var a = function() {};
* 함수 호출
	* apply()
* return
	* 반환값이 없을 경우 undefined
* callback
	* 비동기식 처리시 함수를 매개변수로 전달하여 응답이 왔을 때 처리하도록
* 연속호출
	* this를 리턴하면 연속적으로 메소드 호출가능
* Closure
	* 외부함수보다 내부함수가 오래 살아있을 때
	
	```javascript
		var myFunction = function() {
			var testValue = 0;
			return {
				setValue : function() {
					testValue = newValue;
				}
			};
		}();
	```
	
	* 모듈을 만들 수 있다.
	* 참조형이 아니라서 필요할 때
* Curry, memoization
	* Closure를 이용해 본래의 함수와 전달받은 인수를 유지하여 새로운 함수를 리턴하는 curry와 이전의 결과값을 유지하여 사용하는 memoization을 구현할 수 있다.
	