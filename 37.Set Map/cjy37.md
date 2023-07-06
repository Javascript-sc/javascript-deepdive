## 37장 Set과 Map

#### 37.1 Set
Set 객체는 중복되지 않는 유일한 값들의 집합(set)이다.
Set 객체는 배열과 유사하지만 다음과 같은 차이가 있다. 

- 동일한 값을 중복하여 포함할 수 없다.
- 요소 순서에 의미가 없다.
- 인덱스로 요소에 접근할 수 없다.

Set은 수학적 집합을 구현하기 위한 자료구조로, Set을 통해 교집합, 합집합, 차집합, 여집합 등을 구현할 수 있다.

###### 37.1.1 Set 객체의 생성
Set 객체는 Set 생성자 함수로 생성한다.

```jsx
const set = new Set();
console.log(set); // Set(0) {}
```

Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.
```jsx
const set1 = new Set([1, 2, 3, 3]);
console.log(set1); // Set(3) {1, 2, 3}
```               
Set을 활용하여 중복 요소 제거하기
```jsx
const uniq = array => {...new Set(array)};
console.log(uniq([2, 1, 2, 3, 4, 3, 4])); // [2, 1, 3, 4]
```

###### 37.1.2 요소 개수 확인
Set.prototype.size 프로퍼티를 사용한다.

const { size } = new Set([1, 2, 3, 3]);
console.log(size); // 3
  
size 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티로, size 프로퍼티에 숫자를 할당하여 Set 객체의 요소 개수를 변경할 수 없음.


###### 37.1.3 요소 추가
Set.prototype.add 메서드를 사용한다.
```jsx
const set = new Set();
console.log(set); // Set(0) {}

set.add(1);
console.log(set); // Set(1) {1}
```
add 메서드는 새로운 요소가 추가된 Set 객체를 반환하기 때문에 add 메서드를 호출한 후 add 메서드를 연속적으로 호출(method chaining)할 수 있다.
```jsx
const set = new Set();

set.add(1).add(2); 
console.log(set); // Set(2) {1, 2}
```
Set 객체는 NaN과 NaN을 같다고 평가하여 중복 추가를 허용하지 않음. +0과 -0은 일치 비교 연산자 ===와 마찬가지로 같다고 평가하여 중복 추가를 허용하지 않음.
```jsx
const set = new Set();

set.add(NaN).add(NaN);
console.log(set); // Set(1) {NaN}

set.add(0).add(-0); 
console.log(set); // Set(2) {NaN, 0}
```
Set 객체는 객체나 배열과 같이 자바스크립트의 모든 값을 요소로 지정할 수 있다.

###### 37.1.4 요소 존재 여부 확인

Set.prototype.has 메서드를 사용한다.
has 메서드는 특정 요소의 존재 여부를 나타내는 불리언 값을 반환한다.
```jsx
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true 
```

###### 37.1.5 요소 삭제
Set.prototype.delete 메서드를 사용한다.
```jsx
const set = new Set([1, 2, 3]);

set.delete(2)
console.log(set); // Set(2) {1, 3}
```
존재하지 않는 Set 객체의 요소를 삭제하려 하면 에러 없이 무시됨.

delete 메서드는 삭제 성공 여부를 나타내는 불리언 값을 반환하기 때문에 optional chaining이 불가능하다.

###### 37.1.6 요소 일괄 삭제

Set.prototype.clear 메서드를 사용한다. clear 메서드는 언제나 undefined를 반환한다.
```jsx
set.clear();
console.log(set); // Set(0) {}
```
###### 37.1.7 요소 순회
Set.prototype.forEach 메서드를 사용한다.
forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체(옵션)를 인수로 전달한다.

콜백 함수는 3개의 인수를 전달받는다.

첫 번째 인수 : 현재 순회 중인 요소값
두 번째 인수 : 현재 순회 중인 요소값
세 번째 인수 : 현재 순회 중인 Set 객체 자체
첫 번째 인수와 두 번째 인수는 같은 값이며, Array.prototype.forEach 메서드와 인터페이스를 통일하기 위함일 뿐 다른 의미는 없다.
```jsx
const set = new Set([1, 2]); 
 
set.forEach((v, v2, set) => console.log(v, v2, set));

/*
1 1 Set(2) {1, 2}
2 2 Set(2) {1, 2}
*/
```
Set 객체는 이터러블이다. 따라서 for...of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.
set 객체는 요소의 순서에 의미를 갖지 않지만 Set 객체를 순회하는 순서는 요소가 추가된 순서를 따른다. 이는 ECMAScript 사양에 규정되어 있지는 않지만 다른 이터러블의 순회와 호환성을 유지하기 위함.

