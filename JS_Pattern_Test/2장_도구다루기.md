# 2장. 도구 다루기

- TDD는 코드 결함을 최대한 빨리, 곧 코드 생성 직후 감지하며, 작은 기능 하나라도 테스트를 먼저 작성한 뒤, 최소한의 코드만으로 기능을 구현한다.

---

길벗 - 자바스크립트 패턴과 테스트 Github

[https://github.com/gilbutITbook/006844](https://github.com/gilbutITbook/006844)

---

### 재스민 테스트 방법

```jsx
function createReservation(passenger, flight) {
  return {
    passengerInfomation: passenger,
    flightInfo: flight
  };
}
```

```jsx
describe('createReservation(passenger, flight)', function() {
// describe - 테스트 할 주제

	it('주어진 passenger를 passengerInfo 프로퍼티에 할당한다', function() {
	// it : 테스트의 각 TASK
	  var testPassenger = {
	    firstName: '윤지',
	    lastName: '김'
	  };
	
	  var testFlight = {
	    number: '3443',
	    carrier: '대한항공',
	    destination: '울산'
	  };
	
	  var reservation = createReservation(testPassenger, testFlight);

	  expect(reservation.passengerInfo).toBe(testPassenger);
		// expect : 개발자의 기대 결과
	});
...
```

- it단계에서 실패할 경우, 에러가 발생된다. 이를 통해서 오류를 확인하고 개선하면 된다.

[https://github.com/jasmine/jasmine](https://github.com/jasmine/jasmine)

> **다양한 테스트 프레임워크가 있으므로, 접근 가능한 테스트 프레임워크를 우선적으로 익숙해지는게 좋을 것으로 보임**
> 

---

### TDD를 사용함으로서 생기는 이점

1. 잘못된 코드 발견하기
2. 테스트성을 감안하여 설계하기
    - SOLID 개발 원칙을 준수하면 코드를 테스트할 때 도움이 됨
    테스트성을 설계 목표로 정하면 SOLID한 코드가 작성됨
    
    <aside>
    🔥 기능 하나하나에 단위 테스트를 붙이는 건 너무 힘드니, 빨리 다음 업무로 넘어가고픈 마음이 굴뚝같지만, 참아야한다.
    
    </aside>
    
3. 꼭 필요한 코드만 작성하기
    - TDD 작업절차 (반복)
        - 작은 기능 검증하기 : 실패하는 테스트 작성한 뒤, 테스트를 성공시킬 만큼만 최소한으로 코딩
        - 리팩토링 : 개발중인 코드에서 중복코드 제거
4. 안전한 유지 보수와 리팩토링
    - 프로젝트 제품 코드를 대상으로 확실한 단위 테스트 꾸러미를 구축 가능
5. 실행 가능한 명세
    - 탄탄하게 구축된 단위 테스트 꾸러미는 테스트 대상 코드의 실행 가능한 명세 역할도 함

---

### 의존성 주입

- 객체 또는 의존성 중 어느 하나라도 DB,  설정  파일, HTTP, 기타 인프라등의 외부 자원에 의존하는가?
- 객체 내부에서 발생할지 모를 에러를 테스트에서 고려해야 하나?
- 특정한 방향으로 객체를 작동시켜야 할 테스트가 있는가?
- 이 서드파티(third-party) 제공 객체가 아니라 온전히 내가 소유한 객체인가?

<aside>
🔥 위의 질문 중 하나라도 답변히 “예”라면, 직접 인스턴스화 하지 말고 주입하는 방향으로 생각을 전환하기

</aside>

---

<aside>
🔥 좋은 코드를 짜려면, 인자가 제대로 전달됐는지 타입은 올바른지 확인해야 한다**

</aside>

※ 참고

[DI(의존성주입) in JavaScript ! [번역]](https://velog.io/@moongq/Dependency-Injection)

[의존성 주입이란 무엇이며 왜 필요한가?](https://kotlinworld.com/64)