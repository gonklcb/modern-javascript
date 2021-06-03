# 4.3 가비지 컬렉션
자바스크립트 엔진이 자동으로 수행하는 일로서, 도달 불가능한 상태의 객체를 찾아 메모리에서 삭제하는 메모리 관리 시스템

## 가비지 컬렉션 기준
객체의 도달 가능성 (reachbility)
Root가 참조하는 값이나 체이닝으로 Root에서 참조할 수 있는 값은 도달 가능한 값이 됨 (Root : 변수, 매개변수 등의 태생부터 도달 가능성을 따질 필요없이 늘 도달 가능한 값들)
즉, 가비지 콜렉션 알고리즘의 핵심 개념은 *참조*

## 예시
## 간단한 예시
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

## 참조 두 개 예시
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

## 연결된 객체 예시
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

## 도달할 수 없는 섬
위 연결된 객체의 예시를 보면 객체들이 연결되어 섬 같은 구조를 만듭니다. 이 섬에 도달할 방법이 없는 경우, 섬을 구성하는 객체 전부가 메모리에서 삭제됩니다.
```javascript
family = null
```
![image](https://user-images.githubusercontent.com/33821863/120487900-4fe6ea00-c3f1-11eb-82fa-cf2493338908.png)
객체가 root 값과의 연결이 끊어지면서 섬이 통째로 메모리에서 제거됩니다.

## 내부 알고리즘 : Mark-and-sweep
가비지 콜렉터는 roots 라는 오브젝트의 집합을 가지고 있다가 주기적으로 roots로 부터 시작하여 roots가 참조하는 오브젝트들, roots가 참조하는 오브젝트가 참조하는 오브젝트들... 을 닿을 수 있는 오브젝트라고 표시(mark) 한다. 그 과정에서 닿을 수 없는 오브젝트에 대해 가비지 콜렉션을 수행합니다.
이러한 형태의 알고리즘을 Mark and Sweep이라고 합니다.

2012년 기준으로 모든 최신 브라우저들은 가비지 콜렉션에서 이 알고리즘을 사용합니다.

## 참고
- [모던 자바스크립트](https://ko.javascript.info/garbage-collection)
- [MDN : 자바스크립트의 메모리관리](https://developer.mozilla.org/ko/docs/Web/JavaScript/Memory_Management)   

　   
　   
　   
　   
　   
---   
|이전페이지|다음페이지|
|:---|---:|
|[`◀ 4.2 참조에 의한 객체 복사`](../4.2_object-copy#42-참조에-의한-객체-복사)|[`4.4 메서드와 this ▶`](../4.4_object-methods#44-메서드와-this)|
