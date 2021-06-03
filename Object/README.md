# 4. 객체

## 4.1 객체
- JavaScript는 객체(Object) 기반의 스크립트 프로그래밍 언어로 이루고 있는 거의 모든것이 객체이다.
- 원시 타입(Primitives)을 제외한 나머지 값들(함수, 배열, 정규표현식 등)은 모두 객체이다.
- 객체(Object)는 키(key)과 값(value)으로 구성된 프로퍼티(Property)들의 집합이다.

### 객체 생성하기
1. 객체 생성자 문법
```javscript
let person = new Object();
```
2. 객체 리터럴 문법
```javscript
var person = {};
```

### 리터럴과 프로퍼티
### 대괄호 표기법
### 단축 프로퍼티
### 프로퍼티 이름의 제약사항
### `in` 연산자로 프로퍼티 존재 여부 확인하기
### `for…in` 반복문
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
저장 후 리로드 한 다음에 아래의 내용을 브라우저 개발자 도구의 JavaScript 콘솔에  입력해보세요.

person.name
person.name[0]
person.age
person.interests[1]
person.bio()
person.greeting()
자, 이제 당신은 객체에 포함된 데이터와 함수를 갖게 되었으며, 이것들을 간단하고 멋진 문법을 통해 사용할 수 있게되었습니다!

Note: 만약 여기까지 진행하는데 어려움이 있다면, 제가 만들어놓은 파일과 비교해보세요 — oojs-finished.html (그리고 실행되는 예제도 보세요). Live 버전에서는 텅빈 화면만 보이겠지만, 그게 정상입니다 — 다시, 개발자도구를 열고 객체 구조를 들여다보기 위해 위에 언급된 명령어를 입력해보세요.

자, 이제 뭘 해볼까요? 객체는 각기 다른 이름(위의 예에서는 name 과 age)과 값(예제에서, ['Bob', 'Smith'] 과 32)을 갖는 복수개의 멤버로 구성됩니다. 한 쌍의 이름과 값은 ',' 로 구분되야 하고, 이름과 값은 ':' 으로 분리됩니다. 결국 문법은 아래와 같은 패턴이 됩니다.

var objectName = {
  member1Name: member1Value,
  member2Name: member2Value,
  member3Name: member3Value
};
객체를 구성하는 멤버의 값은 어떤 것이라도 될 수 있습니다. 우리가 만든 person 객체는 문자열, 숫자, 배열 두개와 두개의 함수를 가지고 있습니다. 처음 4개의 아이템은 데이터 아이템인데, 이걸 객체의 프로퍼티(속성) 라고 부릅니다. 끝에 두개의 아이템은 함수인데 이 함수를 통해 데이터를 가지고 뭔가 일을 할 수 있게 됩니다. 이걸 우리는 메소드 라고 부릅니다.

이런 객체는 객체 리터럴(object literal) 이라고 부릅니다. 객체를 생성할 때 컨텐츠를 그대로 대입합니다. 객체 리터럴은 클래스로부터 생성하는 방식과는 다릅니다. 이 방식은 뒤에서 살펴보게 될겁니다.

객체 리터럴을 사용해서 객체를 생성하는 것은 연속된 구조체나 연관된 데이터를 일정한 방법으로 변환하고자 할 때  많이 쓰이는 방법입니다. 예를 들면 서버에게 주소를 데이터베이스에 넣어달라고 요청하는 경우입니다. 각 아이템들을 하나 하나 개별 전송하는 것보다, 하나의 객체를 전송하는 것이 훨씬 효율적입니다. 또 각 아이템들을 이름으로 구분해서 사용하기 원할 때도 배열을 사용하는 것보다 훨씬 쉽습니다.

점 표기법
위에서, 우리는 객체의 프로퍼티와 메소드를 점 표기법을 통해 접근했습니다. 객체 이름(person)은 네임스페이스처럼 동작합니다. 객체내에 캡슐화되어있는것에 접근하려면 먼저 점을 입력해야합니다. 그 다음 점을 찍고 접근하고자 하는 항목을 적습니다. 간단한 프로퍼티의 이름일 수도 있을 것이고, 배열의 일부이거나 객체의 메소드를 호출할 수도 있습니다.

