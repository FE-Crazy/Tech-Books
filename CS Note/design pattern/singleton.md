# 싱글톤 패턴

싱글톤 패턴은 **하나의 클래스**에 오직 **하나의 인스턴스**만 가지는 패턴 ! 

- 보통 데이터베이스 연결 모듈에 많이 사용
- 하나의 인스턴스를 만들어 놓고 해당 인스턴스를 다른 모듈들이 공유하며 사용하기 때문에 인스턴스 생성할 때 드는 비용이 적다. 반면에 의존성이 높아진다는 단점이 있음.

```jsx
const obj = { a: 27 }
const obj2 = { a: 27}
console.log(obj === obj2) // 다른 인스턴스를 가진다.

class Singleton {
    constructor() {
        if (!Singleton.instance) {
            Singleton.instance = this
        }
        return Singleton.instance
    }
    getInstance() {
        return this.instance
    }
}
const a = new Singleton()
const b = new Singleton() 
console.log(a === b) // a,b는 Singleton.instance를 가르킨다. 
```

## 데이터 베이스 연결 모듈

```jsx
const URL = 'mongodb://localhost:27017/kundolapp'
const createConnection = url => ({"url" : url})    
class DB {
    constructor(url) {
        if (!DB.instance) { 
            DB.instance = createConnection(url)
        }
        return DB.instance
    }
    connect() {
        return this.instance
    }
}
const a = new DB(URL)
const b = new DB(URL) 
console.log(a === b) // true
/*
a, b는 DB 인스턴스 기반으로 생성 되었습니다. 이를 통해  인스턴스 생성 비용을 아낄 수 있습니다.
*/
```

실제로 싱글톤 패턴은 node.js 에서 mongoDB 데이터 베이스에서 연결할 때 쓰는 mongoose모듈에서 볼 수 있습니다.  mongoose의 데이터베이스를 연결할 때 쓰는 connect()라는 함수는 싱글톤 인스턴스를 반환,

## 단점

싱글톤 패턴은 TDD를 할 때 걸림돌이 됩니다. TDD는 단위 테스트를 주로 하는데, **단위 테스트는 테스트가 서로 독립적이어야** 하며 테스트를 어떤 순서로든 실행할 수 있습니다. 

하지만 싱글톤 패턴은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이므로 각 테스트마다 독립적인 인스턴스 만들기가 어려움.

### 의존성 주입

싱글톤 패턴은 사용하기가 쉽고 실용적이지만, 모듈 간의 결합을 강하게 만들 수 있다는 단점. 의존성 주입을 통해 모듈간의 결합을 조금 더 느슨하게 만들 수 있다.

<aside>
💡 의존성이란 종속성이라고도 하며 A가 B에 의존성이 있다는 것은 B의 변경 사항에 A또한 같이 변해야한다는 것을 의미.

</aside>

### 의존성 주입의 장점

모듈을 쉽게 교체할 수 있는 구조가 되어 테스팅하기 쉽고 마이그레이션하기도 수월하다.

구현할 때 추상화 레이어를 넣고 이를 기반으로 구현체를 넣어 주기 때문에 애플리케이션 의존성 뱡향이 일관되고, 쉽게 추론할 수 있으며, 모듈간의 관계들이 명확 ! 

### 의존성 주입의 단점

모듈들이 분리되므로 클래수 수가 늘어나는 복잡성이 증가될 수 있으며, 런타임(프로그램이 실행되고 있는 동안의 동작) 패널티가 생기기도합니다.