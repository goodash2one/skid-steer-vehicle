## 📁 디렉토리 구조

```
rpi_ws/
├── dkbuild/                       # 도커 이미지를 빌드하기 위한 스크립트
|   ├── dt/                        # ros2 humble desktop 이미지 
|   └── ssv/                       # RP4 상위 제어 시스템 이미지
|       └── skid_steer_vehicle/    # ros2 package 소스코드
└── dkrun/                         # 도커 이미지를 실행하기 위한 스크립트
```