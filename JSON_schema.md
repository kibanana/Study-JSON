JSON 스키마(schema)
=====
JSON 데이터를 전송받는 측에서 전송받은 데이터가 적법한 형식의 데이터인지 확인할 수 있는 방법.  
적법한 JSON 데이터의 형식을 기술한 문서임  

### JSON 스키마 검증(validation)
- 데이터의 타입이 정확한가?
- 필수로 받아와야 하는 데이터가 포함되어 있는가?
- 데이터가 원하는 범위 안에 있는가?
  
### 검증 키워드(validation keywords)
  
| 검증 키워드 | 설명 |
|--- | --- |
| type | 유효한 데이터의 타입을 명시 |
| properties | 유효한 데이터 이름과 값의 쌍들을 명시 |
| required | 명시한 배열의 모든 요소를 프로퍼티로 가지고 있어야만 유효함 |
| minimum | 최솟값 이상의 숫자만 유효함 |
| maximum | 최댓값 이하의 숫자만 유효함 |
| multipleOf | 명시한 숫자의 배수만 |
| maxLength | 명시한 최대 길이 이하의 문자열만 유효함 |
| minLength | 명시한 최소 길이 이상의 문자열만 유효함 |
| pattern | 명시한 정규 표현식에 해당하는 문자열만  |
  
  
### 메타 데이터(metadata) 키워드
- title
- description
- default
  
  
id라는 식별자를 각각의 스키마에 고유하게 지정할 수 있다.  
각각은 공유 URL을 지정해 줍니다.  

```javascript
{
  "$schema": "http://json-schema.org/schema#",
  "id": "http://yourdomain.com/schemas/myschema.json",
  "title": "Yewon's schema",
  "description": "Yewon is me",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "age": {
      "type": "integer"
    },
    "school": {
      "type": "string"
    },
    "family": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "familyName": {
            "type": "string"
          },
          "age": {
            "type": "integer"
          }
        }
      }
    }
  }
}
```

검증
=====
  
숫자
-----
- 정수 `"type": "integer"`
- 숫자 `"type": "number"`
- 배수 `"type": "number", "multipleOf": 3`
- 범위
  - minimum
  - maximum
  - exclusiveMinimum
  - exclusiveMaximum
  
  exclusive~ 의 값으로는 boolean 값이 오는데,  
  true일 경우에는 초과, 미만  
  false일 경우에는 이상, 이하 이다.
  
  *해당 데이터가 1보다 크거나 같고(n>=1) 10보다는 작은(n<10) 정수 또는 실수인지를 검사하는 예제*
  ```javascript
  {
    "type": "number",
    "minimum": 1,
    "maximum": 10,
    "exclusiveMaximum": true
  }
  ```
  
문자열
-----
`"type": "string"`  
- 문자열 길이  
  : 0을 포함한 양수만 사용 가능
  - minLength
  - maxLength
- 정규 표현식 (regular expression)
  : 문자열에서 특정한 규칙을 가지는 문자열의 집합을 찾아내기 위한 검색 패턴
  
  | 패턴 문자 | 설명 |
  |--- | --- |
  | ^a | 단어의 맨 앞 패턴 검색 |
  | a$ | 단어의 맨 뒤 패턴 검색 |
  | a(b)c | 전체 패턴을 검색한 후에 괄호 안에 명시된 문자열을 저장 |
  | [a-z] | 대괄호([]) 안에 명시된 문자(범위)를 검색 |
  | [^a-z] | 대괄호([]) 안에 명시된 문자(범위) 이외의 문자를 검색 |
  | n+ | 앞의 문자가 1번 이상 나타날 경우를 검색함. {1, }과 같음 |
  | n* | 앞의 문자가 0번 이상 나타날 경우를 검색함. {0, }와 같음 |
  | n? | 앞의 문자가 0번 또는 1번만 나타날 경우를 검색함. {0,1}과 같음  |
  | {n} | 앞의 문자가 정확히 n번 나타날 경우를 검색 |
  | {m,n} | 앞의 문자가 최소 m번이상 최대 n번이하로 나타날 경우를 검색  |
  
객체
-----
- `"type": "object"`
- 프로퍼티(값과 쌍으로 구성) (↑ 참고)
- 필수 프로퍼티
  ```javascript
  {
      "type": "object",
      "properties": {
          "name": {"type": "string"},
          "family": {"type": "string"},
          "age": {"type": "integer"},
          "weight": {"type": "number"}
      },
      "required": ["name", "family"]
  }
  ```
- 프로퍼티의 개수
  ```javascript
  {
    "type": "object",
    "minProperties": 1,
    "maxProperties": 2
  }
  ```
  
배열
-----
```javascript
{
    "type": "array",
    "items": {
        "type": "integer"
    }
}
```

```javascript
{
   "type": "array",
    "items": [
        {
            "type": "string",
            "maxLength": 5
        },
        {
            "type": "string"
        },
        {
            "type": "string"
        }
    ],
    "additionalItems": false
}
```
추가로 다른 배열 요소를 가지는 배열은 검증을 통과할 수 없다
  
- 배열 길이
  ```javascript
  {
    "type": "array",
    "minItems": 3,
    "maxItems": 10
  }
  ```
  
- 중복값
  ```javascript
  {
    "type": "array",
    "uniqueItems": true
  }
  ```
  
Boolean
-----
`"type": "boolean"`
숫자 1과 0을 대신해서 쓸 수 없다.
  
null
-----
`"type": "null"`
  
enum
-----
해당 데이터가 명시된 배열에 속한 값인지 검사함  
유효한 enum 값들은 배열을 사용하여 명시하며, 중복 값을 가질 수 없음  
```javascript
{
    "type": "string",
    "enum": ["웰시코기", "포메라니안", "푸들"]
}
```

스키마 결합
=====
- allOf  
  배열에 나열된 스키마에 대한 검증을 모두 통과
   ```javascript
   {
      "allOf": [
          {"minLength": 3},
          {"maxLength": 5}
      ]
  }
   ```
- anyOf  
  배열에 나열된 하나 이상의 스키마에 대한 검증을 통과
  ```javascript
  {
      "anyOf": [
          {"type": "string"},
          {"type": "number"}
      ]
  }
  ```
- oneOf  
  배열에 나열된 오직 하나의 스키마에 대한 검증만을 통과
  ```javascript
  {
    "oneOf": [
        { "type": "number", "multipleOf": 3 },
        { "type": "number", "multipleOf": 4 }
    ]
  }
  ```
- not  
  JSON 스키마를 만족하지 않는 데이터만을 검사
  ```javascript
  {
    "not": {
        "type": "string"
    }
  }
  ```
