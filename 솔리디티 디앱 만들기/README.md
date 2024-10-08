# 솔리디티 디앱 만들기 모듈
--- 
# 개요

* 솔리디티 디앱 만들기 모듈은 솔리디티 컨트랙트에 기반하여 프론트엔드를 제공하는 디앱 제작을 위해 Ether.js 프론트엔드 라이브러리와 어플리케이션을 관리하는 Hardhat, Scaffold-ETH 패키지 이해 및 실습 자료를 제공한다. Scaffold-ETH를 활용해 다양한 기능을 갖춘 어플리케이션 제작 실습 미션을 포함한다.
* 모듈은 아티클과 미션으로 구성된다. 아티클이란 특정 개념 혹은 현상을 설명하는 자료이다. 아티클은 기술 및 배경의 정의와 출현 배경, 구성 요소, 구동 원리, 특장점, 활용 방안을 포함한다. 반면 미션은 실습을 통해 기술 및 개념 체득을 유도하는 자료이다. 미션은 결과물 설명을 포함하는 목적 및 배경, 사전 설치, 코드와 설명을 포함한 수행 방법, 제출 내용을 포함한다.

# 모듈 구성

솔리디티 베이직 모듈의 구성은 다음과 같다.

|  | 구분 | 설명 | 자료 링크 |
| --- | --- | --- | ----- |
| 웹3 디앱 아키텍처 | 아티클 | 스마트 컨트랙트와 솔리디티 언어의 특징 이해 | [웹3 디앱 아키텍처](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EC%95%84%ED%8B%B0%ED%81%B4/01.%20%EC%9B%B93%20%EB%94%94%EC%95%B1%20%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98.md) |
| Hardhat 솔리디티 개발 환경 설정 | 아티클 | 솔리디티 컨트랙트 배포, 프로젝트 개발을 위한 Hardhat<br>설치 및 사용법 이해 | [Hardhat 솔리디티 개발 환경 설정](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EC%95%84%ED%8B%B0%ED%81%B4/02.%20Hardhat%20%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EA%B0%9C%EB%B0%9C%20%ED%99%98%EA%B2%BD%20%EC%84%A4%EC%A0%95.md) |
| Foundry 솔리디티 개발 환경 설정 | 아티클 | 러스트 툴체인 기반 Foundry의 이해 및 솔리디티 프로젝트 배포, 관리 방법의 이해 | [Foundry 솔리디티 개발 환경 설정](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EC%95%84%ED%8B%B0%ED%81%B4/03.%20Foundry%20%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EA%B0%9C%EB%B0%9C%20%ED%99%98%EA%B2%BD%20%EC%84%A4%EC%A0%95.md) |
| Scaffold-ETH2 설치 및 사용 방법 | 아티클 | 웹3 디앱 백엔드/프론트엔드 패키지 제작을 위한 Scaffold-ETH2 설치 및 사용법 이해 | [Scaffold-ETH2 설치 및  사용 방법](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EC%95%84%ED%8B%B0%ED%81%B4/04.%20Scaffold-ETH2%20%EC%84%A4%EC%B9%98%20%EB%B0%8F%20%EC%82%AC%EC%9A%A9%20%EB%B0%A9%EB%B2%95.md) |
| 분산 스토리지 | 아티클 | 웹3 어플리케이션 제작을 위한 분산 스토리지 개념 이해 | [분산 스토리지](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EC%95%84%ED%8B%B0%ED%81%B4/05.%20%EB%B6%84%EC%82%B0%20%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80.md) |
| 데이터 쿼리 | 아티클 | 웹3 디앱을 위한 데이터 인덱싱 개념과 방법 이해 | [데이터 쿼리](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EC%95%84%ED%8B%B0%ED%81%B4/06.%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%BF%BC%EB%A6%AC.md) |
| My NFT Marketplace | 미션 | NFT 민팅, 구매, 판매가 가능한 마켓플레이스 | [my-nft-marketplace](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/01.%20My%20NFT%20Marketplace.md) |
| Simple Payment | 미션 | buymeacoffee 메시지, 송금 디앱 만들기 | [Simple Payment](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/02.%20Simple%20Payment.md) |
| Staking | 미션 | 예치, 이자율 정산이 가능한 스테이킹 디앱 만들기 | [Staking](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/03.%20Staking.md) |
| Token Vendor | 미션 | 토큰 민팅, 전송 자판기 만들기 | [Token Vendor](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/04.%20Token%20Vendor.md) |
| Oracle | 미션 | 외부 데이터 오라클 디앱 만들기 | [Oracle Part1](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/05.%20Oracle%20(part1).md) [Oracle Part2](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/05.%20Oracle%20(part2).md) [Oracle Part3](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/05.%20Oracle%20(part3).md) |
| Dynamic NFT | 미션 | 온체인 SVG 기반 다이나믹 NFT 디앱 만들기 | [Dynamic NFT](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/06.%20Dynamic%20NFT.md) |
| Dice Game | 미션 | 온체인 RNG 기반 주사위 게임 만들기 | [Dice Game](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/07.%20Dice%20Game.md) |
| Token Swap | 미션 | 토큰 교환이 가능한 탈중앙화 거래소 만들기 | [Token Swap](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/08.%20Token%20Swap.md) |
| State Channel | 미션 | 스테이트 채널 기반 브릿지 디앱 만들기 | [State Channel](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/09.%20State%20Channel.md) |
| Multi Sig | 미션 | Storage, Memory, CallData 활용 실습 | [Multi Sig](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/10.%20Multi%20Sig.md) |
| Crowd Funding | 미션 | 크라우드 펀딩 디앱 만들기 | [Crowd Funding](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/11.%20Crowd%20Funding.md) |
| Lending | 미션 | Aave V2 컨트랙트 기반 대출 디앱 만들기 | [Lending](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/12.%20Lending.md) |
| Decentralized Social | 미션 | 탈중앙화 소설 어플리케이션 만들기 | [Decentralized Social](https://github.com/LudiumAgwn/road-to-bangkok/blob/main/%EC%86%94%EB%A6%AC%EB%94%94%ED%8B%B0%20%EB%94%94%EC%95%B1%20%EB%A7%8C%EB%93%A4%EA%B8%B0/%EB%AF%B8%EC%85%98/13.%20Decentralized%20Social.md) |

# 제안 및 추가

* 솔리디티 디앱 만들기 교육 모듈은 오픈 소스 컨트리뷰션을 통해 지속적으로 자료를 보완, 발전시킨다
* 현존하는 모듈에 제안을 원하는 빌더는 [Issue를 통해 제안 내용을 작성](https://github.com/Ludium-Official/road-to-bangkok/issues)하거나 리포를 포킹해서 개선된 내용을 [Pull Request로 바로 요청](https://github.com/Ludium-Official/road-to-bangkok/pulls)할 수도 있다
* 제안, 요청된 내용은 루디움에서 검토 이후 적절성을 판단하여 자료를 업데이트 한다