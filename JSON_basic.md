JSON (JavaScript Object Notation) 개념
=====
  
**특징**
- 자바스크립트를 확장하여 만들어졌음
- 자바스크립트 객체 표기법을 따름
- 사람과 기계가 모두 읽기 편하도록 고안됨
- 프로그래밍 언어와 운영체제에 독립적임
  
  
**XML(EXtensible Markup Language)  
: 문자 기반의 마크업 언어(text-based markup language) 과 비교**
  
공통점
- 둘 다 데이터를 저장하고 전달하기 위해 고안되었음
- 기계뿐만 아니라 사람도 쉽게 읽을 수 있음
- 계층적인 데이터 구조를 가짐
-  XMLHttpRequest 객체를 이용하여 서버로부터 데이터를 전송받을 수 있음
  
차이점 (JSON은)
- 종료 태그를 사용하지 않음
- XML구문보다 짧음
- XML 데이터보다 더 빨리 읽고 쓸 수 있음
- 배열을 사용할 수 있음
  
JSON 구조
=====
자바스크립트 객체 표기법에 따른 구조로 구성됨

- 데이터가 이름과 값의 쌍으로 이루어짐
- 데이터가 쉼표(,)로 나열됨
- 객체(object) - 중괄호
- 배열(array) - 대괄호
  
JSON 데이터
-----  
이름과 값의 쌍으로 구성됨  
`"name" : "Yewon"`  
  
JSON 값
-----  
타입
- 숫자(number)
  - 정수(integer) : 부호를 가지는, 소수 부분이 없는 수
  - 실수(fraction) : 소수 부분을 가지는 수
  - 지수(exponent) : 매우 큰 수나 매우 작은 수를 e 표기법을 사용하여 표현
- 문자열(string) : 일련의 연속된 문자(유니코드 문자)의 집합  
  큰따옴표만 사용해야 함  
  - 이스케이프 시퀀스(escape sequence)  
  b, f, n, r, t, ", /, \, uHHHH
- boolean
  true, false
- 객체(object) : 데이터 이름과 값의 한 쌍으로 구성된 프로퍼티의 정렬되지 않은 집합
  - 프로퍼티, 쉼표
  - 객체 내의 데이터로 또다른 객체 이용 가능 => 계층구조 형성
- 배열(array)
  - 인덱스는 0부터 시작
  - 여러 타입의 배열 요소를 가질 수 있다
- NULL : 아무런 값도 가지고 있지 않은 빈 값을 의미, 소문자
  - undefined와 null : '값' 자체가 없다는 의미의 undefined 값은 초기화되지 않은 변수나 존재하지 않는 값에 접근할 때 반환됨
  
JSON 객체
----- 
```javascript
{
  "name": "Yewon",
  "age": 19,
  "weight": 52
}
```
  
JSON 배열
-----
```javascript
"person": [
  {"name": "a", "personality": "kind"},
  {"name": "b", "personality": "sensitive"},
  {"name": "c", "personality": "gloomy"}
]
```
