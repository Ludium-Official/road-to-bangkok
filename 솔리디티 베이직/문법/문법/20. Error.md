Error
=====
solidity에서 error처리는 크게 세 가지 주요 방법으로 나뉩니다.

### 1. assert
- `assert`는 내부적 오류를 체크하기 위해 사용됩니다. 보통 개발자가 작성한 코드에 문제가 있을 때 사용합니다.    
- 예를 들어, 논리적인 오류나 불변 조건이 깨질 때 사용합니다. `assert`는 실패할 경우, 모든 가스를 소비하고, 상태를 롤백합니다. 이는 매우 심각한 오류를 나타내며, 실제 배포된 코드에서는 주로 디버깅 목적으로 사용됩니다.

### 2. require
- `require`는 입력 값 검증 및 조건 체크에 사용됩니다.
- 이는 유효성 검사를 위해 주로 사용되며, 실패할 경우 남은 가스를 반환하고 상태를 롤백합니다.
- 사용자 입력, 계약 상호 작용 및 외부 호출을 검사할 때 주로 사용됩니다.

### 3. revert
- `revert`는 특정 조건이 만족되지 않았을 때, 거래를 취소하고 모든 상태 변경을 롤백하기 위해 사용됩니다.
- `require`와 비슷하지만, 더 복잡한 조건을 검사하거나 에러 메시지를 더 명확하게 전달할 때 사용됩니다.

예제코드
------
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Error {
    function testRequire(uint256 _i) public pure {
        // Require should be used to validate conditions such as:
        // - inputs
        // - conditions before execution
        // - return values from calls to other functions
        require(_i > 10, "Input must be greater than 10");
    }

    function testRevert(uint256 _i) public pure {
        // Revert is useful when the condition to check is complex.
        // This code does the exact same thing as the example above
        if (_i <= 10) {
            revert("Input must be greater than 10");
        }
    }

    uint256 public num;

    function testAssert() public view {
        // Assert should only be used to test for internal errors,
        // and to check invariants.

        // Here we assert that num is always equal to 0
        // since it is impossible to update the value of num
        assert(num == 0);
    }

    // custom error
    error InsufficientBalance(uint256 balance, uint256 withdrawAmount);

    function testCustomError(uint256 _withdrawAmount) public view {
        uint256 bal = address(this).balance;
        if (bal < _withdrawAmount) {
            revert InsufficientBalance({
                balance: bal,
                withdrawAmount: _withdrawAmount
            });
        }
    }
}

```

#### 1. testRequire
```solidity
function testRequire(uint256 _i) public pure {
    require(_i > 10, "Input must be greater than 10");
}

```

- 기능: 입력 값 `_i`가 10보다 큰지 확인합니다.
- 설명: `require`는 함수의 시작 부분에서 입력 값이나 조건을 검증하는 데 사용됩니다. 조건이 만족되지 않으면, "Input must be greater than 10"이라는 오류 메시지와 함께 트랜잭션이 취소됩니다.
- 사용 상황: 주로 입력 값의 유효성 검사, 함수 실행 전 상태 확인, 다른 함수 호출의 반환 값 검증 등에 사용됩니다.

#### 2. testRevert
```solidity
function testRevert(uint256 _i) public pure {
    if (_i <= 10) {
        revert("Input must be greater than 10");
    }
}

```

- 기능: 입력 값 `_i`가 10보다 큰지 확인합니다.
- 설명: `revert`는 조건이 복잡하거나 코드 내에서 여러 조건을 체크할 때 사용됩니다. 여기서는 `require`와 동일한 기능을 수행하지만, `if` 문을 통해 조건을 체크하고 조건이 만족되지 않으면 `revert`를 사용하여 트랜잭션을 취소합니다.
- 사용상황: 복잡한 조건을 체크하거나 명확한 오류 메시지를 제공하고 싶을 때 사용됩니다.

#### 3. testAssert
```solidity
uint256 public num;

function testAssert() public view {
    assert(num == 0);
}

```

- 기능: 상태 변수 `num`이 항상 0인지 확인합니다.
- 설명: `assert`는 내부 오류를 검사하거나 불변 조건을 확인하는데 사용됩니다. `assert`가 실패하면 모든 가스를 소비하고 트랜잭션을 롤백합니다. 여기서는 `num`이 절대 변경되지 않는다는 것을 보장하기 위해 사용됩니다.
- 사용 상황: 논리적 오류가 없음을 보장하거나, 상태가 변경되지 않음을 확인할 때 사용됩니다.

#### 4. 사용자 정의 에러 (InsufficientBalance)
```solidity
// custom error
error InsufficientBalance(uint256 balance, uint256 withdrawAmount);

function testCustomError(uint256 _withdrawAmount) public view {
    uint256 bal = address(this).balance;
    if (bal < _withdrawAmount) {
        revert InsufficientBalance({
            balance: bal,
            withdrawAmount: _withdrawAmount
        });
    }
}

```

- 기능: 인출하려는 금액 `_withdrawAmount`가 계약의 잔액 `bal`보다 작은지 확인합니다.
- 설명: 사용자 정의 에러는 가스 비용을 절약하고 더 명확한 오류 메시지를 제공하는데 유용합니다. 여기서는 `InsufficientBalance`라는 사용자 정의 에러를 정의하고, 조건이 충족되지 않으면 해당 에러를 발생시킵니다.
- 사용 상황: 복잡한 오류 상황을 처리하거나, 더 효율적인 에러 처리를 위해 사용자 정의 에러를 사용합니다.

<br/>

Remix에서 실습
-----------
1. Remix에서 새로운 solidity 파일을 생성해서 예제 코드를 복사 붙여넣기 합니다.
2. 예제 코드를 compile 후 deploy합니다.
3. 아래 버튼들이 제대로 동작하는지 확인합니다.

### 1. testRequire

- _i에 11 이상의 값을 전달하여 호출한 경우

<img src="/images/Error/error1.png" width=80% height=80%>

올바르게 작동되는 것을 확인할 수 있습니다.

- _i에 10이하의 값을 전달하여 호출한 경우

<img src="/images/Error/error2.png" width=80% height=80%>

에러가 발생하며 `Input must be greater than 10`라는 오류 메시지와 함께 트랜잭션이 취소됨을 확인할 수 있습니다.

### 2. testRevert

- _i에 11 이상의 값을 전달하여 호출한 경우

<img src="/images/Error/error3.png" width=80% height=80%>

올바르게 작동되는 것을 확인할 수 있습니다.

- _i에 10 이하의 값을 전달하여 호출한 경우

<img src="/images/Error/error4.png" width=80% height=80%>

에러가 발생하며 `Input must be greater than 10`라는 오류 메시지와 함께 트랜잭션이 취소됨을 확인할 수 있습니다.

### 3. testAssert

<img src="/images/Error/error5.png" width=80% height=80%>

`num`이 0으로 초기화되어 있으므로 조건이 만족되어 함수가 정상적으로 실행됩니다. 만약 `num`이 0이 아니면 `assert`가 실패하고 모든 가스를 소모하며 트랜잭션이 실패합니다.

### 4.testCustomError

<img src="/images/Error/error6.png" width=80% height=80%>

계약의 잔액이 `_withdrawAmount`보다 작으므로 `InsufficientBalace` 오류가 발생하고 트랜잭션이 실패합니다. 만약 잔액이 충분하다면 함수가 정상적으로 실행됩니다.

