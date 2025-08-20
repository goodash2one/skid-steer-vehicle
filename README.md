# 🚗 4WD 스키드 스티어 차량 자율 기능 개발

이 리포지토리는 **Raspberry Pi 4**와 **Infineon AURIX TC375** 기반 4WD 스키드 스티어 차량의 자율 기능 개발을 위한 소스 코드와 문서를 관리합니다.

- 프로젝트 기간: 2025.07.23 - 2025.08.08 (약 3주간)  
- 팀 규모: 6명  
- 나의 역할  
  ---
  - 외부 입력(ERU)과 타이머(STM)를 활용한 인터럽트 기반 TC375 센서 펌웨어 개발 (초음파, 엔코더)  
    [초음파 디렉토리](tc375_fw/src/mypj/BSW/ULTRASONIC/)  
    [엔코더 디렉토리](tc375_fw/src/mypj/BSW/ENCODER/)  
  - Raspberry Pi와 TC375간 CAN 통신 설계 및 구현  
    [CAN 디렉토리](tc375_fw/src/mypj/BSW/CAN/)  
  - Raspberry Pi에서 ROS2 기반 시스템 설계 및 구현  
    [ROS2 패키지 디렉토리](rpi_ws/dkbuild/ssv/skid_steer_vehicle/)    
  - Raspberry Pi에서 docker image 관리  
    [Raspberry Pi 디렉토리](rpi_ws/)   

---

## 🎯 프로젝트 목표 (v7.2 기준)

1. **원격 제어**  
   - 조이스틱을 이용한 완전 수동 제어
2. **긴급 제동**
   - ToF 센서를 이용한 거리 기반 긴급 제동
3. **자율 주차**
   - 측후방 초음파 센서를 이용한 자율 주차
4. **모니터링**
   - 스마트폰 어플로 카메라 스트리밍 및 주행 데이터 모니터링

---

## 🛠️ 시스템 아키텍처

### 전체 구조

- **고수준 제어기 (AP):**  
  - Raspberry Pi 4 Model B (8GB)  
  - Platform: ROS2 Humble + Docker
  - 주요 역할  
    - 상태 관리 (Stateflow 기반)
    - PWM 변환
    - 외부 통신(조이스틱, 모바일 앱)
- **저수준 제어기 (MCU):**  
  - Infineon AURIX TC375  
  - 주요 역할:  
    - 실시간 모터 제어  
    - 엔코더 펄스 카운팅/속도 계산  
    - ToF/초음파 센서 데이터 취득 및 전처리  
    - 긴급 제동 로직
    - 자율 후방 주차 로직
- **통신:**  
  - 프로토콜: CAN  
  - 역할: RPi와 TC375 간 제어 명령, 차량 상태, 센서 데이터 교환

---

## 🏗️ 개발 환경 설정

### Raspberry Pi

- Docker로 ROS2 개발 환경 관리
- 설치 및 빌드
  1. Docker 설치: [공식 문서](https://docs.docker.com/engine/install/)
  2. 이미지 빌드
     ```bash
     cd rpi_ws/dkbuild/ssv
     docker build -t ros:ssv .
     ```
  2. 이미지 실행 실행
     ```bash
     cd rpi_ws/dkrun
     ./ssv.sh
     ```

### TC375

- **IDE:** AURIX™ Development Studio
- **DEBUGINH:** UDE Visual Platform

---

## 📁 리포지토리 구조

```
/
├── .github/
├── docs/
├── rpi_ws/            # Raspberry Pi
├── tc375_fw/          # TC375 Firmware
├── simulink_models/   # MATLAB/Simulink 모델
└── README.md
```

---
