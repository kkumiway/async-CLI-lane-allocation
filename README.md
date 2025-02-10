## 🌊 카테부 수영장 레인 배정 시스템 - 비동기 🌊
이 프로그램은 카테부 수영장의 레인 배정 시스템을 구현한 Java 프로그램입니다. 실력에 맞지 않는 레인에서 수영하며 발생하는 불편함을 줄이기 위해 고안되었습니다. 사용자는 수영 경력에 따라 강습 레인과 자유 레인을 선택하여 배정받을 수 있습니다. 또한, 어린이 여부와 핀 사용 여부에 따라 배정되는 레인이 달라집니다.

### 기능
- 수영장 이용 시간: 사용자가 이용 시간을 입력하면, 수영장이 열려 있는지 확인합니다.
- 사용자 정보 입력: 이용자의 이름과 수영 경력을 입력받습니다.
- 어린이 여부 확인: 어린이인 경우 어린이 전용 강습 레인으로 배정됩니다.
- 강습 레인 배정: 강습을 선택한 경우, 사용자의 경력에 맞는 강습 레인에 배정됩니다.
- 자유 레인 배정: 자유 수영을 선택한 경우, 핀을 사용할지 여부에 따라 배정되는 레인이 달라집니다.
- 예외 처리: 잘못된 입력에 대해 안내 메시지를 출력하고 재입력을 유도합니다.

### 패키지 분리: 계층형
```bazaar
├── controller               # 프레젠테이션 계층
│   └── Main.java
│
├── model                    # 도메인 계층
│   ├── Pool.java
│   ├── Lane.java
│   ├── ClassLane.java
│   ├── FreeLane.java
│   └── Person.java
│
├── service                  # 비즈니스 로직 계층
│   └── PoolService.java
│
└── util                     # 유틸리티 클래스
    ├── InputValidator.java
    └── ScriptPrinter.java
```

### 시나리오
```
1. 수영장 이용 시간 입력
    a. 개장 시간과 폐장 시간 사이가 아닌 시간 입력 → 오류 메시지 출력, 재입력 유도
    b. 숫자가 아닌 입력 → 오류 메시지 출력, 재입력 유도
    c. 개장 시간과 폐장 시간 사이의 시간 정상 입력 → 2로 이동
2. 사용자 정보 입력
    2-1. 이름 입력
        a. 빈 문자열 입력 → 오류 메시지 출력, 재입력 유도
        b. 이외 정상 입력 → 2-2로 이동
    2-2. 수영 경력 입력
        a. 입력값이 0보다 작은 경우 → 오류 메시지 출력, 재입력 유도
        b. 숫자가 아닌 입력 → 오류 메시지 출력, 재입력 유도
        c. 이외 정상 입력 → 3으로 이동
3. 어린이 레인 배정
    3-1. 어린이 여부 입력
        a. 0 또는 1이 아닌 숫자 입력 → 오류 메시지 출력, 재입력 유도
        b. 숫자가 아닌 입력 → 오류 메시지 출력, 재입력 유도
        c. 0 입력 → 5로 이동
        d. 1 입력 → 3-2로 이동
    3-2. 어린이 레인 배정
        a. 어린이 레인이 존재하는 경우 → 배정 결과 출력, 프로그램 종료
        b. 어린이 레인이 존재하지 않는 경우 →  오류 메시지 출력, 프로그램 종료
4. 강습/자유 레인 선택
    a. 1 또는 2가 아닌 숫자 입력 → 오류 메시지 출력, 재입력 유도
    b. 숫자가 아닌 입력 → 오류 메시지 출력, 재입력 유도
    c. 1 입력 → 5-1로 이동
    d. 2 입력 → 5-2로 이동
5. 강습 및 자유 레인 배정
    5-1. 강습 레인 배정
        a. 경력에 맞는 강습 레인이 존재하는 경우 → 배정 결과 출력, 프로그램 종료
        b. 경력에 맞는 강습 레인이 존재하지 않는 경우 →  오류 메시지 출력, 프로그램 종료
    5-2. 자유 레인 배정
        5-2-1. 핀 사용 여부 입력
            a. 0 또는 1이 아닌 숫자 입력 → 오류 메시지 출력, 재입력 유도
            b. 숫자가 아닌 입력 → 오류 메시지 출력, 재입력 유도
            c. 1 입력 → 5-2-2로 이동
            d. 나머지 경우 → 5-2-3으로 이동
        5-2-2. 핀 레인 배정
            a. 핀 레인이 존재하는 경우 → 배정 결과 출력, 프로그램 종료
            b. 핀 레인이 존재하지 않는 경우 →  오류 메시지 출력, 프로그램 종료
        5-2-3. 핀 레인 제외 자유 레인 배정
            a. 경력에 맞는 자유 레인이 존재하는 경우 → 배정 결과 출력, 프로그램 종료
            b. 경력에 맞는 자유 레인이 존재하지 않는 경우 →  오류 메시지 출력, 프로그램 종료
```

