07장 - 정규 표현식
====================================

* 다른 언어에서 차용한 부분
    * 구문 : 자바
        - [Javascript Syntax](http://en.wikipedia.org/wiki/JavaScript_syntax)
    * 함수 : Scheme
        - [Scheme](http://en.wikipedia.org/wiki/Scheme_(programming_language))
    * 프로토타입에 의한 상속 : Self
        - [Self](http://selflanguage.org/index.html)
    * 정규표현식 : Perl
        - [Perl](http://www.perl.org/)
        - [perlretut](http://perldoc.perl.org/perlretut.html)
        - [Javascript regex compared to Perl regex](http://stackoverflow.com/questions/3949991/javascript-regex-compared-to-perl-regex)

* 정규 표현식은 간단한 언어구문의 특화된 형태
    > 문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용
* 정규 표현식 사용 메소드
    * regexp.exec
    
    ```javascript
    var myRe=/d(b+)(d)/ig;
    var myArray = myRe.exec("cdbBdbsbz");
    ```
    
    * regexp.test
    
    ```javascript
    var myRe=/d(b+)(d)/ig;
    var checked = myRe.test("cdbBdbsbz");
    console.log("checked = " + checked);
    ```
    
    * string.match
    
    ```javascript
    // 부합되는 것들을 모두 찾아낸다.
    var str = "ABCdEFgHiJKL";
    var myResult = str.match(/[a-z]/g );
    for(var cnt = 0 ; cnt < myResult.length; cnt++){
        console.log(cnt +":" + myResult[cnt]);
    }
    
    console.log("비교");
    
    // 해당하는 것 하나만 찾아낸다.
    var str = "ABCdEFgHiJKL";
    var myResult = /[a-z]/g.exec(str);
    for(var cnt = 0 ; cnt < myResult.length; cnt++){
        console.log(cnt +":" + myResult[cnt]);
    }
    ```
    
    * string.replace
    * string.search
    * spring.split
    
    ```javascript
    var str = "ABCdEFgHiJKL";
    var myResult = str.split(/[a-z]/g , 3);
    for(var cnt = 0 ; cnt < myResult.length; cnt++){
        console.log(cnt +":" + myResult[cnt]);
    }
    ```
    
    * 8장에서 설명!
    
* **같은 문자열에 대해 반복해서 연산을 수행할 때 주목할만한 성능상의 이점이 있다.**
    * 텍스트 에디터 같은 툴이나 프로그래밍 언어에서 특정 패턴을 찾을 수 있게 실질적인 패턴 매칭 기능을 추가
* 정규 표현식 구문
    * 약간의 재해석?
        - 얼마나?
    * Perl의 확장 구문 채택
    * 벨 연구소에서 비롯된 체계 유지 
* 정규 표현식의 어려움
    * 특정 위치의 문자가 연산자로 해석되고 또 조금은 다른 위치에 있는 문자를 리터럴로 간주하기 때문에 이를 작성하는 것은 매우 복잡하고 어렵다.
        - 맞다!
    * 더 안 좋은 것은 이러한 어려움이 정규 표현식을 읽기 어렵게 만들고 수정하기 위험하게 만든다.
    * **정규 표현식을 바르게 읽기 위해서는 복잡한 정규 표현식 체계 전체를 제대로 이해해야 한다.**
    * 주석이나 공백을 허용하지 않아 다소 읽기 어렵다.
        - 빈틉없이 하나로 연결되어 있기 때문에 해석이 어렵다.
        - 탐색이나 검증을 위해 보안 애플리케이션에서 사용될 때 염려되는 부분
            - 제대로 동작하고 있는지 어떻게 확신할텐가?

### 01. 예제


### 02. 정규표현식 객체 생성

### 03. 구성요소

### 참고
* [정규식 표현법](http://kio.zc.bz/Lecture/regexp.html)
