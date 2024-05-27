# Function
Solidity에서 function은 Smart Contract 내에서 특정 작업을 수행하는 코드를 정의하는 데 사용됩니다. Function은 Smart Contract의 핵심 구성 요소로, 상태를 변경하거나 데이터를 조회하는 등의 작업을 수행할 수 있습니다.

## Function의 기본 구조
```solidity
function functionName(parameterList) visibility modifier returns (returnType) {
    // 함수 내용
}
```

### 구성 요소 설명

1. **이름 (Function Name)** : 함수의 이름을 지정합니다.
2. **매개변수 (Parameters)** : 함수가 입력으로 받을 값을 정의합니다. 각 매개변수는 타입과 함께 정의됩니다.
3. **가시성 (Visibility)** : 함수의 접근 범위를 지정합니다.
    - `public` : 누구나 호출할 수 있습니다.
    - `internal` : 동일한 계약 또는 상속받은 계약에서만 호출할 수 있습니다.
    - `private` : 오직 동일한 계약 내에서만 호출할 수 있습니다.
    - `external` : 계약 외부에서만 호출할 수 있습니다. 내부 호출 시에는 `this.functionName` 형태로 호출해야 합니다.
4. **수식어 (Modifiers)** : 함수의 동작을 제한하거나 특정 조건을 추가할 수 있습니다.
5. **반환 값 (Return Values)** : 함수가 반환할 값의 타입을 지정합니다.

이 구조를 통해 Solidity에서 함수를 정의하고 사용하는 방법을 이해할 수 있습니다.

## 예제 코드
Solidity에서 함수는 다양한 방법으로 출력을 반환할 수 있습니다. `public` 함수는 특정 데이터 타입을 입력이나 출력으로 받을 수 없습니다.

```bash
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Function {
    // 함수는 여러 값을 반환할 수 있습니다.
    function returnMany() public pure returns (uint256, bool, uint256) {
        return (1, true, 2);
    }

    // 반환 값을 이름으로 명명할 수 있습니다.
    function named() public pure returns (uint256 x, bool b, uint256 y) {
        return (1, true, 2);
    }

    // 반환 값을 이름에 할당할 수 있습니다.
    // 이 경우 return 문을 생략할 수 있습니다.
    function assigned() public pure returns (uint256 x, bool b, uint256 y) {
        x = 1;
        b = true;
        y = 2;
    }

    // 여러 값을 반환하는 다른 함수를 호출할 때 구조 분해 할당을 사용합니다.
    function destructuringAssignments()
        public
        pure
        returns (uint256, bool, uint256, uint256, uint256)
    {
        (uint256 i, bool b, uint256 j) = returnMany();

        // 값을 생략할 수 있습니다.
        (uint256 x,, uint256 y) = (4, 5, 6);

        return (i, b, j, x, y);
    }

    // 입력 또는 출력으로 맵을 사용할 수 없습니다.

    // 배열을 입력으로 사용할 수 있습니다.
    function arrayInput(uint256[] memory _arr) public {}

    // 배열을 출력으로 사용할 수 있습니다.
    uint256[] public arr;

    function arrayOutput() public view returns (uint256[] memory) {
        return arr;
    }
}

// 키-값 입력으로 함수 호출
contract XYZ {
    function someFuncWithManyInputs(
        uint256 x,
        uint256 y,
        uint256 z,
        address a,
        bool b,
        string memory c
    ) public pure returns (uint256) {}

    function callFunc() external pure returns (uint256) {
        return someFuncWithManyInputs(1, 2, 3, address(0), true, "c");
    }

    function callFuncWithKeyValue() external pure returns (uint256) {
        return someFuncWithManyInputs({
            a: address(0),
            b: true,
            c: "c",
            x: 1,
            y: 2,
            z: 3
        });
    }
}
```

### 여러 값을 반환하는 함수
Solidity에서는 함수가 여러 값을 반환할 수 있습니다.

