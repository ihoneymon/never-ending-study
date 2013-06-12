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
* URL 일치 예제

```javascript
var parse_url=/^(?:([A-za-z]+):)?(\/{0,3})([0-9.\-A-Za-z]+)(?::(\d+))?(?:\/([^?#]*))?(?:\?([^#]*))?(?:#(.*))?$/;
var url = "http://www.ihoney.pe.kr:8080/goodparts?param#fragment";

// parse_url의 exec 메소드 호출


var result = parse_url.exec(url);
var names = ['url', 'scheme', 'slash', 'host', 'port', 'path', 'query', 'hash'];

var blanks = '            ';
for(var i = 0; i < names.length; i++) {
    console.log(names[i] + ':' + blanks.substring(names[i].length), result[i]);
}
```

> 실행결과
> url:          http://www.ihoney.pe.kr:8080/goodparts?param#fragment
> scheme:       http
> slash:        //
> host:         www.ihoney.pe.kr
> port:         8080
> path:         goodparts
> query:        param
> hash:         fragment

* parse_url 분해
<pre>
/^(?:([A-za-z]+):)?(\/{0,3})([0-9.\-A-Za-z]+)(?::(\d+))?(?:\/([^?#]*))?(?:\?([^#]*))?(?:#(.*))?$/;
</pre>

    
    * <pre>^</pre> 문자열의 시작
    * <pre>(?:([A-za-z]+):)?</pre> : 프로토콜 이름(http, ftp 등등) 일치하는 부분
        - (?: ...) : 캡처하지 않는 그룹            
        - 마지막 ? : 이 그룹이 선택적
            - 없거나 한번 반복된다 
        - (...) : 캡처하는 그룹
        - [...] : 문자 클래스
        - A-Za-z : 알파벳 대문자 26자와 소문자 26자 포함
            - '-' : A-Z까지 범위
        - '+' : 문자가 한 번 이상 일치한다는 것
        - ':'는 문자 그대로 그 위치에 ':'가 일치해야 한다.
    * <pre>(\/{0,3})</pre>
        - <pre>\/</pre> : '/'와 일치해야 한다.
            - 정규 표현식 리터럴의 끝으로 잘못 해석되지 않도록 \\(백슬러시)로 이스케이프 처리
        - <pre>{0,3}</pre> : \/(슬래시)가 0에서 3번 일치 중에 하나라는 것을 나타낸다.
    * <pre>([0-9.\-A-Za-z]+)</pre> : 호스트 이름과 일치하는 부분
        - 하나 이상의 숫자나 문자 그리고 '.'나 '-'로 구성
        - '\-' : '-' 하이픈
    * <pre>(?::(\d+))?</pre> : 옵션(마지막 ?)으로 올 수 있는 포트번호
        - '\d' : 숫자 문자(4번째 캡처 그룹)
    * <pre>(?:\/([^?#]*))?</pre> : '/'로 시작하는 옵션 그룹
        - <pre>[^?#]</pre> : '?'와 '#'을 제외한 모든 문자
        - '*' : 0번 이상 일치
        - ?와 #을 제외한 모든 문자 클래스에는 줄 마침 문자, 제어문자뿐만 아니라 일치해서는 안되는 문자가 끼어들 위험성이 있다.
    * <pre>(?:\?([^#]*))?</pre> : ?로 시작하는 옵션 그룹
        - '#'이 아닌 문자가 0번이상 나오는 6번째 캡처 그룹
    * <pre>(?:#(.*))?</pre> : #으로 시작하는 마지막 옵션 그룹
        - '.'는 라인 종료 문자를 제외한 어떤 문자하고도 일치
    * <pre>$</pre> : 문자열의 끝을 의미
        - $를 마지막에 붙임으로써 뒤로 어떤 문자도 없다는 것을 나타낸다.

* 정규 표현식은 길이가 짧고 간단할 때 최상이라고 할 수 있다.
    * 정규 표현식이 제대로 동작하는지 확신할 수 있고 필요한 경우 문제없이 수정가능
    * **단순함이 최상의 전략**

```javascript
var parse_number = /^-?\d+(?:\.\d*)?(?:e[+\-]?\d+)?$/i;

var test = function(num) {
  console.log(parse_number.test(num));
};

test('1');
test('number');
test('98.6');
```
* parse_number 분해
<pre>
/^-?\d+(?:\.\d*)?(?:e[+\-]?\d+)?$/i;
</pre>

    * <pre>/^ $/i</pre> : 텍스트 내의 모든 문자가 정규표현식에 대응해서 일치해야 한다는 뜻
        * 두 문자가 제외되면, 숫자가 포함된 문자열을 알려주는 정규 표현식이 됨
        * '^'만을 사용하면 숫자로 시작하는 문자열에 대응
        * '$'만을 사용하면 숫자로 끝나는 문자열에 대응
        * 'i' 문자가 일치하는지를 검사할 때 대소문자를 구분하지 않게 한다.
    * <pre>-?</pre> : 음수 기호가 옵션
    * <pre>\d+</pre> : d 는 [0-9]와 같은 의미, 뒤에 붙은 +는 하나 이상의 숫자와 일치
    * <pre>(?:\.\d*)?</pre> : 소수점과 그 뒤에 오는 ~개 이상의 숫자에 대응
    * <pre>(?:e[+\-]?\d+)?</pre> : 선택적인 옵션

### 02. 정규표현식 객체 생성
* 정규 표현식 플래스
    * g : global (여러번 일치함, 메소드에 따라 다름)
    * i : insensitive(대소문자 구분하지 않음)    
    * m : multiline(^과 $이 라인 끝 문자에 일치할 수 있음)
    
    ```javascript
    var my_regexp = /"(?:\\.|[^\\\"])*"/g;
    var my_regexp2 = new RegExp("\"(?:\\.|[^\\\\\\\"])*\"", 'g');
    ```
    
    * RegExp 생성자는 프로그래밍 시에는 알 수 없고 실행시에만 알 수 있는 자료를 가지고 정규 표현식을 생성해야할 때 유용
        - 뭔소리고!
        - RegExp 객체 속성
            - global
            - ignoreCase
            - lastIndex
            - multiline
            - source
        - 정규 표현식 리터럴로 만들어진 RegExp는 하나의 인스턴스를 공유

### 03. 구성요소
* 선택
    * "into".match(/in|int/) : 먼저 일치하는 것이 된다.
* 시퀀스
    * 먼저 일치하는 것이 적용 
* 정규표현식 요소
    * 문자, 괄홀로 묶인 그룹, 문자 클래스, 이스케이스 시퀀스 등
    * '/\\[]{}?+*|'같은 문자 제외
* 이스케이프
    * '\\d' : [0-9]와 같은 아라비아 숫자
        - '\\D' : [^0-9]
    * '\\s' : 공백문자 '\\S'
    * '\\w' : [0-9A-Z_a-z]
        - '\\W' : [^0-9A-Z_a-z]
    * '\\b' : 단어 경계를 나타내어 문자 기반으로 일치시키기 쉽게 하기 위해서 고안 
        - '\\w'에 해당하는 규칙이 적용되어 쓸모가 없음
    * '\\1' : 첫번째 그룹에 캡처된 텍스트 
* 그룹
    * 캡처 : 괄호로 묶인 정규 표현식
    * 비캡처 : '(?:..)' 일치하는지 여부를 확인, 캡처하지는 않음
    * 긍정형 룩어헤드 : '(?=)' : 일치하는 부분을 찾은 후에 텍스트를 구릅 시작지점으로 이동, 좋지 않음
    * 부정형 룩어헤드 : '(?!)' : 찾지 못했을 때 이동, 좋지 않음
* 클래스 : '[]'
    * 클래스 제공 편리함
        - 문자의 범위 지정
        - 부정형 클래스 : '[^ '지정된 문자 배제
* 클래스 내의 이스케이프
* 수량자
    * 하나만 사용하면 일치하는 부분을 최대한 많이 찾으려고 함
    * 수량자 뒤에 ?가 붙으면 일치하는 부분을 찾는 일이 나태해  지는 경향이 있어 적게 일치하는 부분을 찾으려고 한다?
        - ?를 붙이지 않는 방법을 찾아라!

### 참고
* [정규식 표현법](http://kio.zc.bz/Lecture/regexp.html)
* [알고 있어야 할 8가지 정규식 표현 from nettuts+](http://blog.outsider.ne.kr/360)