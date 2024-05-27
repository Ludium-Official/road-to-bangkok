### Solidity의 Enum (열거형)

Solidity에서 `enum`은 여러 상태나 선택지를 표현하기 위해 사용되는 데이터 타입입니다.
`enum`는 코드의 가독성을 높이고 상태 관리의 명확성을 제공합니다.

### Enum의 정의 및 사용

#### Enum 정의

`enum`은 스마트 계약 내에서 또는 외부 파일에서 정의할 수 있습니다. `enum`의 기본 정의는 다음과 같습니다.

```solidity
enum <이름> {
    <값1>,
    <값2>,
    <값3>,
    ...
}
```

각 값은 정수로 매핑되며, 첫 번째 값은 0부터 시작합니다.

#### 예제 코드

다음 예제는 배송 상태를 나타내는 `enum`을 정의하고 사용하는 예제입니다:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Enum {
    // 배송 상태를 나타내는 Enum 정의
    enum Status {
        Pending,   // 0
        Shipped,   // 1
        Accepted,  // 2
        Rejected,  // 3
        Canceled   // 4
    }

    // 기본값은 Enum 정의의 첫 번째 값으로 설정됩니다. 여기서는 "Pending"
    Status public status;

    // 상태 값을 반환하는 함수
    function get() public view returns (Status) {
        return status;
    }

    // 상태 값을 업데이트하는 함수
    function set(Status _status) public {
        status = _status;
    }

    // 특정 Enum 값으로 상태를 업데이트하는 함수
    function cancel() public {
        status = Status.Canceled;
    }

    // 상태를 초기값으로 재설정하는 함수
    function reset() public {
        delete status; // 기본값인 Pending으로 재설정
    }
}
```

### Enum의 선언 및 가져오기

Solidity에서는 `enum`을 별도의 파일에서 선언하고 이를 다른 파일에서 가져와 사용할 수 있습니다. 이렇게 하면 코드의 재사용성을 높이고 모듈화를 촉진할 수 있습니다.

#### Enum 선언 파일

다음은 `enum`을 별도의 파일에서 선언하는 예제입니다. 이 파일은 `EnumDeclaration.sol`로 저장됩니다.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

// Enum 선언
enum Status {
    Pending,
    Shipped,
    Accepted,
    Rejected,
    Canceled
}
```

#### Enum 가져오기 파일

이제 다른 파일에서 앞에서 선언한 `enum`을 가져와 사용할 수 있습니다.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import "./EnumDeclaration.sol";

contract Enum {
    Status public status;
}
```

### `enum`의 장점

`enum`을 사용하면 얻을 수 있는 장점은 다음과 같습니다.

1. **가독성**: `enum`을 사용하면 상태나 선택지를 의미 있는 이름으로 표현할 수 있어 코드의 가독성이 높아집니다.
2. **안전성**: 정수 값 대신 명확한 이름을 사용하므로 실수로 잘못된 값을 설정하는 위험이 줄어듭니다.
3. **기본값**: `enum`의 기본값은 정의된 첫 번째 값입니다. 필요에 따라 이를 변경할 수 있습니다.
4. **메모리 관리**: `enum`은 내부적으로 정수로 처리되므로 메모리 사용이 효율적입니다.

### Remix 실습

1. [Remix IDE](https://remix.ethereum.org/)에 접속합니다.
2. 새 파일을 만들어 위 예제 코드를 복사하여 붙여넣고 파일을 저장합니다.
3. 좌측 메뉴에서 "Solidity 컴파일러"를 이용해 코드를 컴파일하고, Deploy합니다.

##### 기능확인

- **초기 상태 확인**
    - 배포 직후, `getStatus` 버튼을 클릭하면 기본값으로 `Pending (0)` 상태가 반환되는 것을 확인합니다.

- **상태 업데이트**
    - `setStatus` 함수에 `1` (Shipped)를 입력하고 `transact` 버튼을 클릭합니다.
    - `getStatus` 버튼을 클릭하여 상태가 `Shipped (1)`으로 업데이트된 것을 확인합니다.

- **특정 상태로 업데이트**
    - `cancel` 버튼을 클릭합니다.
    - `getStatus` 버튼을 클릭하여 상태가 `Canceled (4)`로 업데이트된 것을 확인합니다.

- **상태 재설정**
    - `reset` 버튼을 클릭합니다.
    - `getStatus` 버튼을 클릭하여 상태가 초기값인 `Pending (0)`으로 재설정된 것을 확인합니다.

![image](https://github.com/Joon2000/Solidity-modules/assets/69339099/5a021570-5abe-4eae-a181-147641783524)

![image](https://github.com/Joon2000/Solidity-modules/assets/69339099/77b1aaea-59fe-4531-baad-e1c4756b4460)

![image](https://github.com/Joon2000/Solidity-modules/assets/69339099/d7b6b3da-b2c1-46be-8ac3-2bfdcedefd4f)

![image](https://github.com/Joon2000/Solidity-modules/assets/69339099/da6fbfa6-db52-4069-a271-5da3871d3968)





