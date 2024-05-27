# Function Modifier
Solidity Smart Contract에서 Function Modifier는 함수 호출 전과 후에 실행될 수 있는 코드를 정의하는 데 사용됩니다. Function Modifier는 접근을 제한하거나, 입력값을 검증하거나, 재진입(reentrancy) 공격을 방지하는 등의 목적으로 활용될 수 있습니다.

## Function Modifier 개념

- **onlyOwner** : 함수가 호출될 때 호출자가 계약의 소유자인지 확인합니다. `require(msg.sender == owner, "Not owner");` 문을 통해 호출자가 소유자가 아니면 함수를 중단하고 오류 메시지를 반환합니다.
- **validAddress** : 입력된 주소가 유효한지 확인합니다. `require(_addr != address(0), "Not valid address");` 문을 통해 주소가 0인 경우 함수를 중단하고 오류 메시지를 반환합니다.
- **noReentrancy** : 재진입 공격을 방지합니다. 함수가 실행 중일 때 `locked` 변수를 사용하여 재진입을 방지하고, 함수 실행이 끝나면 `locked` 변수를 초기화합니다. 함수가 중복 실행되는 것을 방지할 수 있습니다.

## 예제 코드
소유자만 접근할 수 있는 기능, 주소 검증, 재진입 방지 기능을 구현합니다.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract FunctionModifier {
    // 이 변수들을 사용하여 함수 수정자의 사용법을 시연합니다.
    address public owner;
    uint256 public x = 10;
    bool public locked;

    constructor() {
        // 계약의 소유자를 트랜잭션의 발신자로 설정합니다.
        owner = msg.sender;
    }

    // 계약의 소유자인지 확인하는 수정자입니다.
    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        // 언더스코어(_)는 함수 수정자 내부에서만 사용되는 특별한 문자로,
        // Solidity에게 나머지 코드를 실행하도록 지시합니다.
        _;
    }

    // 입력된 주소가 유효한지 확인하는 수정자입니다.
    modifier validAddress(address _addr) {
        require(_addr != address(0), "Not valid address");
        _;
    }

    // 소유자를 변경하는 함수입니다.
    // 이 함수는 소유자만 호출할 수 있으며, 유효한 주소가 입력되어야 합니다.
    function changeOwner(address _newOwner)
        public
        onlyOwner
        validAddress(_newOwner)
    {
        owner = _newOwner;
    }

    // 함수가 실행 중일 때 재진입을 방지하는 수정자입니다.
    modifier noReentrancy() {
        require(!locked, "No reentrancy");

        locked = true;
        _;
        locked = false;
    }

    // 재진입 방지 기능이 적용된 함수입니다.
    function decrement(uint256 i) public noReentrancy {
        x -= i;

        if (i > 1) {
            decrement(i - 1);
        }
    }
}
```

### 예제 코드 설명

#### 상태 변수
- `address public owner;`: 계약의 소유자 주소를 저장합니다.
- `uint256 public x = 10;`: 예제에서 사용할 정수형 변수입니다.
- `bool public locked;`: 재진입 방지를 위한 상태 변수입니다.

#### 생성자
```solidity
constructor() {
    owner = msg.sender;
}
```
- 계약의 소유자를 현재 트랜잭션을 보낸 주소로 설정합니다.

#### onlyOwner 수정자
```solidity
modifier onlyOwner() {
    require(msg.sender == owner, "Not owner");
    _;
}
```
- 함수가 호출될 때 호출자가 소유자인지 확인합니다.

#### validAddress 수정자
```solidity
modifier validAddress(address _addr) {
    require(_addr != address(0), "Not valid address");
    _;
}
```
- 입력된 주소가 유효한지 확인합니다.

#### changeOwner 함수
```solidity
function changeOwner(address _newOwner)
    public
    onlyOwner
    validAddress(_newOwner)
{
    owner = _newOwner;
}
```
- 새로운 소유자를 설정하는 함수입니다. `onlyOwner`와 `validAddress` 수정자를 사용하여 접근을 제한하고 입력 값을 검증합니다.

#### noReentrancy 수정자
```solidity
modifier noReentrancy() {
    require(!locked, "No reentrancy");

    locked = true;
    _;
    locked = false;
}
```
- 재진입 공격을 방지하기 위한 수정자입니다.

#### decrement 함수
```solidity
function decrement(uint256 i) public noReentrancy {
    x -= i;

    if (i > 1) {
        decrement(i - 1);
    }
}
```
- `x` 값을 감소시키는 함수입니다. `noReentrancy` 수정자를 사용하여 재진입을 방지합니다.

## Remix에서 실습 
1. Remix에서 새로운 solidity 파일 생성해서 예제 코드를 복사 붙여넣기 합니다.
2. 예제 코드를 compile 후 deploy합니다.
3. 아래 버튼들이 제대로 동작하는지 확인합니다.

- 초기 값입니다. <br/>
<img src= "https://github.com/Joon2000/Solidity-modules/blob/01752bdda7fa47e51918004ff029d72416de6492/images/functionmodifier/fminit.png" width="250px" height="300px" 
  title="fminit" alt="fminit"><br/>
- decrement를 진행한 경우, noReentrancy가 실행돼서 decremency를 못 한다는 log 발생했습니다.
<img src= "https://github.com/Joon2000/Solidity-modules/blob/01752bdda7fa47e51918004ff029d72416de6492/images/functionmodifier/noreentrancy.png" width="1000px" height="100px" 
  title="noreentrancy" alt="noreentrancy"><br/>
- changeOwner owner가 아닌 주소로 실행하면 오류 발생합니다. owner로 실행하는 경우 정상적으로 작동합니다.
<img src= "https://github.com/Joon2000/Solidity-modules/blob/01752bdda7fa47e51918004ff029d72416de6492/images/functionmodifier/changeowner.png" width="1000px" height="200px" 
  title="changeowner" alt="changeowner"><br/>
