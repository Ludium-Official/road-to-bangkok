### Solidity의 View 및 Pure Function

Solidity에서 함수는 상태를 변경할 수 있는지 여부에 따라 `view`와 `pure`로 구분할 수 있습니다.
이 두 가지 함수 타입은 스마트 계약의 상태를 안전하게 관리하고, 상태를 변경하지 않도록 보장하는 데 매우 유용합니다.

### View 함수

**`view` 함수**는 상태 변수를 읽을 수 있지만, 상태를 변경할 수 없음을 명시적으로 보장하는 함수입니다.

- **특징**:
    - 상태 변수의 값을 읽을 수 있습니다.
    - 상태를 변경하는 연산은 수행할 수 없습니다.
    - 상태를 변경하는 함수 호출도 불가능합니다.
- **예제**:
  ```solidity
  // SPDX-License-Identifier: MIT
  pragma solidity ^0.8.24;

  contract ViewExample {
      uint256 public x = 1;

      // 상태를 변경하지 않음을 보장하는 함수
      function addToX(uint256 y) public view returns (uint256) {
          return x + y;
      }
  }
  ```
  위 예제에서 `addToX` 함수는 상태 변수 `x`를 읽어서 `y`와 더한 값을 반환합니다. 이 함수는 상태를 변경하지 않음을 보장하므로 `view`로 선언되었습니다.

### Pure 함수

**`pure` 함수**는 상태 변수를 읽거나 변경하지 않음을 명시적으로 보장하는 함수입니다.

- **특징**:
    - 상태 변수를 읽거나 변경할 수 없습니다.
    - 블록체인 상의 상태에 의존하지 않는 계산을 수행합니다.
    - 주어진 인자만을 사용하여 결과를 반환합니다.
- **예제**:
  ```solidity
  // SPDX-License-Identifier: MIT
  pragma solidity ^0.8.24;

  contract PureExample {
      // 상태를 읽거나 변경하지 않음을 보장하는 함수
      function add(uint256 i, uint256 j) public pure returns (uint256) {
          return i + j;
      }
  }
  ```
  위 예제에서 `add` 함수는 두 입력 값 `i`와 `j`를 더한 결과를 반환합니다. 이 함수는 상태 변수에 의존하지 않으며, 상태를 변경하지 않기 때문에 `pure`로 선언되었습니다.

### View와 Pure 함수의 차이점

- **View 함수**: 상태 변수를 읽을 수 있지만, 상태를 변경하지 않습니다.
    - 예: 상태 변수를 읽어서 값을 계산하거나 반환하는 함수
    - `function viewFunction() public view returns (uint256)`

- **Pure 함수**: 상태 변수를 읽거나 변경하지 않습니다.
    - 예: 함수의 입력 값만을 사용하여 계산을 수행하는 함수
    - `function pureFunction(uint256 a, uint256 b) public pure returns (uint256)`

### 예제 코드

전체 예제 코드는 다음과 같습니다:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract ViewAndPure {
    uint256 public x = 1;

    // 상태를 변경하지 않음을 보장하는 함수
    function addToX(uint256 y) public view returns (uint256) {
        return x + y;
    }

    // 상태를 읽거나 변경하지 않음을 보장하는 함수
    function add(uint256 i, uint256 j) public pure returns (uint256) {
        return i + j;
    }
}
```

이 예제는 두 가지 타입의 함수를 포함하고 있으며, 각 함수가 상태를 어떻게 다루는지 보여줍니다. `addToX` 함수는 `view` 함수로, 상태 변수 `x`를 읽어서 사용하고 있으며, `add`
함수는 `pure` 함수로, 상태 변수와는 무관한 계산을 수행합니다.

### 예제 코드 설명

이 예제는 `view`와 `pure` 함수의 사용법을 보여주는 간단한 스마트 계약입니다.
두 가지 함수 모두 상태를 변경하지 않으며, 각기 다른 방식으로 상태와 상호작용하지 않음을 보장합니다.

##### 상태 변수

- `uint256 public x = 1;`
    - `x`는 상태 변수로, 스마트 계약의 저장소에 저장됩니다.
    - `public` 키워드를 사용하여 이 변수는 외부에서 읽을 수 있습니다.
    - 초기 값은 `1`로 설정되어 있습니다.

##### `view` 함수: `addToX`

- `function addToX(uint256 y) public view returns (uint256)`
    - 이 함수는 하나의 인자 `y`를 입력받습니다.
    - `view` 키워드는 이 함수가 상태 변수를 읽을 수 있지만, 변경할 수 없음을 보장합니다.
    - 함수는 상태 변수 `x`의 값과 입력받은 값 `y`를 더한 결과를 반환합니다.
    - 예를 들어, `addToX(5)`를 호출하면 `x`는 `1`이고 `y`는 `5`이므로, 반환 값은 `1 + 5 = 6`입니다.

##### `pure` 함수: `add`

- `function add(uint256 i, uint256 j) public pure returns (uint256)`
    - 이 함수는 두 개의 인자 `i`와 `j`를 입력받습니다.
    - `pure` 키워드는 이 함수가 상태 변수를 읽거나 변경하지 않음을 보장합니다.
    - 함수는 입력받은 두 값 `i`와 `j`를 더한 결과를 반환합니다.
    - 예를 들어, `add(3, 4)`를 호출하면 반환 값은 `3 + 4 = 7`입니다.

### Remix 실습

1. [Remix IDE](https://remix.ethereum.org/)에 접속합니다.
2. 새 파일을 만들어 위 예제 코드를 복사하여 붙여넣고 파일을 저장합니다.
3. 좌측 메뉴에서 "Solidity 컴파일러"를 이용해 코드를 컴파일하고, Deploy합니다.

##### 기능확인

- **초기 상태 확인**
    - 배포 직후, `x` 변수가 1로 초기화되어 있는지 확인합니다.
    - `x` 변수가 `1`인지 확인하려면 `x` 버튼을 클릭하여 값을 확인합니다.

- **view 함수 테스트 (`addToX`)**
    - `addToX` 함수에 임의의 값 (예: 5)을 입력하고 호출합니다.
    - `addToX(5)` 버튼을 클릭하여 반환값이 `6`(1+5)인지 확인합니다.
    - `x` 값이 변경되지 않았는지 확인합니다.

- **pure 함수 테스트 (`add`)**
    - `add` 함수에 두 개의 임의의 값 (예: 3과 4)을 입력하고 호출합니다.
    - `add(3, 4)` 버튼을 클릭하여 반환값이 `7`(3+4)인지 확인합니다.

![image](https://github.com/Joon2000/Solidity-modules/assets/69339099/2e61c307-721e-4112-ad01-12781827767a)
