# 심화실습-1 보고서

## 1. 제출 정보
| 학년학기 | 2026학년도 1학기 |
| 과목명(학수번호) | 프로그래밍기초와실습 (DASF004-52) |
| 학번 | 2026310215 |
| 이름 | 양반석 |
| 과제명 | 심화실습-1 |

## 2. 현재 상태

### 2.1 배운적 있는 언어 및 현재 수준
Python - 하

### 2.2 실습 환경

| Gemini | GitHub Codespace |

## 3. 코드 리뷰 결과

### 3.1 AI가 생성한 코드를 얼마나 이해할 수 있었는지?

- 이해도: 3점
- 2강까지의 내용을 통해 배웠던 include, define, char와 간단한 if문은 쉽게 이해할 수 있었으나, struct, typedef, strcpy, strcmp 등의 함수가 왜 쓰이는지 전혀 알지 못하는 상태로 코드를 복사하여 실습을 진행했습니다.
  
### 3.2 최초에 입력한 프롬프트와 그 결과물에 대한 평가

#### 최초 프롬프트

C언어로 일정 관리 프로그램을 만드려고해
필요한 기본 기능은 아래와 같아
- 일정 추가 : 제목, 날짜, 시간, 설명 입력
- 일정 조회 : 전체 일정 목록 보기
- 일정 수정 : 기존 일정 정보 변경
- 일정 삭제 : 선택한 일정 제거
만들어줄 수 있어?

#### 최종 코드 및 실행 결과
> 본 문서 가장 아래 `부록` 섹션에서 `최종 결과물 코드`와 `실행 결과`에 각각 코드 및 실행 결과를 복사 & 붙여넣기로 첨부합니다.

### 3.3 최종 결과물을 얻기까지의 경험
AI가 코드를 바로 생성하여 실행은 쉽게 되었고, 오류도 없었지만 코드를 한 줄씩 읽어보려니 모르는 함수가 너무 많아 당황스러웠습니다.
AI의 설명을 들어도 struct라는 개념이 쉽게 와닿지 않았습니다. 코드를 단순히 복사 붙여넣기 하는 것과 직접 짤 수 있는 것 사이의 큰 괴리감을 느낀 실습이었습니다.

## 4. 결론
처음보는 함수가 너무 많아 암호처럼 느껴져서 이해하는데 많이 어려웠습니다. 특히 여러 정보를 묶어서 관리하는 struct 문법은 AI의 설명을 들어도 실제 코드에서 어떻게 적용되는지 이해하기 어려웠습니다.
하지만, 문자열을 제어하는 strcmp, strcpy 등의 새로운 함수를 알아가는게 흥미로웠습니다.
이번 실습 후 AI 덕분에 저같은 초보자도 수준 높은 프로그램을 만들어볼 수 있다는 점이 놀라웠으며, 생성된 코드를 보고 제가 이해할 수 있는 부분이 적어 아쉬움이 남았습니다.
이번 실습을 계기로 AI를 단순히 복사용으로 사용하는 것이 아니라, 모르는 문법을 하나 하나 물어보며 기초를 다지는 학습 도구로 활용해야겠다고 생각했습니다.

## 참고문헌
- Gemini

## 부록

### 실행 결과
--- [ Schedule Manager ] --- (일정 추가)
1. 일정 추가
2. 일정 조회
3. 일정 수정
4. 일정 삭제
0. 종료
선택: 1
[일정 추가]
제목:  오전 회의
날짜 (YYYY-MM-DD): 20250315
시간 (HH:MM): 08:00
설명: 파트 오전 회의
일정이 성공적으로 추가되었습니다.


--- [ Schedule Manager ] --- (일정 조회)
1. 일정 추가
2. 일정 조회
3. 일정 수정
4. 일정 삭제
0. 종료
선택: 2

[전체 일정 목록]
1. [20250315] 08:00 오전 회의 - 파트 오전 회의

--- [ Schedule Manager ] --- (일정 수정)
1. 일정 추가
2. 일정 조회
3. 일정 수정
4. 일정 삭제
0. 종료
선택: 3

[전체 일정 목록]
1. [20250315] 08:00 오전 회의 - 파트 오전 회의

수정할 번호 선택: 1
새 제목 (기존: 오전 회의):  오전 간담회
새 날짜 (기존: 20250315): 20250315
새 시간 (기존: 08:00): 09:00
새 설명 (기존: 파트 오전 회의): 커피 간담회
수정이 완료되었습니다.



