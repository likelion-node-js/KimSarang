# Node.js 스터디

---

# 2. 알아둬야 할 자바스크립트

## 2.1  ES2015+

### 2.1.1  const, let

- `**const**` : 변수 재선언 X, 재할당 X
- `**let**` : 변수 재선언 X, 재할당 O

### 2.1.2  템플릿 문자열

- `**`(백틱)**`을 사용하여 문자열 표현을 쉽게 만들어 준다.
- 변수는 백틱 안에서 `**${변수명}`** 형태로 입력하면 된다.
    
    ```jsx
    const fries = "감자튀김";
    const chika = "치이카와";
    
    let output = "나는 " + fries + "와" + chika + "를 좋아한다.";
    output = **`나는 ${fries}와 ${chika}를 좋아한다.`**;
    // 같은 결과가 나온다.
    ```
    
- 띄어쓰기, 줄바꿈 등에도 활용 가능. 이스케이프 문자( \n , \t )를 사용하지 않아도 된다.
    
    ```jsx
    const multiLineStrings = `
    						I'm starving T_T
    I need some fries
    					Yum good ~~ `;
    
    console.log(multiLineStrings); 
    // 띄어쓰기, 줄바꿈 그대로 출력됨
    ```
    

### 2.1.3  객체 리터럴

- JS에서 가장 일반적인 객체 생성 방법.

```jsx
const newObject = {
	name: 'Sarang', // 속성 나열시 쉼표(,)로 구분
	sayHello () {
		console.log(`Hello! I'm ${this.name}`);
	},
	'favorite-color': 'red', // 식별자로 특수문자 사용시 따옴표로 감싸기.
};
```

### 2.1.4  화살표 함수

- `**⇒**` 기호를 사용하여 `**function**` 키워드를 생략할 수 있다.
    
    ```jsx
    function plus(a,b) {
    	return a + b;	
    }
    
    const sum = (a, b) => {
    	return a + b;	
    }
    // 함수에 return문만 있다면 한 줄로 줄일 수 있음
    // const sum = (a, b) => a + b;
    ```
    

### 2.1.5  구조 분해 할당

- **배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식**
- `**배열**`을 분해해보자
    
    ```jsx
    let arr = ["apple", "red"]
    
    let [fruit, color] = arr;
    console.log(fruit); // apple
    console.log(color); // red
    ```
    
    - `**…**` 을 붙인 매개변수 하나를 추가하면 나머지를 가져올 수 있다
        
        ```jsx
        let [name1, name2, ...namugee] = ["Kim", "Kwon", "Park", "Choi"];
        console.log(name1, name2); // Kim Kwon
        console.log(namugee[0]); // Park
        console.log(namugee[1]); // Choi
        ```
        
- `**객체**`를 분해해보자
    
    ```jsx
    let player = {
      name: "Sarang",
      hp : 50,
      mp: 200,
    };
    
    let {name, hp, mp} = player;
    console.log(name); // Sarang
    console.log(hp); // 50
    console.log(mp); // 200
    
    // :(콜론)과 =(할당 연산자) 활용
    let { mp : mana, job = "homeProtector"} = player;
    console.log(mana); // 200
    console.log(job); // homeProtector
    ```
    
    - 나머지 패턴 `**…`** 을 여기서도 사용해보자
        
        ```jsx
        let player = {
          name: "Sarang",
          hp : 50,
          mp: 200,
        };
        
        let {name, ...rest} = player;
        console.log(rest.hp) // 50
        console.log(rest.mp) // 200
        ```
        

### 2.1.6  클래스

1. `**생성자** (Constructor)` : 객체를 생성할 때 인자를 속성(프로퍼티)에 전달한다. 
    
    ```jsx
    class Person {
      constructor(name, age) { // 인자를 받아 할당한다.
        // fields
        this.name = name; // this는 객체(변수명)를 지칭한다.
        this.age = age; // this.name, this.age는 클래스의 필드(프로퍼티)이다.
      }
    
      // methods
      speak() {
        console.log(`${this.name}: hello!`);
      }
    }
    ```
    

---

1. `**getter**` 와 `**setter**`
    - `getter` : 객체의 특정 속성 값을 가져오는 메소드
        
        → 잘못된 값을 할당할 경우 **예외처리 가능**
        
    - `setter` : 객체의 특정 속성 값을 설정, 변경하는 메소드
    
    ```jsx
    const user = {
    	name: 'Sarang',
      age: 21,
       
        get userName() {
        	return user.name; // 'Sarang'
        },
        set userName(value) {
        	user.name = value;
        }
    }
    ```
    

---

1. `**정적 메소드 (Static)**` : 클래스의 인스턴스가 아닌 클래스 이름으로 곧바로 호출되는 메서드

---

1. `**클래스 상속 (Class Inheritance)**`
- `extends` 키워드를 사용한다.

```jsx
class Shape {
  constructor(width, height, color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }

