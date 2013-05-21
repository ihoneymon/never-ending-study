02장 - 자바스크립트의 좋은 문법들
====================================

> 자바스크립트의 좋은 점들good parts에 해당하는 문법

### 01 공백whitespace
* 공백은 문자를 구분하는 형태나 주석의 형태를 취할 수 있다(즉, 주석 역시 공백)
* 주석
    * 블록 주석 : /* */
    * 한줄 주석 : //
    * 주석을 달 때는 항상 코드에 대해서 정확히 설명
    ```javascript
    /*
        var rm_a a /a*/.match(5);
    */
    ```
    * 한줄 주석 권장
   
### 02 이름names
* 예약어 숙지 필요함
* 참고 사이트 : [JavaScript/Reserved Words](http://en.wikibooks.org/wiki/JavaScript/Reserved_Words)

### 03 숫자numbers
* 자바스크립트는 숫자형이 하나만 존재
* 64비트 부동 소수점 형식을 지닌다. 
    * ex : 1과 1.0은 같은 값
* 지수 부분 : e는 10의 제곱 , 100 === 1e2
* 1.79769313486231570e+308 보다 큰 값은 Infinity로 나타남
* 숫자는 메소드가 있음

### 04 문자열Strings
* 문자열은 작은 따옴표('')나 큰 따옴표("")로 묶어서 나타냄
* 따옴표 안에는 문자 0개 이상을 포함
* 유니코드가 16비트 문자셋이었을 때 개발했기에 자바스크립트 내의 모든 문자는 16비트 유니코드
* 자바스크립트에는 문자 타입char 타입이 없음
* 문자열에는 length 라는 속성이 있음
* 문자열은 변하지 않는다immutable
* 문자열은 메소드가 있음

### 05 문장statements
* 링커linker가 없기 때문에 자바스크립트는 모든 문장을 공통적인 전역 이름 공간namespace에 한데 몰아 넣는다.
* 거짓false에 해당하는 값
    * false
    * null
    * undefined
    * 빈 문자열 ''
    * 숫자 0
    * NaN
    
### 06 표현식expression

### 07 리터럴literals
> 객체 리터럴은 새로운 객체를 생성할 때 편리한 표기법

### 08 함수functions
* 함수 리터럴은 함수값을 정의
* 함수 리터럴은 이름을 가질 수 있는데 이 이름은 자신읠 재귀적으로 호출할 때 사용할 수 있다.
```javascript
function(paramA, paramB) {
    return paramA + paramB;
}
```

