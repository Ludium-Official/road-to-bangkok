DataLocations
=============
data location은 변수 저장 및 처리 방식에 관한 개념으로, 효율성과 보안을 고려한 다양한 메모리 영역을 제공합니다.<br/>
solidity에는 'storage', 'memory', 'calldata'의 세가지 주요 데이터 위치가 있습니다.

Storage
-------
- 특성: 영구 저장 공간
- 위치: 블록체인 상태에 저장
- 비용: 읽기와 쓰기가 비싸다
- 용도: 컨트랙트 상태 변수, 즉 컨트랙트가 종료되더라도 유지되어야 하는 데이터

Memory
-------
- 특성: 임시 저장 공간
- 위치: 함수 호출 동안만 존재하며, 함수가 종료되면 사라짐
- 비용: 읽기와 쓰기 모두 상대적으로 저렴함
- 용도: 함수내에서 임시로 데이터를 저장하고 처리할 때

Calldata
--------
- 특성: 읽기 전용, 불변 데이터 위치
- 위치: 함수 호출 시 전달된 입력 데이터
- 비용: 가스 비용이 적으며, 변경할 수 없음
- 용도: 외부 함수 호출 시 전달되는 인수로, 값이 변경되지 않음을 보장할 때 사용

예제 코드
--------
## Data Locations 예제
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract DataLocations {
    // 상태 변수는 storage에 저장됩니다.
    uint256[] public arr;
    mapping(uint256 => address) map;

    struct MyStruct {
        uint256 foo;
    }

    mapping(uint256 => MyStruct) myStructs;

    function f() public {
        // 상태 변수를 참조하여 _f 함수 호출
        _f(arr, map, myStructs[1]);

        // 매핑에서 구조체를 가져오기 (storage 위치)
        MyStruct storage myStruct = myStructs[1];
        // 메모리에 구조체 생성 (memory 위치)
        MyStruct memory myMemStruct = MyStruct(0);
    }

    // storage 위치의 변수를 인수로 받는 내부 함수
    function _f(
        uint256[] storage _arr,
        mapping(uint256 => address) storage _map,
        MyStruct storage _myStruct
    ) internal {
        // storage 변수와 관련된 작업 수행
    }

    // memory 위치의 배열을 반환하는 함수
    function g(uint256[] memory _arr) public returns (uint256[] memory) {
        // memory 배열과 관련된 작업 수행
    }

    // calldata 위치의 배열을 사용하는 외부 함수
    function h(uint256[] calldata _arr) external {
        // calldata 배열과 관련된 작업 수행
    }
}

```

예제코드 설명
----------
1. Storage 변수
- 'arr', 'map', 'myStructs'는 모두 상태 변수로, 이들은 'storage'에 저장됩니다. 즉, 컨트랙트가 배포된 후에도 지속적으로 유지되는 데이터 입니다.
2. 함수 f()
  
```solidity
function f() public {
        _f(arr, map, myStructs[1]);
        MyStruct storage myStruct = myStructs[1];
        MyStruct memory myMemStruct = MyStruct(0);
    }