  draw() {
    console.log(`drawing ${this.color} color of`);
  }

  getArea() {
    return this.width * this.height;
  }
}

class Triangle **extends** Shape {
  getArea() { 
		// method overriding : 상위 클래스의 메소드를 하위 클래스에서 재정의
    return (this.width * this.height) / 2;
  }

  draw() {
    super.draw(); // super : 부모클래스인 Shape 지칭
    console.log(`🔺`);
  }
}

const semo = new Triangle(300, 200, "blue");
console.log(semo.height) // 200
```

### 2.1.7  프로미스

- 비동기 작업 수행 시 콜백함수를 대체하여 유용하게 사용 가능
1. **state (상태)**
    1. `Pending (대기)` : 처리가 완료되지 않은 상태 (처리 **진행중**)
    2. `Fulfilled (이행)` : **성공**적으로 처리가 완료된 상태
    3. `Rejected (거부)` : 처리가 **실패**로 끝난 상태
    
    ---
    
2. **프로미스 핸들러** : 프로미스의 상태에 따라 실행되는 콜백 함수
    1. `.then()`: 프로미스가 **이행(fulfilled)**되었을 때 실행할 콜백 함수 등록, 새로운 프로미스를 반환
    2. `.catch()` : 프로미스가 **거부(rejected)**되었을 때 실행할 콜백 함수 등록, 새로운 프로미스를 반환
    3. `.finally()` : 프로미스 **이행/거부 여부에 상관없이** 실행할 콜백 함수를 등록, 새로운 프로미스를 반환
    
    ```jsx
    const myPromise = new Promise((resolve, reject) => {
        const data = fetch('서버로부터 요청할 URL');
    
        if(data)
        	resolve(data); // 요청이 성공하여 데이터가 있다면
        else
        	reject("Error"); // 요청이 실패하여 데이터가 없다면
    })
    
    myPromise
        .then((value) => { // 성공적으로 수행했을 때 실행될 코드
        	console.log("Data: ", value); // data 값
        })
        .catch((error) => { // 실패했을 때 실행될 코드
         	console.error(error); // "Error"
        })
        .finally(() => { // 성공하든 실패하든 무조건 실행될 코드
        	
        })
    ```
    
    ---
    
3. **프로미스 체이닝** 
    - 프로미스 핸들러를 연달아 연결하는 것.
    - 여러 개의 비동기 작업을 순차적으로 수행 가능
    
    ---
    
4. **주요 정적 메소드**
    1. `Promise.resolve()` : 인자로 전달된 값을 resolve하는 프로미스 생성
    2. `Promise.reject()` : 인자로 전달된 값을 reject하는 프로미스 생성
    3. `Promise.all()` : 여러 개의 비동기 처리를 한꺼번에 처리할 때 사용

### 2.1.8  async / await

- Promise를 더 쉽고 간결하게 사용하게 해주는 문법!
- `async` 함수의 리턴값은 **무조건 Promise**이다.
- 에러를 발생시킬 때는 `throw`를 사용, 에러를 잡을 때는 `try/catch` 문을 사용
- `await` 은 비동기 처리가 완료될 때까지(resolve) 코드 실행을 일시 중지하고 기다린다. → `async` 함수 내부에서만 사용 가능
    
    ```jsx
    async function getDataOne() {
        const result = await fetchData() // 데이터를 가져오는데 3초의 시간이 걸린다면 이를 기다려줌
        return result
    }
    
    async function getDataTwo() {
        const result = await fetchData() // 데이터를 가져오는데 3초의 시간이 걸린다면 이를 기다려줌
        return result
    }
    
    async function getDataThree () {
        const data1 = await getDataOne() // 3초의 시간이 걸림
        const data2 = await getDataTwo() // data1 가져온 뒤 실행. 3초의 시간이 걸림
        return `${data1}, ${data2}`
    }
    
    getDataThree().then(console.log) // 데이터를 다 가져운 뒤 콘솔에 출력 (6초 소요)
    ```
    

### 2.1.9  Map/Set

- `map`: 키 자료형에 제약이 없는 자료구조 (**객체**와 유사)
    
    **‼ 객체도 키로 사용할 수 있다**
    
    - 주요 메소드 및 프로퍼티
        - `new Map()` : 맵 생성
        - `map.set(key, value)` : key와 함께 value 등록
        - `map.get(key)` : key에 해당하는 value를 반환. ( key가 존재하지 않으면 undefined 반환 )
        - `map.has(key)` : key가 존재하면 true, 존재하지 않으면 false 반환
        - `map.delete(key)` : key와 함께 value 삭제
        - `map.clear()` : 맵의 모든 요소 삭제
        - `map.size` : 요소들의 개수 반환
- `set` : 중복을 허용하지 않은 유일한 값의 집합 (**배열**과 유사)
    - 주요 메소드
        - `new Set(iterable)` : set 생성. iterable 객체를 받으면(배열) 그 안의 값을 복사하여 set에 넣어줌.
        - `set.add(value)` : 값을 추가한다. (자신을 반환함)
        - `set.delete(value)` : 값을 제거한다. 제거에 성공하면 true, 아니면 false 반환
        - `set.has(value)` : Set에 값이 존재하면 true를 반환
        - `set.clear()` : Set을 초기화
        - `set.size` : Set에 몇 개가 들었는지 개수를 반환

### 2.1.10  널 병합/옵셔널 체이닝

- 널 병합 연산자 : `??`
    
    ```jsx
    const foo = null ?? 'default string';
    console.log(foo); // "default string"
    ```
    
    → 좌항(null)의 값이 **null이나 undefined면** **우항**을('default string') 반환하고, 아니면 좌항을(null) 반환한다.
    
- 옵셔널 체이닝 연산자 : `?.`
    
    ```jsx
    const name = person?.name
    ```
    
    → 좌항(person)이 **undefined나 null이면 좌항(person)**을 반환하고, 그렇지 않으면 우항(person.name)을 반환한다
    

## 2.2  프론트엔드 자바스크립트

### 2.2.1  AJAX

- **`AJAX** (**Asynchronous JavaScript and XML**)` : 자바스크립트를 이용해 비동기 방식으로 서버에 데이터를 요청하는 통신 기능.
- 클라이언트에서 서버로 데이터를 요청하고 결과를 응답받을 수 있다

### 2.2.2  FormData

- HTML form 태그의 데이터(속상/값)를 동적으로 제어할 수 있는 기능

### 2.2.3  encodeURIComponent, decodeURIComponent

- `encodeURIComponent` : URI의 특정한 문자를 인코딩해주는 함수
- `decodeURIComponent` : 인코딩한 문자열을 디코딩하는 함수

### 2.2.4  데이터 속성과 dataset

- `HTML`에서 `데이터 속성` 지정하기
    
    ```html
    <div
    	data-user-name="Sarang"
    	data-index="12"
    	data-default="hungry"
    	data-favorite-food="fries"
    >
    </div>
    ```
    
- `Javascript`에서 `dataset`속성으로 접근하기
    
    ```jsx
    const div = document.querySelector('div');
    div.dataset 
    // {userName : 'Sarang', index: '12', default : 'hungry', favoriteFood : 'fries'}
    // -(dash)로 표현된 것들은 camelCase로 변환됨
    ```
    
- `CSS`에서도 접근이 가능하다
    
    ```css
    div[data-user-name='Sarang']{
    	width : 100px;
    }
    ```