## <a name="prepare-your-raspberry-pi"></a>Raspberry Pi 준비

### <a name="install-raspbian"></a>Raspbian 설치

인 경우 hello 라스베리 Pi를 사용 하는 처음으로 tooinstall hello Raspbian 운영 체제 NOOBS hello 키트에 포함 된 hello SD 카드에 사용 해야 합니다. hello [라스베리 Pi 소프트웨어 가이드] [ lnk-install-raspbian] 설명 방법을 tooinstall 라스베리 Pi에 운영 체제. 이 자습서 라스베리 원주율 hello Raspbian 운영 체제를 설치 했다고 가정 합니다.

> [!NOTE]
> hello에 포함 된 hello SD 카드 [라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트] [ lnk-starter-kits] NOOBS 설치에 이미 있습니다. 이 카드의 hello 라스베리 Pi 부팅 수 있으며 tooinstall hello Raspbian 운영 체제를 선택할 수 있습니다.

### <a name="set-up-hello-hardware"></a>Hello 하드웨어 설정

이 자습서에서는 hello에 포함 된 hello BME280 센서 [라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트] [ lnk-starter-kits] toogenerate 원격 분석 데이터. LED tooindicate를 사용 하 여 hello 라스베리 Pi hello 솔루션 대시보드에서 메서드 호출을 처리 하는 경우.

hello 빵 보드에 hello 구성 요소입니다.

- 빨강 LED
- 220옴 저항기(빨강, 빨강, 밤색)
- BME280 센서

hello 다음 다이어그램에서는 어떻게 tooconnect 하드웨어:

![Raspberry Pi의 하드웨어 설정][img-connection-diagram]

hello 다음 표에 요약 되어 hello breadboard에 hello 라스베리 Pi toohello 구성 요소에서 hello 연결:

| Raspberry Pi            | 브레드보드             |색         |
| ----------------------- | ---------------------- | ------------- |
| GND(14 핀)            | LED -ve 핀(18A)      | 자주색          |
| GPCLK0(7 핀)          | 저항기(25A)         | 주황색          |
| SPI_CE0(24 핀)        | CS(39A)               | 파랑          |
| SPI_SCLK(23 핀)       | SCK(36A)              | 노랑        |
| SPI_MISO(21 핀)       | SDO(37A)              | 흰색         |
| SPI_MOSI(19 핀)       | SDI(38A)              | 녹색         |
| GND(6 핀)             | GND(35A)              | 검정         |
| 3.3V(1 핀)           | 3Vo(34A)              | 빨강           |

toocomplete hello 하드웨어 설치 해야합니다.

- Hello 키트에 포함 된 라스베리 Pi toohello 전원 공급 장치를 연결 합니다.
- 키트에 포함 된 hello 이더넷 케이블을 사용 하 여 라스베리 Pi tooyour 네트워크를 연결 합니다. 또는 Raspberry Pi에 대해 [무선 연결][lnk-pi-wireless]을 설정할 수 있습니다.

이제 hello 하드웨어를 라스베리 Pi의 설치를 완료 했습니다.

### <a name="sign-in-and-access-hello-terminal"></a>로그인 및 액세스 hello 터미널

환경을 사용 하는 두 가지 옵션 tooaccess 터미널 라스베리 원주율:

- 키보드 연결된 tooyour 라스베리 Pi를 모니터링 하는 경우에 hello Raspbian GUI tooaccess 터미널 윈도우를 사용할 수 있습니다.

- 액세스 hello 명령줄 데스크톱 컴퓨터의 SSH를 사용 하 여 라스베리 원주율입니다.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Hello GUI에서에서 터미널 윈도우를 사용 하 여

Raspbian에 대 한 hello 기본 자격 증명이 username **pi** 및 암호 **라스베리**합니다. Hello GUI에에서 hello 작업 표시줄에서 hello를 시작할 수 있습니다 **터미널** hello 모양의 아이콘을 모니터를 사용 하 여 유틸리티입니다.

#### <a name="sign-in-with-ssh"></a>SSH를 사용하여 로그인

명령줄 액세스 tooyour 라스베리 Pi에 대 한 SSH를 사용할 수 있습니다. hello 문서 [SSH (보안 셸)] [ lnk-pi-ssh] 설명 방법을 tooconfigure 라스베리 Pi와의 SSH 방법과에서 tooconnect [Windows] [ lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]합니다.

사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>선택 사항: Raspberry Pi의 폴더 공유

필요에 따라 데스크톱 환경 라스베리 원주율 tooshare 폴더를 할 수 있습니다. 공유 폴더를 사용 하면 있습니다 toouse 데스크톱 원하는 텍스트 편집기 (예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime 텍스트](http://www.sublimetext.com/)) tooedit 파일을 사용 하는 대신 프로그램 라스베리 Pi `nano` 또는 `vi`.

Windows와 함께 폴더 tooshare hello 라스베리 Pi에서 Samba 서버를 구성 합니다. 또는 기본 제공 hello를 사용 하 여 [SFTP](https://www.raspberrypi.org/documentation/remote-access/) 바탕 화면에 SFTP 클라이언트와 서버입니다.

### <a name="enable-spi"></a>SPI 사용

Hello 샘플 응용 프로그램을 실행 하기 전에 hello 직렬 주변 SPI (인터페이스) 버스 라스베리 Pi hello에 사용 하도록 설정 해야 합니다. hello 라스베리 Pi hello SPI 버스 통해 hello BME280 센서 장치와 통신합니다. 다음 명령은 tooedit hello 구성 파일 hello를 사용 합니다.

```sh
sudo nano /boot/config.txt
```

Hello 줄을 찾습니다.

`#dtparam=spi=on`

- delete hello toouncomment hello 선 `#` hello 시작 부분에 있습니다.
- 변경 내용을 저장 (**Ctrl-O**, **Enter**) 및 exit hello 편집기 (**Ctrl-X**).
- tooenable SPI, 라스베리 Pi hello를 다시 부팅 합니다. Hello 터미널의 연결을 끊습니다 재부팅 toosign 다시 라스베리 Pi hello를 다시 시작할 때에 사용 해야 합니다.

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/