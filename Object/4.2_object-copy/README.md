# 4.2 참조에 의한 객체 복사
## ◾ 참조에 의한 객체 복사
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
　    
## 참조에 의한 비교
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
　   
## ◾ 객체 복사, 병합과 Object.assign
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
　   
## ◾ 중첩 객체 복사
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
　   
　   
　   
　   
　   
|이전페이지|다음페이지|
|:---|---:|
|[`◀ 4.1 객체 `](../4.1_object#41-객체)|[`▶ 4.3 가비지 컬렉션 `](../4.3_garbage-collection#43-가비지-컬렉션)|
