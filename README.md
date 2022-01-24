## 만들면서 배우는 클린 아키텍처
- [진행 방식](./HOWTO.md)  

## BuckPal 요구사항 분석
- [ ] 돈을 주고받는 API를 만든다.
```text
Request
POST /accounts/send/{sourceAccountId}/{targetAccountId}/{amount}

Response
void
```

### Validation
- [ ] 기본 타입보다는 일급 컬렉션을 활용한다.
- [ ] Validator를 활용해 입력값에 대한 validate를 진행한다.  
  - [ ] (validate) sourceAccountId는 null이 될 수 없다.  
  - [ ] (validate) targetAccountId는 null이 될 수 없다.  
  - [ ] (validate) money는 null이 될 수 없다.  

### Withdraw, Deposit
- [ ] 송금할 수 있는 최대 금액은 1_000_000원이다.
- [ ] 계좌 조회 시 10일 전을 기준으로 활성화되어있는 계좌인지 조회한다.  
- [ ] 계좌 조회 시 10일 전 이후로 계좌 합산 금액이 0원보다 커야한다.
- [ ] 송금 시 송금 계좌에 lock을 건다.  
- [ ] 입금 시 입금 계좌에 lock을 건다.  
  - 순서는 송금, 입금 순으로 lock을 건다.   
- [ ] 송금, 입금이 완료되면 activity 상태를 업데이트해준다.  
- [ ] 송금, 입금이 완료되면 각 계좌를 락 해제한다.

### Activity
- [ ] Activity는 계좌 간의 송금 활동을 나타낸다.   
- [ ] Activity를 등록하고 계좌 간의 송금/입금을 진행한다.  
- [ ] 이 activity를 소유한 계정, source, target 계정을 가진다.  
- [ ] activity의 타임스탬프를 갖는다.
- [ ] 계좌 간에 전달된 금액을 갖는다.  

### Activity Window
- [ ] Activity 여러개를 담고 있는 뷰를 ActivityWindow라고 칭한다.  
- [ ] 가장 첫번째의 activity를 반환할 수 있다. 
- [ ] 가장 마지막의 activity를 반환할 수 있다.
- [ ] window 간의 모든 activities의 값을 더해 잔액을 응답할 수 있다.  
- [ ] window가 담고있는 activities는 null이 될 수 없다.  