#### returnMany 함수
```solidity
function returnMany() public pure returns (uint256, bool, uint256) {
    return (1, true, 2);
}
```
- 세 개의 값을 반환합니다: `1`, `true`, `2`.

#### named 함수
```solidity
function named() public pure returns (uint256 x, bool b, uint256 y) {
    return (1, true, 2);
}
```
- 반환 값을 이름으로 명명하여 반환합니다.

#### assigned 함수
```solidity
function assigned() public pure returns (uint256 x, bool b, uint256 y) {
    x = 1;
    b = true;
    y = 2;
}
```
- 반환 값을 이름에 할당합니다. 이 경우 `return` 문을 생략할 수 있습니다.

#### destructuringAssignments 함수
```solidity
function destructuringAssignments()
    public
    pure
    returns (uint256, bool, uint256, uint256, uint256)
{
    (uint256 i, bool b, uint256 j) = returnMany();

    // 값을 생략할 수 있습니다.
    (uint256 x,, uint256 y) = (4, 5, 6);

    return (i, b, j, x, y);
}
```
- 다른 함수를 호출하여 반환 값을 구조 분해 할당(destructuring assignment)할 수 있습니다.
- 특정 값을 생략할 수도 있습니다.

#### 입력 또는 출력으로 사용할 수 없는 데이터 타입
Solidity에서는 함수의 입력 또는 출력으로 맵을 사용할 수 없습니다.

#### 배열을 입력으로 사용하는 함수
```solidity
function arrayInput(uint256[] memory _arr) public {}
```
- 배열을 입력으로 받을 수 있습니다.

#### 배열을 출력으로 사용하는 함수
```solidity
uint256[] public arr;

function arrayOutput() public view returns (uint256[] memory) {
    return arr;
}
```
- 배열을 출력으로 반환할 수 있습니다.

#### 키-값 입력으로 함수 호출
키-값 쌍을 사용하여 함수를 호출할 수 있습니다.

#### someFuncWithManyInputs 함수
```solidity
function someFuncWithManyInputs(
    uint256 x,
    uint256 y,
    uint256 z,
    address a,
    bool b,
    string memory c
) public pure returns (uint256) {}
```
- 여러 입력을 받는 함수입니다.

#### callFunc 함수
```solidity
function callFunc() external pure returns (uint256) {
    return someFuncWithManyInputs(1, 2, 3, address(0), true, "c");
}
```
- 인자를 순서대로 전달하여 함수를 호출합니다.

#### callFuncWithKeyValue 함수
```solidity
function callFuncWithKeyValue() external pure returns (uint256) {
    return someFuncWithManyInputs({
        a: address(0),
        b: true,
        c: "c",
        x: 1,
        y: 2,
        z: 3
    });
}
```
- 키-값 쌍을 사용하여 함수를 호출합니다.



## Remix에서 실습 
1. Remix에서 새로운 solidity 파일 생성해서 예제 코드를 복사 붙여넣기 합니다.
2. 예제 코드를 compile 후 deploy합니다.
3. 아래 버튼들이 제대로 동작하는지 확인합니다.

-arrayOutput, destructingAssignments, named, returnMany 다양한 함수들이 다양하게 값을 반환해 주는 것을 확인할 수 있습니다.
<img src= "https://github.com/Joon2000/Solidity-modules/blob/2e8525911e6a259d8fb77654988e2ab1e854468d/images/function/functionoutputs.png" width="200px" height="400px" 
  title="functiono" alt="functiono"><br/>
-arrayInput에 값을 넣고 log를 확인해 본 결과입니다. 배열을 입력으로 사용할 수 있는 것을 확인할 수 있습니다.
<img src= "https://github.com/Joon2000/Solidity-modules/blob/2e8525911e6a259d8fb77654988e2ab1e854468d/images/function/functioninputlog.png" width="1000px" height="400px" 
  title="functioni" alt="functioni"><br/>
