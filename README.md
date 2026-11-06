# PLC Control Lab

LS ELECTRIC **XG5000**을 활용한 PLC 래더 로직(Ladder Logic) 제어 프로젝트 저장소입니다.

산업 자동화 설비의 기본 제어 원리를 학습하고, 모터 운전 시퀀스, 자기유지, 타이머, 인터록(Interlock), 고장 래치, 수동 복구 및 최초 고장 원인 기록 기능을 래더 다이어그램(Ladder Diagram, LD)으로 구현합니다.

## 개발 환경

| 항목 | 내용 |
|---|---|
| PLC 개발 도구 | LS ELECTRIC XG5000 v4.82.1 |
| PLC 기종 | XGK-CPUS |
| 시뮬레이션 | XG-SIM |
| 프로그래밍 언어 | Ladder Diagram (LD) |
| 운영체제 | Windows |

본 저장소의 PLC 프로그램은 **XG-SIM 시뮬레이션 환경**을 기반으로 개발하고 검증합니다.

## 프로젝트 목록

| 프로젝트 | 주요 구현 내용 |
|---|---|
| [Motor Control](motor-control/) | START/STOP, 자기유지, READY 5초·RUN 10초 타이머, 상승 에지 검출, 인터록 기반 운전 제어 |
| [Error Latch & Manual Reset](error-reset/) | 고장 래치, 조건부 수동 RESET, 복구 후 재시작 방지, RUN 상태와 MOTOR 출력 분리 |
| [First-out Fault Recording](first-out/) | 최초 고장 원인 구분, 후속 고장 시 기록 유지, 동시 고장 우선순위, 조건부 일괄 RESET |

## 저장소 구조

```text
plc-control-lab/
├── README.md
├── .gitignore
├── motor-control/
│   ├── README.md
│   ├── src/
│   │   └── motor-control.xgwx
│   └── images/
├── error-reset/
│   ├── README.md
│   ├── src/
│   │   └── error-reset.xgwx
│   └── images/
└── first-out/
    ├── README.md
    ├── src/
    │   └── first-out.xgwx
    └── images/
```

각 프로젝트 디렉터리에는 XG5000 프로젝트 원본, 래더 회로 및 시뮬레이션 화면, 구현 기능과 동작 설명을 정리합니다.
