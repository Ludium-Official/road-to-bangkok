# Transient Storage
Smart Contract 내에서 임시 데이터를 저장하는 데 사용되는 'memory' 타입의 변수를 의미합니다. function 호출이 끝나면 사라지며, 블록체인에 영구적으로 저장되지 않습니다.

#### Transient Storage의 특성 
- 임시 저장 : 'memory' 키워드를 사용하여 선언된 변수들은 function 호출 동안에만 존재하며, 함수가 끝나면 소멸됩니다.
- 저장 비용 없음 : 블록체인에 영구적으로 저장되지 않기 때문에 저장 비용이 발생하지 않습니다.
- 빠른 접근 속도 : 영구 저장소인 'storage'에 비해 접근 속도가 빠릅니다.

## 예제 코드
```bash
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

// Make sure EVM version and VM set to Cancun

// Storage - 데이터가 블록체인에 저장됩니다.
// Memory - function 호출 후 데이터가 삭제됩니다.

interface ITest {
    function val() external view returns (uint256);
    function test() external;
}

contract Callback {
    uint256 public val;

    // fallback 함수는 호출된 함수가 존재하지 않을 때 호출됩니다.
    fallback() external {
        val = ITest(msg.sender).val();
    }

    // target 주소의 ITest 인터페이스의 test 함수를 호출합니다.
    function test(address target) external {
        ITest(target).test();
    }
}

contract TestStorage {
    uint256 public val;

    // val 변수를 123으로 설정하고, 호출자의 주소로 빈 데이터를 보냅니다.
    function test() public {
        val = 123;
        bytes memory b = "";
        (bool success, ) = msg.sender.call(b);
        require(success, "Call failed");
    }
}

contract TestTransientStorage {
    uint256 private _transientVal; // 임시 값을 저장하기 위한 변수

    // _transientVal 변수를 321로 설정하고, 호출자의 주소로 빈 데이터를 보냅니다.
    // 이후 임시 값을 0으로 재설정하여 삭제합니다.
    function test() public {
        _transientVal = 321;
        bytes memory b = "";
        (bool success, ) = msg.sender.call(b);
        require(success, "Call failed");
        _transientVal = 0; // 호출 후 임시 값을 수동으로 삭제
    }

    // _transientVal 변수 값을 반환합니다.
    function val() public view returns (uint256) {
        return _transientVal;
    }
}

contract ReentrancyGuard {
    bool private locked; // 잠금 상태를 저장하기 위한 변수

    // Reentrancy 방지를 위한 modifier
    modifier lock() {
        require(!locked, "ReentrancyGuard: reentrant call");
        locked = true;
        _;
        locked = false;
    }

    // 35313 gas
    // 잠금 상태를 체크하고 호출자의 주소로 빈 데이터를 보냅니다.
    function test() public lock {
        // 호출 오류 무시
        bytes memory b = "";
        (bool success, ) = msg.sender.call(b);
        require(success, "Call failed");
    }
}

contract ReentrancyGuardTransient {
    bool private locked; // 잠금 상태를 저장하기 위한 변수

    // Reentrancy 방지를 위한 modifier
    modifier lock() {
        require(!locked, "ReentrancyGuard: reentrant call");
        locked = true;
        _;
        locked = false;
    }

    // 21887 가스 사용
    // 잠금 상태를 체크하고 호출자의 주소로 빈 데이터를 보냅니다.
    function test() external lock {
        // 호출 오류 무시
        bytes memory b = "";
        (bool success, ) = msg.sender.call(b);
        require(success, "Call failed");
    }
}

```


## Remix에서 실습 
1. Remix에서 새로운 solidity 파일 생성해서 예제 코드를 복사 붙여넣기 합니다.
2. 예제 코드를 compile 후 deploy합니다.
3. 아래 버튼들이 제대로 동작하는지 확인합니다.

- Transaction이 완료한 후 데이터가 삭제되므로 val값이 0으로 반환됩니다. <br>

<img src= "https://github.com/Joon2000/Solidity-modules/blob/0382b9c321a2afdd01abcff6d0703dbdecddc9d5/images/transientstorage/transientstorage.png" width="300px" height="200px" 
  title="getStateVariable" alt="getStateVariable"><br/>