--- [ Schedule Manager ] --- (일정 삭제)
1. 일정 추가
2. 일정 조회
3. 일정 수정
4. 일정 삭제
0. 종료
선택: 4

[전체 일정 목록]
1. [20250315] 09:00 오전 간담회 - 커피 간담회

삭제할 번호 선택: 1
삭제가 완료되었습니다.

### 최종 결과물 코드

#include <stdio.h>
#include <string.h>

#define MAX_SCHEDULES 100
#define TITLE_SIZE 50
#define DESC_SIZE 200

// 일정을 저장할 구조체 정의
typedef struct {
    char title[TITLE_SIZE];
    char date[20];   // YYYY-MM-DD
    char time[10];   // HH:MM
    char desc[DESC_SIZE];
} Schedule;

Schedule list[MAX_SCHEDULES];
int count = 0;

// 함수 선언
void addSchedule();
void viewSchedules();
void updateSchedule();
void deleteSchedule();

int main() {
    int choice;

    while (1) {
        printf("\n--- [ Schedule Manager ] ---\n");
        printf("1. 일정 추가\n2. 일정 조회\n3. 일정 수정\n4. 일정 삭제\n0. 종료\n");
        printf("선택: ");
        scanf("%d", &choice);
        getchar(); // 버퍼 비우기

        switch (choice) {
            case 1: addSchedule(); break;
            case 2: viewSchedules(); break;
            case 3: updateSchedule(); break;
            case 4: deleteSchedule(); break;
            case 0: printf("프로그램을 종료합니다.\n"); return 0;
            default: printf("잘못된 선택입니다.\n");
        }
    }
}

// 1. 일정 추가
void addSchedule() {
    if (count >= MAX_SCHEDULES) {
        printf("저장 공간이 부족합니다.\n");
        return;
    }
    printf("\n[일정 추가]\n");
    printf("제목: "); fgets(list[count].title, TITLE_SIZE, stdin);
    list[count].title[strcspn(list[count].title, "\n")] = 0; // 개행 제거

    printf("날짜 (YYYY-MM-DD): "); scanf("%s", list[count].date);
    printf("시간 (HH:MM): "); scanf("%s", list[count].time);
    getchar();

    printf("설명: "); fgets(list[count].desc, DESC_SIZE, stdin);
    list[count].desc[strcspn(list[count].desc, "\n")] = 0;

    count++;
    printf("일정이 성공적으로 추가되었습니다.\n");
}

// 2. 일정 조회
void viewSchedules() {
    if (count == 0) {
        printf("\n등록된 일정이 없습니다.\n");
        return;
    }
    printf("\n[전체 일정 목록]\n");
    for (int i = 0; i < count; i++) {
        printf("%d. [%s] %s %s - %s\n", i + 1, list[i].date, list[i].time, list[i].title, list[i].desc);
    }
}

// 3. 일정 수정
void updateSchedule() {
    viewSchedules();
    if (count == 0) return;

    int idx;
    printf("\n수정할 번호 선택: ");
    scanf("%d", &idx);
    getchar();

    if (idx < 1 || idx > count) {
        printf("번호가 올바르지 않습니다.\n");
        return;
    }

    int i = idx - 1;
    printf("새 제목 (기존: %s): ", list[i].title);
    fgets(list[i].title, TITLE_SIZE, stdin);
    list[i].title[strcspn(list[i].title, "\n")] = 0;

    printf("새 날짜 (기존: %s): ", list[i].date);
    scanf("%s", list[i].date);
    printf("새 시간 (기존: %s): ", list[i].time);
    scanf("%s", list[i].time);
    getchar();

    printf("새 설명 (기존: %s): ", list[i].desc);
    fgets(list[i].desc, DESC_SIZE, stdin);
    list[i].desc[strcspn(list[i].desc, "\n")] = 0;

    printf("수정이 완료되었습니다.\n");
}

// 4. 일정 삭제
void deleteSchedule() {
    viewSchedules();
    if (count == 0) return;

    int idx;
    printf("\n삭제할 번호 선택: ");
    scanf("%d", &idx);
    getchar();

    if (idx < 1 || idx > count) {
        printf("번호가 올바르지 않습니다.\n");
        return;
    }

    for (int i = idx - 1; i < count - 1; i++) {
        list[i] = list[i + 1]; // 데이터 한 칸씩 당기기
    }
    count--;
    printf("삭제가 완료되었습니다.\n");
}