### 클래스 다이어그램
![Image](https://github.com/user-attachments/assets/75d7a011-11d4-4e5e-b349-94daf650fe49)

### 실행 예시
```
************************************************
    🌊🌊🌊 카테부 수영장에 오신 것을 환영합니다! 🌊🌊🌊
************************************************
현재 이용할 수 있는 레인 목록:
-------------------------------------------------
1번 레인 - 강좌명: 어린이 레인, 레인 길이: 25m, 레인 수심: 0.0m
2번 레인 - 강좌명: 초급(최소 경력: 1개월), 레인 길이: 25m, 레인 수심: 1.2m
3번 레인 - 강좌명: 중급(최소 경력: 3개월), 레인 길이: 25m, 레인 수심: 1.2m
4번 레인 - 강좌명: 상급(최소 경력: 6개월), 레인 길이: 50m, 레인 수심: 1.4m
5번 레인 - 강좌명: 마스터(최소 경력: 12개월), 레인 길이: 50m, 레인 수심: 1.4m
6번 레인 - 자유수영(최소 경력: 1개월), 레인 길이: 25m, 레인 수심: 1.2m
7번 레인 - 자유수영(최소 경력: 3개월), 레인 길이: 25m, 레인 수심: 1.2m
8번 레인 - 자유수영(최소 경력: 6개월), 레인 길이: 25m, 레인 수심: 1.2m
9번 레인 - 자유수영(최소 경력: 12개월), 레인 길이: 50m, 레인 수심: 1.4m
10번 레인 - 자유수영(핀 사용), 레인 길이: 50m, 레인 수심: 1.4m
-------------------------------------------------

몇 시에 이용할 예정인가요? (숫자만 입력하세요.) 3
이용 가능 시간이 아닙니다. 다시 입력해주세요.

몇 시에 이용할 예정인가요? (숫자만 입력하세요.) abc
잘못된 입력입니다. 숫자만 입력해주세요.

몇 시에 이용할 예정인가요? (숫자만 입력하세요.) 10
이용 가능합니다.

이름을 입력하세요: Chunsik

수영 경력(개월)을 입력하세요: -1
경력은 0개월 이상의 숫자여야 합니다.

수영 경력(개월)을 입력하세요: abc
잘못된 입력입니다. 숫자만 입력해주세요.

수영 경력(개월)을 입력하세요: 5

어린이인가요? (Yes: 1, No: 0) 2
1 또는 0만 입력해주세요.

어린이인가요? (Yes: 1, No: 0) abc
잘못된 입력입니다. 1 또는 0만 입력해주세요.

어린이인가요? (Yes: 1, No: 0) 1

Chunsik님은 1번 레인(어린이)에 배정되었습니다.

```
### 개발 환경
- 언어: JAVA21
- IDE: IntelliJ IDEA