```

-  `_f(arr, map, myStructs[1]);`: 'storage' 위치의 상태 변수를 인수로 전달합니다.
-  `MyStruct Storage myStruct = myStructs[1];`: 'storage'에서 구조체를 가져와 참조를 저장합니다.
-  `MyStruct memory myMemStruct = MyStruct(0);`: 메모리에서 구조체를 생성합니다. 이 구조체는 'f' 함수 실행중에만 존재합니다.

3. 내부 함수 _f()
```solidity
function _f(
  uint256[] storage _arr,
  mapping(uint256 => address) storage _map,
  MyStruct storage _myStruct
) internal{ ... }
```
- 'storage' 위치의 변수를 인수로 받습니다. 이는 '_f'함수가 호출될 때 전달된 상태 변수를 직접 수정할 수 있음을 의미합니다.

4. 함수 g()
```solidity
function g(uint256[] memory _arr) public returns (uint256[] memory){ ... }
```
- 'memory' 위치의 배열을 인수로 받고, 'memory' 위치의 배열을 반환합니다. 메모리에서 작업을 수행하며, 함수 실행 중에만 유효합니다.

5. 함수 h()
```solidity
function h(uint256[] calldata _arr) external{ ... }
```
- 'calldata' 위치의 배열을 인수로 받습니다. 'calldata'는 함수 호출 시 입력 데이터가 저장되는 위치로, 읽기 전용이며 가스 비용이 적습니다.
<br/>

Remix에서 실습
---------
1. Remix에서 새로운 solidity 파일을 생성합니다.
2. 예제 코드에서 코드가 제대로 작동하도록 함수의 내용을 아래와 같이 수정한 코드를 복사 붙여넣기 합니다.
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract DataLocations {
    uint256[] public arr;
    mapping(uint256 => address) public map;

    struct MyStruct {
        uint256 foo;
    }

    mapping(uint256 => MyStruct) public myStructs;

    // 상태 변수를 초기화하는 함수
    function initialize() public {
        arr.push(1);
        arr.push(2);
        arr.push(3);
        map[1] = msg.sender;
        myStructs[1] = MyStruct(42);
    }

    function f() public {
        // 상태 변수를 참조하여 _f 함수 호출
        _f(arr, map, myStructs[1]);

        // 매핑에서 구조체를 가져오기 (storage 위치)
        MyStruct storage myStruct = myStructs[1];
        // storage 구조체 값을 변경
        myStruct.foo = 100;

        // 메모리에 구조체 생성 (memory 위치)
        MyStruct memory myMemStruct = MyStruct(0);
        myMemStruct.foo = 200;
    }

    // storage 위치의 변수를 인수로 받는 내부 함수
    function _f(
        uint256[] storage _arr,
        mapping(uint256 => address) storage _map,
        MyStruct storage _myStruct
    ) internal {
        // storage 변수와 관련된 작업 수행
        _arr.push(4); // arr 배열에 값 추가
        _map[2] = msg.sender; // map에 새로운 키-값 쌍 추가
        _myStruct.foo = 50; // 구조체 값 변경
    }

    // memory 위치의 배열을 반환하는 함수
    function g(uint256[] memory _arr) public pure returns (uint256[] memory) {
        // memory 배열과 관련된 작업 수행
        uint256[] memory newArray = new uint256[](_arr.length);
        for (uint256 i = 0; i < _arr.length; i++) {
            newArray[i] = _arr[i] * 2;
        }
        return newArray;
    }

    // calldata 위치의 배열을 사용하는 외부 함수
    function h(uint256[] calldata _arr) external pure returns (uint256) {
        // calldata 배열과 관련된 작업 수행
        uint256 sum = 0;
        for (uint256 i = 0; i < _arr.length; i++) {
            sum += _arr[i];
        }
        return sum;
    }

    // 배열 길이를 반환하는 함수
    function getArrLength() public view returns (uint256) {
        return arr.length;
    }

    // 배열 요소를 반환하는 함수
    function getArrElement(uint256 index) public view returns (uint256) {
        require(index < arr.length, "Index out of bounds");
        return arr[index];
    }

    // 특정 구조체 값을 반환하는 함수
    function getMyStruct(uint256 key) public view returns (uint256) {
        return myStructs[key].foo;
    }
}

```
3. 아래 버튼들이 제대로 동작하는지 확인합니다.

### data setting

- initilaize를 호출하고 getArrLength와 getArrElement 함수를 호출하여 배열의 길이와 각 요소를 확인합니다.
<img src = "/images/DataLocations/data_setting.png">


### f 함수 호출
- f 함수를 호출하면 arr 배열에 4가 추가되고, myStructs[1]의 foo 값이 변경됩니다.
- getArrLength와 getArrElement 함수를 호출하고 값을 확인합니다.
- getMyStruct(1) 함수로 foo 값이 100인지 확인합니다.
<img src = "/images/DataLocations/f_function.png">

### g 함수 호출
- 배열 입력란에 [1,2,3]과 같은 배열을 입력하고 g 함수를 호출합니다.
- 반환된 배열 값 [2,4,6]을 확인합니다.
<img src = "/images/DataLocations/g_function.png">

### h 함수 호출
- 배열 입력란에 [1,2,3]과 같은 배열을 입력하고 h 함수를 호출합니다.
- 반환된 합계 값 6을 확인합니다.
<img src = "/images/DataLocations/h_function.png">
