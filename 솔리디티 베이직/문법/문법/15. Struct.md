## Struct란 무엇인가?

Struct(구조체)는 Solidity에서 사용자 정의 데이터 타입을 정의하는 데 사용됩니다. 구조체는 여러 필드를 포함할 수 있으며, 이 필드들은 서로 다른 데이터 타입을 가질 수 있습니다. Struct는 관련 데이터를 그룹화하여 더 쉽게 관리할 수 있도록 합니다.

## Struct의 기본 구조

```solidity
// struct 정의
struct Person {
    string name;
    uint age;
    address wallet;
}
```

## struct 접근하기

구조체의 멤버에 접근하기 위해 멤버 접근 연산자(.)를 사용합니다. 멤버 접근 연산자는 구조체 변수 이름과 접근하려는 구조체 멤버 사이에 마침표를 넣어 작성합니다. 구조체를 사용하여 구조체 타입의 변수를 정의하고 이를 통해 멤버에 접근할 수 있습니다.  

아래 예제 코드를 통해 구조체를 정의하고 접근하는 법을 배워봅시다. 

## 예제 코드

다음 코드는 Solidity에서 구조체를 사용하는 방법을 보여줍니다.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Test {
    // 구조체 정의
    struct Book { 
        string title;
        string author;
        uint book_id;
    }
    
    // Book 구조체 타입의 변수 선언
    Book book;

    // 구조체 인스턴스 설정 함수
    function setBook() public {
        book = Book('Learn Solidity', 'TP', 1);
    }

    // 구조체 멤버에 접근하여 반환하는 함수
    function getBookId() public view returns (uint) {
        return book.book_id;
    }

    function getBookAuthor() public view returns (string memory) {
        return book.author;
    }

    function getBookTitle() public view returns (string memory) {
        return book.title;
    }

}
```

#### struct 정의

```solidity
    struct Book { 
        string title;
        string author;
        uint book_id;
    }
```

Book에 대한 struct를 정의합니다. Book은 title, author, book_id 세 개의 필드를 가집니다.


#### getArr 함수

```solidity
    Book book;
```
- Book 구조체 타입의 변수를 선언합니다. 이 변수는 나중에 구조체 인스턴스를 저장하는 데 사용됩니다.

#### push 함수
```solidity
function setBook() public {
    book = Book('Learn Solidity', 'TP', 1);
}

```
- setBook 함수는 Book 구조체의 인스턴스를 생성하고, book 변수에 할당합니다. 여기서는 제목이 'Learn Solidity'이고, 저자가 'TP'이며, 책 ID가 1인 책을 생성합니다.

#### pop 함수
```solidity
function getBookId() public view returns (uint) {
    return book.book_id;
}
```
- getBookId 함수는 book 변수의 book_id 필드에 접근하여 반환합니다. 이 예제에서는 1이 반환됩니다.

## Remix에서 실습 
1. Remix에서 새로운 solidity 파일 생성해서 예제 코드를 복사 붙여넣기 합니다.
2. 예제 코드를 compile 후 deploy합니다.
3. 아래 버튼들이 제대로 동작하는지 확인합니다.

- setBook 버튼을 눌러 정의된 구조체에 'Learn Solidity', 'TP', 1 의 필드 값을 입력합니다. </br>
  임의의 값을 추가하고, getArr, getLength 버튼을 누르면 array에 추가되었고, length가 1 증가한 것을 확인할 수 있습니다.  

- getBookAuthor, getBookId, getBookTitle을 눌러보며 구조체에 필드 값이 잘 삽입 되었는지 확인합니다. 

![image](https://github.com/Joon2000/Solidity-modules/assets/87323564/8eda4ea2-b365-4dbe-b390-b1ac33119e27)









