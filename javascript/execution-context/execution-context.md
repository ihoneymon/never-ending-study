Javascript Execution Context
================================

****
### 실행코드 종류
* [Chapter 1. Execution Contexts](http://frends.kr/post/chapter-1-execution-contexts/)
> 각각의 코드는 각각의 실행 컨텍스트에 의해 평가
* 전역 코드Global code
* 함수 코드Function Code
* eval 코드eval code

#### ECMAScript
* 1개의 전역 컨텍스트
    * 한개 또는 그 이상의 **함수 실행 컨텍스트**
        - 함수 실행시 함수 실행 컨텍스트에 들어가고 '함수 코드'로 평가
    * 한개 또는 그 이상의 **eval 실행 컨텍스트**
        - eval을 실행시 eval 실행 컨텍스트에 들어가고 'eval 코드'로 평가

### Exectuion Context란 무엇인가?
최초에 스크립트 파일을 읽으면서 생성실행Creation Execution을 마치면 > 각각의 코드는 각각의 생성 컨텍스트에 기록이 되고, 마지막에 실행에 들어가게 되면 생성 컨텍스트가 실행 컨텍스트에 복제되고 초기화작업이 진행된다. 

### Scope
* Global context
* Execution context

### Execution Context Stack이란 무엇인가?

### Execution Context Stack 핵심 5가지

### Execution Context Workflow

### Sample Javascript Execution Context

### Hoising
