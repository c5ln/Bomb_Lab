# CSAPP Bomb Lab 해결 과정 기록

이 문서는 "Computer Systems: A Programmer's Perspective" 과목의 Bomb Lab을 해결한 과정을 기록하고, 각 단계에서 얻은 지식을 정리하기 위해 작성되었습니다.

---

## 1. 프로젝트 목표 및 개요

Bomb Lab은 C 코드로 작성된 실행 파일을 리버싱하여, 어셈블리 코드를 분석하고 각 단계를 통과하는 올바른 입력값을 찾는 과제입니다. 이 과정을 통해 다음을 학습하는 것을 목표로 합니다.

-   x86-64 어셈블리 코드 해독 능력
-   GDB 디버거 사용법
-   스택 프레임, 함수 호출 규약, 제어문 등의 기계 수준 표현 이해

---

## 2. 단계별 해결 과정 

### Phase 1: 단순 문자열 비교

-   **분석 과정**:
    1.  `disas phase_1` 명령어로 어셈블리 코드를 확인했습니다.
    2.  `0x400ef0` 주소에서 `strings_not_equal` 함수를 호출하는 것을 발견했습니다.
    3.  `call` 명령어 직전에 `break`를 설정하고, `info registers`로 `%rdi`와 `%rsi` 레지스터 값을 확인하여 비교 대상 문자열을 알아냈습니다.
-   **핵심 코드 분석**:
    ```assembly
    0x0000000000400ee0 <+20>:    mov    $0x402400,%esi
    0x0000000000400ee5 <+25>:    mov    %rax,%rdi
    0x0000000000400ee8 <+28>:    callq  0x401338 <strings_not_equal>
    ```
-   **Phase_1 Key** : Border relations with Canada have never been better.
