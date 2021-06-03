# 4. 객체

## 4.1 객체
- JavaScript는 객체(Object) 기반의 스크립트 프로그래밍 언어로 이루고 있는 거의 모든것이 객체이다.
- 원시 타입(Primitives)을 제외한 나머지 값들(함수, 배열, 정규표현식 등)은 모두 객체이다.

![image](https://user-images.githubusercontent.com/70567818/120576502-d46f5200-c45d-11eb-8bc1-e5c1e958299d.png)  
객체(Object)는 키(key)과 값(value)으로 구성된 프로퍼티(Property)들의 집합이다.  
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
　   
### ◾ 객체 생성하기
1. 객체 생성자 문법
```javascript
let person = new Object();
```
2. 객체 리터럴 문법
```javascript
var person = {};
```  
　   
### ◾ 리터럴과 프로퍼티
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
　   
### ◾ 표기법
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
#### 1. 점 표기법
```javascript
person.name.first
person.name.last
person.age
```  
![image](https://user-images.githubusercontent.com/70567818/120588741-a9dbc400-c472-11eb-973a-a4a41cf30d14.png)  

*점 표기법으로는 `'hair color'`에 접근할 수 없다.*
　   
#### 2. 괄호 표기법
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
　   
### ◾ 단축 프로퍼티
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
　   
### ◾ `in` 연산자로 프로퍼티 존재 여부 확인하기
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
　   
### ◾ `for…in` 반복문
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
　   
## 4.2 참조에 의한 객체 복사
### ◾ 참조에 의한 객체 복사
원시 타입(Primitive type;  string, number, bigint, boolean, undefined, symbol)은 값이 메모리 공간에 할당된다.   
하지만 객체는 참조 타입(Reference Type)으로 값이 메모리에 직접 할당되지 않고 **메모리의 위치를 참조**하여 간접적으로 접근하게된다.   
```javascriptt
let message = "Hello!";
let phrase = message;
```   
**message**와 **phrase**는 각각 `Hello!`라는 문자열의 갖게 된다.   
　   
```javascript
let user = {
  name: "mirae"
};
let admin = user;
```   
객체는 **user**와 **admin**가 각각 `{ name: "mirae" }`를 저장하는 것이 아닌, 동일한 객체에 대한 참조 값이 저장된다.   
저장된 객체는 한 개 이고, 변수에 저장되는것은 그 객체를 참조할 수 있는 값이 저장된다.   
　   
```javascript
let user = { age: 20 };
let admin = user;

admin.name = 30;
```   
![image](https://user-images.githubusercontent.com/70567818/120596669-fdeca580-c47e-11eb-8a0b-4eb35fec7688.png)   
객체가 각각 저장되는 것이 아니고, 1개를 가지고 참조하여 사용한다.  
위에서 user에 객체가 저장되어 있는 것처럼 보이지만 admin에서 프로퍼티를 수정하면 user의 프로퍼티도 수정된 것을 할 수 있다.   
　    
#### 참조에 의한 비교
```javascript
let a = {};
let b = a;
```   
a와b는 같은 객체를 참조하고 있기 때문에 true가 나오게된다.   
![image](https://user-images.githubusercontent.com/70567818/120597151-a1d65100-c47f-11eb-8138-04ca576d76cd.png)   

```javascript
let a = {};
let b = {};
```   
a와b의 객체 내부 내용은 같지만, 참조하고 있는 객체가 서로 다르기 때문에 false가 나오게 된다.   
![image](https://user-images.githubusercontent.com/70567818/120597223-c3cfd380-c47f-11eb-8866-28f916c44057.png)   
　   
### ◾ 객체 복사, 병합과 Object.assign
객체 복사는 기존 방식으로 하게되면 같은 객체를 참조하게 된다고 앞서 말했다.
그렇기에 객체의 복사는 다른 방법이 필요하다.
- `for…in` 사용
```javascript
const device = {
  phone: 'iPhone SE',
  tablet: 'iPad Pro', 
  watch: 'Apple Watch Series 6'
}
let clone = {}

for (let key in device) {
  clone[key] = device[key];
}
```   
이렇게 복사하면 clone의 property를 수정해도 기존에 있던 device에는 영향을 주지 않는다.   
![image](https://user-images.githubusercontent.com/70567818/120599412-6ee18c80-c482-11eb-8724-d81182b862ad.png)   
　   
- `Object.assign` 사용   
Object.assign()는 대상 객체로 속성을 복사하는 메서드 이다.
```javascript
Object.assign(target, ...sources)
```
target에는 대상 객체가, sources에는 복사해 올 출처 객체가 들어간다. 출처객체는 한개 이상일 수 있다.   

```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);
```   
target도 수정되고 returnedTarget에도 저장되었다.   
target에 source를 덮어씌웠기 때문에 b는 4가 되었다.   
![image](https://user-images.githubusercontent.com/70567818/120600399-af8dd580-c483-11eb-9a73-59c935e44338.png)   
　   
### ◾ 중첩 객체 복사
중첩 객체란 아래와 같이 객체의 프로퍼티가 객체인 구조를 의미한다.   
```javascript
let user = {
  name: {
    first: 'mirae',
    last: 'jang'
  },
  age: 20
};
```
name이라는 객체도 복사했을 때, 같은 것을 참조하는 것이 아닌 서로 다른 객체를 만들어야 한다.  

**deep copy** (참고: https://www.zerocho.com/category/JavaScript/post/5750d384b73ae5152792188d)
```javascript
const obj = {
  a: 1,
  b: 2,
  c: {
    d: 4,
    e: 5
  }
};
let clone = copyObj(obj);

function copyObj(obj) {
  var copy = {};
  if (Array.isArray(obj)) {
    copy = obj.slice().map((v) => {
      return copyObj(v);
    });
  } else if (typeof obj === "object" && obj !== null) {
    for (var attr in obj) {
      if (obj.hasOwnProperty(attr)) {
        copy[attr] = copyObj(obj[attr]);
      }
    }
  } else {
    copy = obj;
  }
  return copy;
}
```   
![image](https://user-images.githubusercontent.com/70567818/120604962-7efc6a80-c488-11eb-9bb6-732eeb15a527.png)   
　   
자바스크립트 라이브러리 **lodash**의 메서드인 **_.cloneDeep(obj)** 를 사용할 수도 있다.   
　   
## 4.3 가비지 컬렉션
자바스크립트 엔진이 자동으로 수행하는 일로서, 도달 불가능한 상태의 객체를 찾아 메모리에서 삭제하는 메모리 관리 시스템

### 가비지 컬렉션 기준
객체의 도달 가능성 (reachbility)
Root가 참조하는 값이나 체이닝으로 Root에서 참조할 수 있는 값은 도달 가능한 값이 됨 (Root : 변수, 매개변수 등의 태생부터 도달 가능성을 따질 필요없이 늘 도달 가능한 값들)
즉, 가비지 콜렉션 알고리즘의 핵심 개념은 *참조*

### 예시
#### 간단한 예시
```javascript
let user = {
  name: "John"
};
```
![image](https://user-images.githubusercontent.com/33821863/120483935-8a4e8800-c3ed-11eb-9c43-6220e738f9d4.png)
위 그림에서 화살표는 객체 참조를 나타냅니다. 전역 변수 `user`가 참조하고 있는 객체는 도달가능한 상태입니다.
```javascript
user = null
```
![image](https://user-images.githubusercontent.com/33821863/120484482-152f8280-c3ee-11eb-850c-d4d42dd1eb95.png)
`user`의 값을 다른 값으로 덮어쓰면 화살표가 사라집니다. 객체 John은 도달할 수 없는 상태가 되었으므로 가비지 콜렉터에 의해 메모리에서 제거됩니다.

#### 참조 두 개 예시
```javascript
let user = {
  name: "John"
};

let admin = user;
```
![image](https://user-images.githubusercontent.com/33821863/120484753-57f15a80-c3ee-11eb-9a81-3e0f68f9a648.png)
참조된 객체를 변수 `admin`으로 복사합니다.
```javascript
user = null
```
앞의 예시와는 달리 `user`의 값을 덮어써도 `admin`을 통해 객체에 접근할 수 있으므로 삭제 되지 않습니다.

#### 연결된 객체 예시
```javascript
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman
  }
}

let family = marry({
  name: "John"
}, {
  name: "Ann"
});
```
![image](https://user-images.githubusercontent.com/33821863/120487040-925bf700-c3f0-11eb-8f52-0432de80f05a.png)
함수 `marry()`는 매개변수로 받은 두 객체를 서로 참조하게 하면서, 두 객체를 포함하는 새로운 객체를 반환합니다.
현재는 모든 객체들이 도달 가능한 상태입니다.

```javascript
delete family.father;
delete family.mother.husband;
```

참조 두 개를 지우면 객체 John으로 들어오는 참조는 모두 사라지므로 John은 메모리에서 제거됩니다.
우리는 위 예시를 통해 외부로 나가는 참조는 도달 가능한 상태에 영향을 주지 않는다는 것을 알 수 있습니다.

#### 도달할 수 없는 섬
위 연결된 객체의 예시를 보면 객체들이 연결되어 섬 같은 구조를 만듭니다. 이 섬에 도달할 방법이 없는 경우, 섬을 구성하는 객체 전부가 메모리에서 삭제됩니다.
```javascript
family = null
```
![image](https://user-images.githubusercontent.com/33821863/120487900-4fe6ea00-c3f1-11eb-82fa-cf2493338908.png)
객체가 root 값과의 연결이 끊어지면서 섬이 통째로 메모리에서 제거됩니다.

### 내부 알고리즘 : Mark-and-sweep
가비지 콜렉터는 roots 라는 오브젝트의 집합을 가지고 있다가 주기적으로 roots로 부터 시작하여 roots가 참조하는 오브젝트들, roots가 참조하는 오브젝트가 참조하는 오브젝트들... 을 닿을 수 있는 오브젝트라고 표시(mark) 한다. 그 과정에서 닿을 수 없는 오브젝트에 대해 가비지 콜렉션을 수행합니다.
이러한 형태의 알고리즘을 Mark and Sweep이라고 합니다.

2012년 기준으로 모든 최신 브라우저들은 가비지 콜렉션에서 이 알고리즘을 사용합니다.

### 참고
- [모던 자바스크립트](https://ko.javascript.info/garbage-collection)
- [MDN : 자바스크립트의 메모리관리](https://developer.mozilla.org/ko/docs/Web/JavaScript/Memory_Management)

## 4.4 메서드와 this
### 메서드
객체 프로퍼티에 저장된 함수
```javascript
user = {
  name: "newstar",
  sayHi: function() {
    alert("Hello");
  }
};
```

### 메서드와 this
함수를 어떤 객체의 메서드로 호출하면 this의 값은 그 객체를 참조합니다.
```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다.
    alert(this.name);
  }

};

user.sayHi(); // John
```
위 예시와 같이 메서드 내부에서 `this`를 사용하면 메서드를 실행한 객체에 접근할 수 있습니다.

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert( user.name ); // Error: Cannot read property 'name' of null
  }

};

let admin = user;
user = null; // user를 null로 덮어씁니다.

admin.sayHi(); // sayHi()가 엉뚱한 객체를 참고하면서 에러가 발생했습니다.
```
위 예시처럼 원본 객체의 이름을 그대로 사용할 수도 있지만, `this`는 호출 시점에 해당 객체가 결정되므로 원본 객체가 다른 값으로 덮어 씌워질 경우, 에러가 발생하게 됩니다.

#### 객체의 프로토타입 체인에서의 this
객체의 프로토타입 체인 어딘가에 정의한 메서드도 마찬가지로 동작합니다.

```javascript
var o = {
  f:function() { return this.a + this.b; }
};
var p = Object.create(o);
p.a = 1;
p.b = 4;

console.log(p.f()); // 5
```

#### Getter와 Setter에서의 this
Getter와 Setter에서도 동일하게 동작합니다. 이 경우에도 `this`는 Getter 혹은 Setter를 포함하는 객체를 참조합니다.

```javascript
function sum() {
  return this.a + this.b + this.c;
}

var o = {
  a: 1,
  b: 2,
  c: 3,
  get average() {
    return (this.a + this.b + this.c) / 3;
  }
};

Object.defineProperty(o, 'sum', {
    get: sum, enumerable: true, configurable: true});

console.log(o.average, o.sum); // 2, 6
```

### 자유로운 this
자바스크립트의 `this`는 모든 함수에서 사용할 수 있으며, 그 값이 런타임, 즉 호출 시점에 결정됩니다. 동일한 함수라도 다른 객체에서 호출했다면 `this`가 참조하는 값이 달라집니다.

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// 별개의 객체에서 동일한 함수를 사용함
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
```

#### 객체 없이 호출하기
객체가 없어도 this가 포함된 함수를 실행할 수 있습니다.
```javascript
function sayHi() {
  alert(this);
}

sayHi(); // undefined
```
위 예시의 경우 `this`는 use strict 모드일 때는 undefined, 아닐 때는 전역 객체(브라우저에서는 window)를 참조하게 됩니다.

하지만 이런 식의 코드는 일반적인 코드가 아닙니다. 함수 본문에 this가 사용되었다면, 객체 컨텍스트 내에서 함수를 호출할 것이라고 예상하시면 됩니다.

### this와 arrow function
화살표 함수는 `this`를 가지지 않습니다. 화살표 함수에서 `this`는 자신을 감싼 정적 범위(lexical context)입니다.

```javascript
let user = {
  firstName: "newstar",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // newstar
```
위의 예시에서 `this`는 `user.sayHi()`의 `this`가 됩니다.
별개의 this가 만들어지는 건 원하지 않고, 외부 컨텍스트에 있는 this를 이용하고 싶은 경우 화살표 함수가 유용합니다.

### 참고
- [모던 자바스크립트](https://ko.javascript.info/object-methods)
- [MDN : this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)











