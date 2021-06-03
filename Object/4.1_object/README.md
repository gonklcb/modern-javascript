# 4.1 객체
- JavaScript는 객체(Object) 기반의 스크립트 프로그래밍 언어로 이루고 있는 거의 모든것이 객체이다.
- 원시 타입(Primitives)을 제외한 나머지 값들(함수, 배열, 정규표현식 등)은 모두 객체이다.

![image](https://user-images.githubusercontent.com/70567818/120576502-d46f5200-c45d-11eb-8bc1-e5c1e958299d.png)  
객체(Object)는 키(key)와 값(value)으로 구성된 프로퍼티(Property)들의 집합이다.  
```javascript
var person = {
  name: ['Bob', 'Smith'],
  age: 32,
  gender: 'male',
  interests: ['music', 'skiing'],
  bio: function() {
    alert(this.name[0] + ' ' + this.name[1] + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  },
  greeting: function() {
    alert('Hi! I\'m ' + this.name[0] + '.');
  }
};
```
　   
## ◾ 객체 생성하기
1. 객체 생성자 문법
```javascript
let person = new Object();
```
2. 객체 리터럴 문법
```javascript
var person = {};
```  
　   
## ◾ 리터럴과 프로퍼티
**리터럴(literal)** 이란 소스 코드의 고정된 값이다.
```javascript
const a = 1;
```
여기에서 리터럴은 a에 저장된 1을 의미한다.   
JavaScript는 리터럴 표기법을 이용해, 필요한 요소들을 열거하는 것 만으로 객체를 만들 수 있다.  
　   
객체의 프로퍼티는 `키(key): 값(value)`으로 이루어져있다.  
- key
  - key는 string으로 들어가고 `''`, `""`를 별도로 사용하지 않아도 되지만  
  두 단어 이상을 사용하려면 `''`, `""`로 묶어주는 것이 필요하다.
  - 변수에서 사용할 수 없는 예약어(`for, let, return`)들도 프로퍼티 key로 사용할 수 있다.
  - `__proto__`는 key로 사용할 수 없다.
- value
  - value에는 모든 자료형이 들어갈 수 있다.  

```javascript
let person = {
  'frist name': 'mirae',
  'last name': 'jang',
  age: 18,
  job: 'developer'
}
```  
　  
❗ **주의하기**  
*const*로 선언되어도 Object 내부의 property는 수정할 수 있다.  
![image](https://user-images.githubusercontent.com/70567818/120580201-bad10900-c463-11eb-981a-af708895745f.png)   
　   
## ◾ 표기법
```javascript
const person = {
  name: {
    first: 'mirae',
    last: 'jang'
  },
  age: 20,
  'hair color': 'brown',
}
```
### 1. 점 표기법
```javascript
person.name.first
person.name.last
person.age
```  
![image](https://user-images.githubusercontent.com/70567818/120588741-a9dbc400-c472-11eb-973a-a4a41cf30d14.png)  

*점 표기법으로는 `'hair color'`에 접근할 수 없다.*
　   
### 2. 괄호 표기법
```javascript
person[name][first]
person[name][last]
person[age]
person[hair color]
```
괄호 표기법을 사용할 때는 key를 감싸는 따옴표(`''` or `""`)가 필요하다.  
![image](https://user-images.githubusercontent.com/70567818/120589060-3edebd00-c473-11eb-82b4-dca1030a9c14.png)  

괄호 표기법에서는 두 단어 이상으로 이루어진 key로도 접근이 가능하다.   
![image](https://user-images.githubusercontent.com/70567818/120589155-60d83f80-c473-11eb-95c2-2e5fc8e9fced.png)   
　   
## ◾ 단축 프로퍼티
프로퍼티의 key와 value가 같다면 축약해서 하나만 적는 것이 가능하다.
```javascript
function makeUser(name, age) {
  return {
    name: name,
    age: age,
  };
}
```
🔽 *프로퍼티 값 단축 구문(property value shorthand)* 적용 
```javascript
function makeUser(name, age) {
  return {
    name,
    age,
  };
}
```   
　   
## ◾ `in` 연산자로 프로퍼티 존재 여부 확인하기
값이 없으면 `undefined`가 나오는것으로도 property의 존재 여부를 확일 할 수 있다.
```javascript
let user = { name: "John", age: 30 };
```   
![image](https://user-images.githubusercontent.com/70567818/120590638-cdecd480-c475-11eb-8987-94058c8a6be5.png)   
　   
하지만 `undefined`로 구분하는 경우 value를 `undefined`로 할당한 것과 구분 할 수 없게 된다.
그래서 확실한 방법은 `in`을 사용하여 확인하는 방법이다.
　   
**`in`** 을 사용하면 Obejct 내부에 찾고자 하는 property가 있는지 확인할 수 있다.
```javascript
'Key' in Object
```  
*key를 따옴표로 감싸지 않으면 원하는 값이 제대로 나오지 않을 수 있기때문에 주의해야 한다.*   
property가 있다면 **true**, 없다면 **flase**값이 나오게 된다.  
![image](https://user-images.githubusercontent.com/70567818/120590789-12787000-c476-11eb-96fc-65cd60bea300.png)   
　   
## ◾ `for…in` 반복문
```javascript
for (variable in object) { ... }
```
`for…in`은 key-value 쌍으로 구성된 데이터의 경우 특정 key가 있는지 확인할 때 사용할 수 있다.

```javascript
var obj = {a: 1, b: 2, c: 3};

for (const prop in obj) {
  console.log(`obj.${prop} = ${obj[prop]}`);
}
```   
![image](https://user-images.githubusercontent.com/70567818/120592298-929fd500-c478-11eb-9d5e-daa857b30d5a.png)   
　   
　   
　   
　   
　   
|이전페이지|다음페이지|
|:---|---:|
||[`▶ 4.2 참조에 의한 객체 복사 `](../4.2_object-copy#42-참조에-의한-객체-복사)|