###### 37.1.8 집합 연산
Set 객체는 집합 연산을 수행할 수 있는 메서드를 제공합니다. 
이를 통해 두 개 이상의 Set 객체를 결합하거나 교집합, 차집합, 합집합 등의 연산을 수행할 수 있습니다.
1) 교집합
   intersection메서드 내의 this는 생성자 함수가 생성한 인스턴스를 가리킨다.
   ```jsx
   Set.prototype.intersection = function (set) {
  const result = new Set();

  for (const value of set) {
    // 2개의 set의 요소가 공통되는 요소이면 교집합의 대상이다.
    if (this.has(value)) result.add(value);
  }

  return result;
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

// setA와 setB의 교집합
console.log(setA.intersection(setB)); // Set(2) {2, 4}
// setB와 setA의 교집합
console.log(setB.intersection(setA)); // Set(2) {2, 4}
   ```
   Set 객체의 주요 집합 연산
add(value): Set에 값을 추가합니다. 이미 값이 존재하는 경우 무시됩니다.
delete(value): Set에서 값을 제거합니다. 값이 성공적으로 제거되면 true를 반환하고, 값이 존재하지 않으면 false를 반환합니다.
has(value): Set에 값이 존재하는지 확인합니다. 값이 존재하면 true를 반환하고, 값이 존재하지 않으면 false를 반환합니다.
clear(): Set의 모든 값을 제거하여 비웁니다.
size: Set에 저장된 값의 개수를 반환합니다.
집합 연산을 수행하는 메서드는 다음과 같습니다:

union(otherSet): 현재 Set 객체와 다른 Set 객체의 합집합을 반환합니다. 두 Set의 모든 고유한 값을 포함합니다.
intersection(otherSet): 현재 Set 객체와 다른 Set 객체의 교집합을 반환합니다. 두 Set에서 공통으로 포함된 값을 반환합니다.
difference(otherSet): 현재 Set 객체에서 다른 Set 객체에 있는 값들을 제외한 차집합을 반환합니다. 현재 Set에는 있지만 다른 Set에는 없는 값을 반환합니다.
subset(otherSet): 현재 Set 객체가 다른 Set 객체의 부분집합인지 확인합니다. 현재 Set의 모든 값을 다른 Set이 포함하고 있는지 확인하여 true 또는 false를 반환합니다.

2) 합집합
합집합은 result를 인스턴스의 set으로 초기화 하고 result에 다른 집합을 합쳐주는데, set은 동일한 값을 가지지않으므로 값이 중복되지않게 합집합을 만들수 있다.

```jsx
Set.prototype.union = function (set) {
  // this(Set 객체)를 복사
  const result = new Set(this);

  for (const value of set) {
    // 합집합은 2개의 Set 객체의 모든 요소로 구성된 집합이다. 중복된 요소는 포함되지 않는다.
    result.add(value);
  }

  return result;
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

// setA와 setB의 합집합
console.log(setA.union(setB)); // Set(4) {1, 2, 3, 4}
// setB와 setA의 합집합
console.log(setB.union(setA)); // Set(4) {2, 4, 1, 3}
```

3) 차집합
차집합 A-B는 집합 A에는 존재하지만 B에는 존재하지 않는 요소로 구성된다.
여기서는 delete 메서드를 사용하면 된다.

4) 부분 집합과 상위 집합
집합 A가 집합 B에 포함되는 경우 집합 A는 B의 부분집합이며 집합 B는 A의 상위집합이다.

#### 37.2 Map
Map 객체는 키와 값의 쌍으로 이루어진 컬렉션이다. Map 객체는 객체와 유사하지만, 다음과 같은 차이가 있다.

키로 사용할 수 있는 값 - 객체 : 문자열 또는 심벌 값 / Map 객체 : 객체를 포함한 모든 값
객체는 이터러블이 아니지만, Map 객체는 이터러블
요소 개수 확인 - 객체 : Object.keys(obj).length / Map 객체 : map.size

###### 37.2.1 Map 객체의 생성

Map 생성자 함수로 생성.
```jsx
const map = new Map();
console.log(map); // Map(0) {}
```
Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성한다. 이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성되어야 한다.
```jsx
const map1 = new Map([['key1', 'value1'], ['key2', 'value2']);

console.log(map1); // Map(2) {"key1" => "value1", "key2" => "vlaue2"}
```
                      
                    
Map 생성자 함수의 인수로 전달한 이터러블에 중복된 키를 갖는 요소가 존재하면 값이 덮어써진다. 따라서 Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없다.

