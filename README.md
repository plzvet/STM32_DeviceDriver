# ⚙️ Linux Device Driver: BMP180 & LCD1602

## 📖 프로젝트 개요
BMP180(I2C) 센서와 LCD1602 디스플레이를 위한 Linux 커널 디바이스 드라이버를 개발하고, 다양한 센서(DHT11, DS1302, Shift Register, Dot Matrix)와 연동하여 하드웨어 제어 및 오실로스코프 파형 분석까지 수행한 프로젝트입니다.

## 🚀 기술 스택
- **언어:** C (Linux Kernel Module)
- **플랫폼:** Raspberry Pi (ARM Linux)
- **기술:** I2C, Bit-banging, SPI(Shift Register), 오실로스코프 분석, Char Device

## 🛠 주요 기능
| 기능 | 설명 |
|---|---|
| 📝 BMP180 드라이버 | I2C 기반 온도/기압 센서 제어 + Timeout 처리 + 파형 분석 |
| 📺 LCD1602 드라이버 | 4bit 모드 구현 → 문자열 출력, 커서 이동 |
| 🌡️ DHT11 센서 | GPIO 비트뱅잉 방식 온습도 측정 |
| 🕒 DS1302 RTC | Serial 비트뱅잉으로 시간 송수신 |
| 🖥 Shift Register & Dot Matrix | SPI 기반 병렬출력 제어 (FND, LED 패턴 표시)

## 🖥 시스템 구성도
![image](https://github.com/user-attachments/assets/10975ed5-a896-451b-ad33-653c7bae825b)

- Sensor ↔ Raspberry Pi ↔ I2C/SPI/GPIO ↔ LCD, Dot Matrix, FND

## 📊 결과 및 성과
- BMP180 무응답 시 Timeout → 시스템 안정성 강화
- 오실로스코프 분석으로 신호 타이밍 최적화
- 다양한 디바이스 드라이버 직접 설계 + 실시간 제어 성공

## 📝 설치 및 실행 방법
```bash
# 커널 모듈 빌드
make

# 커널 모듈 삽입
sudo insmod bmp180_driver.ko
sudo insmod lcd1602_driver.ko

# 디바이스 파일 생성
mknod /dev/bmp180 c 240 0
mknod /dev/lcd1602 c 241 0

# 사용자 공간에서 read/write 호출
cat /dev/bmp180
```

## 📁 프로젝트 구조
```
Device_Driver_Project/
├── bmp180_driver.c
├── lcd1602_driver.c
├── dht11_driver.c
├── ds1302_driver.c
└── shift_register_driver.c
```

## ✉️ 개선 포인트
- LCD 속도 개선 → DMA 전송 적용 고려
- 오류 검출 → CRC/NACK 처리 강화
- RTOS 연동 또는 커널 태스크 분리 적용 가능성

## 🔗 참고자료
[시연 영상] https://youtu.be/vb9hNxRs9ak
---
✅ 키워드: #Linux #DeviceDriver #I2C #SPI #BitBanging #오실로스코프 #커널모듈 #RaspberryPi
