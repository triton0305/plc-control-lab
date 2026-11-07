# PLC Control Lab

LS ELECTRIC **XG5000**에서 하나의 모터 제어 로직을 기본 운전부터 고장 정지·복구, 최초 고장 원인 진단까지 확장한 프로젝트입니다.

## 개발 환경

| 항목 | 내용 |
|---|---|
| PLC 개발 도구 | LS ELECTRIC XG5000 v4.82.1 |
| PLC 기종 | XGK-CPUS |
| 시뮬레이션 | XG-SIM |
| 프로그래밍 언어 | Ladder Diagram (LD) |
| 운영체제 | Windows |

## 제어 로직 발전 과정

### Step 01 · [Motor Control](motor-control/)

START/STOP 제어에 자기유지를 적용하고, 정상 조건이 5초간 연속 유지되어 `READY`가 되면 `START` 상승 에지로 운전을 시작하도록 구성했습니다. 운전은 10초 후 자동 정지하며, `STOP`을 누르거나 도어·비상정지(E-Stop)·센서 인터록(Interlock)의 운전 허가 조건을 벗어나면 정지합니다.

### Step 02 · [Error Latch & Reset](error-reset/)

기본 운전 로직에 고장 래치와 조건부 수동 `RESET`을 추가했습니다. 고장 원인을 해소해도 `ERROR`를 유지하며, 운전 허가 조건이 모두 정상이고 `START`가 해제된 상태에서 `RESET`을 새로 눌러야 해제됩니다. 복구 후에는 정상 조건을 다시 5초간 유지한 뒤 새 `START` 입력이 있어야 운전합니다.

### Step 03 · [First-out Fault Recording](first-out/)

고장 정지와 수동 복구 로직에 최초 고장 원인 기록을 추가했습니다. 후속 고장이 발생해도 최초 원인을 유지합니다. 최초 기록이 비어 있고 같은 PLC 스캔에서 여러 고장을 검출하면 **E-Stop → 도어 → 센서** 순으로 하나를 기록합니다. 유효한 `RESET`으로 `ERROR`와 최초 고장 기록을 함께 해제합니다.

각 폴더에는 상세 README, XG5000 프로젝트 원본(`src/`), 래더 회로 및 시뮬레이션 화면(`images/`)을 정리했습니다.

## 최종 구현 및 검증 결과

최종 래더는 운전 상태(`RUN`)와 모터 출력 명령(`MOTOR`)을 분리합니다. **XG-SIM**에서 고장 시 두 신호의 차단, 후속 고장에도 최초 기록 유지, 같은 스캔의 고장 우선순위, 복구 조건 미충족 시 `RESET` 거부, 유효한 `RESET` 후 모터 정지를 유지한 상태에서 `READY`로 복귀하는 동작을 확인했습니다.

[XG-SIM 검증 결과 17개 항목](first-out/README.md#6-xg-sim-검증-결과)