person.age
person.interests[1]
person.bio()
하위 namespaces
다른 객체를 객체 멤버의 값으로 갖는 것도 가능합니다. 예를 들면, 다음과 같은 name 멤버를 

name: ['Bob', 'Smith'],
아래와 같이 바꿔봅시다.

name : {
  first: 'Bob',
  last: 'Smith'
},
자, 이제 우리는 성공적으로 하위 namespace 를 만들었습니다. 복잡해보이지만, 사실 그렇지도 않습니다. 이 속성을 사용하려면 그저 끝에 다른 점을 하나 찍어주기만 하면 됩니다. JS 콘솔에서 아래와 같이 입력해보세요.

person.name.first
person.name.last
중요: 객체의 속성이 바뀌었으니까, 기존 메소드 코드를 바꿔 줘야 합니다. 기존 코드를

name[0]
name[1]
아래와 같이 바꿔줘야 합니다.

name.first
name.last
그렇지 않으면 기존 메소드는 더 이상 동작하지 않을 것입니다.

괄호 표기법
객체의 프로퍼티에 접근하는 다른 방법으로 괄호 표기법을 사용하는 것이 있습니다. 다음과 같이 사용하는 대신

person.age
person.name.first
이렇게 사용할 수 있습니다.

person['age']
person['name']['first']
이런 방식은 배열 속에 있는 항목에 접근하는 방법과 매우 유사해 보이는데 실제로도 이는 기본적으로 동일한 것입니다. 한 항목을 선택하기 위해 인덱스 숫자를 이용하는 대신에 각 멤버의 값들과 연결된 이름을 이용합니다. 객체가 간혹 연관배열 (associative arrays)이라고 불리는 것이 당연합니다. 연관배열은 배열이 숫자를 값에 연결하는 것과 같은 방법으로 스트링을 값에 매핑합니다.

객체 멤버 설정하기
지금까지는 객체 멤버를 단순히 가져오기만(또는 반환) 했습니다. 설정할 멤버를 간단히 명시하여(점이나 대괄호 표기법을 사용) 객체 멤버의 값을 설정(갱신)하는 것도 물론 가능합니다.

person.age = 45;
person['name']['last'] = 'Cratchit';
위의 코드를 입력한 다음, 객체 멤버값을 아래와 같이 다시 확인해봅시다.

person.age
person['name']['last']
객체 멤버를 설정하는 것은 단순히 기존에 존재하는 프로퍼티나 메소드로 값을 설정하는 것 뿐 아니라, 완전히 새로운 멤버를 생성할 수도 있습니다. JS 콘솔에서 아래 내용을 입력해보세요.

person['eyes'] = 'hazel';
person.farewell = function() { alert("Bye everybody!"); }
자, 이제 새로운 멤버를 테스트해보세요.

person['eyes']
person.farewell()
대괄호 표현의 이점 중 하나는 멤버의 값을 동적으로 변경할 수 있을 뿐아니라, 멤버 이름까지도 동적으로 사용할 수 있다는 것입니다. 자, 만약 사용자가 두개의 텍스트 입력을 통해서 people 데이터에 커스텀 값을 넣고 싶어한다고 가정해봅시다. 그 값은 다음과 같이 얻어올 수 있을겁니다.

var myDataName = nameInput.value;
var myDataValue = nameValue.value;
이제 person 객체에 다음과 같이 새 멤버의 이름과 값을 추가할 수 있습니다.

person[myDataName] = myDataValue;
자, 제대로 동작하는지 보려면 아래와 같이 person 객체에 대괄호를 붙여서 확인해보면 됩니다.

var myDataName = 'height';
var myDataValue = '1.75m';
person[myDataName] = myDataValue;
이제 저장하고 리로드후 아래코드를 입력해보세요.

person.height
점 표기법으로는 위의 예제처럼 멤버의 이름을 동적으로 사용할 수 없고, 상수 값만을 사용해야 합니다.

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