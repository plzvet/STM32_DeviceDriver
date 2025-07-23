# ⚙️ STM32 Bare-Metal Device Driver: BMP180 & LCD1602

## 📖 프로젝트 개요

STM32F4 기반 MCU에서 HAL FUNCTION 사용 없이 BMP180 (I2C 센서)와 LCD1602 (4bit 병렬 디스플레이)를 직접 제어하는 디바이스 드라이버를 구현한 프로젝트입니다.
레지스터 접근 기반 I2C/비동기 병렬 제어, 보정 알고리즘 적용, 타이밍 기반 펄스 제어를 포함하며, UART 출력 및 오실로스코프를 통해 파형 검증까지 수행하였습니다.

## 🚀 기술 스택

* **언어:** C (Bare-metal)
* **플랫폼:** STM32F4, STM32CubeIDE
* **기술:**

  * 레지스터 기반 I2C 통신
  * 1602LCD (4bit 방식) 제어
  * UART 디버깅, 오실로스코프 타이밍 분석

## 🛠 주요 기능

| 기능                             | 설명                                               |
| ------------------------------ | ------------------------------------------------ |
| 📝 BMP180 드라이버                 | 레지스터 접근 기반 I2C 통신, 보정 알고리즘 구현, Timeout 예외 처리 포함  |
| 📺 LCD1602 드라이버                | 4bit 모드 초기화 시퀀스 수동 구현, Enable 펄스 제어, 커서 이동/문자 출력 |

## 🖥 시스템 구성도

```
[BMP180] ⇄ I2C ⇄ [STM32 MCU] ⇄ I2C ⇄ LCD1602 (4bit GPIO)
```

## 📊 결과 및 성과

* BMP180 ID 검증 및 보정값 수신, 온도/기압 계산식 직접 구현
* LCD1602 4bit 모드 안정적 구동 및 실시간 커서 제어
* HAL FUNTION 미사용, 모든 통신 타이밍을 수동 구성하여 신뢰성 확보
* 오실로스코프 기반 SDA/SCL, Enable 펄스 검증
* UART 로그 기반 실시간 디버깅 (센서 ID, 보정값, 계산 결과 등)

## 📝 사용 방법

1. STM32CubeIDE에서 `.c` 파일 포함 후 빌드
2. `main()` 호출
3. UART 시리얼 모니터로 센서 결과 출력 확인
4. LCD1602에 문자열 출력 → 온도/기압 출력 연동 가능

## 📁 프로젝트 구조

```
STM32_Driver_Project/
├── bmp180.c           # BMP180 센서 통신 및 보정 계산
├── bmp180.h
├── 1602lcd.c          # LCD1602 4bit 초기화 및 출력
├── 1602lcd.h
└── delay_us.c         # Enable 펄스 타이밍용 delay 함수
```

## ✉️ 개선 포인트

* LCD 출력 속도 향상을 위한 GPIO 타이밍 최적화
* BMP180 예외 처리 FSM 개선 (I2C 응답 NACK, 재시도 로직)
* RTOS 환경 연동 또는 센서별 Task 분리로 구조 확장 가능
* OLED / GUI 연동 또는 USB CDC 기반 출력 확장 가능

## 🔗 참고자료

* [BMP180 Datasheet (Bosch)](https://cdn-shop.adafruit.com/datasheets/BST-BMP180-DS000-09.pdf)
* \[시연 영상] [I2C LCD](https://youtu.be/vb9hNxRs9ak)

---
