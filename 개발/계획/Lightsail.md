- 개인 테스트 개발용 세팅 위주로 개발 할 예정
- 고정 도메인 5개 목록
	1. [[Nginx]] 서버
		* 같은 리전 사용 예정이라 웹 서버 분리
	2. [[MYSQL]] 서버
		* 개발테스트용
		* 추후 [[RDS]]로 바꿀 수도 있음
	3. API 서버 (백언어 고민)
		1. [[Python]] ([[Flask]])
			* 만드려고 하는 기능에 비해 사이즈가 큼
		2. [[PHP]]
			* 어떤 언어보다 빠르고, 자원소모가 적음
			* 간혹 REST API 미표기 or 지원 없으면 곤란함
		3. [[Node.js]] ([[Express.js]] + [[Typescript]])
			* 싱글스레드 프레임워크
	 1. 나머지 2개 코드 외부 접속 권한으로 유동적 이용
- 월 1만 ~ 5만원 사용 예정

/.obsidian
.gitinore