###### 37.2.2 요소 개수 확인
Map.prototype.size 프로퍼티 사용
```jsx
const { size } = new Map([['key1', 'value1'], ['key2', 'value2']);
                          
console.log(size); // 2
```
size 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티로, size 프로퍼티에 숫자를 할당하여 Map 객체의 요소 개수를 변경할 수 없다.

###### 37.2.3 요소 추가

Map.prototype.set 메서드 사용

map.set('key1', 'value1'); 

set 메서드는 새로운 요소가 추가된 Map 객체를 반환하기 때문에 method chaining 이 가능하다.
```jsx
map
  .set('key1', 'value1')
  .set('key2', 'value2');
```
map 객체에는 중복된 키를 갖는 요소가 존재할 수 없기 때문에 중복된 키를 갖는 요소를 추가하면 값이 덮어지며, 이 때 에러가 발생하지는 않는다.

NaN과 NaN, +0과 -0를 같다고 평가하여 중복 추가 허용하지 않는다.

Map 객체는 키 타입에 제한이 없다. 따라서 객체를 포함한 모든 값을 키로 사용할 수 있음.
```jsx
const map = new Map();

const lee = { name : 'Lee' };
const kim = { name : 'Kim' };

map
  .set(lee, 'developer')
  .set(kim, 'designer');
            
```
###### 37.2.4 요소취득
특정요소를 취득하려면 Map.prototype.get메서드를 사용한다.
get메서드의 인수로 키를 전달하면 Map 객체에서 인수로 전달한 키를 갖는 값을 반환한다. 전달한 키를 갖는 요소가 없다면 undefined를 반환한다.
```jsx
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

map
  .set(lee, 'developer')
  .set(kim, 'designer');

console.log(map.get(lee)); // developer
console.log(map.get('key')); // undefined
```

###### 37.2.5 요소 존재 여부 확인
특정 요소를 가지고 있는지 확인하려면 Map.ptorotype.has메서드를 사용한다. has 메서드는 불리언값을 반환한다!
```jsx
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

console.log(map.has(lee)); // true
console.log(map.has('key')); // false

```

###### 37.2.6 요소 삭제
Map.prototype.delete 메서드를 사용. 삭제 성공 여부를 나타내는 불리언값 반환한다.
```jsx
const lee = { name : 'Lee' };
const kim = { name : 'Kim' };
const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.delete(kim);
```
만약 존재하지 않는 키로 Map 객체의 요소를 삭제하려 하면 에러 없이 무시된다.

###### 37.2.7 요소 일괄 삭제
Map.prototype.clear 메서드를 사용. 언제나 undefined 반환
```jsx
const lee = { name : 'Lee' };
const kim = { name : 'Kim' };
const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.clear();
console.log(map); //Map(0)
```
###### 37.2.8 요소 순회

Map 객체에서 요소를 순회하는 방법은 다양합니다. 가장 일반적인 방법은 for...of 루프를 사용하는 것입니다. for...of 루프를 사용하면 Map 객체의 각 요소를 순차적으로 접근할 수 있습니다. 
예를 들어:

1. for ...of 문
```jsx
const myMap = new Map();
myMap.set("key1", "value1");
myMap.set("key2", "value2");
myMap.set("key3", "value3");

for (const [key, value] of myMap) {
  console.log(key, value);
}
key1 value1
key2 value2
key3 value3
```
위의 예시에서 for...of 루프를 사용하여 Map 객체의 각 요소를 순회하고, 각 요소의 키와 값에 접근합니다. 결과는 다음과 같이 출력됩니다:

2. forEach
또 다른 방법은 forEach 메서드를 사용하는 것입니다. Map 객체의 forEach 메서드는 콜백 함수를 각 요소에 대해 실행하며, 키와 값에 접근할 수 있습니다.
 예를 들어:

```jsx
myMap.forEach((value, key) => {
  console.log(key, value);
});
```
forEach 메서드의 콜백 함수에서 첫 번째 매개변수는 값이고, 두 번째 매개변수는 키입니다. 순서는 forEach 메서드 내부에서 관리되기 때문에 입력 순서대로 요소를 순회합니다.

요소를 순회할 때는 for...of 루프나 forEach 메서드를 선택할 수 있으며, Map 객체의 요소를 효율적으로 처리할 수 있습니다.

