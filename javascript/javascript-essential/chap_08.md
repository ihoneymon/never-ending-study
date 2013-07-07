08장 - 메소드
====================================

* 메소드method
	* 52p, 함수를 객체의 속성에 저장하는 경우

* 배열
	* array.concat(item...)
		- 자신의 복사본에 인수로 넘어온 값들을 추가로 새로운 배열을 반환
		- 문자열인 경우 : 배열을 분해하여 배열에 추가
		- array.push(item..) 참조
	* array.join(구분자)
		- 배열을 문자열로 만든다.
		- 배열의 요소를 각각 문자열로 만들고 이 문자열 사이에 구분자를 붙여서 하나로 합친다.
	* array.pop()
		- pop과 push 메소드는 배열을 스택처럼 동작하게 한다.
		- 배열에서 마지막 요소를 제거하고 제거한 요소를 반환
		- 빈 배열일 경우 undefined를 반환
	* array.push(item...)
		- 인수로 넘어온 항목들을 배열의 끝에 추가
		- concat과 다르게 배열 자체를 수정하여 넘어온 인수 전체를 배열에 추가
	* arrray.reverse()
		- 배열 요소의 순서를 반대로 변경
		- 반환값은 배열 
	* array.shift()
		- 첫 번째 요소를 제거하고 제거한 요소를 반환
		- 빈 배열일 경우 undefined 를 반환
		- pop보다 많이 느림
	* array.unshift(item...)
	* array.slice(start, end)
		- 배열의 특정 부분에 대한 복사본을 만든다.
		- end에 해당하는 첨자를 가진 요소 전까지 복사
		- end 기본값은 배열의 length
		- .splice와 혼동 금지
		- 문자열의 .slice)()와도 구분
	* array.sort(비교 함수)
		- 배열의 내용을 적절하게 정렬
		- 숫자 배열을 제대로 정렬하지 못함
		- 안정적이지 않아 사용하는 것을 권장하지 않음
	* array.splice(start, deleteCount, item..)
* 함수
	* function.apply(thisArg, argArray)
		- this에 연결될 객체(thisArg)와 (옵션) 인수 배열을 넘기면서 함수를 호출
		- apply 호출 패턴
* 숫자
	* number.toExponential(fractionDigits)
	* number.toFixed(fractionDigits)
	* number.toPrecision(precision)
	* number.toString(radix)
* 객체
	* object.hasOwnProperty(name)
* 정규표현식 객체
	* regexp.exec(string)
	* regexp.test(string)
* 문자열
	* string.charAt(position)
	* string.charCodeAt(position)
	* string.concast(string...)
	* string.indexOf(searchString, position)
	* string.lastIndexOf(searchString, position)
	* string.localeCompare(that)
	* string.match(regexp)
	* string.replace(searchValue, replaceValue)
	* string.search(regexp)
	* string.slice(start, end)
	* string.split(separator, limitCount);
	* string.substring(start, end)
	* string.toLocaleLowerCase()
	* string.toLocaleUpperCase()
	* string.toLowerCase()
	* string.toUpperCase()
	* String.fromCharCode(char...)